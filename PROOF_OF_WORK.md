# Proof Of Work

This file tracks the public work that makes the CDD and MemPalace connection credible.

The standard is simple:

- useful bridge work
- tested findings
- visible upstream contribution

## Status

Current stage: four upstream PRs opened

The bridge repo now has a visible upstream contribution trail across docs, fixes, and test coverage work.

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

### MemPalace PR #286

- title: `fix: close ChromaDB clients before cleanup to prevent PermissionError on Windows`
- link: https://github.com/milla-jovovich/mempalace/pull/286
- type: bug fix / test reliability pull request
- source: real Windows test execution findings
- summary:
  Fixes Windows cleanup failures caused by open ChromaDB handles, adds explicit client closing in teardown paths, and adds Windows CI coverage for the regression.
- related issue:
  https://github.com/milla-jovovich/mempalace/issues/275

### MemPalace PR #289

- title: `test: add full test suite for palace_graph.py (37 tests)`
- link: https://github.com/milla-jovovich/mempalace/pull/289
- type: test coverage pull request
- source: bridge-repo contribution streak
- summary:
  Adds broad coverage for palace graph traversal, tunnel detection, graph stats, and fuzzy room matching, while keeping Windows cleanup behavior safe in the test fixtures.

### MemPalace PR #291

- title: `test: add full test suite for general_extractor.py (59 tests)`
- link: https://github.com/milla-jovovich/mempalace/pull/291
- type: test coverage pull request
- source: bridge-repo contribution streak
- summary:
  Adds broad coverage for the general extractor layer, including memory-type extraction, segmentation, prose extraction, sentiment and resolution detection, and confidence filtering behavior.

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

## Community Positioning

The next public step should be contribution-led community participation.

That means:

- mention the work after the PRs exist
- lead with useful contributions, not brand claims
- talk about what was contributed and what was learned
- let CDD enter the conversation as the reason this bridge work exists

See [community/discord-positioning.md](community/discord-positioning.md).

## Contribution Standard

The goal is not to look adjacent to MemPalace.

The goal is to become a contributor to the ecosystem by making structured memory more practical for real software engineering work.
