# Sharing one MCP server across a team: authentication and scoping

Running one MCP server per developer laptop does not scale and spreads credentials everywhere. A shared server is cleaner, if you add identity.

## Authentication

Put the server behind HTTPS and require a per-user token or OAuth. Avoid one shared bearer token, because you cannot tell who did what or revoke one person.

## Scoping tools

Map users or groups to tool sets. A typical split:

- Everyone: read-only tools such as listing services and reading logs.
- On-call engineers: restart and rollback.
- Admins: anything that creates or deletes resources.

## Logging

Record each tool call with user, tool name, arguments and result status. Ship it to the same place as your other audit logs.

## Secrets

The MCP server holds the credentials to downstream systems, not the users. That way tokens never sit in each person's editor config.

## Rate limits

Agents can loop. Put per-user rate limits on write tools.

A deployment guide to [self-host an MCP server for your team](https://peon.sh/blogs/self-host-mcp-server-for-team) covers the container setup. Notes by a contributor to [Peon](https://peon.sh/), an open-source self-hosted deployment platform.
