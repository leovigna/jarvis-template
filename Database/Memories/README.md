# Memories

Agent memory storage for Jarvis - persistent context across sessions.

## Overview

This folder contains memory entries that help Jarvis maintain context across sessions. Memory entries come in three types:

1. **Daily Memories** - Raw logs of each day's events (`YYYY-MM-DD.md`)
2. **Long-Term Memory** - Curated essential knowledge (`MEMORY.md`)
3. **Topical Memories** - Domain-specific persistent context (`Memory-Topic.md`)

## Quick Start

### For Agents

**Every session start:**
1. Read `MEMORY.md` (if in main session, NOT in group chats)
2. Read today's daily memory (`YYYY-MM-DD.md`)
3. Read yesterday's daily memory for recent context
4. Load relevant topical memories for current work

**During the session:**
- Add significant events to today's daily memory
- When user says "remember this", write to appropriate memory file
- Link memories to related tasks and projects

**Heartbeat maintenance (every few days):**
- Review recent daily memories
- Extract learnings to MEMORY.md
- Update topical memories
- Clean up outdated info

### For Users

Memories help Jarvis:
- Remember your preferences and working style
- Maintain project context across sessions
- Learn from past experiences
- Build understanding of your goals

## Memory Types

### Daily (`YYYY-MM-DD.md`)

Daily logs capture what happened each day:
- Events and activities
- Decisions made
- Lessons learned
- Links to tasks and projects
- Session context

**Security**: Personal by default - not loaded in group chats.

### Long-Term (`MEMORY.md`)

Curated knowledge worth keeping indefinitely:
- About your human (preferences, style)
- Important lessons and patterns
- Project context and history
- Technical decisions and reasoning
- Tool configurations
- People and relationships

**Security**: Personal - NEVER load in shared contexts.

### Topical (`Memory-Topic-Name.md`)

Domain-specific persistent context:
- Project-specific knowledge
- Technical area expertise
- Ongoing investigation context
- Decision history for a topic

**Security**: Can be shareable if appropriate (mark with `security_level: shareable`).

## Schema and Templates

Full schema documentation: [[../Schemas/Memory/README]]

Templates available:
- [[../Schemas/Memory/template-daily]] - Daily memory entry
- [[../Schemas/Memory/template-longterm]] - Long-term memory (MEMORY.md)
- [[../Schemas/Memory/template-topical]] - Topical memory

## Viewing Memories

Use the [[Memories.base|Memory Base]] for dynamic views:
- All Memories (table view)
- Daily Memories (chronological)
- Long-Term Memories
- Topical Memories
- Recent Memories (last 30 days)
- Memory Cards (grouped by type)

## Security Best Practices

**CRITICAL**: Memory contains personal context.

- **Main sessions** (1:1 with your human): Load memories freely
- **Group chats** (Discord, shared contexts): DO NOT load personal memories
- Mark `security_level: personal` for sensitive content
- Mark `security_level: shareable` for safe-in-any-context content
- When in doubt, keep it personal

## Memory Maintenance

### Weekly Review

1. Read daily memories from the past week
2. Identify significant patterns or learnings
3. Update MEMORY.md with key insights
4. Update relevant topical memories
5. Remove outdated information

### Monthly Cleanup

1. Archive old daily memories (optional)
2. Review MEMORY.md for relevance
3. Consolidate topical memories if needed
4. Ensure security levels are correct

## Best Practices

1. **Write immediately** - Don't rely on "mental notes"
2. **Link to context** - Connect memories to tasks, projects, people
3. **Curate regularly** - Keep MEMORY.md current and relevant
4. **Separate concerns** - Use topical memories for complex domains
5. **Respect privacy** - Never load personal memories in shared contexts
6. **Timestamp updates** - Note when and why memories change
7. **Clean up** - Remove outdated or incorrect information

## Examples

See the schema README for detailed examples:
- [[../Schemas/Memory/README#Examples]]

## Integration with Workflow

Memories integrate with the rest of the Database system:

```yaml
# In a memory entry, link to related content:
related_project: "[[Database/Projects/Project-Name]]"
related_tasks:
  - "[[Database/Tasks/Task-Name]]"
related_people:
  - "[[Database/People/Person-Name]]"
```

This creates bidirectional links between memories and other documents, making it easy to find relevant context.

---

*Last updated: 2026-01-15*
