---
name: teamwork-ops
description: >
  Manage Teamwork.com operations for ERPNext consulting: create projects, milestones, task lists,
  tasks with time estimates, log time entries, manage CRM contacts/companies, track billable hours,
  and generate client-facing task views. Triggers when: user mentions Teamwork, tasks, time tracking,
  billing, milestones, project setup, CRM, or billable hours.
---

# Teamwork.com Operations

## Project Setup for New Client
Use Teamwork MCP to create:

1. **Company** (CRM): Client company with contact details
2. **Project**: Named `{Client Name} — ERPNext Implementation`
   - Set project owner, start date
   - Enable time tracking, set default billable rate
3. **Milestones** (standard template):
   - Discovery & Requirements
   - Implementation Planning
   - Client Approval
   - Implementation — {Group 1}
   - Implementation — {Group 2} (as needed)
   - Review & Handover
   - Billing & Close
4. **Task Lists**: One per milestone, matching milestone name

## Task Creation Standards
Every task must include:
- Clear title: `{verb} {object} — {DocType/Module}` (e.g., "Create Custom DocType — Fuel Delivery Log")
- Description: What specifically will be done
- Time estimate in hours
- Tags: `standard-config`, `custom-field`, `server-script`, `client-script`, `workflow`, `report`, `print-format`, `integration`, `data-migration`
- Assigned to: the engineer
- Milestone association
- Priority: high / medium / low

**Subtask pattern** for complex tasks:
```
Task: Configure Sales Workflow — Sales Order (est: 4h)
  ├── Subtask: Define workflow states and transitions (1h)
  ├── Subtask: Set role-based permissions per state (1h)
  ├── Subtask: Write notification triggers (1h)
  └── Subtask: Test complete workflow cycle (1h)
```

## Time Logging
After every implementation action:
- Log time entry against the specific task
- Set billable = true (unless internal overhead)
- Include brief description of work done
- Format: `{action}: {detail}` (e.g., "Created: Custom DocType for Fuel Delivery with 12 fields")

## Client-Facing Task Lists
For approval workflows, create a separate task list visible to client:
- Title: "Proposed Scope — Awaiting Approval"
- Tasks mirror the implementation plan but in client-friendly language
- No technical jargon — business outcome focused
- Include time estimates as cost indicators
- Client can comment/approve on tasks

## Billing Report Generation
To generate a billing summary:
1. Query all time entries for the project (use Teamwork MCP)
2. Filter: billable = true, within date range
3. Group by milestone → task
4. Calculate: hours × billable rate
5. Format as table with subtotals per milestone
6. Include grand total

## CRM Operations
- Create/update company records for each client
- Associate contacts (from call participants)
- Link projects to companies
- Track engagement history via task completion
