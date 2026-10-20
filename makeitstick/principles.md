# The principles

A summary of the findings in *Make It Stick* (Brown, Roediger & McDaniel, 2014),
with the git-specific application of each.

---

## 1. Retrieval practice beats rereading

Pulling an answer *out* of memory strengthens it far more than putting it back
in. Every act of recall makes the next recall easier and reshapes the memory to
be more retrievable. Rereading does almost nothing by comparison — but it feels
productive, which is why it stays popular.

**For git:** before you open the cheatsheet, try to write the command from
memory. Getting it wrong first and then checking beats looking it up cleanly.

## 2. Spacing beats massing

Practice spread over time produces much more durable learning than the same
total practice crammed together. The forgetting that happens between sessions is
the mechanism, not the enemy — effortful reconstruction of a partly-faded memory
is what consolidates it.

**For git:** four 45-minute sessions across a week beat one 3-hour Saturday. Come
back to Week 2's branching material during Week 4, when it's gone slightly cold.

## 3. Interleaving beats blocking

Mixing problem types within a session feels messier and tests worse in the short
run, but produces markedly better retention and — crucially — better ability to
*pick the right approach* when problems arrive unlabeled.

**For git:** don't do twenty merges in a row. Mix merge, rebase, reset, and
stash drills in one session. Real work never announces which tool it needs.

## 4. Desirable difficulties

Conditions that slow acquisition often strengthen retention: retrieval with
effort, spacing, interleaving, varied practice, generating an answer before
being shown one. Easy, fluent practice produces fast forgetting.

**For git:** deliberately break the repo and recover it. Work without the
cheatsheet open. Use the CLI before the GUI.

## 5. Beware the illusion of knowing

Fluency with material in front of you is not the same as being able to produce
it. Highlighting, rereading, and watching someone else do it all generate
confidence without competence. The only reliable gauge is testing yourself.

**For git:** "I understand rebase" after reading about rebase means nothing.
Can you, right now, with no notes, squash three commits and explain what changed
about their SHAs?

## 6. Generation and elaboration

Attempting a solution before being taught it — even failing — primes you to
learn the real answer better. Explaining new material in your own words and
connecting it to what you already know builds more retrieval routes to it.

**For git:** before reading about merge conflicts, predict what git will do when
two branches edit the same line. Then check. Explain the staging area to someone
else, out loud.

## 7. Reflection

Reviewing what happened, what you'd do differently, and what it connects to is a
form of spaced retrieval plus elaboration. A few minutes of it is high-yield.

**For git:** after each session, write two sentences in `PROGRESS.md` about what
confused you. Commit it. You get reflection and git practice in one move.

## 8. Calibration against an objective standard

Because your subjective sense of mastery is unreliable, check it against
something external — a quiz, a test, a task you either can or can't complete.

**For git:** the checkpoint questions at the end of each drill. Answer them
aloud, unaided, before moving on. If you hedge, you don't know it yet.

## 9. Effort and struggle build ability

Abilities are substantially trainable, and difficulty during learning is a sign
of construction, not of deficiency. Treating struggle as evidence you're
"not a git person" is the single most expensive mistake available here.

**For git:** everyone finds rebase confusing at first. The confusion is the
work happening.

---

## What this rules out

Tactics that feel like studying and mostly aren't:

- Rereading the cheatsheet
- Highlighting a tutorial
- Watching a video course without a terminal open
- Copy-pasting commands you haven't predicted the effect of
- Blocked practice — one topic drilled until fluent, then abandoned
