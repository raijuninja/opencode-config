---
name: vault-best-practices
description: Shared vault maintenance and improvement patterns. Use when updating vault conventions, capturing project knowledge, archiving projects, maintaining skills, or performing vault health checks. Works across personal and work vaults.
---

# Vault Best Practices

Shared patterns for maintaining and improving Obsidian vaults using the AI agent workflow. These patterns apply to both personal and work vaults that follow the topic/subtopic/project note architecture.

## When to Use This Skill

- Updating vault-wide conventions (naming, frontmatter, types)
- Capturing knowledge from completed projects
- Archiving or reorganizing projects
- Creating, updating, or deprecating skills
- Performing vault health audits
- Identifying patterns that should become new skills

## Shared Note Architecture

### Canonical Note Types

| Type | Purpose | Location |
|------|---------|----------|
| `topic` | Notes you write and maintain — your thinking, domain knowledge | Vault root (flat) |
| `subtopic` | Specific aspect of a parent topic | Vault root (flat) |
| `project` | Time-bound work with a start and end | `Projects/` folder |
| `resource` | External reference material you did NOT write | `Resources/` or next to topics |
| `person` | Contact notes | Vault root or domain folder |
| `moc` | Map of Content — navigation hub | Vault root |
| `inbox-item` | Quick captures awaiting processing | `+/` folder |
| `weekly-review` | Weekly planning and reflection | Reviews folder |
| `monthly-review` | Monthly retrospective | Reviews folder |
| `journal` | Daily notes | Daily notes folder |

### Navigation Pattern

All notes use the `up:` frontmatter field for navigation and discovery:
- `up:` is an **array of wikilinks** pointing to parent note(s)
- Topics: `up: ["[[MOC Name]]"]`
- Subtopics: `up: ["[[Parent Topic]]"]`
- Projects: `up: ["[[MOC Name]]"]` (points to relevant MOC)
- Notes can appear in multiple MOCs via multiple `up:` values
- **Never** point `up:` directly to a pillar or top-level category (except MOCs)

### Discovery Queries

Dataview queries use `contains(up, this.file.link)` to find child notes:

```dataview
TABLE status, dateformat(file.mtime, "yyyy-MM-dd") as "Modified"
FROM ""
WHERE type = "topic" AND contains(up, this.file.link)
SORT file.name ASC
```

## Frontmatter Standards

### Required Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `type` | string | Always | Canonical type value (see table above) |
| `up` | array | Most notes | Parent navigation links |
| `status` | string | Projects, topics | Current state |
| `created` | date | Always | Creation date (YYYY-MM-DD) |
| `last_reviewed` | date | Projects, topics | Last review date |

### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `priority` | string | Project priority |
| `due_date` | date | Project deadline |
| `references` | array | Related internal note links |
| `tags` | array | Searchable labels |

### Deprecated Fields

Do NOT use: `resources` (use inline linking), `area`, `department`, `partner`, `note`, `area-folder`, `area-note`, `project-task`

## Naming Conventions

- **Projects**: `Name - YYMM - Description` (e.g., `CalPERS - 2604 - Withdrawal`)
- **Subtopics**: `ParentTopic Subtopic` (no dash between parent and subtopic)
- **MOC Notes**: Prefixed with emoji (e.g., `🗺️ Technology.md`) — legacy only
- **New content**: Emoji-free filenames, headings, frontmatter values, and status labels

## Project Lifecycle

### Creation
1. Create project folder under `Projects/`
2. Create project note using template
3. Create `AGENTS.md` for agent context
4. Create `MEMORY.md` for project-specific memory
5. Set `status: Planning` or `status: Active`

### Active Work
- Tasks are inline checkboxes in the project note
- Use `last_reviewed` to track when project was last touched
- Update `status` as work progresses

### Completion
1. Set `status: Complete`
2. Set `completed` date
3. Run knowledge capture (see below)
4. Optionally archive

### Archiving
1. Set `status: Archived`
2. Move project folder to `Projects/_Archive/`
3. Update any references in other notes

## Knowledge Capture Workflow

When a project is completed or the user says "knowledge capture" or "wrap this project":

1. **Review project files** — Read the project note and any attached files
2. **Identify new topics** — Any new technology, concept, or domain encountered?
3. **Identify new subtopics** — Any specific aspects worth capturing?
4. **Identify new people** — New contacts introduced?
5. **Identify resources** — URLs, docs, or templates worth keeping?
6. **Update existing notes** — Any notes that need new context or corrections?

For each confirmed item, create notes using the appropriate template. Link back to the project note with `> [!info] Extracted from project: [[Project Name]]`.

## Skill Maintenance

### When to Create a New Skill

Create a new skill when:
- A pattern is used across 3+ sessions
- The pattern is domain-specific and doesn't fit existing skills
- The pattern has specific rules, templates, or workflows
- The agent repeatedly needs the same instructions

### When to Update an Existing Skill

Update an existing skill when:
- A convention changes (naming, frontmatter, types)
- A new best practice is discovered for an existing domain
- A workflow is improved or simplified
- The user corrects the agent's behavior in that domain

### When to Deprecate a Skill

Deprecate a skill when:
- The domain is no longer relevant (e.g., externalized to another vault)
- The pattern is absorbed into a broader skill
- The workflow is replaced by a different approach

### Skill Format

```markdown
---
name: skill-name
description: One-line description. Use when [trigger conditions].
---

# Skill Name

Content here — rules, patterns, examples, workflows.
```

## Vault Health Check

Periodically review the vault for:

### Stale Notes
- Notes not modified in 30+ days — flag for review
- Notes with empty `status` or missing `type` — fix frontmatter

### Orphaned Notes
- Files with no `up:` links — suggest parent
- Files in wrong location — suggest move

### Deprecated Patterns
- Notes with deprecated `type` values — update to canonical types
- Notes with deprecated fields — clean up frontmatter

### Inbox Buildup
- Count items in `+/` — flag if > 10
- Process each item: file, act, or delete

### Skill Drift
- Review skills for outdated conventions
- Check that templates match current standards
- Verify Dataview queries still work after structural changes

## Cross-Vault Pattern Sync

When a best practice is discovered in one vault:

1. **Identify the pattern** — What is the new convention or workflow?
2. **Check applicability** — Does it apply to the other vault?
3. **Update the shared skill** — Add the pattern to `vault-best-practices`
4. **Apply to the other vault** — Update notes, templates, and queries
5. **Document the change** — Note the date and context in the skill

### Patterns That Are Vault-Specific

Some patterns are vault-specific and should NOT be shared:
- Personal: Pillar system, Captain's Log, Nimbus, focus cascade
- Work: WCCUSD workflows, Google Drive sync, partner management

### Patterns That Are Shared

These patterns are shared across vaults:
- Note types and frontmatter standards
- Navigation pattern (`up:` field)
- Project lifecycle (create, active, complete, archive)
- Knowledge capture workflow
- Skill maintenance process
- Naming conventions
- Emoji-free new content policy
- Vault health check process

## Agent Rules

1. **Always use templates** — Never create notes from memory; always use the canonical template
2. **Preserve frontmatter** — When editing notes, keep existing fields valid
3. **Check for existing notes** — Before creating, search for duplicates or related notes
4. **Ask before restructuring** — Do not move or rename notes without confirmation
5. **Update skills on convention changes** — When a convention changes, update this skill
6. **Keep notes under 200 lines** — Split large notes into topic + subtopics
7. **Inline resource linking** — Link external resources inline, don't create standalone resource notes
