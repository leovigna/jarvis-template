# Document Data Model

Generic documents for free-form content that doesn't fit in the Database system. Documents are stored outside of `Database/` and have more flexible structures.

## Location

`Documents/` or appropriate subfolder (e.g., `Documents/AI-Ecosystem/`, `Documents/Research/`, `Documents/Product/`)

## Filename Convention

Descriptive name in title case (e.g., `Product-Requirements.md`, `System-Architecture.md`, `Market-Research.md`)

## When to Create

- Research notes and analysis
- Product requirement documents (PRDs)
- Design documents and architectural specs
- Knowledge base entries (tools, frameworks, companies)
- Long-form writing that doesn't fit Database models
- Documentation that needs flexible structure

## When to Update

- **Content changes**: When information is updated or expanded
- **Metadata changes**: Update `updatedAt` when making edits
- **Related documents**: Add cross-links when creating related content

## Common Frontmatter

All documents should include these base fields:

### Required Properties

| Property | Type | Description |
|----------|------|-------------|
| `createdAt` | date | Creation date (YYYY-MM-DD) |
| `updatedAt` | date | Last update date (YYYY-MM-DD) |
| `author` | wikilink or string | Document author (e.g., `[[Database/People/Team-Member]]` or `"Team Member"`) |

### Optional Properties

| Property | Type | Description |
|----------|------|-------------|
| `tags` | array | Tags for categorization |
| `status` | enum | `draft` \| `in-review` \| `published` \| `archived` |
| `type` | string | Document type (e.g., `research`, `prd`, `design-doc`) |

## Document Types

### Research Documents

For capturing research on tools, companies, frameworks, or topics.

**Location**: `Documents/AI-Ecosystem/[Category]/` or `Documents/Research/`

**Template**: See [template-research.md](template-research.md)

**Use when**:
- Documenting a new tool or framework
- Capturing competitive analysis
- Creating knowledge base entries
- Tracking industry research

### Product Requirements (PRD)

For defining product features and requirements.

**Location**: `Documents/Product/` or `Documents/PRDs/`

**Template**: See [template-prd.md](template-prd.md)

**Use when**:
- Planning new features
- Defining product scope
- Communicating requirements to team
- Creating specifications for development

## Cross-Linking

Documents should link to related content:
- Link to people: `[[Database/People/Team-Member]]`
- Link to projects: `[[Database/Projects/AGI-Assistant]]`
- Link to other documents: `[[Documents/Research/Related-Topic]]`
- Link to tasks: `[[Database/Tasks/Implementation-Task]]`

## Best Practices

1. **Always update `updatedAt`** - Change the date whenever you edit the document
2. **Use appropriate templates** - Choose the right template for your document type
3. **Add cross-links** - Link to related Database entries and other documents
4. **Include metadata** - Fill out frontmatter fields for better organization
5. **Use consistent structure** - Follow template patterns for similar document types
6. **Tag appropriately** - Use tags that help with discovery and filtering
