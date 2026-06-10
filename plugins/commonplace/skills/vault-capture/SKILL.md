---
name: vault-capture
description: Use when bringing external material into the user's Commonplace vault — clipping webpages, saving research, filing sources, or turning raw findings into linked notes with provenance.
---

# Capturing sources into a Commonplace vault

Captured material is only useful if it's findable later and its provenance survives. Capture → connect → distill.

## Clip webpages

`clip_webpage` fetches a URL, extracts the readable article, and saves it as markdown with `source` and `clipped` properties set automatically. It dedupes by URL — re-clipping an existing source returns the existing note instead of a copy.

- File clippings where the vault already files them (look for a `clippings/` or `research/` folder in `vault_overview`; an `AGENTS.md` rule wins if present).
- Localhost/private addresses are refused by design — don't try to work around it.

## Provenance is non-negotiable

Whatever the source (clipped page, conversation, file the user pasted):

- Keep `source` (URL or origin) and a date in frontmatter.
- When you extract a claim into another note, cite the capture: `- [funding] raised $40M Series B #acme (source: [[Acme clip 2026-06]])`.
- `quote_evidence` is how future sessions verify claims — they can only do that if the source note exists and is linked.

## Distill, don't hoard

A clipped article nobody links to is dead weight. After capturing:

1. Add 1–3 **observations** to the relevant topic/entity note summarizing what the source establishes.
2. Link the capture from those notes (`- sourced_from [[the clip]]` or inline wiki links).
3. Tag the capture with the entities it concerns so `search` and tag browsing find it.

## Templates for recurring captures

If the vault captures the same shape repeatedly (companies, papers, meetings), use `list_templates` / `create_from_template` so properties stay consistent and queryable. Suggest a new template to the user if you notice a recurring shape without one.

## Attachments

Binary files live under `attachments/YYYY-MM/` and are referenced with standard markdown: `![diagram](attachments/2026-06/diagram.png)`. Keep that convention; don't invent new attachment locations.
