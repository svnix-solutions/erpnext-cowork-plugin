---
name: client-workflow
description: >
  Manage the full ERPNext consulting engagement lifecycle: from discovery call through
  implementation to billing. Coordinates between Gmail (client communication), Teamwork.com
  (project management, time tracking, billing), and ERPNext (implementation).
  Triggers when: user mentions client engagement, proposal, approval, billing, SOW,
  implementation plan, or engagement phase transitions.
---

# Client Engagement Workflow

## Phase Model

### Phase 1: Discovery & Analysis
**Trigger:** New Gemini transcript arrives in Gmail
**Actions:**
1. Fetch and analyse transcript (use transcript-analysis skill)
2. Create Teamwork.com project for client (if new client)
3. Create milestone: "Discovery & Requirements"
4. Create task: "Analyse transcript" → mark complete
5. Create task: "Send counter-questions" → draft email
6. Log time spent on analysis

### Phase 2: Requirements Refinement
**Trigger:** Client responds to counter-questions
**Actions:**
1. Fetch client reply from Gmail
2. Update requirements matrix with new information
3. Resolve ambiguities, update the analysis document
4. If more questions needed → draft follow-up email, create task
5. If requirements clear → proceed to Phase 3
6. Log time

### Phase 3: Implementation Planning
**Trigger:** Requirements finalised
**Actions:**
1. Generate implementation plan from finalised requirements:
   - Break each requirement into atomic implementation tasks
   - Estimate hours per task (use complexity from analysis)
   - Identify dependencies between tasks
   - Group into logical milestones
   - Calculate total estimated hours and cost
2. Create Teamwork.com structure:
   - Milestone per logical group
   - Task per implementation item with time estimate
   - Subtasks for complex items
   - Tag tasks: `standard-config | custom-field | server-script | client-script | workflow | report | print-format | integration`
3. Generate client-facing proposal document:
   - Scope of work summary
   - Task breakdown with estimates
   - Timeline
   - Assumptions and exclusions
   - Hourly rate and total estimate
4. Create client-facing task list in Teamwork for visibility
5. Draft proposal email to client via Gmail
6. Create task: "Await client approval"
7. Log time

### Phase 4: Approval
**Trigger:** Client approves plan (via email or Teamwork)
**Actions:**
1. Check Gmail for approval email or Teamwork task completion
2. Update Teamwork milestone status
3. Create task: "Begin implementation"
4. Send confirmation email to client with start date
5. Log time

### Phase 5: Implementation
**Trigger:** Approved plan exists, implementation tasks in Teamwork
**Actions:**
For each task in the approved plan:
1. Pick next task from Teamwork (respect dependency order)
2. Start GIF recording
3. Implement on ERPNext (use erpnext-implementation skill)
4. Stop GIF recording, save with task reference
5. Log time to Teamwork task
6. Mark task complete
7. If task has client-visible output → attach GIF/screenshot to Teamwork task
8. Repeat until milestone complete

### Phase 6: Review & Handover
**Trigger:** All implementation tasks complete
**Actions:**
1. Compile work summary:
   - List of changes made with GIF recordings
   - Any deviations from original plan
   - Known limitations or future recommendations
2. Create handover document
3. Share via Teamwork and Gmail
4. Create task: "Client review and acceptance"
5. Log time

### Phase 7: Billing
**Trigger:** Client accepts deliverables
**Actions:**
1. Pull all time entries from Teamwork for the project
2. Calculate billable hours (exclude internal overhead if configured)
3. Generate billing summary:
   - Task-level breakdown with hours
   - Total billable hours × hourly rate
   - Milestone-level subtotals
4. Draft invoice email or update Teamwork billing
5. Create task: "Await payment"
6. Log time

## Client Communication Templates

### Counter-Questions Email
Subject: Follow-up questions from our {date} call — {project_name}
Tone: Professional, specific, shows domain expertise

### Proposal Email
Subject: ERPNext Implementation Proposal — {client_name}
Attach: Implementation plan document
Tone: Confident, clear scope boundaries

### Implementation Update
Subject: Progress Update — {milestone_name}
Include: Completed tasks, next steps, any blockers
Tone: Brief, status-oriented

### Handover Email
Subject: Implementation Complete — {project_name}
Attach: Work summary with recordings
Tone: Celebratory but professional, clear next steps
