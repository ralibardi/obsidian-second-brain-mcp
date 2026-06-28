# PRD: Obsidian Second Brain MCP

## Summary

Obsidian Second Brain MCP lets users connect AI clients to their own Obsidian vault through a self-deployable remote MCP gateway and local vault agent. It is designed for people who use Obsidian as a durable knowledge base and want AI assistants to retrieve, update, and maintain structured notes without handing vault custody to a third-party SaaS.

## Problem

Normal ChatGPT and mobile AI clients cannot directly read and write a local Obsidian vault. Local MCP servers work for desktop agents, but they are not reachable by mobile ChatGPT. Users need a safe bridge that exposes MCP remotely while keeping the vault on their own machine or synced storage.

## Users

- Individual Obsidian users who want their second brain available to ChatGPT/mobile.
- Developers using Codex, Claude, ChatGPT, and other AI agents across many projects.
- Privacy-conscious self-hosters who want remote access without managed SaaS custody.

## Goals

- Provide a generic MCP interface for any Obsidian vault.
- Support remote AI clients through HTTPS.
- Keep note storage and vault indexing local-first.
- Provide safe write tools for AI thread notes, solution notes, and supersession workflows.
- Make the system self-deployable with clear setup and diagnostics.

## Non-goals

- Public SaaS billing.
- Multi-team organizations and seat management.
- Cloud-hosted note indexing.
- Requiring Obsidian desktop plugins.
- Replacing Obsidian Sync, Git, iCloud, Dropbox, or other sync systems.

## Success Criteria

- A user can deploy the gateway and pair a local agent.
- An MCP client can search, read, create, update, append, and supersede notes in a fixture vault.
- ChatGPT/mobile can reach the gateway when it is deployed behind HTTPS.
- Gateway logs do not persist note bodies.
- Write operations cannot escape configured vault roots.
- Documentation is sufficient for a new user to install and validate the flow.

## V1 Defaults

- Self-deployable gateway.
- Local vault agent with outbound-only connection to gateway.
- Markdown source of truth.
- SQLite for gateway metadata.
- Write permission mode defaults to `read-write-confirmed`.
- No cloud note body persistence.
