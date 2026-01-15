# Person Data Model

People - team members, external contacts, and notable industry figures tracked in the Database system.

## Location

| Person Type | Folder |
|-------------|--------|
| Team Member | `Team/` or `Database/People/` |
| External Contact | `Database/People/` |
| Industry Leader | `Documents/AI-Ecosystem/Leaders/` |

## Filename Convention

`First-Last.md` (e.g., `Alice-Smith.md`, `Bob-Jones.md`, `Jane-Doe.md`)

## When to Create

- Adding a team member to the workspace
- Recording a new external contact (client, partner, investor)
- Documenting notable industry figures for research
- Building a contact database for CRM

## When to Update

- **After interactions**: Add entry to Interaction History with date
- **Contact info changes**: Update email, phone, social links
- **Role changes**: Update `role` or `company` fields
- **Relationship updates**: Update `relationship` field
- **Last contact**: Update `last_contact` date after interactions
- **Next actions**: Set `next_action` for follow-up items

## Frontmatter Schema

### Team Member

```yaml
---
type: person
role: Job Title
email: name@company.com
created: 2026-01-15
tags:
  - team
  - team/member
---
```

### External Contact (CRM)

```yaml
---
type: person
company: "[[Database/Companies/Company-Name]]"
role: VP Engineering
email: person@company.com
linkedin: https://linkedin.com/in/username
twitter: https://twitter.com/username
location: San Francisco, CA
relationship: contact
last_contact: 2026-01-15
next_action: Schedule follow-up call
created: 2026-01-15
tags:
  - person
  - contact
  - client
---
```

### Industry Leader

```yaml
---
type: person
role: AI Researcher
company: Research Lab
created: 2026-01-15
tags:
  - leader
  - topic/ai
---
```

## Required Properties

| Property | Type | Description |
|----------|------|-------------|
| `type` | string | Must be `"person"` |

## Optional Properties

| Property | Type | Description |
|----------|------|-------------|
| `role` | string | Job title or role |
| `company` | wikilink | Link to `Database/Companies/` |
| `email` | string | Email address |
| `linkedin` | string | LinkedIn profile URL |
| `twitter` | string | Twitter/X handle URL |
| `location` | string | City, State/Country |
| `relationship` | enum | `contact` \| `colleague` \| `client` \| `partner` \| `investor` |
| `last_contact` | date | Last interaction date (YYYY-MM-DD) |
| `next_action` | string | Follow-up action needed |
| `created` | date | Creation date (YYYY-MM-DD) |
| `tags` | array | Tags for categorization |

## Relationship Values

| Relationship | When to Use |
|--------------|-------------|
| `contact` | General external contact |
| `colleague` | Team member or coworker |
| `client` | Customer or client contact |
| `partner` | Partnership or collaboration contact |
| `investor` | Investor or VC contact |

## Tag Conventions

### Team Members
- Always include `team`
- Person-specific tag: `team/member1`, `team/member2`, `team/member3`

### External Contacts
- Always include `person`
- Relationship tags: `contact`, `client`, `partner`, `investor`
- Company-based tags if applicable

### Industry Leaders
- Always include `leader`
- Topic tags: `topic/ai`, `topic/research`, etc.

## Viewing People

All people automatically appear in views defined in `Database/People.base`:

- **All People** - Complete list
- **By Company** - Grouped by company
- **By Relationship** - Grouped by relationship type
- **Recent Contacts** - Sorted by `last_contact` date
- **Need Follow-up** - People with `next_action` set

## CRM Best Practices

1. **Update after interactions** - Always add dated notes in Interaction History
2. **Set last_contact date** - Update `last_contact` frontmatter after meetings/calls
3. **Track next actions** - Use `next_action` field for follow-up reminders
4. **Link to companies** - Always link external contacts to their `company`
5. **Use embedded queries** - Include task/meeting queries to see related activities
6. **Maintain contact info** - Keep email, LinkedIn, and other contact info current
7. **Document context** - Record how you know them and why the relationship matters

## Team Member Tags

| Person | Tag |
|--------|-----|
| Team Member 1 | `team/member1` |
| Team Member 2 | `team/member2` |
| Team Member 3 | `team/member3` |

## Examples

### Team Member

```yaml
---
type: person
role: Job Title
email: member@company.com
created: 2026-01-15
tags:
  - team
  - team/member
---
```

### External Contact

```yaml
---
type: person
company: "[[Database/Companies/Example-Corp]]"
role: VP Engineering
email: jane@example.com
linkedin: https://linkedin.com/in/janedoe
location: New York, NY
relationship: client
last_contact: 2026-01-15
next_action: Send Q1 report by Jan 31
created: 2026-01-10
tags:
  - person
  - contact
  - client
---
```

### Industry Leader

```yaml
---
type: person
role: AI Researcher & Author
company: OpenAI
created: 2026-01-15
tags:
  - leader
  - topic/ai
  - topic/research
---
```

## Relationship to Other Documents

People connect to multiple document types:

### To Companies
```yaml
company: "[[Database/Companies/Example-Corp]]"
```

### To Tasks (as assignee)
```yaml
# In task file
assignee: "[[Database/People/Person-Name]]"
```

### To Projects (as lead or team member)
```yaml
# In project file
lead: "[[Database/People/Project-Lead]]"
team:
  - "[[Database/People/Team-Member]]"
```

### To Meetings (as attendee or organizer)
```yaml
# In meeting file
attendees:
  - "[[Database/People/Attendee-1]]"
organizer: "[[Database/People/Organizer]]"
```

This creates a network where:
- People show all their tasks, projects, and meetings
- Tasks/projects/meetings show which people are involved
- Companies show all their contacts
- Interaction history is tracked across all document types
