# ERPNext Module & DocType Quick Reference

## Core Modules → Common Customization Areas

### Accounts
- Sales Invoice, Purchase Invoice, Payment Entry, Journal Entry
- Chart of Accounts, Cost Centers, Budgets
- Common asks: custom invoice formats, auto-journal entries, approval workflows

### Stock / Inventory
- Stock Entry, Delivery Note, Purchase Receipt, Stock Reconciliation
- Warehouse, Item, Batch, Serial No
- Common asks: barcode scanning, batch tracking, auto-reorder

### Selling
- Quotation, Sales Order, Sales Invoice
- Customer, Territory, Sales Person
- Common asks: approval workflows, auto-pricing, margin calculations

### Buying
- Supplier Quotation, Purchase Order, Purchase Receipt
- Supplier, Item Supplier
- Common asks: LPO workflows, 3-way matching, supplier portals

### Manufacturing
- BOM, Work Order, Job Card, Production Plan
- Workstation, Operation, Routing
- Common asks: real-time production tracking, quality checkpoints

### HR & Payroll
- Employee, Attendance, Leave, Payroll Entry, Salary Slip
- Common asks: custom leave policies, overtime calculations, integration with biometrics

### Assets
- Asset, Asset Movement, Asset Maintenance
- Common asks: depreciation schedules, maintenance tracking

### Projects
- Project, Task, Timesheet, Activity Type
- Common asks: project billing, resource planning

### CRM
- Lead, Opportunity, Customer
- Common asks: lead scoring, pipeline dashboards

## Integration Points
- **Email**: Email Account, Notification, Email Template
- **WhatsApp**: via Notification channel or webhook
- **Webhooks**: Outgoing webhooks, incoming via Server Script API
- **REST API**: All DocTypes auto-expose REST endpoints
- **Payment Gateways**: Payment Request, Payment Gateway
- **GPS/IoT**: Custom DocTypes + Server Script APIs

## ERPNext URL Patterns
- DocType list: `/app/{doctype-name}` (e.g., `/app/sales-order`)
- New document: `/app/{doctype-name}/new`
- Specific document: `/app/{doctype-name}/{name}`
- Customize Form: `/app/customize-form?doc_type={DocType}`
- DocType definition: `/app/doctype/{DocType Name}`
- Report: `/app/query-report/{Report Name}`
- Print Format: `/app/print-format/{Name}`
- Server Script: `/app/server-script/{Name}`
- Workflow: `/app/workflow/{Name}`
