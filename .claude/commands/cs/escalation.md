---
name: cs:escalation
description: Escalation management with SLA tracking and leadership briefing
argument-hint: "<workspace> <customer-name>"
---
<objective>
Manage customer escalations. Classify severity, identify escalation path, prepare leadership
briefing, track resolution, and update health score. HARD GATE on escalations to leadership.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/sla-tiers.md
@./.claude/csos/references/escalation-paths.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // ESCALATION >>`
2. Load workspace context and customer record
3. Load customer health score, open tickets, recent interactions
4. Load escalation-paths.md for routing rules
5. Load SLA tiers for this customer's segment

## Phase 2: Classify escalation

1. Determine escalation level:
   - Level 1: CSM → Senior CSM (feature gap, minor dissatisfaction)
   - Level 2: Senior CSM → CS Manager (repeated issues, SLA breach)
   - Level 3: CS Manager → VP CS (churn risk, executive complaint)
   - Level 4: VP CS → C-suite (strategic account at risk, legal/security)
2. Classify root cause: Product issue, Service failure, Expectation mismatch, Relationship breakdown, Billing dispute, Security incident
3. Calculate escalation urgency based on:
   - Customer ARR and segment
   - Contract renewal proximity
   - Current health score
   - Number of prior escalations
   - Stakeholder seniority of complainant

## Phase 3: Build escalation brief

Assemble structured briefing:
```
  +-- ESCALATION BRIEF ----------------------------+
  |                                                 |
  |  Customer:     {name}                           |
  |  ARR:          {value}        Segment: {tier}   |
  |  Health:       {score}/100    Trend: {dir}      |
  |  Renewal:      {date} ({days} days)             |
  |  Level:        {1-4}                            |
  |  Root cause:   {classification}                 |
  |                                                 |
  |  TIMELINE:                                      |
  |  {date} — {event that triggered escalation}     |
  |  {date} — {prior relevant interaction}          |
  |  {date} — {prior relevant interaction}          |
  |                                                 |
  |  IMPACT:                                        |
  |  {what is broken/at risk for the customer}      |
  |                                                 |
  |  ACTIONS TAKEN:                                 |
  |  {what CSM has already tried}                   |
  |                                                 |
  |  RECOMMENDED RESOLUTION:                        |
  |  {specific proposed fix with timeline}          |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 4: HARD GATE — Leadership escalation

**If Level 3 or 4:**
```
  !! HARD GATE — LEADERSHIP ESCALATION !!

  This escalation will be routed to: {name, title}
  Customer ARR at risk: {value}

  Escalation brief preview:
  {summary}

  >> Approve escalation to leadership? (y/n)
  >> Type ESCALATE to confirm.
```

Do NOT proceed without explicit typed confirmation. Log gate interaction.

## Phase 5: Route escalation

1. Identify the right person at each level (from escalation-paths.md)
2. Prepare communication:
   - Internal Slack alert (if team mode): channel, urgency tag, brief
   - Email draft to escalation owner with full brief
   - Calendar hold suggestion for escalation call
3. Set escalation SLA:
   - Level 1: Acknowledge in 4 hours, resolve in 48 hours
   - Level 2: Acknowledge in 2 hours, resolve in 24 hours
   - Level 3: Acknowledge in 1 hour, resolve in 8 hours
   - Level 4: Acknowledge in 30 minutes, resolve in 4 hours

## Phase 6: Track and follow up

1. Create escalation record in logs/escalations.md:
   - Date, customer, level, root cause, owner, SLA targets
2. Update customer health score (escalation penalty: -10 to -25 based on level)
3. Set follow-up reminders
4. Display next actions:
```
---------------------------------------------------

  Escalation logged. Owner: {name}
  SLA: Acknowledge by {time}, resolve by {time}

  >> Next: /cs:timeline {workspace} {customer}
     Also: /cs:tickets {workspace} {customer}

---------------------------------------------------
```

</process>
</output>
