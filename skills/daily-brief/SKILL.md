---
name: daily-brief
description: Generate a daily briefing from tasks and notes
---

# Daily Brief Skill

When the user invokes `/daily-brief`, generate a concise daily briefing.

## What to Include

1. **Date & Greeting**: Start with today's date and a brief greeting
2. **Active Tasks**: List tasks with status "in-progress" or "todo" from Database/Tasks
3. **Upcoming Meetings**: Check Database/Meetings for today's meetings (if any)
4. **Recent Activity**: Summarize any recent bookmarks or documents from past 24-48 hours
5. **Priorities**: Highlight urgent or high-priority items

## How to Execute

1. Read relevant files from Database/Tasks directory
2. Check Database/Meetings for today's date
3. Scan Database/Bookmarks for recent additions (last modified date)
4. Synthesize into a brief, scannable summary

## Response Format

```
🌅 DAILY BRIEF - [Date]

📋 ACTIVE TASKS ([count])
• [Task 1] - [status]
• [Task 2] - [status]
• [Task 3] - [status]

📅 TODAY'S MEETINGS ([count])
• [Time] - [Meeting name]

🔖 RECENT ACTIVITY
• [Activity 1]
• [Activity 2]

⚡ PRIORITIES
• [Priority item 1]
• [Priority item 2]
```

## Tone

- Professional and concise
- Actionable information only
- No fluff or filler
- Jarvis signature efficiency

## Error Handling

If directories are empty or inaccessible:
- Acknowledge it briefly
- Offer to help create structure
- Don't make excuses
