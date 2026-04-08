# Codex Normalization Issue Plan

## Recommendation

Open this as a **normalization quality and test coverage** issue, not a "please add Codex support" issue.

Why:

- MemPalace already has Codex JSONL handling in `mempalace/normalize.py`
- the stronger claim is that real-world Codex session ingestion still appears noisy or incomplete in some cases
- there is no Codex-specific normalization coverage in `tests/test_normalize.py`

## Suggested Title

`Codex JSONL normalization quality and test coverage`

## Core Problem

Codex support exists in principle, but real Codex session histories can still benefit from an additional normalization pass before conversation mining.

That suggests a gap between:

- parser support exists

and

- parser coverage is broad enough for clean, durable mining across real session shapes

## Evidence To Mention

- `_try_codex_jsonl()` already exists in `mempalace/normalize.py`
- it only consumes `event_msg`
- it only keeps `user_message` and `agent_message`
- it requires `session_meta`
- it skips `response_item`
- `tests/test_normalize.py` does not currently include Codex fixtures or Codex-specific assertions
- in real-world Codex session mining, direct ingest can still produce noisy results compared with a one-way cleanup step first

## Best Outcome

A maintainer agrees the gap is real, and the next step becomes:

1. add Codex fixtures
2. add Codex normalization tests
3. improve parser behavior only where fixtures prove it is needed

## Tone

Keep it practical and collaborative:

- do not claim the current parser is wrong everywhere
- do not claim `response_item` must be included
- do not pretend one local sample proves the whole space

Instead:

- say real-world session coverage appears incomplete
- say transcript quality matters for mining quality
- offer to help with fixtures and a follow-up PR
