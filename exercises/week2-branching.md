# Week 2 drill — branching, merging, conflicts

Continue in `~/git-practice/w1` (or re-run Week 1 Part A).

## Part A — a clean merge

```bash
git switch -c feat/desserts
printf "tiramisu\npanna cotta\n" > desserts.txt
git add desserts.txt && git commit -m "Add dessert list"

git switch main
git lg                        # note: main does not have desserts.txt
git merge feat/desserts       # "Fast-forward" — no merge commit
git lg
git branch -d feat/desserts
```

Why was that a fast-forward? Because `main` hadn't moved. Git just slid the
pointer forward.

## Part B — a true merge commit

```bash
git switch -c feat/drinks
echo "espresso" > drinks.txt
git add drinks.txt && git commit -m "Add drinks list"

git switch main
echo "focaccia" >> shopping.txt
git commit -am "Add focaccia to shopping"

git merge feat/drinks         # both branches moved -> real merge commit
git lg                        # look at the fork and join in the graph
```

## Part C — make a conflict on purpose

```bash
git switch -c feat/rename
sed -i '1s/.*/# Groceries/' shopping.txt
git commit -am "Rename heading to Groceries"

git switch main
sed -i '1s/.*/# Market List/' shopping.txt
git commit -am "Rename heading to Market List"

git merge feat/rename         # CONFLICT
git status                    # read the guidance it prints
cat shopping.txt              # see the <<<<<<< ======= >>>>>>> markers
```

Resolve it: edit `shopping.txt` so it contains exactly the heading you want and
**no markers**. Then:
```bash
git add shopping.txt
git commit                    # git pre-fills a merge message
git lg
```

## Part D — abort a merge

Create another conflict the same way, then:
```bash
git merge <branch>            # conflict
git merge --abort
git status                    # clean, exactly as before
```

## Part E — Learn Git Branching

Do levels 1–4 of the "Main" track at https://learngitbranching.js.org.
Nothing else in this plan teaches the graph as efficiently.

## Checkpoint

1. When does git fast-forward instead of making a merge commit?
2. What exactly do the conflict markers mean?
3. Why does `git merge --abort` always work but `git commit --amend` on a pushed
   commit is a bad idea?
4. Draw your `git lg` output on paper. Does it match your mental model?
