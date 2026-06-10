---
name: job-cv-tailoring
description: Use when creating or tailoring a CV/resume for a specific role, when the user asks to "make my CV ATS-friendly", when reviewing an existing CV, or before any application is submitted.
---

# CV tailoring

**REQUIRED BACKGROUND:** job-hunt-hq, job-evidence-mining (bullets come from the locker).

## What's actually true about ATS (don't optimize for myths)

Modern ATSs parse, store, and route applications; they do not auto-reject on formatting, and "75% rejected by robots" is vendor folklore. Automated rejection lives in **knockout questions** (eligibility, location, work authorization). The real filter is a human doing a ~7-second triage scan across ~250+ applicants. So the CV must (a) **parse cleanly** into the recruiter's database view and (b) **survive human triage** — title, company, dates, and numbers visible at a glance. Tailored CVs roughly double interview rates; that's where the effort goes.

## Format rules (parse-clean + scannable)

- Single column. No tables, text boxes, graphics, icons, photos, or skill-bars. Contact info in the body, **never in the header/footer layer** (parsers drop it).
- Standard headings: Experience, Education, Skills. Reverse-chronological. Role line = **Title — Company, Dates** (the triage scan reads exactly these).
- Text-based PDF is fine for modern systems (export, then verify text is selectable); DOCX if the posting asks. Never image-based/flattened exports.
- Two pages is right for senior candidates (evidence prefers it over one); cut to what's relevant, not to a page count.

## Content rules

- **Every bullet from the evidence locker.** Accomplishment + exact number + how: "Grew platform org 4→15 while cutting change-failure rate 30%". No locker entry → the bullet doesn't exist (or mine it first). Never invent or round up metrics.
- **Mirror the JD's exact terminology for genuinely held skills** — recruiters search the database by the posting's own words; "engineering leadership" ≠ "EM" to a boolean search. Include both acronym and spelled-out forms once each. This is honest keyword work: in-context, in bullets — keyword-stuffed skill dumps are visible and discarded.
- Use the **standard industry title** (or closest honest equivalent) — title is the #1 recruiter search field. A quirky internal title can honestly translate ("Head of Engineering (Director-level, 40 engineers)").
- Lead with a 2-3 line summary targeted at *this* role family only if it adds targeting (senior roles, career pivots); never an "objective".
- Tailoring = reorder and reweight real experience toward this JD's top requirements; check the JD's must-haves each map to a visible bullet or skill.

## Process

1. Read the role note + JD requirements checklist; read `{{profile}}` and the evidence locker.
2. Draft from the master CV; tailor per above. Coverage check: JD must-have → where on the CV?
3. Honesty pass: every number sourced, every skill provable in an interview.
4. Save as a note in `{{applications}}`, named with role + date. **Register the submission** on the role note: `- submitted [[CV — Acme Head of Eng 2026-06]]` with channel — narrative consistency across versions gets audited before interviews, and you never wonder which CV they're holding.
5. `export_pdf` for the send-ready file.
6. **When the application is actually submitted:** set `status: applied`, the `applied` date, the dated `- [status] applied (…)` observation, and `channel` on the role note. The review skill's funnel math runs on these — an unrecorded submission is invisible to every later metric.

## Don'ts

- No fabricated/rounded-up metrics, no skills the user can't defend live — the CV writes cheques interviews must cash.
- No design flourishes to "stand out" — distinctive *content*, boring format.
- Don't submit the master CV "just this once to save time"; untailored CVs convert at half the rate.
- Don't reuse a tailored CV for a different role without re-running the coverage check.
