# ERPNext Cowork Plugin

A Claude Cowork/Code plugin for end-to-end ERPNext consulting workflows — from client discovery calls to implementation, recording, and billing.

## What It Does

| Phase | Action | Tools Used |
|-------|--------|------------|
| **Discovery** | Fetch Gemini transcript from Gmail, extract requirements | Gmail MCP |
| **Analysis** | Map requirements to ERPNext modules, generate counter-questions | Claude |
| **Planning** | Create implementation plan with time estimates | Claude + Teamwork MCP |
| **Approval** | Share plan with client, track approval | Gmail + Teamwork MCP |
| **Implementation** | Execute changes on ERPNext via browser automation | Browser + GIF recorder |
| **Recording** | Capture GIF of every change for client evidence | GIF creator |
| **Time Tracking** | Log hours to Teamwork tasks automatically | Teamwork MCP |
| **Billing** | Generate billing summary from logged hours | Teamwork MCP |
| **Communication** | Draft and send professional emails at every phase | Gmail MCP |

## Installation

```bash
# If published to a marketplace:
claude plugin marketplace add your-org/erpnext-cowork-plugin
claude plugin install erpnext-cowork@your-org

# Or install from local directory:
claude plugin marketplace add ./path-to-this-repo
claude plugin install erpnext-cowork@local
```

## Configuration

Edit `.claude/settings.local.json` with your details:
- Engineer name, email, title
- Billing rate and currency
- Teamwork.com credentials (or set env vars)
- Default Gmail search patterns

### Environment Variables for Teamwork
```bash
export TEAMWORK_DOMAIN="your-company"
export TEAMWORK_USERNAME="your-email@example.com"
export TEAMWORK_PASSWORD="your-api-token"
```

## Slash Commands

| Command | Description |
|---------|-------------|
| `/erpnext-cowork:analyse-transcript` | Fetch and analyse a client call transcript |
| `/erpnext-cowork:plan-implementation` | Generate implementation plan from requirements |
| `/erpnext-cowork:implement` | Execute approved tasks on ERPNext with GIF recording |
| `/erpnext-cowork:status` | Dashboard view of client engagement progress |
| `/erpnext-cowork:client-email` | Draft and send client communications |
| `/erpnext-cowork:work-summary` | Compile work evidence for client review |
| `/erpnext-cowork:bill-client` | Generate billing report from time entries |

## Typical Workflow

```
/erpnext-cowork:analyse-transcript "Acme Corp call Jan 15"
  → Fetches transcript, produces analysis with counter-questions

/erpnext-cowork:client-email "Acme Corp questions"
  → Drafts and sends counter-questions email

/erpnext-cowork:plan-implementation "Acme Corp"
  → Creates implementation plan, pushes to Teamwork

/erpnext-cowork:client-email "Acme Corp proposal"
  → Sends proposal for approval

/erpnext-cowork:implement "next"
  → Picks next approved task, implements on ERPNext, records GIF, logs time

/erpnext-cowork:status "Acme Corp"
  → Shows progress dashboard

/erpnext-cowork:work-summary "Acme Corp"
  → Compiles all recordings and work for client review

/erpnext-cowork:bill-client "Acme Corp"
  → Generates billing report and invoice email
```

## Connectors Required

- **Google Workspace** — Gmail for transcripts and client communication
- **Teamwork.com** — Project management, time tracking, CRM, billing
- **Atlassian** (optional) — For internal IDEV project tracking
- **Browser automation** — For ERPNext implementation (via Cowork)

## Skills (Auto-Triggered)

- **transcript-analysis** — Fires when transcripts are mentioned
- **erpnext-implementation** — Fires during ERPNext browser tasks
- **client-workflow** — Fires for engagement lifecycle decisions
- **teamwork-ops** — Fires for Teamwork.com operations

## Agents

- **researcher** — Read-only agent for analysis and requirement gathering
- **implementer** — Execution agent for ERPNext browser automation
