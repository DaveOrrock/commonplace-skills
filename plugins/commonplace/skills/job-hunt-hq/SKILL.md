---
name: job-hunt-hq
description: Use when starting any job-hunt work in a Commonplace vault, when unsure where job-hunt notes live or what properties to use, or when setting up dashboards, automation cadence, or the search itself. Background for all other job-* skills.
---

# Job Hunt HQ

The vault is the single source of truth for the entire search: every role, judgment, conversation, and artifact is a note other sessions can query. A judgment that isn't written back didn't happen.

## Placeholder convention (read first)

Folder and note references in all `job-*` skills are placeholders like `{{roles}}`, `{{companies}}`, `{{profile}}`. Resolve them from the vault's `AGENTS.md` (the server injects it). If `AGENTS.md` doesn't define job-hunt locations yet, **ask the user once, then record the mapping in `AGENTS.md`** so every future session inherits it. Never hardcode or guess paths.

Standard placeholders: `{{roles}}` `{{companies}}` `{{applications}}` `{{profile}}` (criteria + positioning) `{{evidence-locker}}` `{{comp-file}}` `{{dossier}}` `{{contacts}}` `{{debriefs}}` `{{journal}}`.

## Data model

**Role note** (one per opportunity, in `{{roles}}`):
```yaml
type: role
company: "[[Acme]]"
status: spotted | triaged | evaluated | applying | applied | screening | interviewing | offer | closed
# spotted = captured, ghost-check pending; triaged = passed ghost-check, awaiting evaluation
next_action: "chase recruiter"     # one line; whoever moves the role sets it
next_action_date: date
fit_score: 0-10        # from job-evaluation; never set without it
dealbreakers_hit: []   # from job-evaluation
salary_min / salary_max: numbers
location: …            # + office days/week if hybrid
source: url
deadline / applied / closed: dates
closed_reason: rejected | withdrawn | ghosted | expired | accepted
channel: cold | referral | sourced | outreach
```

**Company note** (`{{companies}}`): `type: company`, `tier: A | B | C`, plus observations (`- [funding] …`, `- [risk] …`, `- [hiring-signal] …`) and relations (`- hiring_for [[role note]]`).

**Status is a one-way ratchet** except `closed`: never move a role backwards silently — close it with a reason and open a new note if it genuinely reappears.

**Every status change is also logged as a dated observation** on the role note — `- [status] screening (2026-06-12)` — by whichever skill makes the change. This is what makes funnel conversion, days-in-stage, and offer-date projection computable later; the mutable `status` property alone loses history. A role's **tier is its company's `tier`** (follow the `company` link); roles don't carry their own.

**Comp capture is constant:** whenever a compensation number surfaces in *any* job-hunt conversation — recruiter band, posted range, an offer — file it immediately as `- [comp] …` in `{{comp-file}}` (format in job-evidence-mining). Numbers heard and not filed are leverage lost.

**The evidence locker is the honesty backstop** (job-evidence-mining): no metric or claim appears in any CV, letter, message, or interview answer unless it's locker-sourced. Skills reference this rule rather than restating it.

## Lifecycle and which skill owns each step

| Transition | Skill |
|---|---|
| found → `spotted` (capture) → `triaged` (ghost-check passed) | job-scouting |
| `triaged` → `evaluated` (scored against criteria) | job-evaluation |
| company diligence before deep investment | job-company-research |
| `applying` → `applied` (CV + letter, submission registered, `applied` date set) | job-cv-tailoring, job-cover-letters |
| `screening`/`interviewing` | job-interview-prep |
| `offer` → `closed` (accepted — and all other live roles closed `withdrawn`) | job-negotiation |
| weekly metrics, autopsies, pipeline hygiene | job-hunt-review |
| anytime: building the proof base | job-evidence-mining |

## Dashboards

Maintain a HQ note the user glances at daily, built from `aidocs-query` blocks. The centerpiece is a **kanban board** of the live pipeline (Commonplace ≥ 0.3.3) — the user can drag a role between columns and the `status` property updates on the note, so hand-moves and tool-moves stay one system (a hand-drag skips the dated `[status]` observation; the review skill backfills any it finds missing):

```yaml
title: Pipeline
view: board
groupBy: status
columnOrder: [spotted, triaged, evaluated, applying, applied, screening, interviewing, offer]
columns: [fit_score, next_action]
where: [{key: status, op: neq, value: closed}]
```

Add beside it: a deadlines-this-week table, offers in flight, and a closed-roles table with `closed_reason` — the review skill reads that one.

## Automation cadence

Designed for scheduled agent runs; each is idempotent and writes back:
- **Daily (light):** check `{{roles}}` for approaching deadlines; scan target-company careers pages/news for delta-observations (job-scouting watchtower).
- **Weekly:** full job-hunt-review.
- **Per event** (rejection, interview, offer): the owning skill's debrief/autopsy protocol.

When the host supports scheduled tasks, propose setting these up; otherwise run them at session start when stale.

## Session pattern

Start: read `{{profile}}` + HQ dashboards + `recent_changes` since last touch. Work via the owning skill. End: `log_entry` what moved, update role statuses you changed.

## Don'ts

- Don't act on a role with no role note — capture first (job-scouting).
- Don't write `fit_score` without running job-evaluation.
- Don't invent vocabulary: reuse the property names above so dashboards keep working.
