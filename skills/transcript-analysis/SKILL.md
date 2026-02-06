---
name: transcript-analysis
description: >
  Analyse Google Meet / Gemini transcripts from client discovery calls for ERPNext consulting.
  Triggers when: user mentions transcript, call notes, meeting notes, client call, discovery call,
  requirement gathering, or pastes/references a Gemini transcript from Gmail.
  Extracts business requirements, pain points, current workflows, and generates counter-questions.
---

# Transcript Analysis for ERPNext Consulting

## Workflow

### 1. Fetch Transcript
Use Google Workspace MCP to search Gmail for the transcript:
- Search: `from:meet-recordings-noreply@google.com` or `subject:transcript` filtered by client name/date
- Also check Google Drive for shared transcript docs
- If not found via MCP, ask user to paste or provide the email subject/sender

### 2. Parse & Structure
Extract from the raw transcript:

**Business Context**
- Company name, industry, size, current systems
- Who attended (roles, decision-makers vs operators)
- Budget signals, timeline expectations

**Requirements Matrix** — for each requirement found:
- Category: `workflow | report | integration | automation | compliance | data-migration`
- Priority signalled by client: `must-have | nice-to-have | future`
- ERPNext module mapping: which DocType/module addresses this
- Complexity estimate: `simple (< 2h) | medium (2-8h) | complex (> 8h)`
- Standard vs Custom: can ERPNext handle this out-of-box or needs customization?

**Pain Points**
- Current process bottlenecks mentioned
- Manual steps they want automated
- Compliance/audit gaps

**Assumptions & Ambiguities**
- Things the client assumed Claude/you already know
- Contradictions between speakers
- Vague requirements that need clarification

### 3. Generate Counter-Questions
For each ambiguity or incomplete requirement, draft a specific counter-question:
- Frame questions around ERPNext capabilities to guide the client
- Group by module/workflow area
- Prioritize questions that block implementation planning
- Include "did you mean X or Y?" style questions where possible

### 4. Output Format
Produce a structured analysis document:
```
# Client Discovery Analysis — {Client Name} — {Date}

## Executive Summary
{2-3 sentence overview}

## Requirements Matrix
| # | Requirement | Category | Priority | ERPNext Module | Complexity | Standard/Custom |
|---|-------------|----------|----------|----------------|------------|-----------------|

## Pain Points & Current Workflow Gaps
{bullet list}

## Counter-Questions for Client
{numbered list grouped by area}

## Assumptions Made
{bullet list}

## Recommended Next Steps
{action items}
```

### 5. Save & Share
- Save analysis as a file in the working directory
- Offer to create a Teamwork.com task for the follow-up call
- Offer to draft a Gmail reply to the client with counter-questions
