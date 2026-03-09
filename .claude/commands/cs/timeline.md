---
name: cs:timeline
description: Full customer journey timeline with all interactions and milestones
argument-hint: "<workspace> <customer-name>"
---
<objective>
Display the complete customer journey timeline. Show all interactions, milestones,
health score changes, support tickets, expansion events, and key contact changes.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // TIMELINE >>`
2. Load workspace context
3. Load customer record from customers/{customer-name}/
4. Load all related logs: health changes, tickets, check-ins, QBRs, escalations

## Phase 2: Gather timeline events

Collect all events from customer history:

1. **Contract events:** Signed, renewed, expanded, contracted, churned
2. **Onboarding milestones:** Kickoff, integration complete, first value, go-live, TTV achieved
3. **Check-ins:** Scheduled calls, ad-hoc meetings, async updates
4. **QBRs:** Quarterly business reviews with outcomes
5. **Support tickets:** Opened, escalated, resolved (with severity)
6. **Health score changes:** Significant moves (>10 points), triggers
7. **Expansion events:** Upsell conversations, proposals, closed
8. **Contact changes:** Champion added/left, exec sponsor change, new stakeholders
9. **Product adoption:** Feature activations, usage milestones, integration additions
10. **Advocacy:** Reference calls, case studies, reviews, referrals
11. **Escalations:** Opened, resolved, impact

## Phase 3: Display timeline

1. Sort all events chronologically (newest first by default)
2. Display interactive timeline:
```
  +-- CUSTOMER TIMELINE: {name} -------------------+
  |  ARR: ${value}  Health: {score}  Since: {date}  |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+

  {today}
  |
  | [HEALTH]  Score changed: 78 -> 72 (-6)
  |           Trigger: Usage decline detected
  |
  | [TICKET]  P2 — "API rate limiting issue"
  |           Status: Open — 2 days — Within SLA
  |
  {date - 7 days}
  |
  | [CHECK-IN] Monthly sync with {contact}
  |            Notes: Happy with new feature, asked about pricing
  |
  {date - 30 days}
  |
  | [QBR]     Q4 Review — Outcome: Positive
  |           Expansion discussed: +20 seats
  |           Action items: 3 open
  |
  {date - 45 days}
  |
  | [EXPANSION] Upsell closed: +$15K ARR
  |             New module: Analytics Pro
  |
  {date - 90 days}
  |
  | [CONTACT]  Champion departed: {name}
  |            New contact identified: {name}
  |
  ...
```

## Phase 4: Timeline analysis

1. Identify patterns in the timeline:
   - Engagement frequency trend (increasing/decreasing)
   - Ticket volume trend
   - Health score trajectory
   - Time between expansions
   - Stakeholder stability
2. Flag risks visible in the timeline:
   - Decreasing engagement cadence
   - Increasing ticket frequency
   - Champion loss without replacement
   - Long gap since last QBR
   - Health declining over 3+ data points
3. Flag opportunities visible in the timeline:
   - Consistent positive trajectory
   - Multiple expansion events
   - Active advocacy participation
   - High product adoption velocity

## Phase 5: Output and next steps

1. Offer timeline filters: `all | contracts | support | health | contacts | expansion`
2. Offer date range: `last-30 | last-90 | last-year | all-time`
3. Suggest next actions based on timeline analysis:
```
---------------------------------------------------

  >> Next: /cs:health {workspace} {customer}
     Also: /cs:check-in {workspace} {customer}

---------------------------------------------------
```

</process>
</output>
