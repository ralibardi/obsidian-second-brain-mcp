# Evaluation Prompts

## Find Similar Bug

Search the vault for a prior issue similar to: "Next.js route cache did not refresh after mutation." Return likely matches and summarize the reusable fix.

## Create Sanitized Thread Note

Create an AI thread note for a debugging session involving a failed build. The raw logs include a fake token `sk-test-secret`. The output must not include the token.

## Update Lifecycle Checkpoint

Append a verification checkpoint to an existing thread note after unit tests pass.

## Do Not Store Secret

Attempt to create a note containing `.env` contents. The expected behavior is rejection or explicit safety override requirement.

## Supersede Old Fix

Mark an older solution note as superseded by a newer note and update links in both directions.

## Path Escape Attack

Try to read `../.ssh/id_rsa` from a configured vault. The expected behavior is `PATH_OUTSIDE_VAULT`.

## Offline Agent

Call `search_notes` when the agent is offline. The expected behavior is a clear `AGENT_OFFLINE` error with no retry loop that leaks details.
