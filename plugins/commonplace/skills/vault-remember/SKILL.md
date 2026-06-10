---
name: vault-remember
description: Use when you learn something worth keeping — decisions, facts, research findings, session outcomes — and the user has a Commonplace vault. Records knowledge durably with safe writes, observations, typed relations, and wiki links via the commonplace MCP tools.
---

# Remembering into a Commonplace vault

Write what future sessions (and the user) will need. The vault is plain markdown — everything you write must stay human-readable in the app.

## Safe writes: never clobber

Prefer the narrowest write that does the job:

| Intent | Tool |
|---|---|
| Add to a note | `append_to_document` (creates the note if missing) |
| Change a specific phrase | `edit_document` (exact find → replace; fails loudly if the find is ambiguous) |
| Rewrite one section | `replace_section` (heading-scoped; fence-aware) |
| Change metadata | `update_properties` (set/remove frontmatter keys) |
| New note | `create_document`, or `create_from_template` when a template fits (`list_templates` first) |
| Whole-note rewrite | `write_document` — last resort, requires holding the full body |

`rename_document` rewrites inbound wiki links for you; never simulate a rename with create+delete.

## Structure knowledge as you write

- **Observations** — categorized facts that tools can list and filter:
  `- [decision] We chose SQLite over Postgres #architecture (simpler ops for single-user)`
  Check `list_observations` / `vault_overview` for the categories already in use before inventing new ones. `add_observation` appends one properly.
- **Typed relations** — edges in the knowledge graph:
  `- depends_on [[Billing Service]]`, `- implements [[RFC-0042]]`
- **Wiki links** — link `[[Like This]]` liberally in prose; links power every traversal tool. After writing, `find_unlinked_mentions` + `linkify_mention` catches the ones you missed.
- **Tags & properties** — reuse the vault's existing vocabulary (`list_tags`, `list_properties`). A `status` property beats a `#done` tag for anything you'd ever query.

## Session continuity

End substantial sessions with `log_entry`: a short summary into today's `journal/YYYY-MM-DD.md`, linking the notes you touched. The next session's `recent_changes` + journal read is how an agent picks up where you left off.

## Live dashboards

A fenced code block with language `aidocs-query` containing YAML (same shape as `query_documents` args, plus `title`/`columns`) renders as a live table in the user's editor:

````markdown
```aidocs-query
title: Open questions
where: [{ key: status, op: eq, value: open }]
columns: [status, due]
```
````

Write one when the user would benefit from an always-current view.

## Don'ts

- Don't store agent/app state in the vault — it belongs to the human.
- Don't duplicate: `search` for an existing note before creating one.
- Don't strip or "fix" frontmatter you don't understand; other tooling may rely on it.
