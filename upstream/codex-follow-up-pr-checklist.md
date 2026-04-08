# Codex Follow-Up PR Checklist

Use this when resuming the Codex normalization follow-up work.

## Before Coding

- read issue #295:
  https://github.com/milla-jovovich/mempalace/issues/295
- re-read `mempalace/normalize.py`
- re-read `tests/test_normalize.py`
- check whether maintainers commented on the issue with preferences about scope

## Fixture Prep

- collect one or more sanitized Codex JSONL samples
- remove any private or identifying content
- preserve the structural shape that matters
- note which fixture motivated which expected behavior

## Test Plan

- add happy-path Codex normalization test
- add noisy-session Codex normalization test
- add missing-`session_meta` test
- add malformed-line / partial-message resilience test
- confirm expected transcript output precisely

## Implementation Guardrails

- keep changes scoped to Codex normalization
- avoid speculative handling of `response_item`
- do not weaken existing parsers for other formats
- prefer helpers only if they simplify the Codex path cleanly

## Validation

- run normalization tests
- run the broader MemPalace test suite if practical
- note any unrelated Windows-specific failures separately

## PR Packaging

- link back to issue #295
- explain which fixture shapes were added
- explain whether parser behavior changed or tests only were added
- keep the PR description focused on mining quality and coverage

## After Opening The PR

- log the PR in `PROOF_OF_WORK.md`
- update the bridge repo if maintainer feedback changes the plan
