---
name: erpnext-implementation
description: >
  Implement ERPNext customizations via browser automation. Covers: creating/modifying DocTypes
  and fields, writing Server Scripts and Client Scripts, configuring Workflows and permissions,
  building Reports and Print Formats, setting up integrations (WhatsApp, Email, Webhooks).
  Triggers when: user asks to implement, configure, customize, or set up anything on ERPNext,
  or when an approved implementation plan needs execution.
---

# ERPNext Implementation via Browser Automation

## Pre-Implementation Checklist
Before any browser automation on the client's ERPNext instance:
1. Confirm the approved plan exists (check Teamwork.com task or local plan file)
2. Verify ERPNext URL and access credentials are available
3. Start GIF recording for client deliverable (use gif_creator tool)
4. Note the starting time for Teamwork time entry

## Implementation Patterns

### DocType & Field Operations
Navigate to: `{site}/app/customize-form` or `{site}/app/doctype/{name}`

**Create Custom DocType:**
1. Navigate to `/app/doctype/new`
2. Set Module, Name, naming rule
3. Add fields using the field table
4. Set permissions tab
5. Save and verify

**Add Custom Field:**
1. Navigate to `/app/customize-form`
2. Select the target DocType
3. Scroll to field insertion point
4. Add field with correct type, label, options
5. Set properties: mandatory, hidden, depends_on, fetch_from
6. Save

**Field Types Reference:**
- Link → references another DocType
- Select → dropdown with `\n`-separated options
- Table → child table (needs child DocType)
- Small Text / Text Editor / Code → text variants
- Currency / Float / Int → numeric types
- Check → boolean
- Dynamic Link → link type determined by another field

### Server Scripts
Navigate to: `{site}/app/server-script/new`

**Types:**
- `Document Event` — before_save, after_insert, on_submit, etc.
- `API` — creates a whitelisted API endpoint
- `Permission Query` — dynamic permission conditions
- `Scheduled` — cron-based execution

**Template:**
```python
# Document Event: Validate
# DocType: Sales Invoice
if doc.grand_total > 100000:
    frappe.throw("Amount exceeds approval limit")
```

**Always:**
- Test the script after creation using a test document
- Screenshot the script and the successful test result
- Check Error Log after running (`/app/error-log`)

### Client Scripts
Navigate to: `{site}/app/client-script/new`

**Types:** Form Events (setup, refresh, validate, field-change triggers)

**Template:**
```javascript
frappe.ui.form.on('Sales Order', {
    refresh(frm) {
        // Add custom button
        frm.add_custom_button('Generate PO', () => {
            frappe.call({ method: '...', args: { name: frm.doc.name } });
        });
    },
    customer(frm) {
        // Field change handler
        if (frm.doc.customer) {
            frm.set_value('territory', 'Default');
        }
    }
});
```

### Workflow Configuration
Navigate to: `{site}/app/workflow/new`

1. Set Document Type
2. Define states with docstatus mapping:
   - Draft states → docstatus 0
   - Submitted → docstatus 1
   - Cancelled → docstatus 2
3. Add transitions: state → action → next_state + allowed role
4. Set "Is Active" checkbox
5. Test by creating a document and walking through transitions

### Print Formats
Navigate to: `{site}/app/print-format/new`

- Standard: Use Print Format Builder (drag-drop)
- Custom HTML/Jinja: Set format type to "Jinja" and write template
- Always test with Print Preview on a real document

### Integrations

**Email Integration:**
- Navigate to `/app/email-domain` and `/app/email-account`
- Configure IMAP/SMTP or Gmail OAuth
- Set up Email Alert at `/app/notification`

**WhatsApp (via Twilio or direct):**
- Create Notification with channel "WhatsApp"
- Or set up webhook-based integration via Server Script API type

**Webhooks (outgoing):**
- Navigate to `/app/webhook/new`
- Set DocType, event, target URL, headers
- Map fields to request body

**Webhooks (incoming):**
- Create Server Script of type "API"
- Parse `frappe.request.data`
- Process and create/update documents

### Reports
Navigate to: `{site}/app/query-report/new` or `{site}/app/report-builder`

**Script Report:**
1. Set Report Type = "Script Report"
2. Define columns in the report's Python file or script
3. Write the `execute()` function with filters and data query
4. Test with different filter combinations

## Post-Implementation
After each implementation step:
1. Stop GIF recording — save with descriptive name
2. Take a final screenshot of the completed configuration
3. Log time to Teamwork.com task
4. Update task status
5. Note any deviations from the plan
