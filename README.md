# opencode Config

Global opencode configuration and agent skills for personal and work Obsidian vaults.

## Included Skills

- **obsidian-skills** — Official Obsidian agent skills from [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills):
  - obsidian-markdown — Obsidian Flavored Markdown syntax
  - obsidian-bases — Obsidian Bases (.base files)
  - json-canvas — JSON Canvas (.canvas files)
  - obsidian-cli — Obsidian CLI interactions
  - defuddle — Web page markdown extraction

- **vault-best-practices** — Shared vault maintenance and improvement patterns for personal (Gunslinger) and work (AI Kim) vaults.
- **personal-vault** — Gunslinger-specific conventions: pillar system, Captain's Log, focus cascade, Nimbus board.
- **work-vault** — AI Kim-specific conventions: WCCUSD workflows, Google Drive sync, project management.

## Updating obsidian-skills

```bash
rm -rf ~/.config/opencode/skills/obsidian-skills
git clone https://github.com/kepano/obsidian-skills.git ~/.config/opencode/skills/obsidian-skills
rm -rf ~/.config/opencode/skills/obsidian-skills/.git
```

## Cloning on a New Machine

```bash
git clone git@github.com:raijuninja/opencode-config.git ~/.config/opencode
```
