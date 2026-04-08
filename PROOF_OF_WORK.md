# Proof Of Work

This file tracks the public work that makes the CDD and MemPalace connection credible.

The standard is simple:

- useful bridge work
- tested findings
- visible upstream contribution

## Status

Current stage: first upstream PR opened

The bridge repo now has a live upstream contribution trail.

## Planned Proof Points

- upstream pull requests
- upstream issues with reproducible findings
- bridge docs and examples
- retrieval experiments
- notes on what worked and what failed

## Upstream Contributions

### MemPalace PR #285

- title: `docs: add software engineering memory example`
- link: https://github.com/milla-jovovich/mempalace/pull/285
- type: docs/example pull request
- source: bridge-repo work
- summary:
  Adds a software-engineering-focused example showing how MemPalace can be used to organize decisions, incidents, handoffs, and stage-aware retrieval in long-running project work.
- draft materials:
  [upstream/first-pr-plan.md](upstream/first-pr-plan.md),
  [upstream/software-engineering-memory-example.md](upstream/software-engineering-memory-example.md),
  [upstream/first-pr-description.md](upstream/first-pr-description.md),
  [upstream/open-first-pr-workflow.md](upstream/open-first-pr-workflow.md)
- validation note:
  Local test execution produced `115 passed, 2 failed`; the failures appeared unrelated to the docs change and looked like Windows file-lock cleanup issues in existing ChromaDB-backed tests.

### Next Planned Contribution

- target: MemPalace upstream
- type: technical issue and follow-up PR
- topic: Codex session transcript normalization and import quality

## Bridge Experiments

None logged yet.

This section should later capture:

- experiment name
- repo or scenario
- memory structure used
- retrieval outcome
- useful lesson

## Example Integrations

### Software Engineering Memory Example

- what it demonstrates:
  MemPalace as a structured memory layer for software engineering artifacts such as decisions, incidents, handoffs, and validation notes.
- where to find it:
  upstream PR #285 and the local source draft at [upstream/software-engineering-memory-example.md](upstream/software-engineering-memory-example.md)

## Contribution Standard

The goal is not to look adjacent to MemPalace.

The goal is to become a contributor to the ecosystem by making structured memory more practical for real software engineering work.
