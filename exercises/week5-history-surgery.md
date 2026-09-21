# Week 5 drill — history surgery and rescue

Do this in a throwaway repo. You are going to break things deliberately.

```bash
mkdir -p ~/git-practice/w5 && cd ~/git-practice/w5 && git init
for i in 1 2 3 4 5; do echo "line $i" >> f.txt; git add f.txt; \
  git commit -m "Add line $i"; done
git lg
```

## Part A — the three resets

Run each, inspect with `git status` and `git log --oneline`, then restore with
`git reset --hard <original-sha>` before the next one.

```bash
git reset --soft  HEAD~1      # commit undone, changes STAGED
git reset --mixed HEAD~1      # commit undone, changes UNSTAGED
git reset --hard  HEAD~1      # commit undone, changes GONE
```

Write down, in your own words, which of the three areas each variant touched.

## Part B — reflog is the undo button

```bash
git reset --hard HEAD~3       # destroy three commits
git log --oneline             # they're gone
git reflog                    # they are not gone
git reset --hard <sha-from-before-the-reset>
git lg                        # all five commits back
```

Do this twice. The goal is for it to stop feeling scary.

## Part C — interactive rebase

```bash
git rebase -i HEAD~4
```
In the editor, practice each of these (one rebase per goal):
- `reword` — change a commit message
- `squash` / `fixup` — combine two commits into one
- `drop` — delete a commit entirely
- reorder two lines — swap commit order
- `edit` — stop at a commit, change a file, `git commit --amend`,
  `git rebase --continue`

Check `git lg` after each. Note that every SHA changed — these are new commits.

## Part D — revert vs reset

```bash
git revert HEAD               # adds a new commit undoing the last one
git lg                        # history grew; nothing was rewritten
```
Explain to yourself why this, and not `reset`, is correct on a shared branch.

## Part E — stash

```bash
echo "work in progress" >> f.txt
git stash push -m "wip"
git status                    # clean
git switch -c hotfix && echo fix >> f.txt && git commit -am "Hotfix"
git switch main
git stash list
git stash pop
```

## Part F — cherry-pick

```bash
git log --oneline hotfix
git cherry-pick <sha-of-hotfix-commit>
git lg                        # same change, different SHA
```

## Part G — bisect

```bash
for i in $(seq 1 20); do echo "v$i" > app.txt; git commit -am "Change $i"; done
# pick a middle commit and pretend it's where a bug appeared
git bisect start
git bisect bad                # HEAD is broken
git bisect good HEAD~19       # this one was fine
# at each step: test, then `git bisect good` or `git bisect bad`
git bisect reset
```

## Checkpoint

1. `--soft`, `--mixed`, `--hard`: which areas does each reset?
2. When must you use `revert` instead of `reset`?
3. How long does reflog keep unreachable commits, roughly?
4. What is the one kind of loss git *cannot* help you with?
