# Database

Centralized database system for managing tasks, projects, contacts, companies, meetings, and bookmarks using Obsidian Bases.

## Overview

This folder contains structured databases for:
- **Tasks** - Task management and tracking
- **Projects** - Project management and planning
- **People** - Contact relationship management (CRM)
- **Companies** - Company relationship management (CRM)
- **Meetings** - Meeting notes and scheduling
- **Bookmarks** - URL bookmarks and reading list

**Special Directories:**
- **Skills** - User-editable agent skills following [Agent Skills spec](https://agentskills.io/specification) (use `/skill-creator` to create)
- **Schemas** - Data model specifications for all document types (except Skills and Schemas themselves)

All databases use Obsidian Bases for dynamic views, filtering, and inline editing.

## Quick Access

### Databases

![[Tasks.base]]

![[Projects.base]]

![[People.base]]

![[Companies.base]]

![[Meetings.base]]

![[Bookmarks.base]]

### Skills & Schemas

- **[[Skills/README.md|Skills]]** - User-editable agent skills for workflows and automation
- **[[Schemas/README.md|Schemas]]** - Data model specifications and templates

## Database Structure

### Tasks
**Purpose**: Task management and tracking
**Location**: `Database/Tasks/`
**Base File**: [[Tasks.base]]
**Template**: [[Tasks/Task-Template|Task Template]]

**Key Properties**:
- `type`: "task"
- `status`: backlog | active | blocked | done
- `priority`: urgent | high | medium | low
- `assignee`: Link to person
- `project`: Link to project (creates relationship)
- `due`: Due date
- `created`: Creation date

**Relationships**:
- Tasks → Projects (via `project` property)
- Tasks → People (via `assignee` property)

### Projects
**Purpose**: Project management and planning
**Location**: `Database/Projects/`
**Base File**: [[Projects.base]]
**Template**: [[Projects/Project-Template|Project Template]]

**Key Properties**:
- `type`: "project"
- `status`: planning | active | on-hold | completed | archived
- `priority`: urgent | high | medium | low
- `lead`: Link to project lead
- `team`: List of team members
- `start_date`: Project start date
- `target_date`: Target completion date
- `total_tasks`: Total task count
- `completed_tasks`: Completed task count

**Relationships**:
- Projects ← Tasks (backlinks from tasks)
- Projects → People (via `lead` and `team` properties)

### People
**Purpose**: Contact relationship management (CRM)
**Location**: `Database/People/`
**Base File**: [[People.base]]
**Template**: [[People/Person-Template|Person Template]]

**Key Properties**:
- `type`: "person"
- `company`: Link to company (creates relationship)
- `role`: Job title
- `email`: Email address
- `linkedin`: LinkedIn URL
- `twitter`: Twitter handle
- `relationship`: contact | colleague | client | partner | investor
- `last_contact`: Last interaction date
- `next_action`: Follow-up action

**Relationships**:
- People → Companies (via `company` property)
- People ← Tasks (backlinks from tasks assigned to them)
- People ← Projects (backlinks from projects they lead/are on)

### Companies
**Purpose**: Company relationship management (CRM)
**Location**: `Database/Companies/`
**Base File**: [[Companies.base]]
**Template**: [[Companies/Company-Template|Company Template]]

**Key Properties**:
- `type`: "company"
- `industry`: Industry category
- `stage`: seed | series-a | series-b | series-c | public
- `size`: Employee count range
- `website`: Company website
- `linkedin`: LinkedIn URL
- `relationship`: prospect | partner | client | vendor | investor
- `last_interaction`: Last interaction date
- `next_action`: Follow-up action

**Relationships**:
- Companies ← People (backlinks from people working there)

### Meetings
**Purpose**: Meeting notes and scheduling
**Location**: `Database/Meetings/`
**Base File**: [[Meetings.base]]
**Template**: [[Meetings/Meeting-Template|Meeting Template]]

**Key Properties**:
- `type`: "meeting"
- `meeting_date`: Date and time of meeting
- `meeting_type`: team | client | standup | 1on1 | planning
- `attendees`: List of attendees (links to people)
- `organizer`: Meeting organizer
- `project`: Related project
- `company`: Related company (for external meetings)
- `status`: scheduled | completed | cancelled
- `duration`: Meeting length
- `recording`: Link to recording

**Relationships**:
- Meetings → People (via `attendees` and `organizer`)
- Meetings → Projects (via `project` property)
- Meetings → Companies (via `company` property)

### Skills (Special Directory)
**Purpose**: User-editable agent skills for workflows and automation
**Location**: `Database/Skills/`
**Documentation**: [[Skills/README.md]]

**⚠️ Important**: Skills is a **special directory** that doesn't follow standard Database schema patterns:
- Each skill is a **subfolder** (not a markdown file) following the [Agent Skills specification](https://agentskills.io/specification)
- **Always use `/skill-creator`** to create new skills - do not create manually
- Skills have their own structure (SKILL.md, scripts/, references/, assets/)
- Not included in Schemas/ because Skills themselves define their own format

**Structure**: Each skill folder contains:
- `SKILL.md` - Required frontmatter (name, description, optional cron) and instructions
- `scripts/` - Optional executable code
- `references/` - Optional documentation
- `assets/` - Optional templates and files

**Key Features**:
- User-editable directly in Obsidian
- Optional `cron` frontmatter for scheduled execution (e.g., `"0 9 * * 1-5"` for weekdays at 9am)
- Loaded by Jarvis when configured with multiple skill directories
- Create new skills exclusively with `/skill-creator` skill

**Examples**: `daily-standup/` (runs weekdays at 9am via `cron: "0 9 * * 1-5"`)

### Schemas (Special Directory)
**Purpose**: Data model specifications for all document types
**Location**: `Database/Schemas/`
**Documentation**: [[Schemas/README.md]]

**⚠️ Important**: Schemas is a **special directory** that defines the structure for other Database documents:
- Contains **schema definitions** (not data documents)
- Each schema folder defines how to create documents in corresponding Database/ folders
- **Does not define itself** - Schemas/ has its own meta-structure
- **Does not define Skills/** - Skills follow the Agent Skills specification instead

**Available Schemas** (defines structure for):
- **Task** - Actionable work items → `Database/Tasks/`
- **Project** - Major initiatives → `Database/Projects/`
- **Person** - Team members and contacts → `Database/People/`
- **Company** - CRM for organizations → `Database/Companies/`
- **Meeting** - Meeting notes and calls → `Database/Meetings/`
- **Bookmark** - Web content and resources → `Database/Bookmarks/`
- **Document** - Free-form content → various locations

Each schema folder includes:
- README.md with complete specification
- template.md for creating new documents
- Frontmatter property definitions
- Best practices and examples

**Note**: To create a new schema, follow the guidelines in [[Schemas/README.md]]. To create a new skill (not a schema), use `/skill-creator`.

### Bookmarks
**Purpose**: URL bookmarks and reading list
**Location**: `Database/Bookmarks/`
**Base File**: [[Bookmarks.base]]
**Template**: [[Bookmarks/Bookmark-Template|Bookmark Template]]

**Key Properties**:
- `type`: "bookmark"
- `url`: Full URL
- `category`: Category/topic
- `description`: Brief description
- `saved`: Boolean - has content been saved/read
- `rating`: 1-5 star rating
- `last_accessed`: Last accessed date

## Creating New Entries

### Tasks
1. Copy [[Tasks/Task-Template|Task Template]]
2. Save to `Database/Tasks/` with descriptive name
3. Fill frontmatter:
   - Set `status`, `priority`, `due` date
   - Link to `project`: `[[Database/Projects/Project Name]]`
   - Link to `assignee`: `[[Database/People/Person Name]]`
4. Add description and acceptance criteria
5. Task appears automatically in all views

### Projects
1. Copy [[Projects/Project-Template|Project Template]]
2. Save to `Database/Projects/` with project name
3. Fill frontmatter:
   - Set `status`, `priority`, dates
   - Link to `lead`: `[[Database/People/Lead Name]]`
   - Add team members
4. Define objectives, scope, and milestones
5. Create tasks and link them to the project

### People
1. Copy [[People/Person-Template|Person Template]]
2. Save to `Database/People/` with person's name
3. Fill frontmatter:
   - Link to `company`: `[[Database/Companies/Company Name]]`
   - Add contact info (email, LinkedIn, Twitter)
   - Set `relationship` type
4. Add background and interaction history

### Companies
1. Copy [[Companies/Company-Template|Company Template]]
2. Save to `Database/Companies/` with company name
3. Fill frontmatter:
   - Set `industry`, `stage`, `size`
   - Add website and social links
   - Set `relationship` type
4. Add overview and interaction history
5. Create person entries for contacts at the company

### Meetings
1. Copy [[Meetings/Meeting-Template|Meeting Template]]
2. Save to `Database/Meetings/` with descriptive name
3. Fill frontmatter:
   - Set `meeting_date`, `meeting_type`
   - Add `attendees` (links to people)
   - Link to `project` or `company` if applicable
   - Set `duration` and `location`
4. Fill agenda, notes, decisions, and action items
5. Add recording link if available

### Bookmarks
1. Copy [[Bookmarks/Bookmark-Template|Bookmark Template]]
2. Save to `Database/Bookmarks/` with descriptive name
3. Fill frontmatter:
   - Add `url` and `category`
   - Write brief `description`
   - Set `saved` status
4. Add key takeaways and notes

## Relationship Patterns

### Task → Project
```yaml
# In task frontmatter
project: "[[Database/Projects/Project Name]]"
```

### Task → Person (Assignee)
```yaml
# In task frontmatter
assignee: "[[Database/People/Person Name]]"
```

### Project → People (Lead & Team)
```yaml
# In project frontmatter
lead: "[[Database/People/Project Lead]]"
team:
  - "[[Database/People/Team Member 1]]"
  - "[[Database/People/Team Member 2]]"
```

### Person → Company
```yaml
# In person frontmatter
company: "[[Database/Companies/Company Name]]"
```

## Querying Related Data

### Show Project's Tasks
Embed in project note:
```markdown
![[../Tasks.base#All Tasks]]
```

Or use inline query:
````markdown
```base
filters:
  and:
    - file.inFolder("Database/Tasks")
    - project == link(this.file)
views:
  - type: table
    name: Project Tasks
```
````

### Show Company's Contacts
Embed in company note:
````markdown
```base
filters:
  and:
    - file.inFolder("Database/People")
    - company == link(this.file)
views:
  - type: table
    name: Contacts
```
````

## Best Practices

### General
- Always use templates for consistency
- Fill all required frontmatter properties
- Use wikilinks for relationships: `[[Database/Folder/Name]]`
- Update dates when making changes
- Use tags for additional categorization

### Tasks
- Update status daily
- Link tasks to projects for tracking
- Add progress notes for long-running tasks
- Mark done when all acceptance criteria met

### Projects
- Update completion metrics regularly
- Review and adjust target dates
- Document key decisions and changes
- Archive completed projects

### CRM (People & Companies)
- Update last_contact after interactions
- Set next_action for follow-ups
- Keep contact info current
- Document interaction history

### Bookmarks
- Mark as saved after reading
- Add ratings and key takeaways
- Organize with categories and tags
- Clean up outdated bookmarks

## Views & Filters

Each base includes multiple pre-configured views:

**Tasks**: Active, By Person, By Project, Overdue, Backlog, Recently Completed, Kanban
**Projects**: Active, By Lead, By Status, Overdue, Project Board
**People**: All, By Company, By Relationship, Recent Contacts, Need Follow-up
**Companies**: All, By Industry, By Relationship, By Stage, Recent Interactions
**Bookmarks**: All, By Category, By Rating, To Read, Recently Added

All views support:
- Inline editing (click cells to edit)
- Sorting and filtering
- Grouping and summaries
- Multiple layouts (table, cards, list)

## Integration with Existing System

The Database system integrates with the existing folder structure:

- **02-Tasks/**: Legacy task folder - now points to Database
- **01-Team/**: Team member profiles can link to Database/People
- **03-Projects/**: Project documentation can link to Database/Projects
- **04-Knowledge/**: Can reference people, companies, and bookmarks

## Migration Guide

### Moving Existing Tasks
1. Move task `.md` files from `02-Tasks/` to `Database/Tasks/`
2. Update `project` frontmatter to use Database paths
3. Ensure `type: task` is set in frontmatter
4. Tasks will appear automatically in views

### Creating Projects from Existing Data
1. Review existing project documentation
2. Create project entries in `Database/Projects/`
3. Link related tasks to projects
4. Update team member references

