# Resources

Ordered by how useful they are for a beginner. You do not need all of them —
pick one primary reference and stick with it.

## Primary references

- **[Pro Git](https://git-scm.com/book/en/v2)** — free, official, and genuinely
  the best book on git. Chapters 1–3 cover Weeks 1–2 of this plan; Chapter 7
  covers Week 5. Read Chapter 10 ("Git Internals") once you're comfortable; it
  makes everything else click.
- **[GitHub Docs](https://docs.github.com)** — authoritative for anything
  GitHub-specific (PRs, Actions, protection rules).
- **[git-scm.com/docs](https://git-scm.com/docs)** — the man pages, online.
  `git help <command>` gives you the same thing offline.

## Interactive practice

- **[Learn Git Branching](https://learngitbranching.js.org)** — visual, in the
  browser, teaches branching/rebasing better than any article. Do this during
  Week 2. Highest value per hour on this whole list.
- **[Oh My Git!](https://ohmygit.org)** — a card game that teaches git. Good if
  the graph still feels abstract.
- **[GitHub Skills](https://skills.github.com)** — short interactive courses run
  as PRs in a real repo. Good for Week 4.

## When you're stuck

- **[Oh Shit, Git!?!](https://ohshitgit.com)** — recovery recipes by symptom.
  (`docs/recovery.md` in this repo covers the same ground.)
- **[git-flight-rules](https://github.com/k88hudson/git-flight-rules)** — an
  exhaustive "what do I do when…" reference. Bookmark it.

## Understanding the internals

- **[Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up/)**
  — builds git up from the object database. Worth it once commands feel routine.
- **[Think Like (a) Git](https://think-like-a-git.net)** — graph theory framing
  for why git behaves the way it does.

## Tools

- **[`gh` CLI](https://cli.github.com)** — GitHub from the terminal
- **[`delta`](https://github.com/dandavison/delta)** — much better diff output
- **[`lazygit`](https://github.com/jesseduffield/lazygit)** — terminal UI; makes
  `add -p` and interactive rebase far easier. Learn the CLI first, though.
- Your editor's git integration (VS Code, JetBrains) — fine for daily use, but
  don't let it be the only way you know how to do things.

## Conventions worth adopting

- **[Conventional Commits](https://www.conventionalcommits.org)** — `feat:`,
  `fix:`, `docs:` prefixes; enables automated changelogs and versioning
- **[Semantic Versioning](https://semver.org)** — what MAJOR.MINOR.PATCH means
- **[How to Write a Git Commit Message](https://cbea.ms/git-commit/)** — the
  essay behind the seven rules everyone cites
