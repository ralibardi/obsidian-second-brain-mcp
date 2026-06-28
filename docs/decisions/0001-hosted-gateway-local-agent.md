# ADR 0001: Hosted Gateway Plus Local Vault Agent

## Status

Accepted.

## Context

Normal ChatGPT/mobile needs a reachable remote MCP endpoint. A local-only MCP server can serve desktop tools but cannot be reached by mobile ChatGPT. Directly uploading or syncing note bodies to a managed service would undermine the privacy model.

## Decision

Use a remote MCP gateway plus a local vault agent. The gateway is self-deployable in v1 and exposes HTTPS MCP. The local agent connects outbound to the gateway and performs scoped vault operations on the user's machine.

## Consequences

- ChatGPT/mobile can connect through a public HTTPS gateway.
- Users do not need to expose their home machine directly.
- Vault contents remain local by default.
- The system needs pairing, tunnel routing, and offline-agent handling.
- A managed SaaS can be added later without rewriting vault-core logic.

## Alternatives Considered

### Local-only MCP

Simpler and safest, but does not satisfy ChatGPT/mobile remote access.

### Self-hosted single server with mounted vault

Simpler routing, but requires users to mount or sync their vault to a server and weakens the local-first model.

### Public SaaS first

Best onboarding, but requires billing, teams, abuse controls, and much stronger operational security from day one.
