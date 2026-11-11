# Sizing a VPS for remote AI-assisted coding sessions

When an AI coding tool runs builds and tests for you, the dev server does more work than a human typing would. Sizing it right keeps sessions fast.

## What uses resources

- The language server and editor backend: 1 to 2 GB on a large TypeScript or Java project.
- Repeated test runs and builds triggered by the agent. These are CPU bound.
- Local services such as Postgres and Redis in containers: 500 MB to 1 GB.
- Docker image builds, which need disk and RAM in bursts.

## Starting points

- Small web app: 2 vCPU, 4 GB RAM, 40 GB disk.
- Full-stack monorepo: 4 vCPU, 8 GB RAM, 80 GB disk.
- Heavy compile workloads: dedicated vCPU plans, since shared CPU slows down when neighbours are busy.

## Keep costs down

Shut the server down or snapshot and destroy it between work sessions, and prune Docker build cache weekly. Keep production credentials off the box.

A comparison of running [Cursor on a VPS or managed cloud](https://peon.sh/blogs/cursor-vps-managed-cloud) weighs the options. Written by a contributor to [Peon](https://peon.sh/), an open-source self-hosted PaaS.
