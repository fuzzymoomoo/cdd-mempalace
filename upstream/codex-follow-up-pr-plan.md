# Codex Follow-Up PR Plan

This document captures the planned follow-up pull request for MemPalace issue #295.

Issue:

- https://github.com/milla-jovovich/mempalace/issues/295

## Goal

Improve Codex JSONL normalization quality in a test-first way.

The follow-up PR should make Codex conversation mining more reliable without guessing at behavior that has not been proven by fixtures.

## Guiding Rule

Do not start by changing parser behavior.

Start by:

1. collecting representative Codex JSONL fixtures
2. writing normalization tests
3. changing parser logic only where the tests prove a gap

That keeps the PR small, credible, and easier to merge.

## Proposed PR Shape

### Phase 1: Fixtures And Tests

Add Codex-specific fixtures and tests that cover the parser behavior already discussed in issue #295.

Best first target:

- expand `tests/test_normalize.py`

Possible supporting layout if upstream prefers fixtures:

- `tests/fixtures/codex/`

### Phase 2: Parser Adjustment

Only after the tests exist:

- adjust `_try_codex_jsonl()` in `mempalace/normalize.py`
- keep changes bounded to Codex handling only
- avoid touching other normalization paths unless a shared helper clearly improves things

## Initial Test Matrix

The first PR should aim to cover these cases.

### 1. Happy Path

Session includes:

- `session_meta`
- `event_msg` with `user_message`
- `event_msg` with `agent_message`

Expected:

- normalized transcript contains alternating `>` user turns and assistant responses

### 2. Ignore Non-Conversation Noise

Session includes:

- `session_meta`
- `response_item`
- other event types
- valid `event_msg` turns

Expected:

- ignored structures do not pollute the transcript
- valid user and assistant turns still survive

### 3. Missing `session_meta`

Session includes:

- valid `event_msg` turns
- no `session_meta`

Expected:

- current behavior is captured explicitly
- if maintainers want this to normalize anyway, the test becomes the basis for the parser change

### 4. Empty Or Partial Messages

Session includes:

- empty `message`
- unknown `payload.type`
- malformed lines mixed with valid JSONL

Expected:

- parser skips bad lines cleanly
- valid conversation turns still normalize

### 5. Multi-Turn Session

Session includes several alternating user and assistant turns.

Expected:

- transcript preserves order
- multiple `>` user turns are emitted correctly

### 6. Real-World Noisy Session Shape

Use a sanitized fixture based on a real Codex session shape that motivated issue #295.

Expected:

- the normalized transcript is clean enough to feed `convo_miner.py`

This is probably the highest-value fixture in the PR.

## Decision Points To Resolve In The PR

These should be answered by fixtures and maintainer feedback, not assumption.

### Should `session_meta` remain required?

Current parser requires it.

The PR should either:

- preserve that rule and test it explicitly

or

- relax it if fixture-backed evidence shows good Codex sessions can be valid without it

### Should any `response_item` content be kept?

Current parser drops all `response_item` entries.

The default assumption should remain:

- skip them

Unless fixtures show that a useful conversational turn only exists there and not in `event_msg`.

### Should transcript cleanup be stricter?

Possible cleanup improvements:

- collapse duplicate turns
- trim empty lines more aggressively
- drop obvious synthetic/system noise

Only add these if a real fixture proves the need.

## What The PR Should Not Do

- do not redesign all normalization logic
- do not broaden scope to Claude/ChatGPT/Slack normalization
- do not convert one issue into a large refactor
- do not include private or unsanitized session data

## Best Commit Strategy

Prefer 2 commits if the change grows:

1. `test: add Codex normalization fixtures and coverage`
2. `fix: improve Codex JSONL normalization`

If the parser change is tiny, one combined PR is still fine.

## Success Criteria

The follow-up PR is successful if:

- Codex normalization has explicit test coverage
- at least one real-world noisy session shape is represented safely
- any parser change is justified by fixture-backed behavior
- maintainers can review it as a focused improvement, not a speculative rewrite

## Suggested Branch Name

- `fix/codex-normalization-coverage`

## Suggested PR Title

- `test: add Codex normalization coverage`

or, if parser logic changes too:

- `fix: improve Codex JSONL normalization coverage and cleanup`
