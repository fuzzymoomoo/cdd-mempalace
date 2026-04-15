# Customer-Facing Bot Memory

This case study shows how MemPalace can support a customer-facing bot as a continuity layer around live conversation context, objection handling, and human handoff.

The concrete project behind this example is `cdd-sales-bot`, a sales-conversation workbench that is still being built. Even at this early stage, one thing is already obvious during testing:

- customer-centered context changes reply quality
- durable memory changes objection handling
- the combination is much stronger than either one on its own

This is bigger than sales. The same pattern can extend to support bots, customer-service bots, onboarding agents, renewal assistants, and any system that talks to a customer across time.

## What the bot already proves

The current bot already makes several important pieces visible:

- stage-aware conversation state
- objection-aware plan selection
- context assembly from business, knowledge, compliance, deployment, and conversation state
- local prospect memory that carries forward known pains, prior objections, stage, and session count
- handoff capsule generation when a human needs to take over

That means the product already shows the value of memory in miniature. The next step is to widen that into a structured shared-memory surface rather than keeping all durable context inside one local runtime store.

## Why MemPalace fits this pattern

Customer-facing bots do not only need retrieval over product knowledge.

They also need continuity around:

- what this customer already told you
- which objection has already appeared
- what proof is safe to use
- what not to claim
- what a human should inherit if the bot hands off

MemPalace is a strong fit because it gives that context a local-first, durable, retrievable structure without forcing the bot to treat memory as its only operational database.

## Recommended responsibility split

The clean split for this class of system is:

- **Runtime and local store**
  active turn state, streaming messages, short-lived working context, and fast mutable session data
- **MemPalace**
  durable customer memory, objection patterns, approved proofs, governed policy notes, handoff capsules, and retrievable history across sessions

This matters because customer bots need both:

- fast bounded execution for the current turn
- broader continuity that survives the current session

## Suggested memory shape

For a first practical MemPalace setup, a single bot-oriented wing works well:

- `customer-bot`

With rooms such as:

- `accounts`
- `opportunities`
- `objections`
- `products`
- `case-studies`
- `compliance`
- `playbooks`
- `handoffs`
- `transcripts`

This keeps the memory model product-facing and easy to reason about.

For larger deployments, these can later split into multiple wings, but one wing with clear rooms is enough to prove the pattern.

## What belongs in memory

Not every artifact deserves durable memory.

### Ephemeral

These should usually stay out of the palace:

- temporary chain-of-thought-style reformulations
- failed candidate replies
- discarded objection guesses
- raw scratch summaries

### Working

These are useful during a live conversation and often worth selective promotion:

- current opportunity summary
- active objection analysis
- current pain summary
- latest next-step recommendation
- current handoff draft

### Durable and governed

These are strong MemPalace candidates:

- validated account summaries
- accepted objection patterns
- approved case studies
- compliance notes and pricing guardrails
- stakeholder and authority notes
- handoff capsules
- reusable follow-up summaries

This promotion boundary is important. A customer-facing bot should not dump every turn into durable memory and call that continuity.

## High-value retrieval moments

The biggest wins come from a few specific moments.

### 1. Live objection handling

When a customer raises a price, timing, trust, or authority objection, the bot can retrieve:

- prior pains already named by this customer
- earlier objections from the same account
- the relevant objection playbook
- approved claims and guardrails
- the most relevant case study

That turns the bot from "replying to a category" into responding to this customer in this situation.

### 2. Human handoff

If the conversation needs a human, shared memory can preserve:

- current stage
- pains already confirmed
- objections already raised
- what was promised
- what still needs clarification

That reduces repeated questioning and makes the human inherit a cleaner working context.

### 3. Follow-up and return sessions

When the same customer returns days or weeks later, the bot can recover:

- the last meaningful stage
- unresolved objections
- prior case-study or proof paths used
- the last recommended next step

This is where continuity becomes more than transcript search.

## How this generalizes beyond sales

The same structure works for:

- support bots that need issue history and prior explanations
- customer-service bots that need preference and case continuity
- onboarding bots that need rollout status and adoption blockers
- renewal or success bots that need risk signals and stakeholder context

The surface conversation changes, but the underlying memory problem stays the same:

- customers speak across time
- context arrives in fragments
- the next turn is better when prior meaning is still available

## Takeaway

The important idea is not "give the bot more documents."

It is:

- keep the current turn grounded in customer-centered context
- preserve the right durable memory between sessions
- retrieve only the bounded parts that matter now

That is why MemPalace looks like a strong fit for customer-facing bots.

The sales bot is the first concrete example here, but the pattern is broader than sales.
