---
type: task
status: backlog
priority: high
assignee: "[[Database/People/Me]]"
project: "[[Database/Projects/Onboarding]]"
created: 2026-01-15
due: 2026-01-15
tags:
  - task
  - status/backlog
  - onboarding
---

# Collect User Name

## Description

Ask the user for their full name to personalize the workspace and create their profile in the Database/People folder.

## Context

This is the first step in the onboarding process. The user's name will be used throughout the workspace for task assignments, project tracking, and personalization.

## Acceptance Criteria

- [ ] Prompt user for their full name
- [ ] Validate that a name was provided (required field)
- [ ] Store name for use in creating user profile
- [ ] Confirm name with user before proceeding

## Dependencies

- This task should be completed first
- Blocks: [[Database/Tasks/Collect-User-Email]]
- Related to: [[Database/Projects/Onboarding]]

## Notes

The name will be used to create a person profile at `Database/People/[Name].md` and will be the default assignee for tasks.

## Updates

### 2026-01-15
Task created as part of onboarding project setup.
