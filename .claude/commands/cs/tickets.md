---
name: cs:tickets
description: Support ticket triage and management with SLA tracking
argument-hint: "<workspace> [customer-name]"
---
<objective>
Triage and manage support tickets. Classify by severity and type, check SLA compliance,
identify patterns, flag escalations, and update health score impact.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/sla-tiers.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // TICKET TRIAGE >>`
2. Load workspace context and customer portfolio
3. If customer-name provided, filter to that customer only
4. Pull open tickets from connected support tool (Zendesk, Intercom, Freshdesk, etc.)

## Phase 2: Classify tickets

For each open ticket:
1. Classify severity: P0 (Critical/Outage), P1 (High/Degraded), P2 (Medium/Workaround exists), P3 (Low/Question)
2. Classify type: Bug, Feature Request, How-to, Account Issue, Integration, Billing, Security
3. Tag with customer segment (Enterprise/Mid-market/SMB/Strategic)
4. Check if ticket is from a key contact or executive sponsor

## Phase 3: SLA check

1. Load SLA tiers from sla-tiers.md
2. For each ticket, calculate:
   - Time since creation
   - Time since last response
   - SLA target for this severity + segment
   - SLA status: [x] Within SLA, [!] At risk (>75% elapsed), [!!] Breached
3. Display SLA dashboard:
```
  +-  TICKET SLA STATUS  ---------------------+
  |                                            |
  |  Total open:    {N}                        |
  |  Within SLA:    {N}  (green)               |
  |  At risk:       {N}  (yellow)              |
  |  Breached:      {N}  (red)                 |
  |                                            |
  +--------------------------------------------+
```

## Phase 4: Pattern detection

1. Check for repeat tickets from same customer (3+ in 30 days = pattern)
2. Check for same issue across multiple customers (systemic issue)
3. Check for ticket volume spikes vs trailing 30-day average
4. Flag customers with open tickets AND upcoming renewal (within 90 days)
5. Display patterns found:
```
  PATTERNS DETECTED:
  [!] {Customer} — 5 tickets in 14 days (integration issues)
  [!] 3 customers reporting {same issue} — possible systemic bug
  [!] {Customer} — open P1 + renewal in 42 days
```

## Phase 5: Escalation flags

1. Auto-flag for escalation if:
   - P0 ticket open > 1 hour
   - P1 ticket open > 4 hours
   - SLA breached on Enterprise/Strategic customer
   - Executive sponsor submitted ticket
   - Customer health score already below 60
2. For flagged tickets, suggest: `/cs:escalation {workspace} {customer}`

## Phase 6: Health score impact

1. Calculate ticket impact on health score:
   - Open P0/P1: -15 points
   - SLA breach: -10 points
   - 3+ tickets in 30 days: -5 points
   - Resolved within SLA: +2 points (recovery)
2. Update customer health records
3. Log changes in logs/health-changes.md

## Phase 7: Triage output

1. Display prioritized ticket queue (sorted by: SLA urgency, severity, customer tier)
2. For each ticket show: ID, customer, severity, type, age, SLA status, recommended action
3. Suggest next actions:
```
---------------------------------------------------

  >> Next: /cs:escalation {workspace} {customer}
     Also: /cs:timeline {workspace} {customer}

---------------------------------------------------
```

</process>
</output>
