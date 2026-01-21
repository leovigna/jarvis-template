# Skills Directory

Custom slash commands for Jarvis. Each skill teaches the AI how to perform a specific task when invoked.

## What's Here

- **crm**: `/crm` - Research people and companies, add to CRM database with smart linking

## How Skills Work

Skills are instruction sets that become slash commands. When you type `/daily-brief` in chat, Jarvis reads the corresponding SKILL.md file and follows those instructions.

### Structure

```
skills/
└── skill-name/
    └── SKILL.md
```

### Basic SKILL.md Format

```markdown
---
name: skill-name
description: Brief description
user-invocable: true
---

Instructions for what to do when this command is invoked.
```

## Adding Your Own Skills

1. Create a new directory: `skills/my-skill/`
2. Add a `SKILL.md` file with frontmatter and instructions
3. Restart the bot: `clawdbot daemon restart`
4. Use it: `/my-skill`

### Example: Simple Reminder

```markdown
---
name: remind-me
description: Create a quick reminder
user-invocable: true
---

When the user runs `/remind-me [message]`, create a new task file in Database/Tasks with:
- Title: The reminder message
- Status: todo
- Created: Current timestamp
- Due: Ask the user when it's due

Then confirm the reminder was created.
```

## Advanced Features

### Conditional Loading

Only load a skill if certain requirements are met:

```markdown
---
name: video-process
description: Process videos with ffmpeg
metadata: {"clawdbot":{"requires":{"bins":["ffmpeg"],"env":["VIDEO_API_KEY"]}}}
---
```

### Direct Tool Dispatch

Skip the AI model and call a tool directly:

```markdown
---
name: quick-search
description: Fast search without AI processing
user-invocable: true
command-dispatch: tool
command-tool: search
---
```

## Telegram Command Architecture

**Important**: Telegram bots don't support inline parameters (like `/crm john@example.com`). Instead, they use a conversational flow:

1. User invokes the command: `/skill-name`
2. Skill prompts for input: "Please provide..."
3. User responds with the required information

This creates a more natural chat-based interaction pattern. When writing skills, always design them to:
- Accept the command without parameters
- Prompt for necessary input after invocation
- Handle multi-turn conversations to gather required data

Example:
```
User: /remind-me
Assistant: What would you like to be reminded about?
User: Call Sarah tomorrow
Assistant: When should I remind you?
User: 2pm
```

## Best Practices

1. **Keep it focused**: One clear purpose per skill
2. **Be specific**: Clear instructions help the AI perform consistently
3. **Use examples**: Show the expected format in the instructions
4. **Match the vibe**: Keep Jarvis professional and efficient
5. **Test first**: Try it locally before committing
6. **No inline parameters**: Design for conversational input flow (see Telegram Command Architecture above)

## More Info

See `Projects/ClawdAssistant/CustomCommandsAndMCP.md` in the main obsidian workspace for detailed documentation on skills and MCP integration.

## External Skills

Install pre-made skills from ClawdHub:

```bash
clawdhub install <skill-name>
```

Browse skills at [clawdhub.com](https://clawdhub.com)
