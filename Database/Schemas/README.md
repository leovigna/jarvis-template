# Database Schemas

This folder contains the data model specifications for all document types in the Database system. Each schema defines frontmatter properties, conventions, and best practices for a specific document type.

## Available Schemas

| Schema | Location | Description |
|--------|----------|-------------|
| **Task** | [Task/](Task/) | Actionable work items with status tracking and dependencies |
| **Project** | [Project/](Project/) | Major initiatives grouping related tasks |
| **Person** | [Person/](Person/) | Team members, contacts, and industry figures |
| **Company** | [Company/](Company/) | CRM for clients, partners, vendors, investors |
| **Meeting** | [Meeting/](Meeting/) | Meeting notes, calls, and syncs |
| **Bookmark** | [Bookmark/](Bookmark/) | Web content, articles, and resources |
| **Memory** | [Memory/](Memory/) | Agent memory: daily logs, long-term context, and topical knowledge |
| **Document** | [Document/](Document/) | Free-form content like research and PRDs |

## Schema Structure

Each schema folder contains:
- `README.md` - Complete specification with frontmatter schema, conventions, examples
- `template.md` - Ready-to-use template file for creating new documents
- Additional templates for variants (e.g., `template-research.md`, `template-prd.md`)

## Creating a New Schema

When adding a new document type to the Database system:

### 1. Create Schema Folder

Create a new capitalized folder in `Database/Schemas/`:
```
Database/Schemas/YourType/
```

### 2. Write README.md

Document the schema with these sections:

```markdown
# YourType Data Model

Brief description of what this document type represents.

## Location
`Database/YourTypes/`

## Filename Convention
Describe naming pattern (e.g., "Descriptive-Name.md", "YYYY-MM-DD-Title.md")

## When to Create
- Bullet points describing when to create this document type
- User scenarios and triggers

## When to Update
- **Field changes**: When to update specific fields
- **Status changes**: Lifecycle transitions
- **Relationship updates**: When links to other documents change

## Frontmatter Schema

### Required Properties
| Property | Type | Description |
|----------|------|-------------|
| `type` | string | Must be `"yourtype"` |
| ... | ... | ... |

### Optional Properties
| Property | Type | Description |
|----------|------|-------------|
| ... | ... | ... |

## Property Types Reference

- `string` - Text value
- `number` - Numeric value
- `date` - YYYY-MM-DD format
- `wikilink` - Link to another document: `[[Database/Folder/File]]`
- `array` - List of values
- `enum` - One of specific allowed values

## Tag Conventions
- Always include `yourtype`
- Additional tags for filtering

## Viewing Documents
Describe Base views available in `Database/YourTypes.base`

## Best Practices
1. Numbered list of best practices
2. Common patterns and anti-patterns
3. Relationship management

## Examples
Show 2-3 real-world examples with different frontmatter configurations
```

### 3. Create template.md

Provide a starter template:

```markdown
---
type: yourtype
# Add required properties with example values
# Optional properties can be commented out
created: YYYY-MM-DD
tags:
  - yourtype
---

# Title

## Section 1

Content structure...

## Section 2

More structure...
```

### 4. Create Base Views

Create `Database/YourTypes.base` file with Obsidian Bases queries:
```yaml
filters:
  and:
    - file.inFolder("Database/YourTypes")
    - type == "yourtype"
views:
  - type: table
    name: All YourTypes
```

### 5. Update This Index

Add your schema to the table at the top of this README.

## Common Frontmatter Patterns

### Core Metadata
All documents should include:
```yaml
type: documenttype  # Required: identifies document type
created: YYYY-MM-DD # Recommended: creation date
tags: [...]         # Recommended: for filtering and categorization
```

### Relationships
Use wikilinks to connect documents:
```yaml
# Single relationship
project: "[[Database/Projects/Project-Name]]"

# Multiple relationships
team:
  - "[[Database/People/Person-One]]"
  - "[[Database/People/Person-Two]]"
```

### Status Tracking
Most active documents use status enums:
```yaml
status: active  # Common values: backlog, active, done, blocked, completed, archived
```

### Dates
Use ISO 8601 date format:
```yaml
created: 2026-01-15
due: 2026-01-31
meeting_date: 2026-01-20
```

### Arrays and Lists
```yaml
# Simple array
tags:
  - tag1
  - tag2

# Array of wikilinks
attendees:
  - "[[Database/People/Person-One]]"
  - "[[Database/People/Person-Two]]"
```

## Schema Best Practices

### 1. Keep Schemas Minimal
Only require properties that are always needed. Make everything else optional.

### 2. Use Enums for Status
Define specific allowed values for status fields to enable filtering:
```yaml
status: active  # One of: backlog | active | blocked | done
```

### 3. Standardize Date Fields
Always use YYYY-MM-DD format and consistent naming:
- `created` - When document was created
- `due` - When task/project is due
- `start_date` - When project/event starts
- `target_date` - Target completion date
- `meeting_date` - When meeting occurred

### 4. Enable Bidirectional Links
Design schemas so relationships work in both directions:
```yaml
# Task links to Project
project: "[[Database/Projects/AGI-Assistant]]"

# Project can query all its tasks
# Use Base query: project == link(this.file)
```

### 5. Document When to Update
Clearly specify what triggers should update the document, helping users and agents maintain data quality.

### 6. Provide Examples
Include 2-3 realistic examples showing common variations and edge cases.

### 7. Use Templates
Always provide template.md files so users can quickly create properly formatted documents.

## Integration with Obsidian Bases

All schemas are designed to work with [Obsidian Bases](https://github.com/Zachatoo/obsidian-database-plugin):

### Base Queries
Filter documents by frontmatter properties:
```yaml
filters:
  and:
    - file.inFolder("Database/Tasks")
    - status == "active"
    - priority == "urgent"
```

### Relationship Queries
Find documents related to the current file:
```yaml
filters:
  and:
    - file.inFolder("Database/Tasks")
    - project == link(this.file)  # All tasks for this project
```

### View Types
- `table` - Spreadsheet view with columns
- `kanban` - Card view grouped by property
- `list` - Simple list view
- `card` - Card grid view

## Validation and Quality

When creating or updating schemas:

1. Test with real data before committing
2. Ensure Base queries work correctly
3. Verify templates create valid documents
4. Check that relationships are bidirectional
5. Confirm enum values are comprehensive
6. Validate date formats are consistent

## Schema Versioning

When modifying existing schemas:

1. **Additive changes** (new optional properties) - Safe, no migration needed
2. **Breaking changes** (required properties, renamed fields) - Document migration path
3. **Deprecations** - Mark fields as deprecated in README before removing
4. **Data migrations** - Provide scripts or instructions for bulk updates

## Questions and Extensions

To propose a new schema or modify an existing one:

1. Check if the use case fits an existing schema first
2. Consider whether a tag or property would suffice
3. Create a draft schema following the structure above
4. Test with real documents
5. Document the rationale for the new schema
