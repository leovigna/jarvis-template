---
tags:
  - decision
---

# Workspace Conventions

This document defines the standards for organizing and formatting content in your Jarvis workspace.

## File Naming

### General Rules
- Use kebab-case for files: `my-file-name.md`
- Be descriptive but concise
- Avoid special characters (except hyphens)
- No spaces in filenames

### Dated Content
For meeting notes and time-based content:
```
YYYY-MM-DD-Title.md
```
Examples:
- `2026-01-12-Weekly-Sync.md`
- `2026-01-12-Investor-Call.md`

### Person Names
Use natural name format with hyphens:
- `Alice-Smith.md`
- `Bob-Jones.md`

## YAML Frontmatter

All structured content should use YAML frontmatter for metadata.

### Task Frontmatter (Database System)
```yaml
---
type: task
status: active
priority: high
assignee: "[[Database/People/Person Name]]"
project: "[[Database/Projects/Project-Name]]"
created: 2026-01-12
due: 2026-01-20
blocked_by:
  - "[[Database/Tasks/Other-Task]]"
tags:
  - task
  - status/active
  - team/member
---
```

**Required Fields:**
- `type`: task, project, meeting, doc, person
- `status`: For tasks - backlog, active, blocked, done
- `created`: YYYY-MM-DD format

**Optional Fields:**
- `updated`: Last modification date
- `priority`: low, medium, high, urgent
- `assignee`: Link to person (use Database/People/ path)
- `project`: Link to project (use Database/Projects/ path)
- `due`: Deadline date
- `blocked_by`: Array of task links for dependencies (creates DAG)
- `tags`: List of tags

**Note**: Tasks should be created in `Database/Tasks/` to work with the Obsidian Bases system.

### Project Frontmatter (Database System)
```yaml
---
type: project
status: active
priority: high
lead: "[[Database/People/Person Name]]"
team:
  - "[[Database/People/Person Name]]"
  - "[[Database/People/Another Person]]"
start_date: 2026-01-01
target_date: 2026-03-01
total_tasks: 10
completed_tasks: 5
tags:
  - project
  - project/agi-assistant
---
```

**Note**: Projects should be created in `Database/Projects/` for tracking. Detailed project documentation goes in `Projects/` folder.

### Meeting Frontmatter
```yaml
---
type: meeting
date: 2026-01-12
attendees:
  - "[[Person Name]]"
  - "[[Another Person]]"
tags:
  - meeting
  - meeting/weekly
---
```

### Person Frontmatter
```yaml
---
type: person
role: CEO
email: person@company.com
tags:
  - team
---
```

## Tagging System

### Core Tags
- `#task` - Actionable work items
- `#project` - Project documentation
- `#meeting` - Meeting notes
- `#research` - Research findings
- `#decision` - Important decisions
- `#idea` - Future ideas/brainstorming
- `#team` - Team-related content

### Status Tags (Tasks)
- `#status/backlog` - Not yet started
- `#status/active` - Currently in progress
- `#status/blocked` - Waiting on dependencies
- `#status/done` - Completed

### Team Tags
- `#team/alice` - Related to Alice
- `#team/bob` - Related to Bob
- `#team/charlie` - Related to Charlie

### Project Tags
- `#project/project-alpha`
- `#project/project-beta`
- `#project/research`

### Topic Tags
- `#topic/ai` - AI/ML related
- `#topic/engineering` - Technical/engineering
- `#topic/business` - Business/strategy
- `#topic/product` - Product development

## Linking Conventions

### Internal Links
Use wikilinks for all internal references:
```markdown
[[File Name]]
[[File Name|Display Text]]
[[Folder/File Name]]
```

### Always Link To:
1. **People** - `[[Database/People/Person Name]]` for CRM entries, `[[Team/Person-Name]]` for profiles
2. **Projects** - `[[Database/Projects/Project-Name]]` for tracking, `[[Projects/Project-Name/Project Name]]` for docs
3. **Related Tasks** - Reference dependencies with `[[Database/Tasks/Task-Name]]`
4. **Meetings** - Link to meeting notes like `[[Database/Meetings/2026-01-12-Weekly-Sync]]`
5. **Key Concepts** - Link to research/docs on first mention

### External Links
Use standard markdown for external URLs:
```markdown
[Link Text](https://example.com)
```

## Markdown Formatting

### Headings
- Use `#` for title (one per document)
- Use `##` for major sections
- Use `###` for subsections
- Max 4 levels deep

### Lists
- Use `-` for unordered lists
- Use `1.` for ordered lists
- Use `- [ ]` for task checkboxes

### Code
- Use single backticks for inline code: `code`
- Use triple backticks with language for blocks:
  ````markdown
  ```python
  print("Hello")
  ```
  ````

### Tables
Use standard markdown tables:
```markdown
| Column 1 | Column 2 |
|----------|----------|
| Data 1   | Data 2   |
```

## Folder Organization

### Current Structure
- `Database/` - Structured data using Obsidian Bases
  - `Tasks/` - Task tracking
  - `Projects/` - Project tracking
  - `People/` - Contact management (CRM)
  - `Companies/` - Company relationships (CRM)
  - `Meetings/` - Meeting notes
  - `Bookmarks/` - URL bookmarks
- `Documents/` - Research documentation
- `Guides/` - Workspace guides and how-tos
- `Projects/` - Project documentation and notes
- `Team/` - Team member profiles

### Database System
The `Database/` folder uses Obsidian Bases for dynamic views and queries:
- Each database has a `.base` file for views
- Use templates in each subfolder
- Relationships via wikilinks in frontmatter
- Supports filtering, grouping, sorting
- Multiple view types (table, cards, list, kanban)

### Index Files
Every folder should have a `README.md` that:
- Explains the folder's purpose
- Links to key content
- Contains Dataview queries (if applicable)
- Provides navigation to related folders

## For Agents

### Creating New Content
1. Use appropriate template from `Database/Tasks/`, `Database/Projects/`, etc.
2. Include proper frontmatter (see Database/README.md for schemas)
3. Apply relevant tags
4. Link to related content using Database/ paths
5. Update index files if needed

### Modifying Content
1. Update `updated:` field in frontmatter
2. Maintain existing link structure
3. Use relative paths for file references
4. Preserve formatting conventions
5. Add changelog comment if significant

### Committing Changes
Use clear, descriptive commit messages:
```
Add Project roadmap tasks
Update person profile with new projects
Fix broken links in documentation
```

---

*Last updated: 2026-01-15*
