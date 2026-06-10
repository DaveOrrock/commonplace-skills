# Commonplace skills ❧

Claude Code skills and agent documentation for [Commonplace](https://github.com/DaveOrrock/AIDocs) — a local-first, AI-native personal documentation store. Your notes are plain markdown with YAML frontmatter, wiki links, and tags; Commonplace's built-in MCP server gives agents 37 tools to search, traverse, and write them.

This repo teaches agents to use that surface *well*.

## Install

```bash
claude plugin marketplace add DaveOrrock/commonplace-skills
claude plugin install commonplace@commonplace
```

Requires the Commonplace app running with a vault open (the MCP server lives in the app). Connect Claude Code to it with:

```bash
claude mcp add --transport http commonplace http://127.0.0.1:7117/mcp
```

Claude Desktop users: install the one-click `.mcpb` extension from the [latest app release](https://github.com/DaveOrrock/AIDocs/releases/latest) instead.

## The skills

| Skill | When it fires | What it teaches |
|---|---|---|
| **vault-recall** | You need information that might already be in the vault | Orient with `vault_overview`, pick the right finder (keyword vs semantic vs structured vs graph-walk), scout-then-dive reads that don't waste context |
| **vault-remember** | You learned something worth keeping | The narrowest safe write, observations and typed relations, reusing the vault's vocabulary, session continuity via `log_entry` |
| **vault-capture** | Bringing external material in (webpages, research, sources) | `clip_webpage` with provenance, distilling captures into linked observations, templates for recurring shapes |
| **vault-gardening** | Asked to tidy, audit, or reorganize the vault | `vault_health`-driven worklists, link-safe renames, duplicate-merge protocol, verify-and-report discipline |

## The job-hunt suite

Eleven research-backed skills that run a complete job search on the vault — built from evidence on what actually works in 2025-26 hiring (ATS reality, recruiter behavior, decision science; see [docs/job-hunt-design.md](docs/job-hunt-design.md)):

`job-hunt-hq` (data model + dashboards + automation cadence) · `job-scouting` (market map, ghost-job triage, capture) · `job-evaluation` (criteria-gated brutal fit scoring) · `job-company-research` (VC-style diligence with kill criteria) · `job-evidence-mining` (provenance-backed accomplishment locker) · `job-cv-tailoring` (parse-clean, honest, evidence-only CVs) · `job-cover-letters` (short, specific, slop-proof) · `job-outreach` (referrals, dossier, dormant-connection sweeps) · `job-interview-prep` (STAR bank, question heatmap, debrief protocol) · `job-negotiation` (leverage memo, offer-window sync) · `job-hunt-review` (weekly funnel math, rejection autopsies, drift detection — runs scheduled).

Vault locations are `{{placeholders}}` resolved from your vault's `AGENTS.md` — restructure freely.

## Agent manual

[docs/agents.md](docs/agents.md) is the full reference: the contract, markdown conventions (frontmatter, observations, typed relations, journal, live dashboards), the grouped tool catalog, context-economy rules, and a starter `AGENTS.md` to drop in your vault root.

## Versioning

Skills track the app's MCP tool surface. They're written against Commonplace ≥ 0.3.0; tool names are stable, so older app versions largely work too.

## License

MIT
