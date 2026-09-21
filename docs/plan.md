# The 6-Week Plan

Each week: **concepts** (what to understand), **commands** (what to be able to
type from memory), **drill** (the exercise file), and **done when** (an honest
self-test). Don't advance until you can pass the self-test without notes.

---

## Week 1 — Local git: the loop you'll run 50 times a day

**Concepts**
- Snapshot vs diff; the three areas (working tree / index / repository)
- What `.git/` is; what `git init` and `git clone` actually do
- What makes a good commit: one logical change, a message that explains *why*
- `.gitignore` and why build output never belongs in history

**Commands**
```
git init            git clone           git status
git add  (-p)       git commit (-m)     git diff  (--staged)
git log  (--oneline --graph --decorate --all)
git show            git restore         git rm / git mv
```

**Commit messages.** Subject line: imperative mood, ≤50 chars, no trailing
period ("Add retry to upload handler", not "added retries"). Blank line. Then a
body explaining *why*, wrapped at 72 chars. The diff already says what changed;
the message says why it needed to.

**Drill:** [`exercises/week1-local-basics.md`](../exercises/week1-local-basics.md)

**Done when** you can initialize a repo, stage only *part* of a changed file
with `git add -p`, commit it, and explain the difference between `git diff` and
`git diff --staged` out loud.

---

## Week 2 — Branching and merging

**Concepts**
- A branch is a pointer; branching is cheap; branch per unit of work
- Fast-forward merge vs true merge commit
- What a merge conflict *is*: two branches changed the same region of the same
  file, and git refuses to guess
- Branch naming conventions (`feat/…`, `fix/…`, `docs/…`)

**Commands**
```
git branch          git switch (-c)     git merge
git log --graph --oneline --all
git merge --abort   git diff --name-only --diff-filter=U
```

**Conflict markers** look like this, and you resolve them by editing the file
into the state you actually want, then `git add` it:
```
<<<<<<< HEAD
your version
=======
their version
>>>>>>> other-branch
```

**Drill:** [`exercises/week2-branching.md`](../exercises/week2-branching.md)

**Done when** you can deliberately create a conflict, resolve it by hand,
complete the merge, and also abort a merge midway and end up exactly where you
started.

---

## Week 3 — Remotes and GitHub

**Concepts**
- Remotes, `origin`, remote-tracking branches (`origin/main`) as a cache
- `fetch` vs `pull`; upstream tracking (`-u`)
- SSH keys vs HTTPS + personal access token — set up **SSH**, it's less friction
- Fork vs clone vs branch: when each is right
- Anatomy of a GitHub repo: README, LICENSE, `.gitignore`, topics, releases

**Commands**
```
git remote -v / add / set-url
git fetch           git pull            git push -u origin <branch>
git clone           git branch -vv
```

**SSH setup**
```bash
ssh-keygen -t ed25519 -C "you@example.com"
cat ~/.ssh/id_ed25519.pub     # paste into GitHub > Settings > SSH keys
ssh -T git@github.com         # should greet you by username
```

**Drill:** [`exercises/week3-remotes.md`](../exercises/week3-remotes.md)

**Done when** you can explain why `git fetch` never changes your files, and you
have pushed a branch from your machine to GitHub over SSH.

---

## Week 4 — Pull requests and collaboration

Read [`docs/github.md`](github.md) this week.

**Concepts**
- The PR workflow end to end: branch → commits → push → PR → review → merge
- Merge commit vs squash vs rebase-merge, and when each is appropriate
- Writing a PR description someone can review without asking you questions
- Reviewing: how to comment, suggest changes, request changes, approve
- Draft PRs, `Fixes #12` auto-closing keywords, linking issues
- Keeping a PR up to date with `main` (merge base in, or rebase if solo)

**Drill:** [`exercises/week4-pull-requests.md`](../exercises/week4-pull-requests.md)

**Done when** you have opened a PR against your own repo, reviewed it, left an
inline suggestion, applied it, and squash-merged — and can say why you picked
squash.

---

## Week 5 — History surgery and rescue

This is the week that turns git from scary into a tool.

**Concepts**
- `reset --soft / --mixed / --hard`: which of the three areas each one moves
- `revert` vs `reset` — revert for shared history, reset for private
- Interactive rebase: reorder, squash, fixup, edit, drop
- `stash` for "I need to switch contexts right now"
- `reflog` as the undo button for the undo button
- `cherry-pick` for moving one commit somewhere else
- `bisect` for finding the commit that broke something

**Commands**
```
git reset --soft/--mixed/--hard    git revert
git rebase -i HEAD~5               git commit --amend
git stash (push/pop/list)          git reflog
git cherry-pick                    git bisect start/good/bad
```

**Drill:** [`exercises/week5-history-surgery.md`](../exercises/week5-history-surgery.md)

**Done when** you can `git reset --hard` away three commits and then recover all
three using `reflog`, without panicking.

---

## Week 6 — Professional workflow

**Concepts**
- Branching strategies: trunk-based (short-lived branches off `main`) vs
  GitFlow. Default to trunk-based; most teams that use GitFlow regret it.
- Conventional Commits (`feat:`, `fix:`, `chore:`) and why automation likes them
- Tags and semantic versioning; GitHub Releases
- GitHub Actions: a CI workflow that runs on every PR
- Branch protection rules: require review, require green CI, no force-push
- `CODEOWNERS`, issue/PR templates, `CONTRIBUTING.md`
- Contributing to an open-source project: fork → branch → PR → address review

**Commands**
```
git tag -a v1.0.0 -m "..."    git push --tags
git describe --tags           git blame        git log -S"searchterm"
git worktree add              git submodule (know it exists; avoid if you can)
```

**Drill:** [`exercises/week6-professional.md`](../exercises/week6-professional.md)

**Done when** this repo has a green CI check on a PR, a protected `main`, a
tagged release, and you've opened a PR on someone else's open-source project.

---

## After week 6

- Use git for something real and personal — notes, dotfiles, a side project.
  Daily use is what makes it stick.
- When something confuses you, run `git lg` and *look at the graph*. The graph
  answers most questions.
- Keep [`docs/recovery.md`](recovery.md) open in a tab for a month.
