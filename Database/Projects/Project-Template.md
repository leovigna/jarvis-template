---
type: project
status: planning
priority: medium
lead: "[[Database/People/Lead Name]]"
team:
  - "[[Database/People/Team Member 1]]"
  - "[[Database/People/Team Member 2]]"
start_date: YYYY-MM-DD
target_date: YYYY-MM-DD
budget:
total_tasks: 0
completed_tasks: 0
tags:
  - project
  - status/planning
---

# Project Name

## Overview

Brief description of the project and its goals.

## Objectives

- Primary objective 1
- Primary objective 2
- Primary objective 3

## Scope

### In Scope
- Feature/capability 1
- Feature/capability 2

### Out of Scope
- Explicitly not included items

## Key Milestones

- [ ] Milestone 1 - Date
- [ ] Milestone 2 - Date
- [ ] Milestone 3 - Date

## Success Criteria

How will we measure success?
- Metric 1
- Metric 2
- Metric 3

## Resources

### Team
- Lead: [[Database/People/Lead Name]]
- Team members listed in frontmatter

### Budget
- Total: $X
- Breakdown: ...

## Risks & Assumptions

### Risks
- Risk 1 and mitigation
- Risk 2 and mitigation

### Assumptions
- Assumption 1
- Assumption 2

## Related Tasks

```base
filters:
  and:
    - file.inFolder("Database/Tasks")
    - project == link(this.file)
views:
  - type: table
    name: Project Tasks
    groupBy:
      property: status
      direction: ASC
    order:
      - priority
      - due
```

## Notes

