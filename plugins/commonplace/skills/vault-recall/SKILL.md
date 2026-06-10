---
name: vault-recall
description: Use when you need information that might live in the user's Commonplace vault — past decisions, project context, people, research, prior sessions — or when starting work the vault may already cover. Finds knowledge via the commonplace MCP tools without wasting context.
---

# Recalling from a Commonplace vault

The vault is the user's long-term memory. Check it **before** re-researching or asking the user something they may have already written down.

## Orient once per session

Call `vault_overview` first: vault name, folder map, tags, property keys, recent notes. It teaches you the vault's vocabulary — which tags and properties exist is half the battle. If an `AGENTS.md` exists at the vault root, its rules arrive in the server instructions; follow them.

## Pick the right finder

| You have… | Use |
|---|---|
| Keywords or exact phrases | `search` (MiniSearch keyword index; supports `tag:` and field filters) |
| A meaning, not the wording | `semantic_search` (local embeddings; may be unavailable — fall back to `search`) |
| Structured criteria ("status = active", "due before Friday") | `query_documents` with `where` filters; `aggregate` for counts/sums |
| A note, want its neighborhood | `get_backlinks`, `get_links`, `related_documents` |
| A topic, want a working set | `build_context` — walks the wiki-link graph from a seed and returns a trimmed bundle |
| A claim to support | `quote_evidence` — passage-level hits with path, heading, and line numbers |
| "What happened recently?" | `recent_changes` (includes deletions), `note_history` for one note's git history |

## Read cheaply — scout, then dive

Never pull a whole document to answer a narrow question:

1. **Scout:** `read_document` with `include: ["outline", "properties"]` — structure, metadata, and size for a few hundred tokens.
2. **Dive:** re-call with `heading: "<section>"` to read only the section you need.
3. Full-body reads are for short notes or when you genuinely need everything.

In `query_documents`, pass `fields` to limit which properties come back per doc.

## Traversal beats search for connected knowledge

Wiki links are the vault's structure. A note's `relations` (typed links like `- depends_on [[X]]`) and `observations` (categorized facts) are parsed and returned by `read_document` and `build_context` — prefer reading those over regex-hunting the body.

## When recall comes up empty

Say so, then check `find_unlinked_mentions` for the term (it may exist under another name) and `list_tags` / `list_properties` for adjacent vocabulary before concluding the vault doesn't know.
