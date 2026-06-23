---
name: vault-best-practices
description: Shared vault maintenance and improvement patterns. Use when capturing project knowledge, archiving projects, maintaining skills, or performing vault health checks. Works across personal and work vaults.
---

# Vault Best Practices

Shared patterns for maintaining and improving Obsidian vaults using the AI agent workflow. These patterns apply to both personal and work vaults that follow the topic/subtopic/project note architecture.

## When to Use This Skill

- Capturing knowledge from completed projects
- Archiving or reorganizing projects
- Creating, updating, or deprecating skills
- Performing vault health audits
- Identifying patterns that should become new skills
- **Starting a session** — pull latest global skills: `cd ~/.config/opencode && git pull`

> Note types, frontmatter standards, and naming conventions are covered by the vault-level `note-creation` skill in `.opencode/skills/`.

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

### Closing a Project

**Knowledge capture is REQUIRED before closing any project.** The point of closure depends on vault:

| Vault | Closure point | Capture trigger | Status after capture |
|-------|--------------|-----------------|----------------------|
| Personal | Archive | At archive time | `🗄️ Archived` → move to `_Archive/` |
| Work | Complete | At complete time | `🟢 Complete` → stays in `Projects/` for review |

**Universal steps:**
1. **Capture knowledge** (see Knowledge Capture Workflow below) — extract learnings into topics/subtopics
2. Set `status` based on vault closure point
3. Set `completed` date
4. Update `last_reviewed`
5. Personal only: move to `_Archive/`

**Never close a project without completing knowledge capture first.**

## Knowledge Capture Workflow

**Always run before closing a project** (archive in personal, complete in work). Also run on demand when the user says "knowledge capture" or "wrap this project".

When triggered:

1. **Review project files** — Read the project note and any attached files
2. **Identify new topics** — Any new technology, concept, or domain encountered?
3. **Identify new subtopics** — Any specific aspects worth capturing?
4. **Identify new people** — New contacts introduced?
5. **Identify resources** — URLs, docs, or templates worth keeping?
6. **Update existing notes** — Any notes that need new context or corrections?

For each confirmed item, create notes using the appropriate template. Link back to the project note with `> [!info] Extracted from project: [[Project Name]]`.

## Inbox Processing

When the user says "process my inbox", "process +", or similar, read all items in the inbox folder (`+/` for work vault, `+Inbox/` for personal vault), determine the appropriate note type for each, create notes, and delete the processed inbox files. The inbox folder should be empty after processing (only the dashboard file remains). Delete all processed files including non-markdown files (PDFs, zips, shortcuts, etc.) that were handled during processing.

### Processing Rules

1. **Read all inbox items** — Files in `+/` with `type: inbox-item`
2. **Prevent duplicates** — Before creating, search vault for existing notes on the same subject. If a topic already exists, append inbox content to the existing note's Notes section instead of creating a duplicate
3. **Classify each item**:
   - New topic → create at vault root, `type: topic`, `up:` to most relevant MOC
   - New subtopic → create at vault root, `type: subtopic`, `up:` to parent topic
   - New person → create at vault root, `type: topic`, `person` tag
   - Resource → save to `Resources/`, `type: resource`
   - Discard → already done, duplicate content, or no longer relevant
4. **Create notes using templates** — Always use the canonical template (see `note-creation` skill)
5. **Delete processed items** — Remove the inbox file from `+/` after successfully creating the note or confirming discard
6. **Report** — Summarize what was created and discarded

### Workflow

```
User: "process my inbox"
  → Agent lists all inbox items with proposed destinations
  → User confirms or adjusts
  → Agent creates notes, deletes processed items
  → Agent reports: "Created X topics, Y subtopics. Discarded N items."
```

## Agent Shared Sync

Notes with `shared: true` frontmatter sync bidirectionally between personal (Gunslinger) and work (AI Kim) vaults via `work-sync` (`SYSTEM/Scripts/work-sync/`). Separate from `brittish: true` (Brittish vault sync).

- **Syncs only on the work machine** where both vaults are local
- **On macOS/Omarchy**: edit `shared: true` notes as source-of-truth; sync catches up later
- **Conflict resolution**: newest-wins
- **State manifest**: `.work-sync-state.json` (auto-generated)

## Agent System Documentation

Each vault should maintain documentation for the agent harness. Verify on session start.

### Expected Notes (both vaults)

| Note | Type | Content |
|------|------|---------|
| `🗺️ Agent System.md` | MOC | Dataview listing of agent-related topics |
| `Agent System Architecture.md` | Topic | Full architecture: skills, prompts, rules propagation, machine context, shared vs vault-specific patterns |

### Minimum Sections (architecture note)

- Skill locations (global vs vault-local, sync methods)
- How rules propagate across vaults
- Machine context model
- Shared vs vault-specific patterns
- Session startup flow
- Agent Shared Sync (`shared: true` workflow)

### Agent Check (session start)

1. Verify `🗺️ Agent System.md` exists with correct type and structure
2. Verify `Agent System Architecture.md` exists with minimum sections
3. If notes exist in work vault with different names, adapt — content pattern matters, not filenames
4. On work machine: verify `Agent System Architecture.md` has `shared: true` for bidirectional sync

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
- Project lifecycle (create, active, capture, close)
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
8. **Capture knowledge before closing** — Never archive or complete a project without first extracting learnings into topics/subtopics
