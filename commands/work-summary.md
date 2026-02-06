---
description: Compile a work summary with GIF recordings, screenshots, and task details for client review and approval. Used before handover or billing.
---

# Work Summary

Compile all recorded work for a client engagement into a reviewable deliverable.

## Input
- $ARGUMENTS: client name or project reference

## Steps

1. **Gather artifacts** from the working directory:
   - GIF recordings matching client name pattern
   - Screenshots
   - Analysis and plan documents
   - Any generated scripts or configurations

2. **Pull task data** from Teamwork:
   - All completed tasks with descriptions
   - Time entries per task
   - Comments and notes

3. **Generate summary document:**

```markdown
# Work Summary — {Client Name}
## Date Range: {start} to {end}

## Overview
- Tasks completed: {count}
- Total hours: {hours}
- Milestones delivered: {list}

## Detailed Work Log

### {Milestone 1}

#### {Task 1.1}: {Title}
- **Time**: {hours}h
- **What was done**: {description}
- **Recording**: [View GIF]({filename})
- **Notes**: {any deviations or observations}

#### {Task 1.2}: {Title}
...

## Recommendations for Future Work
{items identified during implementation but out of current scope}

## Sign-Off
Please review the above work summary and confirm acceptance.
Client approval required to proceed with invoicing.
```

4. **Save** as `{client}-work-summary-{date}.md`
5. **Offer to send** via Gmail or share in Teamwork
