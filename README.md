# Compose ops notes

Short, practical notes on running containerized apps and their supporting services on your own servers, written by a contributor to [Peon](https://peon.sh/), an open-source self-hosted deployment platform.

- [Uptime Kuma alert fatigue: tuning retries, intervals and groups](uptime-kuma-alert-fatigue-tuning-retries-intervals-and-groups.md): Settings that stop Uptime Kuma from paging you for every blip while still catching real outages.
- [Moving existing uploads from AWS S3 to self-hosted object storage with rclone](moving-existing-uploads-from-aws-s3-to-self-hosted-object-storage-with.md): A step by step copy plan for migrating an app bucket from AWS S3 to a self-hosted S3-compatible server.
- [Sharing one MCP server across a team: authentication and scoping](sharing-one-mcp-server-across-a-team-authentication-and-scoping.md): How to run a single MCP server for several people without giving everyone the same powers.
- [Git hooks or webhooks for push to deploy: picking the trigger](git-hooks-or-webhooks-for-push-to-deploy-picking-the-trigger.md): Comparing a server-side Git hook with a webhook from a Git host as the trigger for deploys to your own server.
- [Cache headers for a static site served from your own server](cache-headers-for-a-static-site-served-from-your-own-server.md): Which Cache-Control values to use for HTML, hashed assets and images on a self-hosted static site.
- [Sizing a VPS for remote AI-assisted coding sessions](sizing-a-vps-for-remote-ai-assisted-coding-sessions.md): How much CPU, memory and disk a remote dev server needs when an AI coding tool is building and testing your project.
- [Sidekiq beside a Rails container: concurrency, memory and graceful shutdown](sidekiq-beside-a-rails-container-concurrency-memory-and-graceful-shutd.md): Running Sidekiq as its own container next to a Rails app, with settings that avoid lost jobs and memory creep.
- [Moving Netlify Functions into a container: a migration note](moving-netlify-functions-into-a-container-a-migration-note.md): How to port Netlify Functions to a small container service when you self-host the rest of the site.

Licensed CC BY 4.0.
