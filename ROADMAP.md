# cdd-mempalace Roadmap

## Current Release

This repository starts as a docs-first bridge between CDD and MemPalace.

The immediate goal is to make the integration story clear and useful before building helper tooling around it.

## Track 1: Mapping And Shared Language

Near-term work:

- refine the CDD to MemPalace mapping
- define recommended room and artifact naming patterns
- document what belongs in working memory versus governed memory
- document provenance expectations for retrieved memory

Success looks like:

- the mapping is understandable without private context
- two contributors can organize a project similarly using the docs alone

## Track 2: Examples And Evaluation

Near-term work:

- publish one end-to-end engineering memory example
- publish handoff and retrieval examples
- capture retrieval findings and failed patterns
- evaluate what kinds of artifacts help most during planning and implementation

Success looks like:

- the repo contains concrete examples instead of only philosophy
- tradeoffs and limitations are visible, not hidden

## Track 3: Upstream Contribution Loop

Future work:

- contribute documentation improvements upstream
- contribute engineering-focused examples upstream where useful
- propose import or structure improvements backed by real findings
- link accepted contributions back into this repository

Success looks like:

- the bridge repo produces reusable value for the MemPalace ecosystem
- the relationship is based on contribution, not proximity

## Track 4: Helper Tooling

Later work may include:

- import and export helpers for project memory
- example MCP workflows
- repo-local conventions for durable engineering memory
- evaluation helpers for retrieval quality

Success looks like:

- tooling expresses the docs cleanly
- helpers stay understandable and portable

## Deliberate Non-Goals

- forking MemPalace as the main public artifact
- presenting this repo as official MemPalace work
- tying CDD permanently to one storage layer
- publishing private machine-local workflows as if they were general guidance
