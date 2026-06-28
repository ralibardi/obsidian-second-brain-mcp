# Architecture

## Chosen Architecture

The system uses a hosted MCP gateway plus a local vault agent. The first release is self-deployable, but the components are shaped so a managed SaaS gateway can be added later without rewriting vault logic.

```text
MCP Client
(ChatGPT / Codex / Claude)
        |
        | HTTPS Streamable HTTP MCP
        v
Gateway
(auth, tool schemas, routing, audit metadata)
        |
        | outbound tunnel from agent
        v
Local Vault Agent
(vault validation, Markdown tools, permission checks)
        |
        v
Obsidian Vault
(Markdown source of truth)
```

## Components

### Gateway

The gateway exposes the remote MCP endpoint. It authenticates clients, maps sessions to paired vault agents, forwards tool calls, and records metadata-only audit events. It must not persist note bodies by default.

### Local Vault Agent

The local agent runs on the user's machine. It connects outbound to the gateway, validates configured vault roots, enforces permissions, and executes read/write operations via the shared vault core.

### Vault Core

Vault core is a reusable library for path-safe Markdown operations. It parses and preserves YAML frontmatter, validates vault-relative paths, searches notes, renders templates, updates notes with optimistic concurrency, and applies supersession links.

### MCP Contracts

MCP contracts define tool names, descriptions, request schemas, response schemas, and error semantics. Gateway and agent share these contracts to prevent schema drift.

## Data Flow

1. AI client calls a tool on the gateway MCP endpoint.
2. Gateway authenticates the client token or OAuth session.
3. Gateway resolves the requested user, vault, and active agent connection.
4. Gateway forwards the validated tool request to the local agent.
5. Agent validates permissions and vault-relative paths.
6. Agent executes the vault operation locally.
7. Agent returns a bounded response to the gateway.
8. Gateway returns the MCP response to the AI client and stores metadata-only audit details.

## Persistence

Gateway persistence is SQLite in v1 and stores users, agents, vault registrations, token hashes, pairing state, sessions, and audit metadata. Local agent persistence stores local config and vault registrations under the user config directory. Obsidian notes remain in the user's vault.

## Deployment Shape

The gateway is distributed as Docker and a Node service. The agent is distributed as an npm package with a CLI and later can be wrapped as a desktop app or Homebrew package.
