# GitHub: the collaboration layer

Git is the version control tool. GitHub is a hosting service plus a set of
collaboration features built on top of it. Everything below is GitHub, not git.

## Pull requests

A PR is a request to merge one branch into another, wrapped in a review
conversation. The lifecycle:

1. `git switch -c feat/thing` — branch off up-to-date `main`
2. Commit in small, logical steps
3. `git push -u origin feat/thing`
4. Open the PR (GitHub prints a link after the push, or use the web UI)
5. CI runs; reviewers comment
6. Push follow-up commits to address feedback — the PR updates automatically
7. Merge, then delete the branch

### Writing a PR description

The reviewer's time is the scarce resource. A good description covers:

- **What** changed, in one or two sentences
- **Why** — the problem or issue being solved (`Fixes #42` links and auto-closes)
- **How to verify** — the command they should run, or what to click
- Anything you're unsure about, called out explicitly

Keep PRs small. A 200-line PR gets a real review; a 2000-line PR gets "LGTM".

### Merge strategies

| Strategy | Result | Use when |
|---|---|---|
| **Merge commit** | Keeps every commit + adds a merge commit | History of the work matters |
| **Squash and merge** | All commits become one on `main` | The default for most teams — `main` stays clean and each commit maps to one PR |
| **Rebase and merge** | Commits replayed onto `main`, no merge commit | You want linear history *and* individual commits |

If unsure, squash. It makes `git bisect` and `git revert` behave predictably.

### Reviewing

- **Comment** — thoughts, no verdict
- **Approve** — good to merge
- **Request changes** — blocks merge until resolved
- **Suggested changes** — propose exact replacement lines; the author applies
  them with one click. Use these for nits instead of prose.

Review norms that make you pleasant to work with: distinguish blocking issues
from preferences (prefix nits with "nit:"), explain *why*, and approve rather
than nitpick when the change is fine.

## Issues and project management

- Issues track bugs, features, questions. Labels, milestones, assignees.
- `Fixes #12`, `Closes #12`, `Resolves #12` in a PR body auto-closes the issue
  when the PR merges.
- Reference across repos: `owner/repo#12`.
- **Projects** give you boards/tables over issues and PRs.
- **Discussions** for open-ended Q&A that isn't a bug.

## GitHub Actions (CI)

A workflow is YAML in `.github/workflows/`. Minimal example that runs on PRs:

```yaml
name: CI
on:
  pull_request:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run checks
        run: ./scripts/check.sh
```

Key ideas: **events** trigger **workflows**, which contain **jobs** (parallel by
default), which contain **steps** (sequential). Steps either `run` a shell
command or `uses` a prebuilt action.

## Branch protection

On `main`, in Settings → Branches (or Rulesets), typically:
- Require a pull request before merging
- Require at least 1 approving review
- Require status checks to pass
- Block force pushes and deletions

This is what stops "oops I pushed to main at 2am".

## Repo hygiene files

| File | Purpose |
|---|---|
| `README.md` | What it is, how to run it |
| `LICENSE` | Without one, nobody may legally use it |
| `.gitignore` | Keep build output and secrets out of history |
| `CONTRIBUTING.md` | How to propose changes |
| `CODEOWNERS` | Auto-request reviews from the right people |
| `.github/PULL_REQUEST_TEMPLATE.md` | Prompts for a good description |
| `.github/ISSUE_TEMPLATE/` | Structured bug reports |

## Contributing to open source

1. **Fork** the repo (your own copy on GitHub)
2. Clone your fork; add the original as a second remote:
   ```bash
   git remote add upstream https://github.com/original/repo
   ```
3. Stay current: `git fetch upstream && git merge upstream/main`
4. Branch, commit, push **to your fork**
5. Open a PR from your fork's branch to the original repo's `main`
6. Read their `CONTRIBUTING.md` first. Start with a docs fix or a small bug —
   large unsolicited PRs usually stall.

## Other GitHub features worth knowing

- **Gists** — single-file snippets with version history
- **Releases** — tags plus notes and binaries
- **GitHub Pages** — static site straight from a repo
- **Dependabot** — automatic dependency update PRs
- **Secret scanning / Code scanning** — security alerts on your code
- **`gh` CLI** — `gh pr create`, `gh pr checkout 42`, `gh run watch`. Once you're
  comfortable in the browser, this is much faster.
