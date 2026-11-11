# Moving Netlify Functions into a container: a migration note

Netlify Functions are convenient until you want to self-host. Each function is a handler, so the port is mostly mechanical.

## Steps

1. Create a small HTTP server (Express, Hono or Fastify) with one route per function.
2. Adapt the handler signature. Netlify passes an event with `body`, `headers` and `queryStringParameters`. Map those from the request object.
3. Move environment variables from the Netlify UI to your deploy platform.
4. Keep the old paths. Proxy `/.netlify/functions/*` to the new service, or update the frontend calls.
5. Containerize with a small Node image and a health check route.

## Things that differ

- No automatic scaling to zero. One container is always running, which also means no cold starts.
- Scheduled functions become cron jobs on the server.
- Background functions become a queue and worker.

## Static part

Serve the built site from the same server or a CDN, with the API on a subpath.

A side-by-side look at [Peon vs Netlify](https://peon.sh/compare/peon-vs-netlify) covers pricing and features. Written by a contributor to [Peon](https://peon.sh/), an open-source self-hosted PaaS.
