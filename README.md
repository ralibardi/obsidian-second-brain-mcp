# Obsidian Second Brain MCP

A self-deployable remote MCP bridge for connecting AI clients such as ChatGPT, Codex, Claude, and other MCP-capable tools to a user-owned Obsidian vault.

The system uses a hosted MCP gateway plus a local vault agent. The gateway is reachable by ChatGPT/mobile over HTTPS, while the local agent runs on the user's machine and performs scoped Markdown reads and writes against configured vault roots.

## Goals

- Let any user connect their own Obsidian vault to MCP-capable AI clients.
- Keep the Obsidian vault as the Markdown source of truth.
- Support ChatGPT/mobile through a reachable remote MCP gateway.
- Keep vault contents local by default; the gateway does not persist note bodies.
- Provide reusable tools for AI thread notes, solution notes, topic notes, and supersession history.

## Architecture

```text
AI Client / ChatGPT Mobile
        |
        | HTTPS Streamable HTTP MCP
        v
Remote MCP Gateway
        |
        | outbound agent tunnel
        v
Local Vault Agent
        |
        | scoped filesystem access
        v
User Obsidian Vault
```

## Initial Scope

This repository starts as a documentation-first bootstrap. The first implementation milestone is a TypeScript monorepo with:

- `apps/gateway` for the remote MCP gateway.
- `apps/agent` for the local vault agent.
- `packages/vault-core` for Markdown and path-safe vault operations.
- `packages/mcp-contracts` for shared tool schemas.
- `packages/auth` for pairing and token helpers.
- `packages/cli` for setup and diagnostics.

## Documentation

- [Product requirements](docs/prd.md)
- [Architecture](docs/architecture.md)
- [Implementation phases](docs/implementation-phases.md)
- [MCP tools](docs/mcp-tools.md)
- [Security model](docs/security.md)
- [Deployment](docs/deployment.md)
- [Local agent](docs/local-agent.md)
- [System prompt](docs/prompts/system-prompt.md)
- [Evaluation prompts](docs/prompts/eval-prompts.md)
- [ADR 0001](docs/decisions/0001-hosted-gateway-local-agent.md)

## License

MIT.
