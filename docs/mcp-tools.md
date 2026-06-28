# MCP Tool Surface

## Tool Design Rules

- Tools operate on configured vault ids and vault-relative paths.
- Tools return bounded results with explicit truncation metadata.
- Write tools return summaries and file metadata, not large raw diffs by default.
- Responses identify note content as untrusted input for the AI client.

## V1 Tools

### `health_check`

Checks gateway, agent, and vault availability.

### `list_vaults`

Lists vaults configured for the authenticated user and active agent.

### `search_notes`

Searches Markdown notes by query, path, title, tags, properties, and body. Results include path, title, frontmatter summary, snippets, and score.

### `read_note`

Reads one note by vault-relative path. Supports optional frontmatter-only and excerpt modes.

### `create_note`

Creates a Markdown note with optional frontmatter. Rejects existing paths unless explicit overwrite semantics are later added.

### `update_note`

Updates an existing note using optimistic concurrency through file hash or mtime.

### `append_to_note`

Appends a lifecycle entry or section content to an existing note.

### `create_ai_thread_note`

Creates a structured AI thread note with problem, context, decisions, implementation summary, verification, outcome, follow-ups, and related links.

### `create_solution_note`

Creates a reusable solution note with symptoms, root cause, solution pattern, verification, known limits, and related threads.

### `mark_superseded`

Marks an older note as superseded, links it to a newer note, and updates the newer note's supersedes metadata.

## Error Semantics

- `AGENT_OFFLINE`: no active local agent for the selected vault.
- `VAULT_NOT_FOUND`: requested vault is not registered.
- `PATH_OUTSIDE_VAULT`: path failed safety validation.
- `PERMISSION_DENIED`: tool violates configured permission mode.
- `CONFLICT`: optimistic concurrency check failed.
- `CONTENT_REJECTED`: content failed policy or secret-like safety checks.
