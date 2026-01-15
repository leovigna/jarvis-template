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

# Full Name

## Role & Background

Current role and background information.

## Contact Information

- Email: [[email]]
- LinkedIn: [[linkedin]]
- Twitter: [[twitter]]
- Location: [[location]]
- Company: [[company]]

## Relationship

Type: [[relationship]]
How we know each other, context of relationship.

## Interaction History

### YYYY-MM-DD
Notes from meeting/interaction...

## Tasks & Projects

Related tasks or projects involving this person.

```base
filters:
  and:
    - file.inFolder("Database/Tasks")
    - assignee == link(this.file)
views:
  - type: table
    name: Tasks
    order:
      - status
      - priority
```

## Notes

Additional context, interests, preferences, etc.
