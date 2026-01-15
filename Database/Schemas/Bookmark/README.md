# Bookmark Data Model

Bookmarks for saving and organizing web content, articles, and resources in the `Database/Bookmarks/` folder.

## Location

`Database/Bookmarks/`

## Filename Convention

Descriptive name (e.g., `Claude-API-Documentation.md`, `youtube-eIoohUmYpGI.md` for videos)

## When to Create

- User requests to save a URL or web resource
- Saving articles, documentation, or blog posts for later reading
- Storing YouTube videos or other media content
- Building a reading list or research collection

## When to Update

- **Mark as read**: Set `saved: true` after reading/reviewing
- **Add rating**: Set `rating` field (1-5) after reviewing
- **Update access date**: Update `last_accessed` when revisiting
- **Add takeaways**: Fill in Key Takeaways section with notes
- **Categorization**: Update `category` or `tags` for better organization

## Frontmatter Schema

### Required Properties

| Property | Type | Description |
|----------|------|-------------|
| `type` | string | Must be `"bookmark"` |
| `url` | string | Full URL to the resource |
| `created` | date | Creation date (YYYY-MM-DD) |

### Optional Properties

| Property | Type | Description |
|----------|------|-------------|
| `category` | string | Category/topic (Research, Tools, Documentation, etc.) |
| `description` | string | Brief description of the content |
| `saved` | boolean | Has content been saved/read (true/false) |
| `rating` | number | 1-5 star rating after reviewing |
| `last_accessed` | date | Last accessed date (YYYY-MM-DD) |
| `tags` | array | Tags for categorization |

## Tag Conventions

- Always include `bookmark`
- Use `to-read` for unread bookmarks
- Use category tags like `docs`, `article`, `video`, `research`
- Use topic tags for subject matter

## Viewing Bookmarks

All bookmarks automatically appear in views defined in `Database/Bookmarks.base`:

- **All Bookmarks** - Complete list
- **By Category** - Grouped by category
- **By Rating** - Grouped by rating (highest first)
- **To Read** - Bookmarks with `saved: false`
- **Recently Added** - Sorted by creation date

## Bookmark Management Best Practices

1. **Mark as saved** - Update `saved: true` after reading
2. **Add ratings** - Rate content (1-5) for future reference
3. **Categorize consistently** - Use standard categories (Research, Tools, Documentation, etc.)
4. **Extract takeaways** - Always add key takeaways in the document body
5. **Link to projects** - Reference bookmarks in related projects or tasks
6. **Clean up regularly** - Remove outdated bookmarks or mark as archived
7. **Update access dates** - Keep `last_accessed` current for frequently referenced content

## Categories

Common categories to use:

- **Research** - Research papers, articles, studies
- **Tools** - Software tools, libraries, frameworks
- **Documentation** - Official docs, guides, tutorials
- **Blog** - Blog posts, opinion pieces
- **Video** - YouTube videos, recorded talks
- **Reference** - Quick reference materials, cheatsheets
- **Reading List** - Long-form content to read later

## Examples

### Article Bookmark

```yaml
---
type: bookmark
url: https://blog.example.com/ai-agents
category: Blog
tags:
  - bookmark
  - article
  - ai-agents
description: Deep dive into autonomous AI agent architectures
saved: true
rating: 5
created: 2026-01-15
last_accessed: 2026-01-15
---
```

### YouTube Video

```yaml
---
type: bookmark
url: https://youtu.be/eIoohUmYpGI
category: Video
tags:
  - bookmark
  - video
  - to-watch
description: Conference talk on MCP servers
saved: false
rating:
created: 2026-01-15
last_accessed:
---
```

### Documentation

```yaml
---
type: bookmark
url: https://docs.anthropic.com/claude
category: Documentation
tags:
  - bookmark
  - docs
  - reference
description: Claude API official documentation
saved: true
rating: 5
created: 2026-01-15
last_accessed: 2026-01-15
---
```

## Integration with YouTube Skill

The `/youtube` skill automatically creates bookmarks for YouTube videos:
- Extracts video ID from any YouTube URL format
- Fetches and saves transcript directly to the bookmark
- Sets appropriate frontmatter and formatting
- See `/youtube` skill for details
