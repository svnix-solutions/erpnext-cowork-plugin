---
description: Generate a billing summary for a client from Teamwork.com time entries. Calculates billable hours, creates task-level breakdown, and optionally drafts an invoice email.
---

# Bill Client

Generate a billing report from logged Teamwork.com time entries.

## Input
- $ARGUMENTS: client name or Teamwork project name/ID

## Steps

1. **Find project** in Teamwork by name or ID
2. **Pull all time entries** for the project
   - Filter by date range if specified
   - Filter billable = true
3. **Build billing table:**

```
| Milestone | Task | Hours | Rate | Amount |
|-----------|------|-------|------|--------|
| Discovery | Analyse transcript | 1.5 | $X | $Y |
| Implementation | Create DocType - Delivery | 3.0 | $X | $Y |
| ... | ... | ... | ... | ... |
| **TOTAL** | | **{sum}** | | **${total}** |
```

4. **Include summary:**
   - Total billable hours
   - Total amount
   - Date range covered
   - Number of tasks completed
   - Milestone completion status

5. **Generate deliverable:**
   - Save billing report as markdown file
   - Offer to create a DOCX/PDF invoice (if docx/pdf skill available)

6. **Draft invoice email** to client via Gmail with:
   - Summary of work completed
   - Billing table
   - Payment terms
   - Attached: detailed billing report + work recordings

7. **Update Teamwork:**
   - Create task "Invoice sent — awaiting payment"
   - Tag with billing milestone
