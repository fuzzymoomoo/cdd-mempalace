# cdd-mempalace

Bridge work between **CDD (Context-Driven Development)** and **MemPalace**.

This repository explores how structured, local-first memory can support a context-driven software workflow for real engineering work:

- preserving design decisions
- organizing project knowledge
- improving AI recall
- reducing repeated explanation
- making human and multi-LLM handoffs more durable

## Why This Exists

CDD treats software development as a problem of context management as much as code generation.

The challenge is not only getting an AI to produce code. The challenge is giving people and machines the right memory, structure, and retrieval model so work can stay coherent across time.

That makes MemPalace a strong fit.

MemPalace provides a local-first, structured memory model with navigable spaces such as wings, halls, and rooms. This repo explores how that kind of memory can support practical software engineering workflows inside CDD.

## Relationship To MemPalace

This project is:

- built on top of MemPalace concepts and workflows
- intended to integrate with and contribute back to the MemPalace ecosystem
- a public bridge between CDD and structured long-term memory

This project is **not** an official MemPalace repository.

Upstream project:

- [MemPalace](https://github.com/milla-jovovich/mempalace)

## What This Repo Aims To Do

- define a recommended CDD to MemPalace mapping model
- publish examples of engineering memory that are understandable to both humans and agents
- evaluate retrieval and handoff quality for software work
- document what works, what does not, and what should be contributed upstream

## Core Idea

A practical first-pass mapping looks like this:

| CDD concept | MemPalace concept | Use |
| --- | --- | --- |
| Product / major system | Wing | Top-level memory boundary |
| Knowledge class / subsystem area | Hall | Retrieval and organization scope |
| Task stream / feature / decision cluster | Room | Working area for a topic |
| Durable artifacts | Drawers / stored materials | Specs, notes, decisions, transcripts |

More detail lives in [MAPPING.md](MAPPING.md).

## Current Contents

- [MAPPING.md](MAPPING.md)
  First-pass mapping between CDD concepts and MemPalace structure.
- [ROADMAP.md](ROADMAP.md)
  Public direction for the bridge work.
- [PROOF_OF_WORK.md](PROOF_OF_WORK.md)
  Track upstream contributions, experiments, and examples.
- [examples/README.md](examples/README.md)
  Early examples of how the bridge should work in practice.

## Proof Of Work

This repo is intended to earn credibility through useful public work, not adjacency.

Proof points will include:

- upstream pull requests
- issues opened with tested findings
- example integrations
- engineering-focused documentation
- retrieval experiments and evaluation notes

The running log for that lives in [PROOF_OF_WORK.md](PROOF_OF_WORK.md).

## Early Status

Active public integration work.

Right now this repository is part lab, part adapter, and part documentation trail for using structured memory in real software engineering workflows.

Current momentum includes multiple live upstream MemPalace pull requests spanning:

- engineering memory docs and examples
- Windows cleanup and test reliability fixes
- graph-layer test coverage
- extractor-layer test coverage

## Philosophy

**Ideas are cheap. Code should be too.**

The scarce resource is not typing. It is preserving the right context, at the right fidelity, in a form both people and machines can use.

That is the problem this repo is trying to solve.

## License

This repository is licensed under the GNU Affero General Public License v3.0. See [LICENSE](LICENSE).
