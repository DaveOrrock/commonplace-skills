---
name: vault-gardening
description: Use when asked to tidy, audit, reorganize, or improve a Commonplace vault — fixing broken links, merging duplicates, normalizing tags, strengthening the wiki-link graph, or reviewing vault health.
---

# Gardening a Commonplace vault

Gardening is maintenance of the user's knowledge, not yours. Diagnose broadly, propose, then make narrow verified changes — never bulk-rewrite on a hunch.

## Diagnose first

- `vault_health` — broken wiki links, orphan notes (no links in or out), untagged notes, stale notes. This is the worklist.
- `vault_overview` — tag and property vocabulary; spot near-duplicates (`#ml` vs `#machine-learning`) and inconsistent property keys.
- `recent_changes` — what's been touched lately; recent notes are the ones worth wiring into the graph first.

## Safe renovation tools

| Job | Tool | Why it's safe |
|---|---|---|
| Rename/move a note | `rename_document` | rewrites every inbound `[[link]]` |
| Merge tag variants | `rename_tag` | updates every occurrence vault-wide |
| Wire in orphans | `find_unlinked_mentions` → `linkify_mention` | only links text that already mentions the note |
| Fix one passage | `edit_document` | exact-match find/replace, fails loudly on ambiguity |
| Restructure a note | `replace_section` | scoped to one heading, code-fence aware |

`delete_document` moves to trash, but **ask the user before deleting anything** — a note that looks dead to you may matter to them.

## Merging duplicates

1. Read both (`read_document` with outline first), confirm they're truly the same topic.
2. Move unique content into the survivor (`append_to_document` / `replace_section`).
3. `rename_document` the loser to the survivor's name is NOT how merges work — instead update inbound links by checking `get_backlinks` on the loser, edit those notes to point at the survivor, then propose deletion to the user.

## Strengthening the graph

For each orphan or weakly-linked note: does an existing note mention it (`find_unlinked_mentions`)? Should it carry typed relations (`- part_of [[Project]]`)? Does it deserve the vault's standard properties? Three small edits beat one speculative reorganization.

## Verify and report

After a gardening pass, re-run `vault_health` and report the delta (broken links 12 → 0, orphans 8 → 3). `sync_vault` afterwards if the vault uses git sync, and `log_entry` a summary of what changed so the next session knows.
