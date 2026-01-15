---
type: project
status: active
priority: high
lead: "[[Database/People/Me]]"
team: []
start_date: 2026-01-15
target_date: 2026-01-15
total_tasks: 3
completed_tasks: 0
tags:
  - project
  - status/active
  - onboarding
---

# Onboarding

## Overview

Gather essential information from new users to personalize their workspace and set up CRM integration.

## Objectives

- Collect user's name for personalization
- Optionally collect email address for communication
- Gather company information (ideally website) for CRM enrichment
- Use Firecrawl to automatically gather additional company data
- Create initial CRM entries with enriched data

## Scope

### In Scope
- User name collection (required)
- Email address collection (optional)
- Company name/website collection
- Automated company data enrichment via Firecrawl
- CRM entry creation

### Out of Scope
- Advanced user preferences
- Team setup
- Integration with external tools beyond Firecrawl

## Key Milestones

- [x] Create Onboarding project
- [ ] Create tasks for user data collection
- [ ] Implement Firecrawl integration for company data
- [ ] Test onboarding flow

## Success Criteria

- User provides required information (name)
- Company data is successfully enriched via Firecrawl
- CRM entries are created with complete information
- User has a personalized workspace setup

## Resources

### Team
- Lead: User

## Related Tasks

```base
filters:
  and:
    - file.inFolder("Database/Tasks")
    - project == link(this.file)
views:
  - type: table
    name: Onboarding Tasks
    groupBy:
      property: status
      direction: ASC
    order:
      - priority
      - due
```

## Notes

This project helps new users get started with the workspace by collecting essential information and setting up their CRM system automatically.
