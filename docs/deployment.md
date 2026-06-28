# Deployment

## V1 Deployment Model

V1 is self-deployable. A user deploys their own gateway and runs their own local vault agent. This avoids managed SaaS custody and keeps the system usable for privacy-conscious users.

## Gateway Requirements

- Public HTTPS URL for ChatGPT/mobile and other remote MCP clients.
- Persistent SQLite volume.
- Secret environment variables for setup token and signing keys.
- WebSocket support for local agent tunnels.

## Local Development

Planned command:

```bash
pnpm dev
```

Planned services:

- gateway on local HTTP port;
- agent connected to gateway;
- fixture vault for e2e tests.

## Docker Compose

Docker Compose will run the gateway and a test fixture agent. Real local agents should normally run on the user machine, not inside the gateway container.

## Deployment Targets

- Docker on a VPS.
- Fly.io.
- Railway.
- Render.
- Cloudflare-compatible notes if the websocket and MCP transport constraints fit.

## ChatGPT/Mobile Notes

ChatGPT mobile cannot reach a private localhost MCP server. Users need a reachable HTTPS gateway and an agent connected from the machine that has vault access.
