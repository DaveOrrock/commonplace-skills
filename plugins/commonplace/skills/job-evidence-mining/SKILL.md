---
name: job-evidence-mining
description: Use when building or refreshing the user's bank of proven accomplishments — before CV work, before interview prep, when the user can't remember concrete wins, or as a scheduled sweep over an accumulating vault. Also when capturing compensation data points from recruiter conversations.
---

# Evidence mining

**REQUIRED BACKGROUND:** job-hunt-hq.

CVs, letters, and interview answers are only as good as the evidence behind them — and human memory under-reports. The vault remembers: old project notes, dailies, meeting notes, and review documents contain quantified wins the user has forgotten. Mine them into one queryable locker with provenance.

## The evidence locker

`{{evidence-locker}}` holds one entry per accomplishment as an observation with a backlink to the primary source:

```markdown
- [win] Cut p95 search latency 675ms → 9.4ms via reverse-link map #performance ([[2026-03-14]])
- [scope] Grew platform team 4 → 15 across 3 quarters #leadership ([[Q3 planning note]])
- [story] Vendor outage war room — led cross-team recovery in 6h #incident ([[postmortem]])
```

Categories that earn their keep: `[win]` (quantified result), `[scope]` (size of mandate: people, budget, systems), `[story]` (STAR-shaped situations), `[skill-proof]` (evidence a claimed skill was used for real), `[testimonial]` (quoted praise, with who/when).

**Provenance is the rule: every entry links its source note.** An accomplishment with no source gets `#unverified` and a prompt for the user to confirm the number — invented or misremembered metrics die in interviews.

## Mining sweep (repeatable, scheduled-friendly)

1. `semantic_search` the vault for outcome language: shipped, launched, reduced, grew, saved, fixed, migrated, hired, "% improvement", incident, award.
2. Walk recent `{{journal}}` months and project notes' Results/Retro sections.
3. For each hit not already in the locker: extract the claim, **keep the number exact** (don't round up), file with backlink.
4. Diff against the user's existing CV/master profile — anything on the CV *not* in the locker needs sourcing or flagging.

Track coverage: every claimed skill in `{{profile}}` should have ≥1 `[skill-proof]`; every CV bullet should map to a locker entry. Gaps are the work list.

## Comp intelligence (same discipline, different asset)

`{{comp-file}}` accumulates every compensation data point as it's encountered — recruiter bands ("recruiter said £130-150 for this level"), posted ranges, levels.fyi clips, offer numbers — each as `- [comp] £X-Y, <role family>, <stage/size>, <source> (date)`. Before any salary conversation, job-negotiation reads this file; the user never anchors blind. Capture is *passive and constant*: whenever a number appears in any job-hunt conversation, file it.

## Don'ts

- Don't polish while mining — locker entries are raw, exact, sourced; wordsmithing happens in CV/letter skills.
- Don't inflate ("~40%" becomes "40%", never "nearly 50%"). The locker is the honesty backstop for every downstream artifact.
- Don't file duplicates — search the locker first; enrich the existing entry instead.
