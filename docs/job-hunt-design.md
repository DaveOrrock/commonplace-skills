# Job-hunt skill set — design

Research-driven design for the `job-*` skills (June 2026). Sources: ATS/CV evidence review, recruiter-behavior research, decision-science and pipeline research, divergent ideation pass. Key findings the skills encode:

## What the research says (and the skills enforce)

1. **ATS auto-rejection is mostly myth; human triage under volume is the real filter.** ATSs parse, store, and route; rejection lives in knockout questions and overloaded humans (~250+ applications/posting, 7-second triage scans). → CV skill optimizes for *parse-clean + human-scannable*, not robot-beating.
2. **Tailoring and channels beat volume.** Tailored CVs ~2x interview rate; 100+ spray applications convert 3.6x worse than 11-20 targeted; referrals convert ~40x cold inbound; senior hires skew to sourced/referral. → Scouting and outreach skills push warm channels and a capped, targeted pipeline.
3. **AI-slop is the new spam filter.** Recruiters discard generic-enthusiasm, uniform-rhythm, zero-specifics applications on sight. Distinctiveness and verifiable specifics now carry the signal polish used to. → Materials skills enforce evidence-backed specificity and ban slop patterns.
4. **Structured scoring beats gut, and equal weights are fine** (Dawes: improper linear models). The dangerous failure is not bad weights but *unpre-registered criteria* — desperation creep, sunk cost after interview rounds, halo from charm and titles. → Evaluation skill refuses to run without written criteria and discounts verbal promises.
5. **Ghost jobs are ~20-45% of postings.** Age, cross-board date mismatches, and careers-page absence are detectable. → Scouting skill triages before any effort is spent.
6. **Negotiation: always counter** (~94% of negotiated offers stand; +12-19% average lift); leverage is built from logged eagerness signals and synchronized offer windows, not courage in the moment. → Negotiation skill compiles evidence collected throughout the process.
7. **Baseline agent testing showed**: with crisp criteria in context, agents evaluate rigorously; without them, nothing forces consistency or persistence. The skills' core job is *making the criteria and evidence exist in the vault* and writing every judgment back as comparable, queryable notes.

## The skill set (11)

| Skill | Job |
|---|---|
| `job-hunt-hq` | Hub: data model, lifecycle states, placeholder convention, dashboards, automation cadence. Background for all others. |
| `job-scouting` | Market map, finding roles, ghost-job triage, capture with structured properties, hiring-signal watching. |
| `job-evaluation` | Brutal fit scoring: criteria gate → dealbreakers → equal-weight rubric → recorded scorecard. Discipline skill. |
| `job-company-research` | VC-style diligence memo: runway, layoff recidivism, Glassdoor protocol, exec churn, pre-registered kill criteria. |
| `job-evidence-mining` | Build the evidence locker: mine the vault for quantified wins with provenance; comp intelligence file. |
| `job-cv-tailoring` | ATS-reality CV: parse-clean format, honest JD mirroring, evidence-locker bullets only, version registry. |
| `job-cover-letters` | Short, specific, slop-proof letters that carry the "why this/why me" the CV can't. |
| `job-outreach` | Referrals, warm intros, recruiter/HM messages, candidate dossier, dormant-connection sweeps, follow-up cadence. |
| `job-interview-prep` | STAR bank, question heatmap, interviewer film study, collection plan, debrief protocol feeding the leverage journal. |
| `job-negotiation` | Leverage memo from logged signals, comp file, always-counter, offer-window synchronization, reference choreography. |
| `job-hunt-review` | Weekly: funnel base rates, stale-deal sweep, rejection autopsy (48h quarantine, ACH at 4+), desperation-creep detector, positioning-drift diff. Designed to run scheduled. |

## Conventions

- **Placeholders:** vault locations are written `{{roles}}`, `{{companies}}`, `{{applications}}`, `{{profile}}`, `{{evidence-locker}}`, `{{journal}}` etc. Skills resolve them from the vault's `AGENTS.md` (or ask once and record there). The vault owner restructures freely; skills never hardcode paths.
- **Data model** lives in `job-hunt-hq` only; other skills reference it.
- **Everything is written back** as notes/observations/properties so dashboards and future sessions see it. A judgment that isn't in the vault didn't happen.

## Testing applied

- RED baselines (2): obvious-mismatch and marginal-role + sunk-cost scenarios run without skills; agent rigor held *when criteria were provided* — failure mode identified as missing pre-registration/persistence, not sycophancy alone. GREEN verification re-runs the marginal scenario with skills installed and checks criteria-gating + scorecard persistence behavior. Application tests on scouting/CV skills check retrieval and constraint compliance.
