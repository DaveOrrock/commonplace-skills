---
name: job-hunt-review
description: Use for the weekly job-search review, after any rejection, when the search feels stuck or the user is demoralized, when deciding what to focus on next week, or as a scheduled maintenance run over the pipeline.
---

# Job hunt review

**REQUIRED BACKGROUND:** job-hunt-hq.

The review keeps a months-long search honest: it replaces vibes with the user's own base rates, converts losses into exactly one unit of signal each, and catches the slow failure modes (drift, staleness, tilt) that no single session notices. **Designed to run scheduled and unattended** — it reads the pipeline, writes its findings, and leaves a short report in `{{journal}}`.

## Weekly run

1. **Funnel math (the personal base-rate console).** From role-note properties, compute: applications sent, response/screen/onsite/offer conversions, median days-in-stage — this week and cumulative. Contextualize against external base rates (≈3% of applicants interviewed; senior candidates convert better; 20-30 targeted applications with zero interviews = materials/targeting problem, not noise). Write the table to the report; the dashboards stay live, the report is the interpretation.
2. **Stale-deal sweep.** Every open role with no new observation in 10+ days: draft the next action (follow-up message, chase, prep) or force an explicit close (`closed_reason: ghosted` etc.) with one line of reason. No zombie pipeline flattering the dashboard. Follow-ups 7-10 days after applying put the user in a tiny minority — drafting them is cheap.
3. **Desperation-creep detector.** Trend `fit_score` and salary band of *pursued* roles over the search. Quality trending down while volume trends up = tilt. Flag it with the numbers and quote the user's own week-1 `{{profile}}` criteria back to them before the next application proceeds.
4. **Positioning-drift diff.** Monthly: diff `{{profile}}`'s history (note history / git). Distinguish dated, deliberate edits ("learned the market") from silent erosion — present the month-1 sentences against today's. Drift without a dated decision gets surfaced, not judged.
5. **Assumptions check (monthly).** The search rests on load-bearing assumptions ("my title transfers", "remote roles exist at my level", "Q3 picks up"). Rate each confirmed/unconfirmed/refuted from accumulated evidence; name which single wrong assumption would invalidate the most pipeline.
6. **Next week's focus.** From all the above: 3 concrete actions, max. Tie each to a specific role or gap. Log the report with `log_entry`.

## Rejection protocol

**48-hour quarantine:** log the fact immediately (status, `closed_reason`, date) — but no analysis for 48h; same-day autopsies produce rumination, not signal. After 48h: one structured pass — controllable vs noise, exactly one actionable lesson filed as an observation, funnel stats updated. Then it's closed.

**At 4+ rejections, run competing hypotheses (ACH).** List plausible explanations as columns ("comp expectations high", "story unclear at this seniority", "weak system-design answers", "market timing"); quote evidence from every debrief and rejection note as rows (`quote_evidence` helps); score which hypotheses the evidence actually *discriminates between* — the comfortable story and the supported story are often different. The surviving hypothesis sets next week's focus; revisit as evidence accumulates.

## Morale (evidence, not pep)

When the user is down, the vault has receipts: their own conversion rates vs base rates ("this ghosting is statistically unremarkable; your screen→onsite rate improved month-over-month"), the evidence locker, eagerness signals from live processes. Show the data. If two rejections landed in a week, the poker rule applies: 48h without new applications — decisions made on tilt are the expensive kind.

## Don'ts

- Don't let a "productive" week of low-fit applications pass the review — the creep detector exists for exactly that.
- Don't autopsy inside the quarantine window, even if asked — offer the date it unlocks.
- Don't report metrics without interpretation; the user needs "what this means and what to do", not a spreadsheet.
