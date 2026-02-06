---
description: Execute an approved implementation task on ERPNext via browser automation. Records GIF, logs time to Teamwork.com. Provide task reference or pick from Teamwork task list.
---

# Implement on ERPNext

Execute approved implementation tasks on a client's ERPNext instance via browser automation.

## Input
- $ARGUMENTS: Teamwork task ID, task name, or "next" to pick the next unstarted task

## Pre-Flight
1. **Verify approval**: Check that the implementation plan has been approved
   - Look for approval flag in Teamwork milestone status
   - Or ask user to confirm approval
2. **Get ERPNext URL**: Ask for site URL if not already known in this session
3. **Get task details**: Fetch from Teamwork or local plan file

## Execution Loop
For each task:

1. **Announce**: State what will be implemented and the expected outcome
2. **Start timer**: Note start time for Teamwork time entry
3. **Start GIF recording**: Begin capturing browser actions
4. **Navigate to ERPNext**: Open the appropriate page for the task type:
   - DocType work → `/app/doctype/` or `/app/customize-form`
   - Server Script → `/app/server-script/new`
   - Client Script → `/app/client-script/new`
   - Workflow → `/app/workflow/new`
   - Report → `/app/query-report/new`
   - Print Format → `/app/print-format/new`
   - Integration → `/app/webhook/new` or `/app/notification/new`
5. **Implement**: Follow the erpnext-implementation skill patterns
6. **Verify**: Test the implementation (create test record, trigger workflow, etc.)
7. **Screenshot**: Capture the final result
8. **Stop GIF recording**: Save as `{client}-{task-ref}-{date}.gif`
9. **Log time to Teamwork**: With description of work done
10. **Mark task complete** in Teamwork
11. **Report**: Summarize what was done, any deviations, issues found

## Error Handling
- If ERPNext throws an error, screenshot it, log the issue
- Create a "blocked" comment on the Teamwork task
- Suggest fix or ask user for guidance
- Do NOT proceed to next task until resolved

## Post-Implementation
After all tasks in a milestone are complete:
- Offer to compile work summary with all GIFs
- Offer to send progress update email to client
- Offer to move to next milestone
