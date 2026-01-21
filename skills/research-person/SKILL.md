---
name: research-person
description: Research a person online and update Database/People

---

# Research Person Skill

When invoked with `/research-person [name or email]`, research the person online and create or update their Database/People entry.

## Execution Process

### 1. Check for Duplicates FIRST
Read Database/People/ and match by priority:
- Email address (highest priority)
- LinkedIn URL
- Full name (case-insensitive)
- Name variations (e.g., "John Smith" vs "J. Smith")

If fuzzy match found, ask user to confirm. If multiple matches, show differentiators (company, role, email) and let user decide.

### 2. Research Online
Use web search to find:
- LinkedIn, Twitter/X profiles
- Current company and role
- Location and contact info
- Professional background and achievements
- Recent news or notable projects

Focus on publicly available professional information only.

### 3. Create or Update File

**If updating existing entry:**
- Read current file
- Merge new information with existing data
- Preserve user-added notes, interaction history, custom tags, relationship info
- Add update note with date

**If creating new entry:**
- Generate filename: "First-Last.md"
- Use Person-Template.md format

**File structure:**
```markdown
---
type: person
company: "[[Database/Companies/Company Name]]"
role: Job Title
email: email@example.com
linkedin: https://linkedin.com/in/username
twitter: https://twitter.com/username
location: City, Country
relationship: contact
last_contact: YYYY-MM-DD
next_action:
tags:
  - person
  - contact
---

# Full Name

## Role & Background
Current role and background information.

## Contact Information
- Email: [email]
- LinkedIn: [linkedin]
- Twitter: [twitter]
- Location: [location]

## Relationship
Type: contact
[Context about how/why added to database]

## Professional Background
[Career summary, expertise, achievements]

## Notes
[Additional context, interests, relevant information]

---
*Research Date: [current date]*
*Sources: [list sources]*
```

## Response Format

**New Entry:**
```
✅ Research completed for [Person Name]
📍 New profile: Database/People/[Filename].md

Key Info:
• Role: [Job Title] at [Company]
• Location: [Location]
• LinkedIn: [Yes/No]

Summary: [2-3 sentence summary]
Sources: [N] reviewed
```

**Updated Entry:**
```
✅ Research completed for [Person Name]
📍 Updated: Database/People/[Filename].md

Updates:
• [What changed]
• [What changed]

Sources: [N] reviewed
```

## Best Practices

- Always check duplicates before creating files
- Verify information from multiple sources
- Clearly indicate uncertain/unavailable information
- Only include publicly available information
- Add research date and sources for reference
- When updating, document what changed and when
- If minimal info found, save what you have
- If name ambiguous, ask for clarification
- If email domain suggests company, infer affiliation
- Preserve all user-added content when updating

## Tone

Professional, factual, organized, efficient.
