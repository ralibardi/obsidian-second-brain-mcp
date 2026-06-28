# Implementation Phases

## Phase 0: Repository Bootstrap

Create the public repository, clone it locally, add documentation, and commit the product plan.

## Phase 1: Product And Technical Design

Finalize PRD, architecture, tool surface, security model, prompts, and deployment model.

## Phase 2: Monorepo Scaffold

Create a TypeScript pnpm workspace with `apps/gateway`, `apps/agent`, `packages/vault-core`, `packages/mcp-contracts`, `packages/auth`, `packages/cli`, and `fixtures/vault-basic`.

## Phase 3: Vault Core

Implement local Markdown operations, path safety, frontmatter preservation, search, create/update/append, AI thread notes, solution notes, and supersession.

## Phase 4: Local Vault Agent

Implement the local daemon, setup CLI, vault registration, outbound gateway connection, permission modes, and diagnostics.

## Phase 5: Remote MCP Gateway

Implement Streamable HTTP MCP endpoint, gateway-agent routing, auth, SQLite metadata, and the v1 MCP tools.

## Phase 6: ChatGPT And Mobile Compatibility

Document HTTPS requirements, client setup, tool descriptions, privacy disclosures, and mobile usage expectations.

## Phase 7: Security Hardening

Add threat model coverage, rate limits, token rotation, audit safety, request limits, and adversarial tests.

## Phase 8: Packaging And Distribution

Publish npm packages, Docker image, Docker Compose, deployment templates, and upgrade docs.

## Phase 9: Testing And Evaluation

Add unit, integration, e2e, and prompt eval suites. CI must verify the fixture vault workflow and security invariants.

## Phase 10: Documentation And Initial Release

Complete quickstart, troubleshooting, examples, release notes, and tag `v0.1.0` once acceptance criteria are met.
