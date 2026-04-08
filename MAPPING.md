# CDD To MemPalace Mapping

This document captures the first recommended mapping between CDD concepts and MemPalace structure.

The purpose is not to force CDD to depend on one memory layer. The purpose is to define a clear bridge for one strong local-first memory substrate.

## Design Principles

- keep the mapping understandable to humans
- keep retrieval scopes explicit
- preserve durable artifacts instead of reducing everything to summaries
- separate working memory from governed memory
- make provenance visible whenever retrieval feeds active work

## Core Structure Mapping

| CDD concept | MemPalace structure | Notes |
| --- | --- | --- |
| Product / major system / bounded context | Wing | Top-level memory domain |
| Knowledge class or subsystem area | Hall | Helps retrieval stay focused |
| Feature area / incident / decision cluster / task stream | Room | Main working memory unit |
| Raw durable artifacts | Drawers / stored materials | Source notes, docs, transcripts, code notes |

## Recommended Room Types

Use room naming to make intent visible:

- `feature-<slug>`
- `decision-<slug>`
- `incident-<slug>`
- `release-<slug>`
- `pattern-<slug>`
- `handoff-<slug>`

## Recommended Artifact Types

CDD artifacts that map well into durable memory:

- context bundles
- decision records
- provenance artifacts
- handoff capsules
- reusable patterns
- validation outputs
- architecture notes
- repo-local operational docs

## Working Memory vs Governed Memory

CDD should distinguish between:

- `ephemeral`
  Active chat or scratch thinking
- `working`
  Session summaries, handoff notes, active investigations
- `governed`
  Validated docs, accepted decisions, reusable patterns, approved outputs

The MemPalace bridge should favor `working` and `governed` material.

## Retrieval Guidance

Retrieval should be shaped by the current stage, not by generic search alone.

Examples:

- planning stage
  Retrieve prior decisions, constraints, comparable designs, and open risks.
- implementation stage
  Retrieve task-local notes, code conventions, validated examples, and handoff capsules.
- validation stage
  Retrieve expected outputs, acceptance criteria, prior incidents, and known failure modes.

## Provenance Expectations

When CDD work uses memory retrieved through this bridge, the provenance record should capture:

- source path or source identifier
- wing
- hall
- room
- timestamp if available
- retrieval mode
- which retrieved artifacts materially influenced the output

## Non-Goals

This mapping does not claim:

- that MemPalace is the whole CDD stack
- that CDD should depend exclusively on MemPalace
- that all chat history belongs in durable memory

The bridge exists to make one integration pattern clear, testable, and useful.
