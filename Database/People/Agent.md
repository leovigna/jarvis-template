---
type: person
role: AI Agent
tags:
  - agent
  - system
---

# Agent

## Overview

This is a special person entry representing AI agents (like Claude Code) that can be assigned tasks in the Database system.

## Usage

When agents create tasks autonomously or are assigned work, they can reference this person entry:

```yaml
assignee: "[[Database/People/Agent]]"
```

## Task Assignment

Tasks assigned to Agent typically represent:
- Automated background work
- Scheduled agent operations
- System maintenance tasks
- Research and analysis work performed by AI

## Notes

This is a system-level person entry to enable proper task tracking and accountability when agents perform work in the workspace.
