# Week 6 drill — professional workflow

Use your `git-practice` repo on GitHub for parts A–E.

## Part A — CI on every PR

Create `.github/workflows/ci.yml`:

```yaml
name: CI
on:
  pull_request:
  push:
    branches: [main]

jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Check for conflict markers
        run: |
          if grep -rn '^<<<<<<< ' --include='*.md' .; then
            echo "Unresolved conflict markers found"; exit 1
          fi
      - name: Check every markdown file is non-empty
        run: |
          find . -name '*.md' -empty -print -exec false {} +
```

Push it on a branch, open a PR, and watch the check run. Then deliberately
commit a file containing `<<<<<<< HEAD` and confirm CI goes red.

## Part B — protect `main`

Settings → Branches (or Rulesets) → add a rule for `main`:
- Require a pull request before merging
- Require status checks to pass (select your `check` job)
- Block force pushes

Now try `git push origin main` directly. It should be rejected. Good.

## Part C — tag a release

```bash
git switch main && git pull
git tag -a v0.1.0 -m "First release: week 1-6 curriculum"
git push origin v0.1.0
git describe --tags
```
On GitHub, turn the tag into a Release with notes.

## Part D — repo hygiene

Add, each via its own PR:
- `.github/PULL_REQUEST_TEMPLATE.md` (What / Why / How to verify)
- `.github/ISSUE_TEMPLATE/bug_report.md`
- `CONTRIBUTING.md` describing your own branch naming and commit conventions
- `LICENSE` (MIT is a fine default)

## Part E — conventional commits

Redo one small change using `feat:`, `fix:`, and `docs:` prefixes. Then:
```bash
git log --oneline --grep '^feat'
```
Notice how machine-readable history enables changelog automation.

## Part F — contribute to open source

Find a real project. Good hunting grounds: the `good first issue` label,
docs typos in a tool you already use, https://goodfirstissue.dev.

1. Read their `CONTRIBUTING.md` **first**
2. Fork → clone → `git remote add upstream <original>`
3. `git switch -c fix/typo-in-readme`
4. Small, focused commit
5. Push to your fork, open the PR against their `main`
6. Respond to review politely and promptly

A merged one-line docs fix teaches you more than a week of reading.

## Checkpoint

1. What do branch protection rules actually prevent?
2. Why do teams adopt Conventional Commits?
3. What's the difference between a tag and a branch?
4. Walk through the full fork → PR flow from memory.
