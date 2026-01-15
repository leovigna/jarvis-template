# Skills

User-editable agent skills that extend Claude's capabilities with specialized workflows, automation, and domain knowledge.

## Structure

This folder contains skills following the [Agent Skills specification](https://agentskills.io/specification):

```
skill-name/
├── SKILL.md (required)
│   ├── YAML frontmatter with name and description
│   └── Markdown instructions
├── scripts/ (optional)
├── references/ (optional)
└── assets/ (optional)
```

## Skills vs Internal Skills

| Location | Purpose | Editable |
|----------|---------|----------|
| **Database/Skills/** | User-created skills and workflows | ✅ Yes - edit directly in Obsidian |
| **.claude/skills/** | System skills (skill-creator, document-format, etc.) | ❌ No - maintained by template |

## Creating Skills

Use the `/skill-creator` skill for guided creation, or create manually:

1. Create folder: `Database/Skills/your-skill-name/`
2. Create `SKILL.md` with frontmatter:

```yaml
---
name: your-skill-name
description: What it does and when to use it
cron: "0 9 * * *"  # Optional: cron expression for scheduled execution
---

# Your Skill Name

Instructions...
```

3. Add optional scripts/, references/, assets/

## Scheduled Skills (Cron)

Skills can optionally include a `cron` field in frontmatter for scheduled execution:

```yaml
---
name: daily-standup
description: Creates daily standup notes
cron: "0 9 * * 1-5"  # Every weekday at 9am
---
```

Common cron patterns:
- `"0 9 * * *"` - Daily at 9am
- `"0 9 * * 1-5"` - Weekdays at 9am
- `"0 17 * * 5"` - Every Friday at 5pm
- `"0 0 1 * *"` - First day of each month at midnight

Not all skills need cron scheduling - only add this field if the skill should run automatically on a schedule.

## Jarvis Configuration

To use skills from this directory, configure Jarvis to load from multiple directories:

```yaml
skills:
  directories:
    - .claude/skills      # Internal skills
    - Database/Skills     # User-editable skills
```

See documentation for details.

## Examples

See existing skills in this folder like `daily-standup/` for reference.
