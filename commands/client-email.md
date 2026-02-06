---
description: Draft a client email for any engagement phase — counter-questions, proposal, progress update, handover, or invoice. Uses Gmail MCP to send. Provide client name and email type.
---

# Client Email

Draft and optionally send a professional client email via Gmail.

## Input
- $ARGUMENTS: `{client-name} {email-type}`
- Email types: `questions` | `proposal` | `update` | `handover` | `invoice` | `custom`

## Behaviour per Type

**questions**: Draft counter-questions from the latest analysis. Attach analysis summary.
**proposal**: Draft implementation proposal. Attach plan document.
**update**: Pull latest completed tasks from Teamwork, summarize progress.
**handover**: Compile all deliverables, GIF recordings, and change summary.
**invoice**: Attach billing report, include payment terms.
**custom**: Ask user what to communicate, draft accordingly.

## Email Standards
- Subject line: Always include project/client name
- Professional but warm tone
- Clear call-to-action (approve, review, pay, schedule call)
- Brief — busy clients don't read long emails
- Bullet points for action items
- Always cc relevant stakeholders if known

## Workflow
1. Look up client email from Teamwork CRM or ask user
2. Gather relevant data (analysis, plan, tasks, time entries)
3. Draft email
4. Show draft to user for review
5. On approval, send via Gmail MCP
6. Log the communication as a Teamwork task/comment
