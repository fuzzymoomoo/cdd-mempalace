# Examples

This folder holds small, public-safe examples that show how CDD and MemPalace can work together in practice.

## Initial Example: Engineering Memory Flow

Imagine a team working on a customer onboarding feature.

The active project contains:

- a planning note
- a decision record about workflow ownership
- a handoff capsule from one model to another
- a validation note describing what must be checked before release

### Suggested Memory Shape

- `Wing`
  `product-onboarding`
- `Hall`
  `knowledge`, `history`, `patterns`, `validation`
- `Rooms`
  `feature-onboarding-flow`
  `decision-workflow-owner`
  `handoff-onboarding-implementation`
  `validation-onboarding-release`

### Example Retrieval By Stage

Planning:

- retrieve the feature room
- retrieve related decisions
- retrieve any comparable patterns

Implementation:

- retrieve the handoff capsule
- retrieve validated examples
- retrieve the active feature room

Validation:

- retrieve the validation room
- retrieve the expected outputs
- retrieve prior incident or failure notes if they exist

### Why This Matters

The value is not just search.

The value is that memory becomes:

- durable
- structured
- stage-aware
- understandable to both humans and agents

Future examples in this folder should include real bridge workflows, retrieval notes, and links to any upstream findings they produced.

## Additional Examples

- [hades-shared-memory-handoff.md](hades-shared-memory-handoff.md)
  A real case study showing Codex-to-Claude planning continuity over MemPalace, the resulting Hades master plan, and the operational lessons that turned into the `continuity cycle` term.
- [hades-four-wave-delivery-experiment.md](hades-four-wave-delivery-experiment.md)
  A concrete experiment note describing four Hades delivery waves executed in series across Claude and Codex, using shared memory, handoff capsules, and continuity cycles with much less correction churn than earlier iterations.
- [multi-agent-continuity-cycle-outline.md](multi-agent-continuity-cycle-outline.md)
  A scoped outline for a possible HexNest-plus-MemPalace example showing shared-memory handoff with orchestration.
- [chaos-personal-operating-system-memory.md](chaos-personal-operating-system-memory.md)
  A public-safe case study showing how an ADHD-first local operating system can use MemPalace as an optional continuity and retrieval layer without replacing its core task and capture store.
