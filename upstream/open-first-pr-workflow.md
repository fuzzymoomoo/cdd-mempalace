# Open The First MemPalace PR

This is the exact workflow for opening the first upstream MemPalace contribution cleanly from this machine.

The recommended first PR is:

- title: `docs: add software engineering memory example`
- target file: `examples/software_engineering_memory.md`

## Before You Start

Because this machine is currently configured with a work email in global git config, set the author identity locally in the forked repo before committing.

Recommended:

- use your personal GitHub email
- or use your GitHub `noreply` email

## Step 1: Fork MemPalace In The Browser

Open:

- https://github.com/milla-jovovich/mempalace

Then click:

- `Fork`

This should create:

- `https://github.com/fuzzymoomoo/mempalace`

## Step 2: Clone Your Fork

```powershell
cd C:\Code\Alexandria
git clone https://github.com/fuzzymoomoo/mempalace.git
cd mempalace
```

## Step 3: Add Upstream Remote

```powershell
git remote add upstream https://github.com/milla-jovovich/mempalace.git
git fetch upstream
git branch --set-upstream-to=origin/main main
```

## Step 4: Set Repo-Local Git Identity

Replace the email below with your personal GitHub email or GitHub `noreply` email.

```powershell
git config user.name "Warrick Galloway"
git config user.email "YOUR_GITHUB_EMAIL_HERE"
```

## Step 5: Create A Branch

```powershell
git checkout -b docs/software-engineering-memory-example
```

## Step 6: Add The Example File

Create this file in the MemPalace fork:

- `examples/software_engineering_memory.md`

Copy the contents from:

- [software-engineering-memory-example.md](/C:/Code/Alexandria/cdd-mempalace/upstream/software-engineering-memory-example.md)

If you want a pure shell copy on this machine:

```powershell
Copy-Item `
  -LiteralPath C:\Code\Alexandria\cdd-mempalace\upstream\software-engineering-memory-example.md `
  -Destination C:\Code\Alexandria\mempalace\examples\software_engineering_memory.md
```

## Step 7: Review The Diff

```powershell
git status --short
git diff -- examples/software_engineering_memory.md
```

## Step 8: Run Upstream Tests

MemPalace asks contributors to run:

```powershell
pytest tests/ -v
```

For a docs-only PR this is still a good habit if the repo is already set up locally.

## Step 9: Commit

```powershell
git add examples/software_engineering_memory.md
git commit -m "docs: add software engineering memory example"
```

## Step 10: Push Your Branch

```powershell
git push -u origin docs/software-engineering-memory-example
```

## Step 11: Open The Pull Request

Open this URL in the browser after pushing:

- `https://github.com/milla-jovovich/mempalace/compare/main...fuzzymoomoo:mempalace:docs/software-engineering-memory-example?expand=1`

Use:

- title from [first-pr-description.md](/C:/Code/Alexandria/cdd-mempalace/upstream/first-pr-description.md)
- body from [first-pr-description.md](/C:/Code/Alexandria/cdd-mempalace/upstream/first-pr-description.md)

## Step 12: Log The PR Back In cdd-mempalace

Once the PR is open:

- add the PR link to `PROOF_OF_WORK.md`
- note whether any maintainer feedback changes the bridge assumptions

## Suggested Follow-Up

After the docs PR is open, the next strong upstream move is:

- open a Codex transcript normalization issue backed by your tested findings

That creates a nice sequence:

1. useful docs/example contribution
2. real technical finding from actual bridge work
