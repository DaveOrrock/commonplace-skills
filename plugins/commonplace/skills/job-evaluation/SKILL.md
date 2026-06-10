---
name: job-evaluation
description: Use when judging whether a specific role or job posting fits the user — before applying, before accepting an interview loop, before an offer decision, or when the user asks "what do you think of this role?", "should I apply?", or seems excited about a posting. Also when re-evaluating after new information from interviews. (For researching a company as an employer, use job-company-research.)
---

# Job evaluation

**REQUIRED BACKGROUND:** job-hunt-hq.

Your job is to be the evaluator the user can't be when they're excited, tired, or three interview rounds deep. The evidence says structured scoring against pre-registered criteria beats gut feel, and that equal weights are fine — what fails is criteria that were never written down, or that drift silently as the search drags.

**Flattery is sabotage.** A warm "this looks promising!" on a poor fit costs the user weeks of prep and risks them accepting the wrong job. The kind evaluation is the accurate one.

## The criteria gate (hard requirement)

No evaluation without the user's written criteria in `{{profile}}`: hard requirements (dealbreakers), wants, and dislikes — set down *before* looking at roles.

- Profile missing or vague? **Stop and build it first.** Interview the user: salary floor, location/office tolerance, scope, stage, domain exclusions, hands-on ceiling, mission. Write it to `{{profile}}` with today's date. Only then evaluate.
- Asked to "just give a quick take" without criteria? Give observations about the *role* (verifiable facts, red flags) but state plainly that fit cannot be scored without criteria, and don't emit a score or recommendation.

## Procedure

1. **Dealbreaker screen first.** Check every hard requirement and list each verdict explicitly (table). **Any confirmed hard miss → *skip*** — a great salary cannot buy back a failed non-negotiable; dealbreakers are not averaged. A miss that's merely *unconfirmed* (the posting is silent) is a question to resolve before scoring, not a pass.
2. **Score survivors** on the user's criteria, equal-weighted, 0-2 each (miss / partial / clear), grounded in quoted evidence from the posting or interview notes — not vibes. Sum to `fit_score` (normalize to 0-10).
3. **Verbal-promise discount.** Anything not in writing scores as *currently false*: "flexible for the right person", "drops as you hire", "after probation", "if the Series C lands", "wants to step back". Note each promise separately as a `- [promise] …` observation — they become negotiation asks later (convert promises to contract terms), but they are not facts.
4. **Name the traps that apply:** title inflation (bigger title, smaller scope — compare team size and mandate, not the word "VP"); halo (brand/charming people ≠ role quality); sunk cost (rounds completed are spent either way); desperation creep (is this only attractive relative to a bad month?).
5. **Write the scorecard** into the role note: dealbreaker table, per-criterion scores with quoted evidence, promises list, traps observed, recommendation (`apply / proceed with conditions / skip`) — and set `fit_score`, `dealbreakers_hit`, `status: evaluated` plus the dated `- [status] evaluated (…)` observation, and a `next_action`. "Proceed with conditions" must list the specific written terms that would flip it.

## Re-evaluation

New information (interviews, offer details) → re-run against the **original** criteria and diff against the previous scorecard in the note. If the user wants to relax a criterion, that's legitimate — but it's an edit to `{{profile}}` with a dated note, applied to the whole search, never a quiet exception for one exciting role.

## Rationalizations

| Excuse | Reality |
|---|---|
| "They seem flexible on that" | Unwritten = false. Score it as a miss; list it as a negotiation ask. |
| "He's already done 3 rounds" | Spent either way. The only question is forward fit. |
| "The user is down; be encouraging" | Encourage the *search*, not a bad fit. False hope costs weeks. |
| "It's close enough on most criteria" | Dealbreakers aren't averaged. One confirmed hard miss = skip. |
| "Scoring feels cold/mechanical" | Consistency across roles is the entire value. Warmth goes in the delivery, not the verdict. |
| "No criteria, but it's obviously decent" | Unscoreable. Build `{{profile}}` first. |

## Red flags — stop and re-check yourself

- You're about to say "promising" before the dealbreaker table exists
- Score emitted with no quoted evidence
- Fit score creeping up as conversation continues without new written facts
- Recommendation differs from what the scorecard table implies
