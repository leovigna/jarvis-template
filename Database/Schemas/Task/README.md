# Task Data Model

Tasks are actionable work items tracked in the `Database/Tasks/` folder.

## Location

`Database/Tasks/`

## Filename Convention

Descriptive name in title case (e.g., `Integrate-Zep-Memory.md`, `Setup-Database-Schema.md`)

## When to Create

- User requests a new task, action item, or work to be tracked
- Action items from meetings that need follow-up
- Breaking down project work into trackable units
- Assigning work to team members or the agent

## When to Update

- **Status changes**: Move from `backlog` → `active` → `done` (or `blocked`)
- **Progress updates**: Add notes in the Updates section with date
- **Due date changes**: Update `due` field when timeline shifts
- **Blocking issues**: Set `status: blocked` and add `blocked_by` reference
- **Completion**: Set `status: done` when all acceptance criteria met

## Frontmatter Schema

### Required Properties

| Property | Type | Description |
|----------|------|-------------|
| `type` | string | Must be `"task"` |
| `status` | enum | `backlog` \| `active` \| `blocked` \| `done` |
| `priority` | enum | `urgent` \| `high` \| `medium` \| `low` |
| `assignee` | wikilink | Link to `Database/People/` (e.g., `[[Database/People/Team-Member]]` or `[[Database/People/Agent]]`) |
| `created` | date | Creation date (YYYY-MM-DD) |

### Optional Properties

| Property | Type | Description |
|----------|------|-------------|
| `project` | wikilink | Link to `Database/Projects/` |
| `due` | date | Due date (YYYY-MM-DD) |
| `blocked_by` | wikilink or array | Task(s) this depends on |
| `tags` | array | Tags for categorization |

## Status Values

| Status | When to Use |
|--------|-------------|
| `backlog` | Not yet started, awaiting approval or prioritization |
| `active` | Currently in progress |
| `blocked` | Waiting on dependencies or external factors |
| `done` | Completed |

## Tag Conventions

- Always include `task`
- Status tag matches status: `status/backlog`, `status/active`, `status/blocked`, `status/done`
- Additional tags as needed for filtering

## Task Dependencies (DAG)

Use `blocked_by` to create task dependency chains:

**Single dependency:**
```yaml
blocked_by: "[[Database/Tasks/Setup-Database]]"
```

**Multiple dependencies:**
```yaml
blocked_by:
  - "[[Database/Tasks/Task-A]]"
  - "[[Database/Tasks/Task-B]]"
```

This creates a directed acyclic graph (DAG) where tasks can:
- Execute in order based on dependencies
- Show clear blocking relationships
- Enable automatic task chains
- Support parallel execution of independent tasks

## Agent-Assigned Tasks

For tasks assigned to the AI agent (`[[Database/People/Agent]]`):

1. Create with `status: backlog` for planning/review
2. User reviews and approves by changing to `status: active`
3. Agent executes active tasks in future sessions
4. Agent marks as `done` when complete

## Viewing Tasks

All tasks automatically appear in views defined in `Database/Tasks.base`:

- **Active Tasks by Priority** - Grouped by priority
- **My Tasks (by person)** - Per-person views
- **Tasks by Project** - Grouped by project
- **Blocked Tasks** - Tasks with status = blocked
- **Tasks with Dependencies** - Tasks with unresolved blockers
- **Overdue Tasks** - Active tasks past due date
- **Backlog** - Grouped by project
- **Recently Completed** - Last 20 completed tasks
- **Active Tasks (Kanban)** - Card view grouped by status

## Task Management Best Practices

1. **Update status daily** - Keep status current to reflect actual work
2. **Link to projects** - Always link tasks to projects for tracking
3. **Add progress notes** - Use Updates section for long-running tasks
4. **Mark done when complete** - Only mark done when all acceptance criteria met
5. **Use dependencies** - Link related tasks with `blocked_by` for clear workflows
6. **Update task counts** - When creating/completing tasks, update `total_tasks` and `completed_tasks` in the project frontmatter

## Examples

### Simple Task

```yaml
---
type: task
status: active
priority: medium
assignee: "[[Database/People/Team-Member]]"
project: "[[Database/Projects/AGI-Assistant]]"
created: 2026-01-15
due: 2026-01-20
tags:
  - task
  - status/active
---
```

### Task with Dependencies

```yaml
---
type: task
status: backlog
priority: high
assignee: "[[Database/People/Agent]]"
project: "[[Database/Projects/Backend]]"
created: 2026-01-15
due: 2026-01-22
blocked_by: "[[Database/Tasks/Design-Database-Schema]]"
tags:
  - task
  - status/backlog
---
```

### Task Chain (DAG)

Create multiple dependent tasks forming a workflow:

```
Design API → Implement Backend → Add Frontend
```

**Task 1**: `Database/Tasks/Design-API.md`
```yaml
type: task
status: active
assignee: "[[Database/People/Team-Member]]"
```

**Task 2**: `Database/Tasks/Implement-Backend.md`
```yaml
type: task
status: backlog
assignee: "[[Database/People/Agent]]"
blocked_by: "[[Database/Tasks/Design-API]]"
```

**Task 3**: `Database/Tasks/Add-Frontend.md`
```yaml
type: task
status: backlog
assignee: "[[Database/People/Team-Member-2]]"
blocked_by: "[[Database/Tasks/Implement-Backend]]"
```
