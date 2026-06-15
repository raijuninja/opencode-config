---
name: personal-vault
description: Gunslinger personal vault conventions — pillar system, Captain's Log, focus cascade, Nimbus board. Use when working in the personal vault.
---

# Personal Vault — Gunslinger

Vault-specific conventions for the personal knowledge management vault. Supplements the shared `vault-best-practices` skill.

## Vault Location

- **Omarchy (Linux):** `/home/james/Obsidian/Gunslinger/`
- **Work (Windows):** `c:\Users\james.contreras\Obsidian\Gunslinger\`

## 7 Life Pillars

Pillar notes sit at vault root with `type: pillar`. Each is a review dashboard with a full focus cascade.

| # | File | Value | MOC |
|---|------|-------|-----|
| 1 | 🏛️ 1 🕊️ Soul (Spiritual Life) | soul | 🗺️ Spirituality |
| 2 | 🏛️ 2 🦾 Body (Physical Health) | body | 🗺️ Health |
| 3 | 🏛️ 3 🌱 Personal Life | personal | 🗺️ Learning, Technology, Cars, Home, Adventures |
| 4 | 🏛️ 4 🫀 Key Relationships | relationships | 🗺️ Relationships |
| 5 | 🏛️ 5 🏫 Job | job | — |
| 6 | 🏛️ 6 💼 Business | business | 🗺️ Business |
| 7 | 🏛️ 7 💵 Financial Life | financial | 🗺️ Finance |

### Focus Cascade

Each pillar note stores its own cascade:

```yaml
focus_10yr: "Vision"
focus_5yr: "5-year target"
focus_1yr: "Annual goal"
focus_monthly: "Monthly priority"
focus_weekly: "This week's focus"
focus_daily: ["Habit 1", "Habit 2"]
```

Completed focus items are archived in a `## 🏁 Completed Focus` table in the note body.

### Pillar Attention

DataviewJS block on every daily note and the Bridge — derives from `missions_completed` entries:
- `"PillarNoteName::item"` — pillar daily focus items
- `"ProjectName::project-work"` — project work
- `"mission::emoji task text"` — pillar-tagged tasks

## Captain's Log

Managed by the Journals plugin. Three journals:

| Journal | Folder | Template |
|---------|--------|----------|
| Daily | `Captains Log/01 - Daily Notes/YYYY/MM-Month/` | `📔 Captains Log.md` |
| Weekly | `Captains Log/02 - Weekly Reviews/` | `📅 Weekly Review (Personal).md` |
| Monthly | `Captains Log/03 - Monthly Reviews/` | `📅 Monthly Review.md` |

### Daily Note Structure

- **Reviews Due** — DataviewJS fires on Sundays (weekly) and month-end (monthly)
- **Missions** — H2 with `BUTTON[daily-task]` and `BUTTON[schedule]`
- **Mission Log** — H4 sub-heading, read by Day Planner plugin
- **Nimbus** — Daily pillar missions + active projects + mission log tasks
- **Pillar Attention** — 7 pillars ranked by neglect

### Nimbus Board

DataviewJS block showing:
1. **Daily Missions** — active pillars with `focus_daily` items, each with its own checkbox
2. **Active Projects** — projects with `pillar:` field and active status
3. **Mission Log** — pillar-tagged tasks from the current note

### Day Planner Integration

The `#### Mission Log` heading is read by Day Planner:
- `plannerHeading: "Mission Log"`
- `plannerHeadingLevel: 4`
- Timestamped tasks (`HH:mm - HH:mm`) appear on timeline
- Untimestamped tasks appear in "Unscheduled tasks" sidebar
- Syncs to Google Calendar

## Project Conventions

- `pillar:` field on projects links them to their pillar dashboard
- `pillar:` is an array of wikilinks — NEVER set on topics/resources
- Projects have both `up:` (→ MOC) and `pillar:` (→ pillar)

## Templates

Templates live in `SYSTEM/TEMPLATE/`. QuickAdd scripts in `SYSTEM/Scripts/` power note creation.

Quick Creator menu:
```
── Create ──
  ⚙️ New Project
  🌿 New Topic
  📚 New Resource
  👤 New Person Contact
  🗺️ New Topic MOC
  💼 New Meeting
  📥 Quick Inbox Capture
── Personal Only ──
  🌿 New Pillar
  🔥 New Recipe
── Review ──
  📅 Weekly Review
```

## Brittish Sync

Bidirectional sync with the Brittish shared vault (`/home/james/Obsidian/Brittish/`). Opt-in via `shared: true` frontmatter. Managed by `SYSTEM/Scripts/brittish-sync/`.

## Metadata Menu FileClasses

FileClass definitions in `SYSTEM/_fileClasses/` constrain field editing:
- `pillar.md` — pillar fields, focus cascade
- `journal.md` — journal-date
- `project.md` — pillar, status, priority
- `topic.md` — status
- `subtopic.md` — inherits topic

## Emoji Policy

- Legacy existing notes may keep emojis in filenames and headings
- ALL new content: emoji-free filenames, headings, frontmatter values, labels
