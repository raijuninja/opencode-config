---
name: work-vault
description: AI Kim work vault conventions — WCCUSD workflows, Google Drive sync, project management, partner/person tracking. Use when working in the work vault.
---

# Work Vault — AI Kim

Vault-specific conventions for the work knowledge management vault. Supplements the shared `vault-best-practices` skill.

## Vault Structure

```
WCCUSD/                        # Work vault root
├── [Topics].md                # Flat topic notes
├── [ParentTopic Subtopic].md  # Flat subtopic notes
├── +/                         # Work inbox
├── Projects/                  # WCCUSD project folders
│   └── _Archive/              # Archived projects
├── Resources/                 # Reference material
├── Review/                    # Weekly reviews
└── SYSTEM/                    # Vault infrastructure
```

### Key Conventions

- Topics/subtopics are FLAT in `WCCUSD/` root, never nested in subfolders
- Subtopics named `ParentTopic Subtopic` (no dash)
- `_*` folders are special (archive, summer, tools) — never manually move files into them

## Note Types

| Type | Location | Description |
|------|----------|-------------|
| `topic` | `WCCUSD/` root | Your notes on a subject |
| `subtopic` | `WCCUSD/` root | Specific aspect of a parent topic |
| `project` | `WCCUSD/Projects/` | Time-bound work |
| `person` | `WCCUSD/` root | Contact notes (`up: [[Contacts]]`) |
| `resource` | `WCCUSD/Resources/` | External reference material |
| `inbox-item` | `WCCUSD/+/` | Quick capture |
| `weekly-review` | `WCCUSD/Review/` | Weekly planning |

### Person Template Conventions

- `type: person` (not `type: topic` with a person tag)
- `up:` defaults to `[[Contacts]]`
- Capture: name, org, title, email, relationship type

## Project Conventions

### Status Values

```
🟣 Planning
🔵 In Progress
🟡 On Hold
☀️ Summer
🟢 Complete
🗄️ Archived
```

### Priority Values

```
🔴 Critical
🟠 High
🟡 Medium
🟢 Low
```

### Naming

`Name - YYMM - Description`

### Multi-Project Programs

Parent + child project scaffolding. Parent projects contain multiple child subprojects.

### Auto-Archive

Projects with `🗄️ Archived` status get moved to `_Archive/` folder.

## Template Conventions

- Emoji-free filenames for ALL new notes
- Topic/subtopic sections: Overview (as `> [!abstract] Overview` callout), Notes, Projects dataview, Subtopics dataview
- NO standalone resource notes — link external resources inline in Notes section
- `references:` frontmatter for internal note links only
- Use `> [!abstract] Overview` callout format (not plain blockquote)

## Google Drive Sync

Drive sync fields on notes:

```yaml
gdrive_id_wccusd: xyz789
gdrive_url_wccusd: https://docs.google.com/...
last_synced_wccusd: '2026-02-05T...'
sync_hash_wccusd: ghi012
```

Sync managed externally via AI Kim scripts. WCCUSD Google Drive sync is NOT managed in Gunslinger.

## Workflows

### Pre-Work Scan

Before starting project work, search vault for existing topics, subtopics, people, and partners related to the subject. Report what exists, flag what's missing. Don't auto-create.

### Knowledge Capture

**Captured at project completion time** (before boss review). When the user says "knowledge capture" or "wrap this project", or when closing a project:

- New topics encountered
- New subtopics
- New people/partners
- Resources to save
- Existing notes to update

Create notes using templates. Link back to the project note with `> [!info] Extracted from project: [[Project Name]]`. Add spawned notes to the project's `references:` array so they appear in the Dataview below.

### Completed Projects — Spawned Knowledge

Use this query on completed projects to review what was learned:

```dataview
TABLE WITHOUT ID
  file.link as "Project",
  dateformat(completed, "MMM dd") as "Completed",
  references as "Knowledge Spawned"
FROM "WCCUSD/Projects"
WHERE type = "project" AND status = "🟢 Complete"
SORT completed DESC
```

### Project Status Review

Periodically review active project statuses, update frontmatter, and archive completed work.

## Emoji Policy

Emoji-free filenames for ALL new notes. Legacy existing content may retain emojis.

## Macros and QuickAdd

- Quick Creator unified entry point for note creation
- Context Actions menu on each note for type-appropriate actions
- WCCUSD dashboard refresh via dashboard button
