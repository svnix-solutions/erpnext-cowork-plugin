---
description: Show current status of a client engagement — phase, task completion, hours logged, next actions. Pull from Teamwork.com project data.
---

# Engagement Status

Show a dashboard view of a client engagement.

## Input
- $ARGUMENTS: client name or Teamwork project name/ID. If empty, list active projects.

## Output

```
# {Client Name} — Engagement Status

## Current Phase: {phase}
## Progress: {completed}/{total} tasks ({percentage}%)

### Milestones
| Milestone | Status | Tasks | Hours Logged |
|-----------|--------|-------|--------------|
| Discovery | ✅ Complete | 3/3 | 2.5h |
| Planning | ✅ Complete | 2/2 | 3.0h |
| Implementation | 🔄 In Progress | 5/12 | 14.0h |
| Review | ⏳ Pending | 0/3 | 0h |

### Current Tasks (In Progress / Next Up)
1. 🔄 Configure Workflow — Purchase Order (est: 4h, logged: 1.5h)
2. ⏳ Write Server Script — Auto-numbering (est: 2h)
3. ⏳ Set up WhatsApp notification (est: 3h)

### Hours Summary
- Total estimated: 42h
- Total logged: 19.5h
- Remaining estimate: 22.5h
- Billable: 19.5h × $rate = $amount

### Blockers
- {any tasks with "blocked" status or comments}

### Last Client Communication
- {most recent email from/to client from Gmail}
```
