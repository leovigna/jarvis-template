# Project Data Model

Projects are major initiatives or workstreams tracked in the `Database/Projects/` folder.

## Location

`Database/Projects/`

## Filename Convention

Descriptive project name (e.g., `MCP-Server-Development.md`, `AGI-Assistant.md`)

## When to Create

- User requests a new project, initiative, or workstream
- Starting a major feature or product development effort
- Grouping related tasks under a common goal
- Tracking cross-functional work with multiple team members

## When to Update

- **Status changes**: Update `status` field as project progresses
- **Task metrics**: Update `total_tasks` and `completed_tasks` as tasks are created/completed
- **Timeline adjustments**: Update `target_date` when timeline changes
- **Milestone completion**: Check off milestones in Key Milestones section
- **Team changes**: Update `lead` or `team` array when team composition changes
- **Budget updates**: Adjust `budget` if allocation changes
- **Project completion**: Set `status: completed` or `status: archived` when done

## Frontmatter Schema

### Required Properties

| Property | Type | Description |
|----------|------|-------------|
| `type` | string | Must be `"project"` |
| `status` | enum | `planning` \| `active` \| `on-hold` \| `completed` \| `archived` |
| `priority` | enum | `urgent` \| `high` \| `medium` \| `low` |
| `lead` | wikilink | Project lead in `Database/People/` |
| `total_tasks` | number | Total number of tasks (update as tasks are added) |
| `completed_tasks` | number | Completed tasks (update when tasks finish) |

### Optional Properties

| Property | Type | Description |
|----------|------|-------------|
| `team` | array | Wikilinks to team members in `Database/People/` |
| `start_date` | date | Project start date (YYYY-MM-DD) |
| `target_date` | date | Target completion date (YYYY-MM-DD) |
| `budget` | number | Project budget amount |
| `tags` | array | Tags for categorization |

## Status Values

| Status | When to Use |
|--------|-------------|
| `planning` | Initial planning phase, not yet started |
| `active` | Currently in progress |
| `on-hold` | Paused or blocked |
| `completed` | Successfully finished |
| `archived` | Historical/cancelled projects |

## Tag Conventions

- Always include `project`
- Status tag matches status: `status/planning`, `status/active`, `status/on-hold`, `status/completed`, `status/archived`

## Viewing Projects

All projects automatically appear in views defined in `Database/Projects.base`:

- **Active Projects** - Grouped by priority
- **Projects by Lead** - Grouped by project lead
- **Projects by Status** - Grouped by status
- **Overdue Projects** - Projects past target date
- **Project Board** - Card view grouped by status
- **All Projects** - Complete list

## Project Management Best Practices

1. **Update task counts** - When creating tasks for a project, increment `total_tasks`. When completing tasks, increment `completed_tasks`
2. **Use embedded Base queries** - Include the Related Tasks query to see all project tasks inline
3. **Link to people** - Always use wikilinks to people in the `Database/People/` folder
4. **Track milestones** - Use the Key Milestones section with checkboxes to track progress
5. **Update target dates** - Adjust `target_date` as the project evolves
6. **Document decisions** - Keep notes on key decisions and changes in the Notes section
7. **Archive when done** - Set `status: archived` for completed/cancelled projects to declutter active views

## Examples

### Simple Project

```yaml
---
type: project
status: planning
priority: medium
lead: "[[Database/People/Team-Member]]"
team:
  - "[[Database/People/Team-Member-2]]"
start_date: 2026-01-15
target_date: 2026-03-01
total_tasks: 0
completed_tasks: 0
tags:
  - project
  - status/planning
---
```

### Project with Budget and Team

```yaml
---
type: project
status: active
priority: urgent
lead: "[[Database/People/Team-Lead]]"
team:
  - "[[Database/People/Team-Member-1]]"
  - "[[Database/People/Team-Member-2]]"
start_date: 2026-01-15
target_date: 2026-03-31
budget: 100000
total_tasks: 15
completed_tasks: 3
tags:
  - project
  - status/active
---
```

## Relationship to Tasks

Projects are connected to tasks via the `project` field in task frontmatter:

```yaml
# In task file: Database/Tasks/Implement-Feature.md
project: "[[Database/Projects/AGI-Assistant]]"
```

This creates a bidirectional relationship where:
- Tasks show which project they belong to
- Projects can query and display all their tasks using Base queries
- Project metrics (`total_tasks`, `completed_tasks`) track progress
