# Local Vault Agent

## Purpose

The local vault agent runs on the user's machine and is the only component with filesystem access to Obsidian vaults.

## Responsibilities

- Register one or more vault roots.
- Validate vault paths and symlinks.
- Enforce permission mode.
- Execute Markdown reads and writes via vault core.
- Maintain outbound connection to gateway.
- Report health and diagnostics.

## Planned CLI

```bash
obsidian-mcp init
obsidian-mcp agent start
obsidian-mcp vault list
obsidian-mcp vault add
obsidian-mcp doctor
obsidian-mcp token revoke
```

## Init Inputs

- Gateway URL.
- Pairing token.
- Vault path.
- Vault display name.
- Permission mode.

## Permission Defaults

Default permission mode is `read-write-confirmed`. Users may choose `read-only` for safer retrieval-only use or `read-write-auto` for trusted self-hosted automation.

## Config Storage

The agent stores config in the platform user config directory. It must not store raw note contents or client prompts.
