---
type: company
industry: Industry Name
stage: startup
size: 1-10
location: City, Country
website: https://example.com
linkedin: https://linkedin.com/company/name
twitter: https://twitter.com/company
relationship: prospect
last_interaction: 2026-01-15
next_action:
tags:
  - company
  - prospect
---

# Company Name

## Overview

Brief description of what the company does.

## Details

- **Industry**: [[industry]]
- **Stage**: [[stage]] (seed/series-a/series-b/public/etc)
- **Size**: [[size]] employees
- **Location**: [[location]]
- **Website**: [[website]]

## Relationship

Type: [[relationship]] (prospect/partner/client/vendor/investor/etc)
Context of relationship.

## Contacts

People we know at this company:

```base
filters:
  and:
    - file.inFolder("Database/People")
    - company == link(this.file)
views:
  - type: table
    name: Contacts
    order:
      - role
      - file.name
```

## Interaction History

### YYYY-MM-DD
Notes from meeting/interaction...

## Projects & Opportunities

Related projects or business opportunities.

## Notes

Additional context, competitive intel, etc.
