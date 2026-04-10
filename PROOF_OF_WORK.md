# Proof Of Work

This file tracks the public work that makes the CDD and MemPalace connection credible.

The standard is simple:

- useful bridge work
- tested findings
- visible upstream contribution

## Status

Current stage: five upstream PRs, one technical issue, and a sixth upstream-ready docs branch prepared from maintainer feedback

The bridge repo now has a visible upstream contribution trail across docs, fixes, test coverage work, a Codex normalization follow-up PR drawn from real use, and a maintainer-requested example pack prepared for upstream.

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

### MemPalace Issue #295

- title: `Codex JSONL normalization quality and test coverage`
- link: https://github.com/milla-jovovich/mempalace/issues/295
- type: technical issue
- source: real Codex session mining findings
- summary:
  Raises a normalization-quality and test-coverage gap for Codex JSONL ingest, based on real session history where direct normalization still produced noisy transcripts for conversation mining.
- supporting drafts:
  [upstream/codex-normalization-issue-plan.md](upstream/codex-normalization-issue-plan.md),
  [upstream/codex-normalization-issue-body.md](upstream/codex-normalization-issue-body.md)

### MemPalace PR #334

- title: `fix: normalize incomplete Codex sessions and add coverage`
- link: https://github.com/milla-jovovich/mempalace/pull/334
- type: normalization fix / test coverage pull request
- source: follow-up work from issue #295
- summary:
  Adds Codex JSONL normalization coverage, locks in current behavior around ignored noise and `session_meta`, and fixes the incomplete-session case where real Codex user turns were falling back to raw JSONL.
- related issue:
  https://github.com/milla-jovovich/mempalace/issues/295
- planning docs:
  [upstream/codex-follow-up-pr-plan.md](upstream/codex-follow-up-pr-plan.md),
  [upstream/codex-follow-up-pr-checklist.md](upstream/codex-follow-up-pr-checklist.md)
- local validation note:
  `tests/test_normalize.py` passed locally with `7 passed`; the broader run with `tests/test_convo_miner.py` and `tests/test_miner.py` still hit unrelated Windows file-lock cleanup failures.
- CI checklist:
  `lint`, `test (3.9)`, `test (3.11)`, `test (3.13)`
- CI status note:
  required checks were still waiting to report when this record was updated on 2026-04-09

### MemPalace example pack requested in Issue #301

- issue:
  https://github.com/milla-jovovich/mempalace/issues/301#issuecomment-4215975119
- type:
  maintainer-requested docs/example follow-up
- status:
  upstream-ready branch prepared on fork
- branch:
  https://github.com/fuzzymoomoo/mempalace/tree/docs/cdd-workflow-example
- compare link:
  https://github.com/milla-jovovich/mempalace/compare/main...fuzzymoomoo:mempalace:docs/cdd-workflow-example?expand=1
- summary:
  Packages a worked `examples/cdd-workflow/` directory with a room layout, decision record, planning context bundle, and handoff capsule format so new users can copy a practical engineering-memory workflow.
- supporting drafts:
  [upstream/cdd-workflow-pr-description.md](upstream/cdd-workflow-pr-description.md),
  [upstream/issue-301-follow-up-comment.md](upstream/issue-301-follow-up-comment.md)
- validation note:
  The example pack was mined into a disposable palace locally and retrieval was verified with a room-filtered `postgresql` search against the decision record.

### Next Planned Contribution

- target: MemPalace upstream
- type: follow-up activity
- topic: respond to maintainer feedback and CI results on PR #334, then choose the next Codex-ingest or retrieval-quality improvement

## Bridge Experiments

### Hades Shared-Memory Handoff

- scenario:
  Codex prepared a review handoff, Claude cold-started from MemPalace plus authoritative files, produced the Hades master plan and a Wave 1 implementation handoff, and Codex then reviewed and normalized the durable outputs.
- artifacts:
  [examples/hades-shared-memory-handoff.md](examples/hades-shared-memory-handoff.md)
- retrieval outcome:
  The handoff flow was strong enough to produce a materially useful master plan without requiring the incoming actor to replay the full chat history.
- useful lesson:
  The refresh step has to be explicit. Writing the handoff is not enough; the next cold-start actor only benefits once the new durable artifacts are indexed. That lesson is now captured in the `continuity cycle` term.

### Multi-Agent Continuity Cycle Outline

- scenario:
  MemPalace issue #358 opened a concrete collaboration path: keep MemPalace as the memory substrate, let HexNest provide orchestration, and frame the joint example around explicit handoff plus cold-start resumption.
- artifacts:
  [examples/multi-agent-continuity-cycle-outline.md](examples/multi-agent-continuity-cycle-outline.md)
- useful lesson:
  The strongest next step is not a full distributed-memory design. It is a narrow example showing how orchestration and shared memory meet at the handoff boundary.

### Hades Four-Wave Delivery Experiment

- scenario:
  Four Hades implementation waves were delivered in series across Claude and Codex, with higher-context planning and lower-cost execution coordinated through MemPalace retrieval, handoff capsules, and explicit continuity cycles.
- artifacts:
  [examples/hades-four-wave-delivery-experiment.md](examples/hades-four-wave-delivery-experiment.md)
- observed result:
  The run reached Wave 4 before the first manual smoke pass without the usual between-wave correction loop, which was materially better than earlier transcript-only iteration patterns.
- useful lesson:
  Shared memory does not replace testing, but it can reduce rediscovery, tighten handoffs, and make mixed-cost multi-agent delivery noticeably more stable.

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
