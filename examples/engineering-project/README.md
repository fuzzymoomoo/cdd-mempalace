# Example: Engineering Project Memory

This example shows a real CDD project memory layout for a software engineering team.

It is intentionally small. The goal is to show the structure clearly, not to be exhaustive.

## How to use this

1. Copy `mempalace.yaml` into the root of your project repository.
2. Run `mempalace mine .` to index your project notes, decision records, and docs.
3. Use `mempalace search` or the MCP tools to retrieve the right context at each stage.

## What is in this example

```
mempalace.yaml                         ← palace structure for this project
decisions/
  use-postgresql.md                    ← architecture decision record (ADR)
context-bundles/
  sprint-2-planning.md                 ← assembled context for a planning session
```

## The mempalace.yaml structure

The rooms map to CDD stages and artifact types:

| Room | What goes in it |
|------|----------------|
| `decisions` | Architecture decisions, tradeoffs, rejected approaches |
| `implementation` | Active notes, code patterns, handoff capsules |
| `incidents` | Bug post-mortems, root cause analysis, workarounds |
| `planning` | Sprint context bundles, goals, constraints |
| `validation` | Acceptance criteria, release checklists, failure modes |

## Stage-aware retrieval

The value of this structure is that you retrieve different rooms at different stages.

**At planning:**
- retrieve `decisions` to surface prior choices and constraints
- retrieve `incidents` to surface known failure modes
- retrieve `planning` to find comparable prior sprint context

**At implementation:**
- retrieve `implementation` for active handoff notes and patterns
- retrieve `decisions` when touching areas that had prior tradeoffs

**At validation:**
- retrieve `validation` for acceptance criteria and release checks
- retrieve `incidents` for known failure modes to re-verify

## What CDD adds

CDD treats this retrieval pattern as a first-class part of the delivery process,
not an afterthought. Context assembly is structured and stage-aware rather than
"paste the whole chat and hope."

MemPalace provides the storage and retrieval layer. CDD provides the discipline
for what to store, when to retrieve, and how to validate that the output was
actually grounded in the right context.

See [MAPPING.md](../../MAPPING.md) for the full CDD-to-MemPalace mapping.
