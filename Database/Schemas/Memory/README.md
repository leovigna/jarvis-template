# Memory Data Model

Memory entries store Jarvis's persistent memory across sessions, including daily logs and curated long-term memories.

## Location

`Database/Memories/`

## Filename Convention

- **Daily memories**: `YYYY-MM-DD.md` (e.g., `2026-01-15.md`)
- **Long-term memories**: `MEMORY.md` (single curated file)
- **Topical memories**: `Memory-Topic-Name.md` (e.g., `Memory-Project-Context.md`)

## When to Create

### Daily Memory Entries
- At the start of each session (read today's and yesterday's entries)
- When significant events occur during the session
- At the end of major work sessions to capture context
- When user explicitly asks to "remember" something

### Long-Term Memory (MEMORY.md)
- During heartbeat maintenance (periodic curation)
- When patterns emerge from daily entries worth preserving
- When lessons are learned that should persist indefinitely
- During major project milestones or decisions

### Topical Memories
- For specific ongoing projects or domains that need persistent context
- When a topic accumulates enough information to warrant its own memory file
- For specialized knowledge that doesn't fit in daily logs or MEMORY.md

## When to Update

- **Daily entries**: Add throughout the session as events unfold
- **MEMORY.md**: Review and update during heartbeat cycles (every few days)
- **Topical memories**: Update when relevant work occurs in that domain
- **Security level changes**: When sharing context changes (main session vs group chat)

## Frontmatter Schema

### Required Properties

| Property | Type | Description |
|----------|------|-------------|
| `type` | string | Must be `"memory"` |
| `memory_type` | enum | `daily` \| `longterm` \| `topical` |
| `created` | date | Creation date (YYYY-MM-DD) |

### Optional Properties

| Property | Type | Description |
|----------|------|-------------|
| `session_id` | string | Claude Code session identifier |
| `session_type` | enum | `main` \| `group` \| `shared` - context of session |
| `security_level` | enum | `personal` \| `shareable` - can this be loaded in shared contexts? |
| `topic` | string | For topical memories, the subject area |
| `related_project` | wikilink | Link to `Database/Projects/` if relevant |
| `related_tasks` | array | Links to `Database/Tasks/` entries |
| `related_people` | array | Links to `Database/People/` entries |
| `tags` | array | Tags for categorization |
| `updated` | date | Last modification date |

## Memory Types

| Type | Purpose | Security |
|------|---------|----------|
| `daily` | Raw logs of what happened each day | Personal by default |
| `longterm` | Curated memories worth keeping indefinitely | Personal by default |
| `topical` | Domain-specific persistent context | Shareable if appropriate |

## Security Considerations

**CRITICAL**: Memory contains personal context that should NOT leak to strangers.

- **Main sessions** (direct chats with your human): Load MEMORY.md and relevant memories freely
- **Shared contexts** (Discord, group chats, other people): DO NOT load personal memories
- Use `security_level: personal` for sensitive content
- Use `security_level: shareable` for general knowledge that's safe in any context

## Tag Conventions

- Always include `memory`
- Type tag: `memory/daily`, `memory/longterm`, `memory/topical`
- Session type: `session/main`, `session/group`, `session/shared`
- Topic tags for categorization: `topic/project`, `topic/learning`, `topic/decision`

## Memory Lifecycle

```
Daily Logs → Review during heartbeats → Extract to MEMORY.md → Archive old dailies
```

1. **Capture**: Write to daily memory files as events happen
2. **Review**: During heartbeats, read recent daily files
3. **Curate**: Extract significant learnings to MEMORY.md
4. **Archive**: Old daily files can be moved to archive or kept for reference
5. **Maintain**: Remove outdated info from MEMORY.md over time

## Viewing Memories

Memories can be viewed through:
- Direct file reading in main sessions
- Base views in `Database/Memories.base`
- Search and filtering by tags, dates, topics
- Links from related tasks and projects

## Memory Management Best Practices

1. **Write it down immediately** - Don't rely on "mental notes" that won't survive restarts
2. **Separate personal from shareable** - Mark security levels appropriately
3. **Curate regularly** - Review daily logs every few days and update MEMORY.md
4. **Link to related content** - Connect memories to tasks, projects, people
5. **Remove stale info** - Clean up MEMORY.md when context changes
6. **Use topical memories** - Create separate files for complex ongoing topics
7. **Timestamp updates** - Always note when memories are modified

## Examples

### Daily Memory Entry

