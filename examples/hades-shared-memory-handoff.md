# Hades Shared-Memory Handoff Case Study

This case study captures a real shared-memory handoff flow between Codex and Claude while planning the next phase of `alexandria-hades`.

It is intentionally richer than the upstream-friendly example because it preserves the CDD framing, the Hades architecture implications, and the lessons learned from actually running the workflow.

## Scenario

The goal was to review the latest Hades and CDD planning direction, produce one authoritative Hades master plan, and then hand off into implementation.

The work moved across actors in series:

1. Codex prepared a Hades review handoff capsule
2. Claude started from a cold session, used MemPalace first, and validated the cited source files
3. Claude produced `hades-master-plan.md` plus a Wave 1 implementation handoff
4. Codex reviewed the result, cleaned the durable artifacts, refreshed shared memory, and packaged the workflow as a reusable example

## Durable artifacts used

- `alexandria-hades/docs/hades-master-plan.md`
- `alexandria-hades/docs/handoffs/2026-04-09-1040-hades-master-plan-review-handoff.md`
- `alexandria-hades/docs/handoffs/2026-04-09-1230-hades-wave1-implementation-handoff.md`
- `cdd/plan/hades-memory-provider-spec.md`
- `cdd/plan/implementation-phases.md`
- `cdd/plan/shared-memory-operating-model.md`
- `cdd/plan/llm-human-handoff-protocol.md`
- dashboard planning docs

## What worked well

- The incoming actor did not need the previous full chat transcript to become useful
- MemPalace retrieval plus named authoritative files gave a good cold-start surface
- The resulting master plan was materially useful, not just a summary
- The Wave 1 implementation handoff was bounded, actionable, and source-linked
- The workflow produced both working-memory artifacts and durable planning artifacts

## Gaps we found

The workflow also exposed some important operational rules:

1. The refresh step must be explicit
   Writing the master plan and handoff was not enough. The latest durable artifacts needed a MemPalace refresh before another cold-start actor could reliably retrieve them.

2. ASCII-safe durable metadata matters
   Smart punctuation and encoding drift leaked into knowledge graph facts and some generated docs. That made later cleanup harder than it needed to be.

3. Graceful degradation should be explicit, not vague
   A handoff line that implied "null or empty, never errors" was too loose for the `MemoryProvider` contract. Structured unavailable results are better than silent empties.

4. Shared-memory actions need a common name
   The team was saying "run the workflow," but the workflow itself had become specific enough to deserve a reusable term.

## The reusable term

CDD now calls the standard cross-actor memory workflow a:

`continuity cycle`

A continuity cycle means:

1. save durable artifacts in indexed paths
2. create or update the handoff capsule
3. refresh shared memory if durable context changed
4. let the next actor start with a wake-up pass against the refreshed memory surface

This gives humans, Claude, Codex, and later Hades one shared action phrase.

## Why this matters for CDD

CDD is trying to make human-plus-agent collaboration durable and governable, not just convenient in one chat window.

This case study matters because it demonstrates:

- shared memory as a real continuity substrate
- explicit handoffs as a first-class collaboration artifact
- retrieval plus validation as a better cold-start pattern than transcript dumping
- a practical bridge from methodology to actual project work

## Why this matters for Hades

The outcome was not just a successful handoff. It also produced an authoritative plan for:

- Phase 9 retrieval-driven context assembly
- the `MemoryProvider` runtime adapter
- dashboard convergence
- context isolation and cardinality safety
- stage-aware retrieval profiles

That makes this a useful example of how shared memory can support real architecture and implementation planning, not just note storage.

## Recommended future use

This pattern is worth repeating whenever:

- a long-running design or implementation effort changes actors
- token or rate limits force a switch
- the next step depends on preserving decisions and source references
- a repo needs resumable work across humans and multiple LLMs

## Related bridge work

- [upstream/software-engineering-memory-example.md](../upstream/software-engineering-memory-example.md)
- MemPalace PR #285
- MemPalace issue #295
- MemPalace PR #334
