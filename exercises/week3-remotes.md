# Week 3 drill — remotes and GitHub

## Part A — SSH setup

```bash
ssh-keygen -t ed25519 -C "you@example.com"      # accept defaults
cat ~/.ssh/id_ed25519.pub
```
Paste the public key into GitHub → Settings → SSH and GPG keys → New SSH key.
Verify:
```bash
ssh -T git@github.com
# "Hi <username>! You've successfully authenticated..."
```

## Part B — push your practice repo

Create an empty repo on GitHub named `git-practice` (no README — you already
have one). Then:
```bash
cd ~/git-practice/w1
git remote add origin git@github.com:<you>/git-practice.git
git remote -v
git push -u origin main
git branch -vv                # main now tracks origin/main
```

## Part C — fetch is not pull

Edit `README.md` **on github.com** and commit there. Then locally:
```bash
git fetch origin
git status                    # "behind by 1 commit"
cat README.md                 # UNCHANGED — fetch touched nothing
git log --oneline origin/main # but the cache knows about it
git diff HEAD origin/main
git pull                      # now your files change
```

Make sure you can articulate what `fetch` did and didn't do.

## Part D — a rejected push

```bash
# edit README.md on github.com again and commit there
echo "local change" >> README.md
git commit -am "Local change"
git push                      # REJECTED: non-fast-forward
git pull --rebase             # replay your commit on top of theirs
git push                      # succeeds
git lg
```

## Part E — clone vs fork

```bash
cd ~/git-practice
git clone git@github.com:<you>/git-practice.git clone-test
cd clone-test && git remote -v && git lg
```
Then fork any public repo on GitHub, clone your fork, and add the original as
`upstream`:
```bash
git remote add upstream https://github.com/<original-owner>/<repo>.git
git fetch upstream
git remote -v                 # two remotes: origin (yours), upstream (theirs)
```

## Checkpoint

1. What is `origin/main`, precisely?
2. Why does `git fetch` never cause a conflict?
3. What does the `-u` in `git push -u origin feature` do?
4. When do you fork instead of just branching?
