# "I broke it" — recovery map

Find your symptom. Most of these are fully reversible.

---

**I edited a file and want the last committed version back**
```bash
git restore <file>          # discards your edits — unrecoverable, be sure
```

**I staged something I didn't mean to**
```bash
git restore --staged <file>     # unstages, edits survive
```

**My last commit message has a typo** (and it's not pushed)
```bash
git commit --amend
```

**I forgot a file in the last commit** (and it's not pushed)
```bash
git add forgotten.txt
git commit --amend --no-edit
```

**I want to undo the last commit but keep the work**
```bash
git reset --soft HEAD~1     # changes stay staged
git reset HEAD~1            # changes stay in working tree (unstaged)
```

**I committed to `main` but meant to commit to a branch**
```bash
git branch feature/my-work      # bookmark the work
git reset --hard origin/main    # move main back
git switch feature/my-work      # continue there
```

**I need to undo a commit that's already pushed**
```bash
git revert <sha>            # creates an inverse commit; safe for shared history
git push
```
Do **not** use `reset --hard` + force-push on a shared branch.

**I ran `git reset --hard` and lost commits**
```bash
git reflog                  # find the SHA from before the reset
git reset --hard <sha>
```
`reflog` records every position of HEAD for ~90 days. This works after bad
resets, bad rebases, bad amends, and deleted branches.

**I deleted a branch that had work on it**
```bash
git reflog                  # find its last commit
git switch -c <branch> <sha>
```

**I'm in a conflicted merge and want out**
```bash
git merge --abort
```

**I'm mid-rebase and it's going badly**
```bash
git rebase --abort
```

**Detached HEAD — I made commits and don't want to lose them**
```bash
git switch -c rescue-branch     # names the commits you're sitting on
```

**My push was rejected (non-fast-forward)**
```bash
git pull --rebase       # or plain `git pull` to merge
git push
```
If you truly need to overwrite the remote branch (your own, unshared):
```bash
git push --force-with-lease     # refuses if someone else pushed meanwhile
```
Never plain `--force` on anything anyone else uses.

**I committed a secret**

Rotate the secret first — assume it's compromised the moment it's pushed.
Removing it from history requires rewriting history (`git filter-repo` or
BFG Repo-Cleaner) plus a force-push plus everyone re-cloning. The rotation is
the part that actually protects you.

**I committed a huge file and the repo is slow**

Same situation: it's in history forever until history is rewritten. Prevent it
with `.gitignore` and Git LFS for genuinely large assets.

---

## The one thing that isn't recoverable

Uncommitted, unstaged changes destroyed by `git restore` or `git reset --hard`.
Git never saw them, so git can't bring them back. When in doubt:
`git stash` instead of discarding.
