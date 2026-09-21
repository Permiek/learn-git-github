# Cheatsheet — grouped by intent

Organized by "what am I trying to do", not alphabetically.

## Starting out
```bash
git init                          # new repo here
git clone <url> [dir]             # copy an existing repo
git clone --depth 1 <url>         # shallow, fast, no full history
```

## Seeing what's going on
```bash
git status                        # read this constantly
git status -sb                    # compact version
git diff                          # working tree vs staged
git diff --staged                 # staged vs last commit
git diff main..feature            # between two branches
git log --oneline --graph --decorate --all     # aliased above as `git lg`
git log -p <file>                 # history of one file, with diffs
git log -S"someString"            # commits that added/removed that string
git show <sha>                    # one commit in full
git blame <file>                  # who last touched each line
```

## Saving work
```bash
git add <file>                    # stage a file
git add -p                        # stage hunk by hunk — learn this one
git add -A                        # stage everything, including deletions
git commit -m "Subject"           # commit staged changes
git commit                        # open editor for a proper message body
git commit --amend                # fix the last commit (only if unpushed)
git commit --amend --no-edit      # add staged changes to last commit, same msg
```

## Branching
```bash
git branch                        # list local
git branch -vv                    # list with tracking info
git switch <branch>               # change branch
git switch -c <branch>            # create and change
git switch -                      # back to previous branch
git branch -d <branch>            # delete (safe; refuses if unmerged)
git branch -D <branch>            # delete (force)
git branch -m <new-name>          # rename current branch
```

## Combining work
```bash
git merge <branch>                # merge into current branch
git merge --abort                 # bail out of a conflicted merge
git rebase main                   # replay current branch on top of main
git rebase --continue / --abort
git cherry-pick <sha>             # copy one commit onto current branch
```

## Remotes
```bash
git remote -v
git remote add origin <url>
git fetch origin                  # update cache; touches nothing else
git pull                          # fetch + merge
git pull --rebase                 # fetch + rebase
git push -u origin <branch>       # push and set upstream
git push --force-with-lease       # safe force push; never plain --force
git push origin --delete <branch> # delete a remote branch
```

## Undoing (see recovery.md for the full map)
```bash
git restore <file>                # discard working-tree changes to a file
git restore --staged <file>       # unstage, keep changes
git reset --soft  HEAD~1          # undo commit, keep changes staged
git reset --mixed HEAD~1          # undo commit, keep changes unstaged (default)
git reset --hard  HEAD~1          # undo commit AND discard changes — dangerous
git revert <sha>                  # new commit that undoes <sha>; safe on shared
git reflog                        # everywhere HEAD has been; your safety net
```

## Context switching
```bash
git stash push -m "wip: login"
git stash list
git stash pop                     # apply and drop
git stash apply stash@{1}         # apply, keep in stash
git worktree add ../hotfix main   # second working dir, same repo
```

## Finding a bad commit
```bash
git bisect start
git bisect bad                    # current commit is broken
git bisect good <sha>             # this old one worked
# ... test, then `git bisect good` or `git bisect bad` each step
git bisect reset
```

## Tags and releases
```bash
git tag -a v1.2.0 -m "Release 1.2.0"
git push origin v1.2.0
git tag -l "v1.*"
git describe --tags
```

## Config
```bash
git config --list --show-origin
git config --global core.excludesfile ~/.gitignore_global
git config --global rerere.enabled true    # remember conflict resolutions
```
