# Weekly recap agent instructions

You run as a scheduled task on Friday evenings (~17:45 Europe/London), after that day's lesson has gone out. Your job: send a summary of everything covered this week.

## 1. Orient

- `git pull` first. Read `config.md`, `curriculum.md` (Progress + Log), `feedback.md`.
- This week's lessons = files in `lessons/` dated Monday–Friday of the current week (Europe/London). Read all of them in full.
- If there are no lessons this week, stop without emailing and say so in the final summary. If `recaps/<today>.md` exists, stop (no duplicate).
- Search Gmail (`subject:("Stochastic Calculus" "Day <N>") newer_than:2d`, then `get_thread`) for any reply to today's lesson that arrived after the lesson was sent; if found, grade it in the recap and log it in `feedback.md` as in `PROMPT.md` step 2 (then the next daily run will see it as already handled — note `Graded in Week <W> recap` in the entry).

## 2. Write the recap

1. **This week in one paragraph**: the story arc — how each day built on the previous one, ending where the next week picks up.
2. **Day-by-day summary**: for each lesson, 3–5 bullets: key definitions, the main theorem/formula (written out), the intuition, and the Python idea.
3. **Formula sheet**: every key formula from the week in one compact list.
4. **How you did**: from `feedback.md` this week — strengths, concepts still `open`, and a specific suggestion for each weak spot. If there were no replies, one encouraging line inviting them to reply to lessons.
5. **Weekend challenge (interactive)**: 3 synthesis questions that combine at least two of this week's topics (one MC, one derivation, one coding task), with "reply with your answers — they'll be graded in Monday's lesson". Put full solutions in the archive file only.
6. **Next week**: the upcoming roadmap items and why they follow from this week.

Review it for correctness (formulas, signs, numeric claims) before sending.

## 3. Archive

Write `recaps/YYYY-MM-DD.md` with the recap plus a `## Solutions` section for the weekend challenge. Note in `feedback.md` any entries graded here. Commit with message `Week <W> recap`, `git pull --rebase && git push` (retry once on failure; still send the email if it fails).

The next Monday daily run should grade replies to the weekend challenge: add a line to the top of the recap file `Weekend challenge thread subject: <subject>` so the daily agent can find it, and the daily agent's step 2 already looks at replies to recap threads in the last 7 days.

## 4. Email

Gmail `send_message`: `to`/`cc` from `config.md`, subject `Stochastic Calculus — Week <W> Recap — <YYYY-MM-DD>`, `htmlBody` as simple clean HTML plus a plain-text `body` fallback. No solutions in the email.

## 5. Final summary

State the week number, lessons covered, whether the push and email succeeded, and anything that failed.
