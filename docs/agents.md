# Commonplace for agents

Commonplace is a local-first markdown knowledge base designed for two users: a human (in the desktop app) and their AI agents (over MCP). This guide is the agent-facing manual: the conventions, the tool surface, and the workflows that make a vault genuinely useful as long-term memory.

For one-click setup see the README: Claude Desktop installs the `.mcpb` extension; Claude Code runs `claude mcp add --transport http commonplace http://127.0.0.1:7117/mcp`. The Claude Code plugin in this repo (`claude plugin marketplace add DaveOrrock/commonplace-skills`) adds four skills that teach these workflows: `vault-recall`, `vault-remember`, `vault-capture`, `vault-gardening`.

## The contract

- **Markdown is the truth.** Every document is a plain `.md` file with optional YAML frontmatter. Anything you write must stay readable to a human in the app (and in any other editor).
- **The vault belongs to the human.** Agents read it to recall and write to it to remember — but never store agent/app state, scratch data, or anything the human wouldn't want to see in their notes.
- **Links are structure.** `[[Wiki links]]` are the graph; every traversal tool (`get_backlinks`, `related_documents`, `build_context`) is powered by them. Link liberally.
- **Vault-specific rules live in `AGENTS.md`** at the vault root. The server injects it into MCP instructions automatically. Its rules override this guide.

## Conventions

### Frontmatter properties
```yaml
---
type: project
status: active
due: 2026-07-01
tags: [infra, q3]
aliases: [The Big Migration]
---
```
Properties are typed (string/number/date/boolean/list) and queryable via `query_documents` and `aggregate`. `aliases` feed link resolution and search. Reuse the vault's existing keys (`list_properties`) before inventing new ones.

### Observations — categorized, parseable facts
```markdown
- [decision] Chose SQLite over Postgres #architecture (single-user, simpler ops)
- [risk] Vendor contract expires 2026-09 #billing
```
The `[category] fact #tags (context)` shape is parsed and returned structurally by `read_document`, `list_observations`, and `build_context`. Categories are an open set — but check `vault_overview` for ones already in use.

### Typed relations — edges with meaning
```markdown
- depends_on [[Billing Service]]
- implements [[RFC-0042]]
- competitor_of [[OtherCo]]
```
A bullet of the form `- verb [[Target]]` is a typed graph edge. Use them for anything a future query like "what depends on X?" should find.

### Journal
`journal/YYYY-MM-DD.md` holds daily notes. `log_entry` appends a timestamped session summary there — end substantial sessions with one, linking the notes you touched.

### Attachments
Binary files live in `attachments/YYYY-MM/`, referenced as `![alt](attachments/2026-06/file.png)`.

### Live dashboards
A fenced block with language `aidocs-query` containing YAML (the `query_documents` argument shape plus `title`/`columns`) renders as a live table in the human's editor:

````markdown
```aidocs-query
title: Active projects
where: [{ key: status, op: eq, value: active }]
columns: [status, due]
sortBy: due
```
````

## The tool surface (37 tools)

**Orient** — `vault_overview` (call first: folders, tags, properties, recent), `vault_health` (broken links, orphans, untagged).

**Recall** — `search` (keyword), `semantic_search` (by meaning; may be unavailable on some machines — fall back to `search`), `query_documents` + `aggregate` (structured), `read_document` (supports `include` parts and `heading`-scoped section reads), `quote_evidence` (passage-level, cite-able hits), `build_context` (graph-walk a topic into a working set), `related_documents`, `get_links`, `get_backlinks`, `list_documents`, `list_tags`, `list_properties`, `list_observations`, `list_tasks`.

**Remember** — `append_to_document` (never clobbers; creates if missing), `edit_document` (exact find/replace), `replace_section` (heading-scoped, fence-aware), `update_properties`, `add_observation`, `create_document`, `write_document` (full rewrite — last resort), `create_from_template` + `list_templates`, `log_entry`.

**Reorganize** — `rename_document` (rewrites inbound links), `rename_tag` (vault-wide), `find_unlinked_mentions` + `linkify_mention`, `delete_document` (to trash — confirm with the human first).

**Capture & output** — `clip_webpage` (readable-article extraction, URL dedupe, SSRF-guarded), `export_pdf`.

**Continuity & sync** — `recent_changes` (includes a deletion journal), `note_history` (per-note git log), `sync_vault` (git pull/push with conflict copies).

## Context economy

Tool responses are deliberately compact (minified JSON, empty fields pruned). Hold up your end:

1. **Scout before reading.** `read_document` with `include: ["outline", "properties"]` shows structure and size for a fraction of the cost; then read just the `heading` you need.
2. **Limit fields.** `query_documents` accepts `fields` to trim properties per doc.
3. **Prefer narrow writes.** `replace_section` / `append_to_document` / `edit_document` mean you never hold a whole document in context to change one part.

## Live updates

`GET /events` on the same host/port is a server-sent-events stream of vault changes (`{type, path}`). Long-running local agents should subscribe instead of polling `recent_changes`.

## Session pattern

```
start:  vault_overview → recent_changes → read today's/yesterday's journal
work:   recall before researching; remember as you learn; link as you write
end:    log_entry summary → (sync_vault if the vault uses git)
```

## Starter AGENTS.md

Drop this at the vault root and adapt — the server serves it to every connected agent:

```markdown
# Agent conventions for this vault

## Layout
- projects/ — one note per project (type: project; status: active/paused/done)
- people/ — one note per person (type: person)
- research/ — clipped articles and sources (clip_webpage files here)
- journal/ — daily notes (log_entry writes here)

## Rules
- Reuse existing tags and properties; ask before inventing new vocabulary.
- Record findings as observations on the relevant entity note, with sources.
- Typed relations to use: works_on, depends_on, sourced_from, related_to.
- Never delete or rewrite whole notes without asking.
- End every substantial session with log_entry.
```
