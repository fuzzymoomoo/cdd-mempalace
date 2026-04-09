# Proposed MemPalace PR: `docs: add worked cdd workflow example for engineering memory`

This PR adds a small, copyable `examples/cdd-workflow/` pack for people who want to use MemPalace for software engineering memory.

## What is included

- `examples/cdd-workflow/README.md`
- `examples/cdd-workflow/mempalace.yaml`
- a sample decision record
- a sample planning context bundle
- a sample handoff capsule

## Why this shape

- it keeps the example practical and repo-local
- it shows how durable artifacts can be mined and retrieved by stage
- it gives users a concrete handoff format for human-to-agent or agent-to-agent continuity
- it stays MemPalace-first and copyable even if people are not using the broader CDD methodology

## Also included

- a small root README link so the worked example is easier to discover

## Validation

- mined the example locally into a disposable palace with `mempalace --palace <temp> mine .`
- verified retrieval with `mempalace --palace <temp> search "postgresql" --room decisions`
- in plain Windows PowerShell, the CLI banner required forced UTF-8 output because of an existing console encoding issue, but the example content itself mined cleanly

## Context

This is intended to answer the request in MemPalace issue #301 for an upstream-friendly `examples/cdd-workflow/` example pack.
