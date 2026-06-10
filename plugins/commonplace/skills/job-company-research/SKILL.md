---
name: job-company-research
description: Use when researching a company the user might work for — before an interview loop, before accepting an offer, when a company joins the target map, or when the user asks "what do we know about X?" in a job-hunt context.
---

# Company research

**REQUIRED BACKGROUND:** job-hunt-hq.

Frame: **"would I invest four years of my life?"** — VC-style diligence, written as a memo with pre-registered kill criteria, *before* the offer exists. A shiny offer must not be allowed to override red flags spotted calmly in week 2.

## The memo

Write/extend the company note in `{{companies}}`: a `## Diligence` section plus observations for everything verifiable, each with source: `- [funding] $40M Series B 2025-03, ~18mo runway implied #acme (TechCrunch)`. End the memo with **kill criteria** — pre-registered conditions that mean walk away (e.g. "another layoff round", "CTO departs", "runway < 12mo without a term sheet") — and a verdict: `pursue / pursue with eyes open / avoid`.

## What to dig for

**Viability (startups):** last raise date + amount → implied runway (raise ÷ ~18-24mo burn for the headcount; sanity-check team size vs money). Raise >20 months ago with no revenue story = elevated risk. Ask-in-interview list: months of runway, plan if the next raise slips.

**Layoff recidivism:** any layoff in the last 12 months is a *leading* indicator — ~70% of repeat layoffs come within 12 months of the first, and repeat rounds are common. Search layoffs.fyi, news. One round ≠ disqualifying; pattern + vague comms = kill-criteria candidate.

**Glassdoor protocol (signal vs noise):** read the most recent 20-30 reviews (≤18 months). A theme appearing 3-4+ times across independent reviews and teams = systemic signal; one dramatic review = noise; themes only in old reviews = possibly fixed (verify in interview). Beware coordinated burying (sudden wave of 5-star reviews) — AI-generated review volume is now material. Output: themes as observations, plus **specific interview questions** that test each theme without citing reviews ("how do priorities get set week to week?").

**Leadership:** exec churn in 18 months (LinkedIn), founder/CEO background, who the role reports to and *their* tenure. For the user's evaluation: signs of founder-retained control ("architectural sign-off", very involved CEO) get logged as observations — job-evaluation consumes them.

**People (interviewer film study):** when a loop is scheduled, build/refresh a note per interviewer in `{{contacts}}`: role, tenure, public talks/posts, what they likely ego-invest in, past interview-question reports (Glassdoor interview section). job-interview-prep consumes these.

## Where to look

Careers page + ATS board (real openings, growth shape), Companies House / annual filings (UK), Crunchbase/news for funding, layoffs.fyi, LinkedIn (headcount trend, churn, the panel), Glassdoor (protocol above), the product itself (sign up, use it), engineering blog/GitHub (real stack vs claimed). Clip the load-bearing sources into the vault (`clip_webpage`) so claims keep provenance.

## Don'ts

- Don't research after falling in love — the memo exists to precede the offer.
- Don't average away red flags ("great product, so the Glassdoor stuff is probably fine"); list them and let kill criteria do their job.
- Don't cite Glassdoor in interviews; convert to neutral questions.
- Don't let the memo go stale across a long loop — refresh signals before final rounds and again before accepting.
