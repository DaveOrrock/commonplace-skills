---
name: job-scouting
description: Use when finding new roles, capturing a job posting into the vault, checking whether a posting is real, building a target-company market map, or watching companies for hiring signals. Also when the user pastes a job URL or says "I found a role".
---

# Job scouting

**REQUIRED BACKGROUND:** job-hunt-hq (data model, placeholders).

Two modes: **hunting** (proactive search against the market map) and **capture** (a specific posting arrives). Either way, nothing enters the pipeline without triage — effort spent on a ghost job or an obvious mismatch is stolen from real opportunities.

## The market map beats the job board

Maintain `{{companies}}` as a tiered universe (A: would drop everything; B: strong; C: opportunistic) built from the user's `{{profile}}`. When hunting, search where the map points — company careers pages first, then boards. Every captured role should cite which map slot it fills; if a role's company isn't on the map, that's a prompt to research it or question why you're looking at it.

Web-search patterns that work: `site:` queries on target careers pages and the major ATS domains (`boards.greenhouse.io`, `jobs.lever.co`, `jobs.ashbyhq.com`, `apply.workable.com`) with title keywords — postings there are usually real and fresher than aggregator copies.

## Ghost-job triage (before any effort)

20-45% of postings are never filled. Check, in order:
1. **Age + reposts** — live 30+ days or repeatedly reposted = suspect.
2. **Cross-board date mismatch** — "3 days ago" on one board, "47 days" on another = recycled.
3. **Careers-page presence** — not on the company's own site = treat as unverified.
4. **Evergreen shape** — vague description, no named team/manager, identical posting across many cities.

Record the verdict as an observation on the role note: `- [triage] posted 6d, on careers page, named team #real`. Suspect roles get `status: triaged` with a `- [risk] likely ghost: …` observation — visible, not deleted.

## Capture

Use `clip_webpage` on the posting URL (it dedupes by URL and stamps `source`/`clipped`). Then create/update the **role note** in `{{roles}}` with the full data model from job-hunt-hq, extracting: title, salary band (numbers, not strings), location + office days, deadline, named team/manager, and the JD's stated requirements as a checklist section. Link `company: "[[…]]"` — create a stub company note if none exists. The clipped posting is provenance; the role note is the working surface.

**Move fast on real, fresh postings.** Reviews typically start within 24-72h and many close once a slate forms; applying early is one of the few free advantages left. A fresh A-tier match should jump the queue into evaluation same-day.

## Signals watchtower (scheduled)

On daily/periodic runs, sweep A/B-tier company notes: clip careers-page deltas and news, append delta-observations (`- [signal] 3 new senior eng postings this week`, `- [signal] CFO departed`). A momentum spike (funding + exec departure + cluster of adjacent postings) can mean an unposted leadership role — flag it as an outreach opportunity rather than waiting for the posting.

## Don'ts

- Don't skip triage because the role looks exciting — excitement is exactly when ghost-checks get skipped.
- Don't bulk-capture mediocre matches to make the pipeline look healthy; 11-20 targeted applications outconvert 100+ sprayed ones ~3.6x.
- Don't evaluate fit here — that's job-evaluation, with the criteria gate. Scouting only answers "real and worth evaluating?"
