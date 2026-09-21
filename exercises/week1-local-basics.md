# Week 1 drill — the local loop

Work in a scratch directory. Type every command; don't paste the block.

## Part A — a repo from nothing

```bash
mkdir -p ~/git-practice/w1 && cd ~/git-practice/w1
git init
echo "# Recipes" > README.md
git status                    # read it. what does it say to do?
git add README.md
git status                    # read it again. what changed?
git commit -m "Add README"
git log --oneline
```

Now inspect what you made:
```bash
git show HEAD
git cat-file -p HEAD          # the raw commit object — tree, author, message
```

## Part B — the three areas

```bash
printf "pasta\ntomato\nbasil\n" > shopping.txt
git add shopping.txt
printf "pasta\ntomato\nbasil\ngarlic\n" > shopping.txt

git diff                      # staged vs working tree  -> shows garlic
git diff --staged             # last commit vs staged    -> shows the first 3
```

Stop and make sure you understand why those two outputs differ. This is the
single most common source of confusion in Week 1.

```bash
git add shopping.txt
git commit -m "Add shopping list"
```

## Part C — partial staging

```bash
printf "pasta\ntomato\nbasil\ngarlic\nolive oil\n" > shopping.txt
sed -i '1i # Shopping' shopping.txt     # macOS: sed -i '' '1i\'$'\n''# Shopping'
git add -p shopping.txt
```
Stage **only** the header hunk (`y` / `n` per hunk; `?` lists all options).
Then:
```bash
git commit -m "Add heading to shopping list"
git status                    # olive oil should still be uncommitted
git commit -am "Add olive oil"
```

## Part D — ignoring things

```bash
mkdir build && echo "junk" > build/out.o
git status                    # build/ shows as untracked
echo "build/" > .gitignore
git status                    # gone; .gitignore is now untracked
git add .gitignore && git commit -m "Ignore build output"
```

## Part E — write one real commit message

Make any change, then run bare `git commit` (no `-m`) and write:
- a subject line in imperative mood, ≤50 chars, no period
- a blank line
- two sentences on *why*, wrapped at 72 chars

## Checkpoint

1. What are the three areas, and which command moves between each pair?
2. `git diff` vs `git diff --staged` — which compares what?
3. What does `git add -p` let you do that `git add` doesn't?
4. Why should `build/` never be committed?
