# Meeting Data Model

Meetings, calls, and syncs documented in the `Database/Meetings/` folder.

## Location

| Meeting Type | Folder |
|--------------|--------|
| Daily Standup | `Meetings/Dailies/` or `Database/Meetings/` |
| Weekly Sync | `Meetings/Weeklies/` or `Database/Meetings/` |
| External Call | `Meetings/External/` or `Database/Meetings/` |
| Team Meeting | `Database/Meetings/` |
| Client/Customer | `Database/Meetings/` |

## Filename Convention

| Meeting Type | Format |
|--------------|--------|
| Daily | `YYYY-MM-DD-Daily.md` |
| Weekly | `YYYY-MM-DD-Weekly-Sync.md` |
| External | `YYYY-MM-DD-Company-Name.md` |
| Other | `YYYY-MM-DD-Meeting-Title.md` |

## When to Create

- Before or immediately after any meeting
- Daily standups or weekly syncs
- External client/partner calls
- Planning sessions or retrospectives
- 1:1 meetings

## When to Update

- **Before meeting**: Fill in agenda and attendees
- **During meeting**: Take notes in Discussion section
- **After meeting**: Complete action items, decisions, and next steps
- **Status changes**: Update `status` from `scheduled` → `completed` or `cancelled`
- **Follow-up**: Create task files for action items and link them
- **Recording added**: Add `recording` link if available

## Frontmatter Schema

### Required Properties

| Property | Type | Description |
|----------|------|-------------|
| `type` | string | Must be `"meeting"` |
| `meeting_date` | datetime | Date and time (YYYY-MM-DD HH:MM) |
| `meeting_type` | enum | `team` \| `client` \| `standup` \| `1on1` \| `planning` \| `external` |
| `status` | enum | `scheduled` \| `completed` \| `cancelled` |

### Optional Properties

| Property | Type | Description |
|----------|------|-------------|
| `attendees` | array | Wikilinks to people in `Database/People/` |
| `organizer` | wikilink | Meeting organizer from `Database/People/` |
| `project` | wikilink | Related project from `Database/Projects/` |
| `company` | wikilink | Related company from `Database/Companies/` (for external meetings) |
| `duration` | string | Meeting length (e.g., "60 minutes", "30 min") |
| `location` | string | Location or platform (Zoom, Office, Google Meet, etc.) |
| `recording` | string | Link to recording |
| `tags` | array | Tags for categorization |

## Meeting Type Values

| Type | When to Use |
|------|-------------|
| `team` | Internal team meetings |
| `client` | Client or customer meetings |
| `standup` | Daily standup or check-in |
| `1on1` | One-on-one meetings |
| `planning` | Planning sessions, sprint planning |
| `external` | External partner or vendor meetings |

## Tag Conventions

- Always include `meeting`
- Type tag matches meeting_type: `team`, `client`, `standup`, `1on1`, `planning`, `external`
- Additional tags: `weekly`, `daily`, `investor`, `customer`, `retrospective`

## Viewing Meetings

All meetings automatically appear in views defined in `Database/Meetings.base`:

- **Upcoming Meetings** - Scheduled meetings sorted by date
- **Recent Meetings** - Recently completed meetings
- **By Type** - Grouped by meeting type
- **By Project** - Grouped by project
- **By Company** - Grouped by company (external meetings)

## Meeting Management Best Practices

1. **Create in advance** - Set up meeting notes before the meeting with agenda
2. **Link attendees** - Always link to people in `Database/People/`
3. **Take live notes** - Document discussion in real-time during meeting
4. **Capture decisions** - Explicitly list all decisions made
5. **Convert action items to tasks** - Create task files for important action items and link them
6. **Add recordings** - Include link to recording in `recording` field
7. **Update status** - Mark as `completed` after meeting finishes
8. **Link to context** - Connect to related `project` or `company` for context

## Examples

### Team Meeting

```yaml
---
type: meeting
meeting_date: 2026-01-15 10:00
meeting_type: team
attendees:
  - "[[Database/People/Team-Member]]"
  - "[[Database/People/Team-Member-2]]"
  - "[[Database/People/Kevin-El-Sayed]]"
organizer: "[[Database/People/Team-Member]]"
project: "[[Database/Projects/AGI-Assistant]]"
status: completed
duration: 45 minutes
location: Zoom
recording: https://zoom.us/rec/share/xxxxx
tags:
  - meeting
  - team
  - weekly
---
```

### External Client Meeting

```yaml
---
type: meeting
meeting_date: 2026-01-16 14:00
meeting_type: client
attendees:
  - "[[Database/People/Team-Member]]"
  - "[[Database/People/Client-Contact]]"
organizer: "[[Database/People/Team-Member]]"
company: "[[Database/Companies/Client-Corp]]"
status: scheduled
duration: 60 minutes
location: Google Meet
tags:
  - meeting
  - client
  - external
---
```

### Daily Standup

```yaml
---
type: meeting
meeting_date: 2026-01-15 09:00
meeting_type: standup
attendees:
  - "[[Database/People/Team-Member]]"
  - "[[Database/People/Team-Member-2]]"
  - "[[Database/People/Kevin-El-Sayed]]"
organizer: "[[Database/People/Team-Member]]"
status: completed
duration: 15 minutes
location: Zoom
tags:
  - meeting
  - standup
  - daily
---
```

## Relationship to Other Documents

Meetings connect to multiple document types:

### To People (Attendees)
```yaml
attendees:
  - "[[Database/People/Team-Member]]"
  - "[[Database/People/Team-Member-2]]"
```

### To Projects
```yaml
project: "[[Database/Projects/AGI-Assistant]]"
```

### To Companies
```yaml
company: "[[Database/Companies/Client-Corp]]"
```

### To Tasks (Action Items)
In meeting body:
```markdown
## Action Items
- [ ] [[Database/Tasks/Follow-Up-Task]] - Assigned to [[Database/People/Team-Member-2]]
```

This creates a network where:
- Meetings show all related people, projects, and companies
- People can query all meetings they attended
- Projects can show all related meetings
- Companies can track interaction history through meetings
