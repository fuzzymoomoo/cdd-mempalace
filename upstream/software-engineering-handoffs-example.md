# Software Engineering Handoffs With Shared Memory

This example shows how MemPalace can support a practical handoff between two actors working on the same software project.

The core idea is simple:

- one actor stops
- another actor resumes later
- both use the same shared memory surface instead of starting from a blank chat

## Why this matters

In real software work, important context is often spread across:

- repo docs
- design notes
- decision records
- issue notes
- handoff summaries

When that context is only present in one chat session, the next actor has to rediscover too much. MemPalace helps by making the durable parts retrievable across sessions.

## Minimal workflow

### Outgoing actor

1. Save durable artifacts in indexed repo paths
2. Create or update a handoff capsule in `docs/handoffs/`
3. Refresh MemPalace after those durable artifacts are written

### Incoming actor

1. Search for the handoff capsule
2. Use its retrieval hints to query related project memory
3. Open the authoritative files named in the handoff
4. Validate the current state before acting

This keeps the handoff grounded in durable sources instead of relying on chat memory alone.

## Example memory shape

- `Wing`
  `project-alpha`
- `Rooms`
  `handoffs`
  `decisions`
  `planning`
  `incidents`
  `validation`

Example durable artifacts:

- architecture notes
- decision records
- release notes
- implementation handoffs
- validation summaries

## Example handoff capsule contents

At minimum, the handoff capsule should include:

- current goal
- current state
- key decisions made
- important source files or docs
- retrieval hints
- open questions
- next recommended action
- refresh status

## Why the refresh step matters

The handoff only becomes useful to the next cold-start actor if the new durable artifacts are actually indexed.

That means:

- writing the handoff is not enough
- the shared memory refresh is part of the workflow

## Optional additions

For longer-running work, the team can also record:

- diary summaries of major sessions
- knowledge graph facts for durable decisions
- project-specific wake-up prompts

These are helpful, but the essential path is still:

`durable artifact -> refresh -> wake-up -> validate -> continue`

## What this demonstrates

MemPalace is useful here not because it stores everything, but because it lets durable project memory stay large while the active prompt stays small.

That makes it a strong fit for:

- human-to-human handoffs
- human-to-agent handoffs
- agent-to-agent handoffs
- long-running repo-local engineering work
