# Learn Git & GitHub

A self-paced, hands-on plan to go from "I've heard of git" to confidently
collaborating on real projects.

This repository **is** the course. You learn git by doing git *to this repo*:
every exercise is something you actually run here, commit, and push.

## How this is organized

| File | What it's for |
|---|---|
| [`docs/plan.md`](docs/plan.md) | The 6-week curriculum, week by week |
| [`docs/mental-model.md`](docs/mental-model.md) | How git actually works underneath — read this early |
| [`docs/cheatsheet.md`](docs/cheatsheet.md) | Commands grouped by what you're trying to do |
| [`docs/recovery.md`](docs/recovery.md) | "I broke it" — how to undo almost anything |
| [`docs/github.md`](docs/github.md) | PRs, reviews, Issues, Actions, the collaboration layer |
| [`docs/resources.md`](docs/resources.md) | Vetted books, tutorials, games, references |
| [`exercises/`](exercises/) | One drill per week, with a checklist |
| [`PROGRESS.md`](PROGRESS.md) | Tick things off as you go |

## Start here

1. Read [`docs/mental-model.md`](docs/mental-model.md) (~15 min). Do not skip it.
   Most git confusion is a broken mental model, not a forgotten command.
2. Open [`docs/plan.md`](docs/plan.md) and begin Week 1.
3. Do the matching drill in [`exercises/`](exercises/).
4. Update [`PROGRESS.md`](PROGRESS.md) and commit it. That commit *is* practice.

## Time commitment

About **4–6 hours per week for 6 weeks**. It works at half speed over 12 weeks
too — the sequence matters more than the pace. The only hard rule: do not read
ahead without doing the drills. Git is muscle memory.

## One-time setup

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase false     # merge on pull; safe default
git config --global core.editor "code --wait"   # or vim, nano, etc.

# Make your history readable
git config --global alias.lg "log --oneline --graph --decorate --all"
```

Then verify: `git config --list --show-origin`
