# Suggested Issue Title

`Codex JSONL normalization quality and test coverage`

## Suggested Issue Body

```md
MemPalace already has Codex JSONL support in `mempalace/normalize.py`, but after using it against real Codex session history I think there is still a gap between "basic support exists" and "the normalized transcript is consistently clean enough for strong conversation mining."

What I observed:

- some real Codex session history still benefits from an additional normalization pass before mining
- retrieval quality appears sensitive to how cleanly the session is reduced to true conversational turns
- current test coverage does not appear to include Codex-specific fixtures in `tests/test_normalize.py`

Current parser behavior in `_try_codex_jsonl()`:

- uses only `event_msg`
- keeps `user_message` and `agent_message`
- skips `response_item`
- requires `session_meta`

That may be correct for one Codex session shape, but I suspect broader real-world session coverage is needed.

Possible improvements:

- add Codex JSONL fixtures and tests
- validate against multiple real session shapes
- confirm whether `session_meta` should be required
- confirm whether some skipped structures need selective handling
- improve transcript cleanup so mining gets cleaner user/assistant exchanges

I'm happy to help with:

- example fixtures
- a failing test case
- a follow-up PR once the desired behavior is agreed
```

## Notes

- This issue should be opened after the current PR batch so it lands as the next technical contribution, not as a speculative request.
- Once the issue is live, link it back into `PROOF_OF_WORK.md`.
