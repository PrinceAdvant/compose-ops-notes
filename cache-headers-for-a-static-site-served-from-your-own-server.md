# Cache headers for a static site served from your own server

Static sites are fast by default, but wrong cache headers make them either stale or slow.

## Three groups of files

- **HTML.** `Cache-Control: no-cache`. Browsers revalidate each time with an ETag, so new deploys show up immediately.
- **Hashed assets** such as `app.3f9c2b.js`. `Cache-Control: public, max-age=31536000, immutable`. The filename changes when content changes.
- **Unhashed images and fonts.** A middle value such as `max-age=86400`.

## Example for Caddy

```
@hashed path_regexp \.[0-9a-f]{6,}\.(js|css)$
header @hashed Cache-Control "public, max-age=31536000, immutable"
header /*.html Cache-Control "no-cache"
```

## Compression

Enable gzip and zstd or Brotli for text files. Serve precompressed files if your build produces them.

## Check it

`curl -I https://example.com/` and confirm the headers per file type after every proxy config change.

Server setup is in the guide to [deploy a static site on your own server](https://peon.sh/blogs/deploy-static-site-own-server). Notes by a contributor to [Peon](https://peon.sh/), an open-source self-hosted deployment platform.
