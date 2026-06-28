# Security Model

## Core Security Principle

The gateway routes access; the local agent owns vault access. The gateway must not become a silent note database or broad filesystem proxy.

## Threats

- Malicious MCP client attempts unauthorized reads or writes.
- Prompt injection in notes instructs the model to exfiltrate data.
- Path traversal attempts escape the configured vault root.
- Symlinks point outside the vault.
- Pairing tokens are replayed.
- Client or agent tokens leak.
- Gateway compromise exposes metadata or active routes.
- Agent impersonation routes requests to the wrong machine.

## Guardrails

- All file paths are vault-relative.
- Absolute paths from MCP clients are rejected.
- Path traversal is rejected before filesystem access.
- Symlink targets must stay inside the configured vault root.
- Write operations use permission modes and optional confirmation.
- Pairing tokens are single-use and short-lived.
- Stored tokens are hashed.
- Logs contain metadata and summaries only, never full note bodies.
- Request body sizes are bounded.
- Offline agents fail closed.
- Note contents returned to AI clients are treated as untrusted data.

## Permission Modes

- `read-only`: search and read only.
- `read-write-confirmed`: writes require user or client confirmation when supported.
- `read-write-auto`: writes are allowed without confirmation, intended only for trusted self-host deployments.

## Audit Events

Audit events include timestamp, user, vault id, agent id, tool name, success/failure, target vault-relative path, response size, and a human-readable summary. They do not include note bodies, secrets, or raw prompts.

## Required Security Tests

- Unauthorized client is denied.
- Wrong user cannot access another agent.
- Path traversal fails.
- Symlink escape fails.
- Offline agent returns a safe error.
- Secret-like writes are blocked or require explicit override.
- Gateway logs do not include note bodies.
