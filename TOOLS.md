---
summary: "Tool configurations"
read_when:
  - Every session start
---
# TOOLS.md - Local Notes

Skills define *how* tools work. This file is for *your* specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:
- Camera names and locations
- SSH hosts and aliases  
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras
- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH
- home-server → 192.168.1.100, user: admin

### TTS
- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

## Current Configuration

### TTS Voice (voice-reply skill)
- Preferred voice: "echo" (warm, conversational)
- Speed: 1.2 (slightly faster than normal)
- Model: gpt-4o-mini-tts (fast, cost-effective)

Available voice options: alloy, echo, fable, onyx, nova, shimmer

---

Add whatever helps you do your job. This is your cheat sheet.
