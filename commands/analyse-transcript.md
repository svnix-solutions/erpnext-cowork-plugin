---
description: Fetch a client call transcript from Gmail, analyse it, extract requirements, and generate counter-questions. Provide client name or email subject to search.
---

# Analyse Client Transcript

Fetch and analyse a client discovery call transcript for ERPNext consulting.

## Steps

1. **Fetch transcript from Gmail** using Google Workspace MCP:
   - Search by: client name, email subject, date, or sender `meet-recordings-noreply@google.com`
   - If $ARGUMENTS provided, use as search query
   - If multiple results, show list and ask user to pick
   - If no results found, ask user to paste the transcript directly

2. **Analyse using transcript-analysis skill** — extract:
   - Business context and attendees
   - Requirements matrix with ERPNext module mapping
   - Pain points and current workflow gaps
   - Ambiguities and assumptions

3. **Generate counter-questions** for each ambiguity

4. **Save analysis** to `{client-name}-discovery-{date}.md`

5. **Offer next actions:**
   - Draft counter-questions email to client
   - Create Teamwork.com project and initial tasks
   - Proceed directly to implementation planning (if requirements are clear)
