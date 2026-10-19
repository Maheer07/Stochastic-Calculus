# Stochastic-Calculus

Archive and memory for a daily, interactive stochastic-calculus-for-quant-finance course delivered by email.

- `curriculum.md` — the lesson roadmap and progress pointer. The daily agent reads it to decide what today builds on.
- `lessons/YYYY-MM-DD.md` — one file per weekday lesson (each email is ~15–20 minutes): the concept, worked example, exercises, and the full solutions (solutions are emailed the *next* day, after you have had a chance to reply).
- `recaps/YYYY-MM-DD.md` — the Friday-evening weekly summaries.
- `feedback.md` — your replies and how you did. Topics you struggled with get reinforced in later lessons.
- `PROMPT.md` — instructions the 11:00 daily lesson agent follows.
- `WEEKLY.md` — instructions the Friday-evening recap agent follows.
- `config.md` — recipients and schedule notes. Edit this to change who receives the emails.

## How the interactive loop works

1. Each lesson email ends with a "Your turn" section: a quick-check multiple-choice question, a short derivation, and a small Python simulation to run.
2. **Reply to the lesson email** with your answers (rough working is fine — a photo of handwritten maths works too, or just "skip").
3. The next morning's agent reads your reply, grades it, and opens the new email with personalised feedback, then reveals the full solutions to yesterday's exercises.
4. Anything you got wrong or flagged as confusing goes into `feedback.md` and is reinforced in upcoming lessons and the Friday recap.

You can also reply with free-form questions ("why is dW² = dt?") and they will be answered at the top of the next email.

The schedule is run by Claude Code scheduled tasks: weekday lessons around 11:00 Europe/London, weekly recap Friday ~17:45 Europe/London.