```yaml
---
type: memory
memory_type: daily
created: 2026-01-15
session_id: "session-abc123"
session_type: main
security_level: personal
tags:
  - memory
  - memory/daily
  - session/main
---

# 2026-01-15 Memory

## Morning Session

Started work on Database refactoring. User wants to clean up old task files.

## Key Events

- Removed Placeholder Labs specific data
- Genericized README and AGENTS.md
- Started work on Memory schema

## Decisions

- Memory will use Database/Memories/ instead of flat memory/ directory
- Following existing schema patterns for consistency

## Notes

User emphasized importance of making this a clean template for Jarvisbot users.

## Links

- [[Database/Tasks/Genericize-Repository-Remove-Placeholder-Labs-Info]]
- [[Database/Tasks/Create-Memory-Schema]]
```

### Long-Term Memory (MEMORY.md)

```yaml
---
type: memory
memory_type: longterm
created: 2026-01-01
updated: 2026-01-15
security_level: personal
tags:
  - memory
  - memory/longterm
---

# Jarvis's Long-Term Memory

## About My Human

[Personal context about your human - preferences, habits, working style]

## Important Lessons

### Always Write Things Down
Files persist across sessions. "Mental notes" don't. When asked to remember something, immediately write it to a file.

### Security Matters
Never load MEMORY.md in group chats or shared contexts. Personal data should stay personal.

## Project Context

### Active Projects

- [[Database/Projects/Project-Name]] - Brief context about the project

### Past Learnings

- Lesson learned from previous work
- Pattern that emerged over time

## Decisions and Preferences

### Working Style
- User prefers X approach over Y
- Always ask before doing Z

### Technical Decisions
- We use X library for Y because Z
- Architectural decision: reasoning

## Tools and Setup

### Environment
- Key tools and configurations
- Important paths and locations

## People

### Team Members
- [[Database/People/Person-Name]] - Role and context

## Ongoing Concerns

- Things to watch out for
- Known issues or limitations
```

### Topical Memory

```yaml
---
type: memory
memory_type: topical
topic: "Database Refactoring"
created: 2026-01-15
updated: 2026-01-15
security_level: shareable
related_project: "[[Database/Projects/Workspace-Refactor]]"
tags:
  - memory
  - memory/topical
  - topic/database
  - topic/architecture
---

# Memory: Database Refactoring

## Context

Working on refactoring the workspace Database system to be more generic and work well with Jarvisbot.

## Key Decisions

1. **Memory Location**: Using Database/Memories/ instead of flat memory/ directory
   - Rationale: Consistent with other Database schemas
   - Benefit: Can use Obsidian Bases queries
   - Trade-off: Slightly more structure than flat files

2. **Schema Approach**: Following existing pattern from Task, Project, etc.
   - Full README.md with specifications
   - Templates for quick creation
   - .base file for views

## Progress

- [x] Removed Placeholder Labs data
- [x] Genericized all READMEs
- [ ] Create Memory schema
- [ ] Merge AGENTS.md files

## Technical Notes

- Memory should support daily logs and long-term curation
- Security levels important for group chat vs main session distinction
- Link to related tasks and projects for context

## Related

- [[Database/Tasks/Create-Memory-Schema]]
- [[Database/Tasks/Merge-AGENTS-Files]]
- [[AGENTS]]
```

## Integration with Jarvis

Memory entries are designed for Jarvisbot's workflow:

### Session Start
1. Read MEMORY.md (if in main session)
2. Read today's daily memory (Database/Memories/YYYY-MM-DD.md)
3. Read yesterday's daily memory for recent context
4. Load any relevant topical memories

### During Session
- Add significant events to today's daily memory
- When user says "remember this", write to appropriate memory file
- Link memories to related tasks, projects, decisions

### Heartbeat Cycles
- Review recent daily memories
- Extract learnings to MEMORY.md
- Update topical memories for ongoing work
- Clean up outdated information

### Group Chats
- DO NOT load MEMORY.md (personal context)
- Can reference shareable topical memories if appropriate
- Keep personal and shared contexts separate

## Memory vs Other Document Types

- **Memory** - Personal agent context, learnings, session logs
- **Meeting** - Formal meeting notes with attendees and outcomes
- **Task** - Actionable work items with status tracking
- **Document** - Formal documentation and research
- **Bookmark** - Saved web resources and references

Use Memory for agent-specific context that needs to persist across sessions but isn't formal documentation.
