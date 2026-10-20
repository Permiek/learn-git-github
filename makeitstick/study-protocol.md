# The study protocol

How to run [`../docs/plan.md`](../docs/plan.md) so it sticks. This replaces
"read the week, do the drill" with something less comfortable and more durable.

## The weekly shape

Four sessions, not one. Roughly 45–75 minutes each, on different days.

| Session | What you do |
|---|---|
| **1 — Generate, then learn** | *Before* reading the week: answer this week's checkpoint questions cold. You'll fail most. That's the point — it primes the reading. Then read the week's concepts. |
| **2 — Drill** | Do the week's exercise file. Cheatsheet **closed**. Look things up only after attempting from memory. |
| **3 — Interleave** | Do this week's drill again *mixed with* a random drill from an earlier week (see the rotation below). |
| **4 — Retrieve and reflect** | Closed-book: answer this week's checkpoint questions *and* a prior week's. Write two sentences in `PROGRESS.md` about what's still shaky. Commit it. |

## The interleaving rotation

In session 3 each week, revisit an earlier week rather than the most recent one:

| Current week | Also drill |
|---|---|
| 2 | Week 1 partial staging (`add -p`) |
| 3 | Week 1 commit hygiene + Week 2 conflict resolution |
| 4 | Week 2 merge vs fast-forward |
| 5 | Week 3 fetch vs pull, rejected push |
| 6 | Week 2 conflicts + Week 5 reflog recovery |

Mixing feels worse than blocking. Retention data says do it anyway.

## The spacing schedule

Retrieve each week's material at expanding intervals. A topic you can recall
easily isn't due yet; wait until it's slightly hard.

```
Week 1 material  -> retrieve in weeks 2, 4, and 6
Week 2 material  -> retrieve in weeks 3, 5, and after the course
Week 3 material  -> retrieve in weeks 4 and 6
Week 4 material  -> retrieve in week 6
Week 5 material  -> retrieve in week 6 and one month later
```

## The rules that make it work

1. **Cheatsheet closed by default.** Attempt from memory, fail, *then* look.
   The failed attempt is what makes the lookup stick.
2. **Predict before you run.** Before pressing enter on any drill command, say
   what it will do to the working tree, the index, and HEAD. Then check with
   `git status` and `git lg`. Wrong predictions are the most valuable events in
   the whole course.
3. **No advancing on comfort.** The gate is the checkpoint questions answered
   aloud, unaided. Feeling like you understood the reading is not evidence.
4. **Break things deliberately.** Week 5 exists because recovery under mild
   panic is the actual skill. Do `reset --hard` on purpose, repeatedly, until
   `reflog` is reflex.
5. **Two sentences of reflection per session,** committed. It's reflection,
   spaced retrieval, and git practice at once.

## A one-month booster

Four weeks after finishing, do one 45-minute session:

- Answer 10 random questions from [`retrieval-questions.md`](retrieval-questions.md)
- Redo the Week 5 reflog recovery drill from scratch
- Open a PR on something real

This single session is worth more than several hours of rereading, because by
then the material has faded enough that retrieving it is genuinely effortful.

## Tracking honestly

In `PROGRESS.md`, don't tick a box for having *read* something. Tick it for
having *produced* it unaided. The distinction is the whole point of the book.
