# Company Data Model

Companies are tracked for CRM, partnerships, clients, vendors, and competitive intelligence in the `Database/Companies/` folder.

## Location

`Database/Companies/`

## Filename Convention

Company name (e.g., `Placeholder-Labs.md`, `Anthropic.md`)

## When to Create

- Adding a new company to track (client, partner, vendor, investor, prospect)
- Recording company information from meetings or conversations
- Building a CRM database of business relationships
- Tracking competitive intelligence

## When to Update

- **After interactions**: Add entry to Interaction History section with date
- **Relationship changes**: Update `relationship` field when status changes
- **Contact updates**: Update `last_interaction` date
- **Next actions**: Set `next_action` for follow-up items
- **Company changes**: Update `stage`, `size`, `industry` as company evolves
- **New contacts**: Create person entries and link via the Contacts query

## Frontmatter Schema

### Required Properties

| Property | Type | Description |
|----------|------|-------------|
| `type` | string | Must be `"company"` |
| `relationship` | enum | `prospect` \| `partner` \| `client` \| `vendor` \| `investor` \| `competitor` |

### Optional Properties

| Property | Type | Description |
|----------|------|-------------|
| `industry` | string | Industry category (AI, SaaS, etc.) |
| `stage` | enum | `seed` \| `series-a` \| `series-b` \| `series-c` \| `public` \| `startup` |
| `size` | string | Employee count range (1-10, 11-50, 51-200, 201-500, 500+) |
| `location` | string | City, Country or Region |
| `website` | string | Company website URL |
| `linkedin` | string | LinkedIn company page URL |
| `twitter` | string | Twitter/X handle URL |
| `last_interaction` | date | Last interaction date (YYYY-MM-DD) |
| `next_action` | string | Follow-up action needed |
| `tags` | array | Tags for categorization |

## Relationship Values

| Relationship | When to Use |
|--------------|-------------|
| `prospect` | Potential client or partner, early conversations |
| `partner` | Active partnership or collaboration |
| `client` | Paying customer or active client relationship |
| `vendor` | Company we purchase from or use services from |
| `investor` | Current or potential investor |
| `competitor` | Competitive intelligence tracking |

## Tag Conventions

- Always include `company`
- Relationship tag matches relationship: `prospect`, `partner`, `client`, `vendor`, `investor`, `competitor`
- Industry tags: `ai`, `saas`, `fintech`, etc.
- Status tags: `active`, `churned`, `pipeline`

## Viewing Companies

All companies automatically appear in views defined in `Database/Companies.base`:

- **All Companies** - Complete list
- **By Industry** - Grouped by industry
- **By Relationship** - Grouped by relationship type
- **By Stage** - Grouped by funding stage
- **Recent Interactions** - Sorted by `last_interaction` date

## CRM Best Practices

1. **Update after interactions** - Always add dated notes in Interaction History section
2. **Set last_interaction date** - Update `last_interaction` frontmatter after meetings/calls
3. **Track next actions** - Use `next_action` field for follow-up reminders
4. **Link contacts** - Create person entries in `Database/People/` and link via `company` field
5. **Use embedded queries** - Include Contacts Base query to see all people at the company
6. **Document context** - Record why the relationship matters and what's at stake
7. **Track opportunities** - Note potential projects, deals, or partnerships

## Examples

### Prospect Company

```yaml
---
type: company
industry: AI
stage: series-a
size: 11-50
location: San Francisco, CA
website: https://example.com
linkedin: https://linkedin.com/company/example
twitter: https://twitter.com/example
relationship: prospect
last_interaction: 2026-01-15
next_action: Send follow-up email about partnership
tags:
  - company
  - prospect
  - ai
---
```

### Client Company

```yaml
---
type: company
industry: Enterprise SaaS
stage: public
size: 500+
location: New York, NY
website: https://bigcorp.com
linkedin: https://linkedin.com/company/bigcorp
relationship: client
last_interaction: 2026-01-10
next_action: Quarterly business review scheduled for Q1
tags:
  - company
  - client
  - enterprise
  - active
---
```

### Investor

```yaml
---
type: company
industry: Venture Capital
stage: n/a
size: 11-50
location: Menlo Park, CA
website: https://vcfirm.com
linkedin: https://linkedin.com/company/vcfirm
relationship: investor
last_interaction: 2026-01-08
next_action: Monthly update call on Jan 30
tags:
  - company
  - investor
  - vc
---
```

## Relationship to People

Companies are connected to people via the `company` field in person frontmatter:

```yaml
# In person file: Database/People/John-Doe.md
company: "[[Database/Companies/Example-Corp]]"
```

This creates a bidirectional relationship where:
- People show which company they work for
- Companies can query and display all their contacts using Base queries
- Interaction history can reference both people and companies
