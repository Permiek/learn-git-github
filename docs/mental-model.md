# The Mental Model

Read this before memorizing any commands. Almost every "git is confusing"
moment comes from not having this picture.

## 1. A commit is a snapshot, not a diff

A commit stores: the **full tree** of your files at that moment, a pointer to
its **parent** commit(s), an author, a message, and a timestamp. Git hashes all
of that into a 40-character SHA-1 id.

Git *shows* you diffs (by comparing two snapshots), but it *stores* snapshots.
This is why branching and switching are instant: it's just moving a pointer.

```
A ── B ── C          each letter is a complete snapshot
          ^
          main       a branch is a sticky note on a commit
```

## 2. A branch is a movable pointer, nothing more

`main`, `feature/login` — these are 41-byte files containing a commit SHA.
Creating a branch is free. Deleting a branch deletes the sticky note, not the
commits.

`HEAD` is a pointer to *which branch you're on*. "Detached HEAD" just means HEAD
points straight at a commit instead of at a branch — not an error, just a state.

## 3. The three places a file can live

```
  working tree  ──git add──>  staging area  ──git commit──>  repository
  (your files)                ("the index")                  (history)
```

- **Working tree** — what you see in your editor.
- **Staging area / index** — what will go into the *next* commit. This is git's
  best feature and the thing other tools lack: you choose exactly what to commit.
- **Repository** — the permanent, hashed history in `.git/`.

`git status` reports on the boundaries between these three. Read its output
carefully — it literally tells you the command to move things around.

## 4. Local vs remote are separate repositories

`origin/main` is **your local cache** of where `main` was on GitHub the last
time you talked to it. It is not live.

- `git fetch` — update that cache. Changes nothing in your working tree. Safe.
- `git merge` — combine another branch into yours.
- `git pull` = `fetch` + `merge` (or `+ rebase`). That's all it is.
- `git push` — send your commits to the remote and move its branch pointer.

When someone says "push rejected, non-fast-forward", it means: the remote branch
has commits you don't have. Fetch, integrate, then push.

## 5. Merge vs rebase

Both combine work. They differ in the history they leave behind.

**Merge** creates a new commit with two parents. History is truthful and
non-linear.

```
A ── B ────── M   <- main
      \      /
       C ── D
```

**Rebase** replays your commits on top of another branch, creating *new* commits
with new SHAs. History is linear and clean, but rewritten.

```
A ── B ── C' ── D'   <- your branch, replayed
```

**The golden rule:** never rebase commits that other people have already pulled.
Rewriting shared history forces everyone else to clean up. Rebase your own
un-pushed work freely; merge when history is shared.

## 6. Almost nothing is truly lost

Commits are immutable and reachable via `git reflog` for ~90 days, even after a
bad reset or a deleted branch. Uncommitted changes are the only genuinely
fragile thing.

**Practical rule: commit early and often.** A commit is a save point. You can
always tidy the history later with `git rebase -i`.
