Absolutely open to it - I packaged the upstream-friendly `examples/cdd-workflow/` version and pushed it to my fork here:

- Branch: https://github.com/fuzzymoomoo/mempalace/tree/docs/cdd-workflow-example
- Compare / PR link: https://github.com/milla-jovovich/mempalace/compare/main...fuzzymoomoo:mempalace:docs/cdd-workflow-example?expand=1

What is in the pack:

- `examples/cdd-workflow/README.md`
- `examples/cdd-workflow/mempalace.yaml`
- a sample decision record
- a sample planning context bundle
- a sample handoff capsule using the exact structure you called out

I also added a small root README pointer so the worked example is easier to discover.

Validation I ran locally:

- mined the example into a disposable palace with `mempalace --palace <temp> mine .`
- verified retrieval with `mempalace --palace <temp> search "postgresql" --room decisions`

One small note: in plain Windows PowerShell I had to force UTF-8 output for the CLI banner because of an existing console encoding issue, but the example content itself mined cleanly.

On the technical side, #334 is now up for the Codex normalization gap, so I am treating this workflow example as the docs track and #334 as the normalization track.

If the packaging looks right to you, I can keep iterating on the example from there instead of expanding scope too early.
