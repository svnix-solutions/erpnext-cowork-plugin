---
description: Generate an ERPNext implementation plan from a requirements analysis. Creates task breakdown, time estimates, milestones, and a client-facing proposal. Optionally pushes to Teamwork.com.
---

# Plan Implementation

Generate a detailed ERPNext implementation plan from an existing requirements analysis.

## Input
- $ARGUMENTS: path to analysis file, or client name to search for existing analysis
- If no analysis found, prompt user to run `/erpnext-cowork:analyse-transcript` first

## Steps

1. **Load requirements analysis** from file or context

2. **Generate implementation tasks** for each requirement:
   - Map to specific ERPNext action (create DocType, add field, write script, etc.)
   - Estimate hours using complexity rating:
     - Simple (standard config): 0.5 - 2h
     - Medium (custom fields, basic scripts): 2 - 8h
     - Complex (workflows, integrations, reports): 8 - 20h
   - Identify dependencies between tasks
   - Tag each task with implementation type

3. **Group into milestones** by functional area or module

4. **Calculate totals:**
   - Hours per milestone
   - Total project hours
   - Estimated cost (ask for hourly rate if not configured)
   - Suggested timeline

5. **Generate two documents:**

   **Technical Plan** (internal — for the engineer):
   - Detailed task list with ERPNext specifics
   - Dependencies and execution order
   - Technical notes and gotchas

   **Client Proposal** (external — for approval):
   - Business-language task descriptions
   - Time and cost estimates
   - Scope boundaries (what's included/excluded)
   - Assumptions
   - Timeline

6. **Offer to push to Teamwork.com:**
   - Create project (if new)
   - Create milestones and task lists
   - Create tasks with estimates and tags
   - Create client-visible task list for approval

7. **Offer to send proposal via Gmail**
