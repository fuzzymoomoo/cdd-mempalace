# Hades Four-Wave Delivery Experiment

## Summary

This experiment tested whether shared memory, bounded handoffs, and an explicit continuity ritual could let multiple agents deliver several implementation waves in series without the usual correction churn between each step.

The result was promising.

Across four Hades implementation waves, work moved between Codex and Claude, with planning and review done by a higher-tier model and bounded implementation slices executed by a lower-cost model. The flow used MemPalace retrieval, repo-local handoff capsules, and an explicit `continuity cycle` between major steps.

Before the first manual smoke pass, the run reached Wave 4 without needing the normal between-wave bug-fix loop that had been common in earlier iterations.

## Setup

- project: `alexandria-hades`
- methodology context: CDD planning docs in the private `cdd` repo
- shared memory layer: MemPalace
- orchestration pattern: serial handoff between agents, not parallel delegation
- continuity primitive: durable artifacts + handoff capsule + refresh + cold-start wake-up

## Working Pattern

The delivery flow looked like this:

1. one agent produced or refined durable planning artifacts
2. those artifacts were stored in indexed repo paths
3. a handoff capsule named the current state, sources, decisions, and next bounded task
4. MemPalace was refreshed so the new state became retrievable
5. the next agent started cold from retrieval plus the authoritative files

That pattern is what we now call a `continuity cycle`.

## Waves Delivered

### Wave 1

Foundation work:

- created `memory-provider.js`
- created `dashboard-engine.js`
- refactored the dashboard provider to use the new engine
- consolidated duplicate `ContextAssembler` wiring

### Wave 2

Retrieval core:

- added retrieval profile files
- mapped stage profiles into the CDD model files
- implemented real `search()` and `healthCheck()` behavior in the memory provider
- injected the memory provider into the context assembler
- added cardinality guard and memory-result merge behavior

### Wave 3

Planning memory:

- implemented `wakeUp()`
- wired wake-up into planning session startup
- surfaced shared-memory wake-up results in the planning webview
- added promotion flow from memory item to planning signal

### Wave 4

Dashboard evolution:

- implemented the first real dashboard slice
- added `Overview`, `Context`, `Timeline`, `Palace`, `Health`, and `Workstream`
- preserved the legacy payload shape while evolving the UI

## Observed Result

The interesting result was not just that the code landed.

The interesting result was that four consecutive waves were delivered in series across two agents and two model tiers without stopping for corrective debugging between each wave before the first manual smoke pass.

That does not prove the workflow eliminates bugs.

It does suggest that:

- shared memory reduced repeated rediscovery
- bounded handoffs kept the next task clear
- continuity cycles made cold starts practical
- lower-cost execution became more viable once the higher-context planning work had been externalized into durable artifacts

## First Manual Smoke Pass

The first manual smoke pass after Wave 4 was encouraging:

- the dashboard opened cleanly
- navigation buttons worked
- planning sessions still opened
- wake-up content appeared
- the major touched surfaces were intact

That smoke pass also surfaced a bounded follow-up fix slice:

- some wake-up results were noisy or poorly scoped
- Hades was missing from the discovered project list
- the promote-to-signal flow was not yet usable enough in practice

Those were then fixed as a focused follow-up pass, which is a much better failure mode than discovering broad breakage after every wave.

## Follow-Up Manual Validation

After that focused fix pass, Hades was tested again as a product surface rather than as a code diff.

This pass was specifically about Hades itself:

- not executing downstream prompts
- not running generated stages end to end
- just validating the extension behavior, shared memory integration, persistence, and planning flow

Observed during that pass:

- `Open CDD Dashboard` worked cleanly
- initial dashboard load worked without visible console errors
- dashboard refresh worked
- project selection updated the dashboard correctly
- dashboard navigation buttons worked:
  - Planning
  - Contexts
  - Outputs
  - History
  - Views
  - Browse Context
- planning artifacts still opened correctly
- planning session startup worked
- shared memory appeared for the active project
- promote-to-signal worked after the planning UI fixes
- promoted items persisted and duplicate promotion was blocked cleanly
- state persistence looked good across reopening the planning flow
- manager surfaces looked healthy
- delivery and export flows looked healthy

This pass was run with MemPalace connected.

## Important Testing Nuance

One useful nuance surfaced during testing:

The planning-side `Shared Memory` panel is currently project-scoped, not mode-scoped.

That means selecting a different planning mode updates the planning form fields, but does not yet change the shared-memory result set in a meaningful way. This is expected from the current implementation: the panel is driven by project wake-up retrieval, not by the stage-aware retrieval profile system used later in context assembly.

That is not a failure of the current design, but it is a clear next refinement:

- selected driving-context titles should become bounded retrieval hints
- planning-mode or stage intent should influence the wake-up query more directly
- query isolation still needs to remain strict

So the current state is:

- project-aware shared memory works
- promote-to-signal works
- stage-aware retrieval exists in the assembly layer
- mode-aware shared-memory planning retrieval is still a next-step refinement

## Remaining Gaps After Validation

The post-fix validation result was strong, but not "done forever."

Known remaining gaps:

- the planning shared-memory panel should become more mode-aware
- graceful degradation was validated by code path earlier, but this test pass did not manually force MemPalace offline through the VS Code setting path
- downstream prompt execution and generated-stage behavior still need their own separate validation passes

## Why This Matters

This is a useful bridge result for CDD and MemPalace because it shows a concrete, non-theoretical benefit:

- MemPalace acted as continuity infrastructure
- handoff capsules turned session boundaries into resumable checkpoints
- the continuity cycle gave agents a shared operational ritual
- the planning burden and the implementation burden could be split more intentionally across model cost tiers

## Caution

This is still a bounded project experiment, not a universal claim.

Important caveats:

- the work happened in one project family
- the agents still relied on good planning artifacts
- manual smoke testing still mattered
- the first post-Wave-4 smoke pass did reveal follow-up fixes
- the validation described here focused on Hades as an interactive workbench, not on downstream generated artifacts or end-to-end execution of prompts
- mode-aware shared-memory retrieval in planning is not complete yet

So the right reading is not "the process removed bugs."

The right reading is "the process materially reduced coordination loss and correction churn in a multi-wave, multi-agent implementation run."

## Takeaway

For this Hades run, the combination of MemPalace, handoff capsules, and continuity cycles made serial multi-agent delivery feel much more stable than earlier iterations that depended on chat transcript continuity alone.

The stronger claim after the follow-up validation is this:

multi-wave delivery with shared memory did not remove the need for testing, but it did move the failure pattern from "every wave needs corrective debugging before the next wave can start" toward "a coherent implementation run followed by a bounded, intelligible validation pass."
