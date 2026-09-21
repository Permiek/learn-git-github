# Week 4 drill — pull requests

Use your `git-practice` repo on GitHub.

## Part A — a PR end to end

```bash
git switch main && git pull
git switch -c docs/add-usage
# make 2–3 small, separate commits
git push -u origin docs/add-usage
```
Open the PR (GitHub prints a link, or use the web UI, or `gh pr create`).
Write a description with **What**, **Why**, and **How to verify**.

## Part B — review your own PR

On the Files changed tab:
- Leave a normal comment on one line
- Leave a **suggested change** on another (the `±` / suggestion button)
- Submit the review

Then apply the suggestion via "Commit suggestion", and:
```bash
git pull                      # bring GitHub's commit back down
git lg
```

## Part C — respond to feedback with a new commit

Make another change locally, commit, push. Watch the PR update itself. Note that
you did *not* need to open a new PR — that's the point of a PR tracking a branch.

## Part D — the three merge strategies

Squash-merge this PR. Then repeat Parts A–C on two more small branches and merge
one with "Create a merge commit" and one with "Rebase and merge". After each:
```bash
git switch main && git pull
git lg
```
Compare the three shapes of history. Decide which you'd want as a default.

## Part E — link an issue

Open an issue ("Add a license"). Create a branch, add a `LICENSE` file, and put
`Fixes #1` in the PR body. Merge it and confirm the issue closed itself.

## Part F — clean up

```bash
git switch main && git pull
git branch -d docs/add-usage
git fetch --prune             # drop stale origin/* refs
git branch -a
```

## Checkpoint

1. What are the three merge strategies and when would you pick each?
2. What does a reviewer need from a description to review without asking you?
3. Why are small PRs reviewed better than large ones?
4. What does `git fetch --prune` clean up?
