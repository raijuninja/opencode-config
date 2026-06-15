# Vault Best Practices — Agent Skills

Shared vault maintenance and improvement patterns for Obsidian vaults using the AI agent workflow. Works across personal and work vaults that follow the topic/subtopic/project note architecture.

## Installation

### OpenCode (Global)

Clone this repo into your OpenCode skills directory:

```bash
git clone https://github.com/YOUR_USERNAME/vault-best-practices.git ~/.opencode/skills/vault-best-practices
```

OpenCode auto-discovers all `SKILL.md` files under `~/.opencode/skills/`. No config changes needed. Restart OpenCode after cloning.

### Manual

Copy `skills/vault-best-practices/SKILL.md` to your vault's `.opencode/skills/vault-best-practices/` directory.

## What This Covers

- **Shared note architecture** — Canonical types, navigation patterns, discovery queries
- **Frontmatter standards** — Required/optional/deprecated fields
- **Project lifecycle** — Creation, active work, completion, archiving
- **Knowledge capture workflow** — Extract learnings from completed projects
- **Skill maintenance** — When to create, update, or deprecate skills
- **Vault health checks** — Periodic review patterns
- **Cross-vault sync** — How to share best practices between personal and work vaults

## What This Does NOT Cover

Vault-specific patterns like:
- Personal: Pillar system, Captain's Log, Nimbus, focus cascade
- Work: WCCUSD workflows, Google Drive sync, partner management

These should be maintained in vault-specific skills.

## Updating

Pull the latest changes to update:

```bash
cd ~/.opencode/skills/vault-best-practices && git pull
```

## License

MIT
