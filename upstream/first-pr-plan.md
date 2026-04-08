# First MemPalace PR Plan

## Recommendation

Start with a small docs/example pull request, not a code-heavy pull request.

Recommended scope:

- add one new file under `examples/`
- show how MemPalace can be used for software engineering memory
- keep the example generic and useful without introducing CDD branding into the upstream repo

## Why This First

This is the strongest first move because:

- MemPalace explicitly lists docs and tutorials as a good first contribution area
- the upstream repo already has an `examples/` folder with short setup and workflow docs
- it gives you a public, useful contribution quickly
- it makes the bridge credible without overreaching

## Proposed Upstream File

- `examples/software_engineering_memory.md`

This fits the existing `examples/` layout and is specific enough to be understandable at a glance.

## What The PR Should Do

- explain why software engineering is a strong use case for structured memory
- show a small memory shape using wings, halls, and rooms
- show how memory retrieval helps during planning, implementation, and validation
- avoid claiming MemPalace is only for engineers
- avoid introducing private repo assumptions

## What The PR Should Not Do

- do not lead with CDD branding
- do not introduce Hades, Alexandria, or internal naming
- do not promise benchmark claims outside what upstream already supports
- do not turn the first PR into a large tutorial suite

## Suggested Sequence

1. Open a docs PR with the example in this folder.
2. After it is open, log it in `PROOF_OF_WORK.md`.
3. After the first docs PR lands or gets traction, open the Codex transcript normalization issue as the next proof-of-work step.

## Validation Checklist

Before opening the PR:

- confirm the example file name still fits upstream structure
- run upstream tests if you clone and edit locally
- keep the commit message docs-focused, for example:
  - `docs: add software engineering memory example`

## Why This Supports CDD

This is useful to CDD because it makes the memory layer tangible in public:

- CDD stays the methodology
- MemPalace stays the memory substrate
- the bridge repo becomes the place where the relationship is explained and evidenced
