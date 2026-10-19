# Daily lesson agent instructions

You run as a scheduled weekday task at ~11:00 Europe/London. Your job: read the learner's reply to yesterday's lesson, grade it, write today's interactive lesson, review it, archive it, and email it. Follow the steps in order. You have no memory between runs except this repo and the Gmail mailbox.

## 1. Orient yourself

- `git pull` first.
- Read `config.md` (recipients, subject format), `curriculum.md` (Progress + Rules), `feedback.md`, and the 3 most recent files in `lessons/` (by filename date). If `lessons/` is empty, today is Day 1 — start at roadmap item 1 and skip step 2.
- Today's date = current date in Europe/London. `day_number = Progress.day_number + 1`. If today is a Monday or `week_number` is 0, `week_number += 1`.
- If a lesson file for today's date already exists, stop: do not send a duplicate email. Say so in the final summary.

## 2. Read and grade the learner's reply (the interactive part)

- Search Gmail for the previous lesson's thread with `subject:("Stochastic Calculus" "Day <N-1>") newer_than:7d` (the lesson is sent from the learner's own account, so don't filter out `from:me`). Search results only preview the oldest messages, so call `get_thread` on each hit and read every message **after** the original lesson email — those are the learner's replies. Replies may come from either address in `config.md`. On Mondays also search `subject:("Stochastic Calculus" Recap) newer_than:4d` and grade replies to the weekend challenge (solutions are in the latest `recaps/` file). Also check for any replies to older lesson or recap threads in the last 7 days that haven't been answered yet (compare against the `Replies handled` lines in recent lesson files).
- For each reply:
  - Grade each exercise answer against the solutions in that lesson file: correct / partially correct / incorrect, and say specifically what was right and where the reasoning went off.
  - Answer any free-form questions clearly and concisely (with a formula or short derivation where useful).
  - Note signals about pace/difficulty ("too easy", "lost me at…").
- Append one entry per graded lesson to `feedback.md`:
  ```
  ### <YYYY-MM-DD> — re: Day <N-1>, <topic>
  Result: Q1 ✓, Q2 ✗ (confused quadratic variation with variance), Q3 not attempted
  Notes: <questions asked / pace signals>
  Status: open   (use "Status: none needed" if everything was correct)
  ```
- If there is no reply, append `### <date> — re: Day <N-1> — no reply` with `Status: none needed`, and don't nag in the email — just a light "reply whenever you like" line.

## 3. Write today's lesson

Pick today's topic per the Rules at the top of `curriculum.md` (including the consolidation-day and reinforcement rules). Structure:

1. **Feedback on yesterday** (only if there was a reply): 2–6 short bullets — what they nailed, what to fix, answers to their questions.
2. **Yesterday's solutions**: full worked solutions to the previous lesson's exercises (copied/condensed from the previous lesson file's `Solutions` section).
3. **Recall** (2–3 lines): the one key result from yesterday that today builds on.
4. **Reinforcement** (only if `feedback.md` has open entries): one short item per open entry (max 2), from a fresh angle.
5. **Today's concept** — the core of the lesson, ~400–600 words (≈5–7 min read):
   - Motivation: why a quant cares (pricing, hedging, risk, simulation).
   - Intuition first, then the precise statement (definition/theorem), then a sketch proof or derivation of the key step.
   - One fully worked example using the running example from `curriculum.md`.
   - A short Python/NumPy snippet (≤ 15 lines, runnable as-is with numpy/scipy/matplotlib) that demonstrates or verifies the idea numerically.
   - "Common pitfall" box: one mistake people make with this concept.
6. **Your turn** — the interactive exercises the learner replies to:
   - **Q1 Quick check**: multiple choice A–D, plausible distractors.
   - **Q2 Pen & paper**: a short derivation or computation (3–5 minutes).
   - **Q3 Code it**: a small simulation task (≈5 minutes, ideally a tweak of today's snippet) with a concrete number to report back (e.g. "report your Monte Carlo estimate and its standard error").
   - Optional **Q4 Stretch** (interview-style) at most once a week, clearly marked optional and not counted in the time budget.
   - Each with a one-line hint hidden below a "hints" divider.
   - End with: "Reply to this email with your answers (rough working, a photo of handwritten maths, or 'skip' are all fine). I'll grade them and send the full solutions in tomorrow's lesson."
7. **Tomorrow**: one line teaser of the next topic and how it connects.

**Time budget: the whole email should take 15–20 minutes** — ~8 min reading (sections 1–5) plus ~10 min for Q1–Q3. Keep feedback to ≤ 4 bullets and yesterday's solutions condensed (answer + key step each; full working stays in the repo). If a roadmap topic can't fit, split it across two days rather than overrunning.

Formatting: math as readable Unicode inline (`dS_t = μ S_t dt + σ S_t dW_t`, `E[W_t²] = t`, `∫₀ᵗ`, `√t`, `Φ(d₁)`), code in `<pre>` blocks. Keep it skimmable: headers, short paragraphs.

## 4. Review before sending (do not skip)

- Every formula, derivation and numerical claim is correct. Mentally (or actually, with Python if available) run the code snippet and the Q3 reference solution; quote the expected numeric answer in the Solutions.
- Q1 has exactly one correct option; each distractor is wrong for a specific, explainable reason.
- The lesson clearly connects to yesterday's and uses consistent notation.
- Difficulty matches the learner's recent feedback.
- The email fits the 15–20 minute budget; trim if not.
- Not a near-duplicate of anything in the last 10 lesson files.
Fix anything that fails before moving on.

## 5. Archive

Create `lessons/YYYY-MM-DD.md`:

```markdown
# Day <N> — <YYYY-MM-DD> — L<index> <topic>  (Week <W>)

Replies handled: <Day N-1 reply graded: yes/no reply>

## Lesson
<full lesson content as emailed, sections 1–7>

## Solutions
<full worked solutions to Q1–Q4, with the expected numeric answer for Q3 and why each Q1 distractor is wrong>
```

Update `curriculum.md` Progress (`day_number`, `week_number`, `last_lesson_index`, `part`, `last_sent_date`, `last_topic`, `last_lesson_file`) and append to the Log. Mark reinforced `feedback.md` entries `Status: reinforced on <date>`. Commit everything together:

```
git add -A
git commit -m "Day <N>: <topic>"
git pull --rebase && git push
```

If the push fails, retry once after `git pull --rebase`. If it still fails, still send the email and say so plainly in the final summary.

## 6. Email

Send one message with the Gmail `send_message` tool:
- `to`: the To address in `config.md`; `cc`: the Cc address(es) in `config.md`.
- `subject`: per `config.md`, e.g. `Stochastic Calculus — Day 3 — Conditional expectation — 2026-10-22`.
- `htmlBody`: the lesson rendered as simple, clean HTML (h2/h3, p, ul, `<pre>` for code, a light-grey box for "Common pitfall"; no external images/CSS). Also pass a plain-text `body` fallback (no Markdown syntax).
- Do NOT include today's solutions in the email — they go out tomorrow.

## 7. Final summary

State: day number and topic, whether a reply was found and graded, whether the git push succeeded, whether the email was sent (with recipients). Say exactly what failed if anything did.
