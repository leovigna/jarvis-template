---
type: task
status: backlog
priority: high
assignee: "[[Database/People/Me]]"
project: "[[Database/Projects/Onboarding]]"
created: 2026-01-15
due: 2026-01-15
blocked_by:
  - "[[Database/Tasks/Collect-User-Email]]"
tags:
  - task
  - status/backlog
  - onboarding
  - automation
---

# Collect Company Information with Firecrawl Integration

## Description

Ask the user for their company name and ideally their company website. Use Firecrawl to automatically gather additional company information and enrich the CRM entry.

## Context

Company information is essential for CRM setup. By collecting the company website, we can use Firecrawl to automatically gather:
- Company description
- Industry/sector
- Company size
- Social media links (LinkedIn, Twitter)
- Additional public information

This automates CRM data entry and ensures comprehensive company profiles.

## Acceptance Criteria

- [ ] Prompt user for company name (required)
- [ ] Prompt user for company website URL (optional but recommended)
- [ ] If website provided, use Firecrawl to scrape company information
- [ ] Extract relevant data: description, industry, size, social links
- [ ] Create company entry in Database/Companies with enriched data
- [ ] Link user's profile to the company
- [ ] Handle cases where website is not provided or Firecrawl fails gracefully

## Dependencies

- Blocked by: [[Database/Tasks/Collect-User-Email]]
- Related to: [[Database/Projects/Onboarding]]

## Notes

Use the `mcp__firecrawl__firecrawl_scrape` tool to fetch company website data. Extract structured information using appropriate prompts. Create a well-formatted company profile in Database/Companies following the Company schema.

Key information to extract:
- Company overview/description
- Industry or sector
- Company size (if available)
- LinkedIn company page
- Twitter/X handle
- Other relevant public information

## Updates

### 2026-01-15
Task created as part of onboarding project setup with Firecrawl integration requirement.
