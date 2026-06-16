---
name: personal-vault
description: Gunslinger personal vault conventions. Use when working in the personal vault.
---

# Personal Vault — Gunslinger

Vault-specific conventions for the personal knowledge management vault. See the vault-level `.opencode/skills/` for detailed instructions on each area below.

## Vault Location

- **Omarchy (Linux):** `/home/james/Obsidian/Gunslinger/`
- **Work (Windows):** `c:\Users\james.contreras\Obsidian\Gunslinger\`

## Available Skill Files (vault-local)

These reside in `.opencode/skills/` inside the vault and provide detailed instructions:

| Skill | What it covers |
|-------|----------------|
| `pillar-system` | 7 Life Pillars, focus cascade, Captain's Log, Nimbus board, mission tracking |
| `note-creation` | Quick Creator, templates, frontmatter standards, canonical types |
| `dataview` | Query patterns, MOC conventions, MetaBind status |
| `brittish-sync` | Bidirectional vault-to-vault sync via `shared: true` |
| `meal-planning` | Multi-person meal planning, recipe metadata, shopping list aggregation |

## Emoji Policy

- Legacy existing notes may keep emojis in filenames and headings
- ALL new content: emoji-free filenames, headings, frontmatter values, labels

## How Rules Sync Across Vaults

This vault (Gunslinger) and the work vault (AI Kim) share conventions via the `vault-best-practices` global skill. When that skill is updated on either machine, the other vault picks up the changes on its next session (via `git pull`).

### What's Shared (propagated automatically)

- Note types, frontmatter standards, naming conventions
- Project lifecycle (create, active, capture, close)
- Knowledge capture workflow, inbox processing
- Skill maintenance process
- Emoji-free new content policy

### What's Vault-Specific (stays local)

- **Personal only:** Pillar system, Captain's Log, Nimbus board, focus cascade, Brittish sync, meal planning
- **Work only:** WCCUSD workflows, Google Drive sync, partner management, multi-project programs

### Syncing Agent Rules

When working in this vault, check that `AGENTS.md` includes the shared rules from `vault-best-practices` (see its Agent Rules section). If any shared rules are missing, add them. The current shared minimum is:

- Knowledge capture before project closure
- Pull global skills at session start (`cd ~/.config/opencode && git pull`)
- Always use templates for note creation
- Check for existing notes before creating duplicates
- Ask before restructuring
