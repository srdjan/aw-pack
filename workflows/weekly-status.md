---
description: Generate a weekly status report with actionable maintainer suggestions
on:
  schedule: weekly on monday
  workflow_dispatch: {}
engine: claude
timeout-minutes: 10
permissions:
  issues: read
  pull-requests: read
  contents: read
tools:
  github:
    toolsets: [issues, pull_requests, repos]
safe-outputs:
  create-issue:
    max: 1
---

# Weekly Status Report

Generate a comprehensive weekly status report for ${{ github.repository }}.

## Repository Context

{{#import shared/repo-context.md}}

## Data to Collect

Gather activity from the past 7 days:

1. **Issues**: List all issues opened, closed, and currently open. Note their labels and assignees.

2. **Pull Requests**: List all PRs opened, merged, and closed. Categorize each PR by the project's architectural components as described in the repository context above. If no architecture is documented, categorize by directory (e.g., src/, tests/, docs/, config/).

3. **Commits**: Summarize the commit activity on the main branch. Group by category (features, fixes, docs, refactors).

4. **Breaking Changes**: Flag any changes to public APIs, type definitions, serialization formats, database schemas, or CLI interfaces.

## Report Format

Create a GitHub issue with the title: `Weekly Status: [date range]`

Begin the issue body with: `*Automated weekly report by Repo Assist.*`

Use this structure:

```
## Summary

[2-3 sentence overview of the week's activity]

## Suggested Actions for Maintainer

- [ ] [Specific actionable item with issue/PR number]
- [ ] [Another action - review, merge, close, or respond]
- [ ] [Prioritized: security first, then stale items, then reviews]

## Issues

### Opened
[list with labels]

### Closed
[list with resolution summary]

### Needs Attention
[issues open >7 days without response, or with stale discussions]

## Pull Requests

### Merged
[list with component tags and brief description]

### Open
[list with status - ready for review, draft, needs changes, stale]

## Commit Activity

[grouped summary by category]

## Breaking Change Watch

[any changes to public APIs, type definitions, serialization formats, or schemas]

## Metrics

- Issues opened: X
- Issues closed: X
- PRs merged: X
- PRs open: X
- Commits to main: X
- Average issue age (open): X days
```

## Guidelines

- The "Suggested Actions" section is the most important part. Make each item specific and actionable with issue/PR numbers.
- If there was no activity in a section, write "No activity this week" rather than omitting the section.
- Keep the report concise. Maintainers should be able to scan it in under 2 minutes.
- Do not create a report if there is zero activity across all categories. Silence is better than an empty report.
