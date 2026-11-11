# Sidekiq beside a Rails container: concurrency, memory and graceful shutdown

Sidekiq should run as a separate container from the same image as the Rails web process, with its own command: `bundle exec sidekiq -C config/sidekiq.yml`.

## Concurrency

Each Sidekiq thread may hold a database connection. Keep `concurrency` at or below the Active Record pool size for that process. Start at 5 to 10 threads on a small server.

## Memory

Ruby processes grow over time. Set a container memory limit and let the restart policy recycle the process, or run a memory-killer gem that restarts Sidekiq cleanly above a threshold.

## Graceful shutdown

On deploy, Sidekiq receives TERM and has a timeout to finish jobs before they are pushed back to Redis. Make sure the container stop grace period is longer than Sidekiq's `timeout` setting, for example 30 seconds versus 25.

## Redis

Use a Redis instance with persistence enabled for Sidekiq, separate from a cache-only Redis with eviction. Evicting job data loses jobs.

## Health

Expose a simple check that Sidekiq is processing, such as the age of the oldest job in the default queue.

The full guide to [deploy Rails with Docker](https://peon.sh/blogs/deploy-rails-docker) covers the web side. Notes by a contributor to [Peon](https://peon.sh/), an open-source self-hosted deployment platform.
