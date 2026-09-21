# Retrieval question bank

Answer **out loud or in writing, with no notes open**, before scrolling to the
answers. A hedged answer counts as wrong. Getting it wrong and then reading the
answer is more valuable than getting it right easily — so don't peek to protect
your score.

Use these in session 1 (cold, before reading) and session 4 (after drilling) of
each week, and in the one-month booster.

---

## Week 1 — Local basics

1. Name the three areas a change can live in, and the command that moves it
   between each adjacent pair.
2. `git diff` and `git diff --staged` — which comparison does each make?
3. What does a commit object actually store?
4. What can `git add -p` do that `git add` can't, and when would you want it?
5. You committed and immediately noticed a typo in the message. It isn't pushed.
   What do you run?
6. Why should build output never be committed?

## Week 2 — Branching and merging

7. Physically, what *is* a branch?
8. Under what condition does git fast-forward instead of creating a merge commit?
9. What do `<<<<<<<`, `=======`, and `>>>>>>>` delimit?
10. You're halfway through a conflicted merge and want to be exactly where you
    started. What do you run?
11. What is `HEAD`, and what does "detached HEAD" mean?
12. After resolving a conflict by editing the file, what two commands finish the
    merge?

## Week 3 — Remotes

13. What is `origin/main`, precisely? Is it live?
14. Why can `git fetch` never cause a merge conflict?
15. `git pull` is shorthand for which two commands?
16. What does `-u` do in `git push -u origin feature`?
17. Your push is rejected as "non-fast-forward". What does that mean, and what
    are your two options?
18. When do you fork a repo instead of branching in it?

## Week 4 — Pull requests

19. Name the three GitHub merge strategies and one reason to pick each.
20. Why does squash-merging make `git revert` and `git bisect` behave better?
21. You pushed three more commits to a branch that already has an open PR. What
    do you have to do to the PR?
22. What three things does a reviewer need from a PR description?
23. What does `Fixes #12` in a PR body do?

## Week 5 — History surgery

24. `reset --soft`, `--mixed`, `--hard` — which of the three areas does each
    move?
25. When must you use `revert` rather than `reset`?
26. You ran `git reset --hard HEAD~3` an hour ago and need those commits. What
    now?
27. What does interactive rebase do to commit SHAs, and why does that matter?
28. What is the one category of loss git genuinely cannot recover?
29. What problem does `git bisect` solve, and roughly how?
30. State the golden rule of rebasing.

## Week 6 — Professional workflow

31. What's the difference between a tag and a branch?
32. What do branch protection rules actually prevent?
33. Why do teams adopt Conventional Commits — what does it enable?
34. In a GitHub Actions workflow, what's the relationship between events, jobs,
    and steps?
35. Walk through the full fork → PR flow from memory.
36. Why is `--force-with-lease` safer than `--force`?

---
---

# Answers

Only now.

1. Working tree → (`git add`) → staging area/index → (`git commit`) →
   repository. `git restore` and `git restore --staged` move things back.
2. `git diff` = staged vs working tree (what you haven't staged yet).
   `git diff --staged` = last commit vs staged (what's about to be committed).
3. The complete tree of files at that moment, parent commit pointer(s), author,
   committer, timestamp, and message — hashed together into a SHA.
4. Stage selected *hunks* within a file rather than the whole file. Use it when
   one file contains two unrelated changes that belong in separate commits.
5. `git commit --amend`. Safe only because it isn't pushed.
6. It's regenerable, it bloats history permanently, and it causes conflicts on
   every merge. Once in history it's there until history is rewritten.
7. A file containing a commit SHA — a movable pointer, nothing more. Creating
   and deleting them is cheap and doesn't touch commits.
8. When the current branch hasn't moved since the other branch diverged, so the
   target commit is a direct descendant. Git just slides the pointer forward.
9. `<<<<<<<` to `=======` is your side (HEAD); `=======` to `>>>>>>>` is
   theirs. You replace the whole block with what you actually want.
10. `git merge --abort`.
11. A pointer to the branch you're currently on. Detached HEAD means HEAD points
    directly at a commit instead of at a branch — not an error, but new commits
    there belong to no branch until you make one.
12. `git add <file>` then `git commit`.
13. Your local cache of where `main` was on the remote the last time you
    communicated with it. Not live — it only updates on fetch/pull.
14. It only updates remote-tracking refs. It never touches your working tree or
    your branches, so there's nothing to conflict with.
15. `git fetch` + `git merge` (or `git rebase` with `--rebase`).
16. Sets the upstream, so future bare `git push` / `git pull` know which remote
    branch this one tracks, and `git status` can report ahead/behind.
17. The remote branch has commits you don't have; your push would lose them.
    Either integrate first (`git pull` or `git pull --rebase`, then push), or —
    only on a branch nobody else uses — `git push --force-with-lease`.
18. When you don't have write access: contributing to someone else's project.
    Within a repo you can write to, just branch.
19. **Merge commit** — preserves every commit plus a join; use when the shape of
    the work matters. **Squash** — one commit per PR on `main`; the sane
    default. **Rebase and merge** — linear history keeping individual commits.
20. Each PR becomes exactly one commit on `main`, so reverting a feature is
    reverting one SHA, and bisect steps land on whole, coherent changes rather
    than half-finished intermediate states.
21. Nothing. A PR tracks a branch — pushing updates it automatically.
22. What changed, why (ideally linking an issue), and how to verify it.
23. Auto-closes issue 12 when the PR merges, and links the two.
24. `--soft` moves HEAD only (changes stay staged). `--mixed` moves HEAD and
    resets the index (changes stay in the working tree, unstaged). `--hard`
    moves all three (changes destroyed).
25. Whenever the commit is already on a shared branch. `revert` adds a new
    inverse commit and rewrites nothing, so nobody else has to clean up.
26. `git reflog`, find the SHA from before the reset, `git reset --hard <sha>`.
    Reflog keeps unreachable commits for ~90 days by default.
27. It creates *new* commits with new SHAs. That's why rebasing shared history
    is destructive — everyone else's copies now disagree with yours.
28. Changes that were never committed or stashed — destroyed by `git restore` or
    `git reset --hard`. Git never saw them, so it can't restore them.
29. Finding which commit introduced a bug. Binary search over history: you mark
    a known-good and known-bad commit, git checks out the midpoint, you test and
    say good or bad, repeat — log₂(n) tests instead of n.
30. Never rebase commits that others have already pulled.
31. A tag is a fixed label on one specific commit; a branch is a pointer that
    moves as you commit. Tags mark releases, branches track work.
32. Direct pushes to protected branches, force-pushes, branch deletion, and
    merging without review or green CI.
33. Machine-readable commit history: automated changelogs, automatic semantic
    version bumps, and filterable history (`git log --grep '^feat'`).
34. An **event** (push, pull_request, schedule) triggers a **workflow**, which
    contains **jobs** that run in parallel by default, each containing **steps**
    that run sequentially. A step either `run`s a shell command or `uses` an
    action.
35. Fork on GitHub → clone your fork → add the original as `upstream` →
    `git fetch upstream && git merge upstream/main` to stay current → branch →
    commit → push to *your fork* → open a PR from your branch to their `main` →
    address review.
36. `--force-with-lease` refuses the push if the remote branch has moved since
    you last fetched, so you can't silently destroy someone else's commits.
    Plain `--force` overwrites unconditionally.
