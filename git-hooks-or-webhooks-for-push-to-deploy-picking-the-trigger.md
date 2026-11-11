# Git hooks or webhooks for push to deploy: picking the trigger

Push to deploy needs something to notice the push. There are two common triggers.

## Server-side Git hook

You push to a bare repository on the server, and a `post-receive` hook checks out the code and rebuilds.

- Pros: no third party, works offline from GitHub, simple to understand.
- Cons: the server must accept SSH pushes from every developer, and the deploy logic lives in a shell script that is easy to break.

## Webhook from the Git host

You push to GitHub, GitLab or Forgejo, which sends a signed HTTP request to your server. A small service verifies the signature and starts the deploy.

- Pros: code review and CI happen before deploy, developers do not need server access.
- Cons: you need a public endpoint and must verify the signature correctly.

## My default

Webhook, with signature checks, a deploy queue so two pushes do not build at once, and a branch filter so only `main` deploys to production.

A full walkthrough of [git push to deploy on your own server](https://peon.sh/blogs/git-push-to-deploy-own-server) builds both. Written by a contributor to [Peon](https://peon.sh/), an open-source self-hosted PaaS.
