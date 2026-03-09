---
name: cs:renewal
description: Renewal tracking and preparation -- risk assessment, pricing, negotiation, status tracking
argument-hint: "<workspace-name> [customer-name]"
---
<objective>
Track and prepare for customer renewals. Show upcoming renewals, assess risk, review pricing, guide negotiation, and track status. Single customer deep-dive or portfolio renewal pipeline.

**HARD GATE: All contract changes require explicit approval.**

Workspace and optional customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/BENCHMARKS.md
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/playbooks.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // RENEWALS >>`
2. Parse workspace and optional customer from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, RENEWALS.md, HEALTH-SCORES.md, EXPANSION.md
4. Load playbooks for renewal process

## Portfolio renewal pipeline (no customer specified)
5. Display full renewal pipeline:
```
+----------------------------------------------------------+
|  RENEWAL PIPELINE -- {Workspace}                          |
+----------------------------------------------------------+

  This month ({n} renewals, ${total ARR})
    {Customer-1}   ${ARR}   Health: 85   Status: RENEWING     Low risk
    {Customer-2}   ${ARR}   Health: 62   Status: AT RISK      High risk
    {Customer-3}   ${ARR}   Health: 91   Status: EXPANDING    Upsell

  Next month ({n} renewals, ${total ARR})
    {Customer-4}   ${ARR}   Health: 78   Status: PENDING      Medium risk
    {Customer-5}   ${ARR}   Health: 45   Status: AT RISK      Critical

  This quarter ({n} renewals, ${total ARR})
    Renewing:      {n}   ${value}
    Expanding:     {n}   ${value}  (+${expansion})
    Contracting:   {n}   ${value}  (-${contraction})
    At risk:       {n}   ${value}
    Churned:       {n}   ${value}

  Forecast
    GRR forecast:  {pct}%  (target: {target}%)
    NRR forecast:  {pct}%  (target: {target}%)
    Revenue at risk: ${value}

----------------------------------------------------------
```

## Single customer renewal (customer specified)
6. Deep-dive on specific renewal:
```
+----------------------------------------------------------+
|  RENEWAL -- {Customer Name}                               |
+----------------------------------------------------------+

  Contract Details
    Current ARR:     ${value}
    Contract term:   {months} months
    Start date:      {date}
    Renewal date:    {date} ({n} days away)
    Auto-renew:      {yes/no}
    Payment status:  {current/overdue}

  Health Assessment
    Overall health:  {score}/100 ({status})
    Usage trend:     {up/down/flat}
    Engagement:      {high/medium/low}
    NPS:             {score}
    Support health:  {good/fair/poor}

  Renewal Risk Score: {LOW/MEDIUM/HIGH/CRITICAL}
```

## Risk assessment
7. Calculate renewal risk based on:
   - Health score (weighted heavily)
   - Usage trend (declining = high risk)
   - NPS score (detractor = high risk)
   - Support history (open escalations = risk)
   - Stakeholder stability (champion changes = risk)
   - Competitor signals (mentions = risk)
   - Payment history (delays = risk)

8. Assign renewal probability:
   - 90%+ = Low risk (healthy, engaged, expanding)
   - 70-89% = Medium risk (some concerns, needs attention)
   - 50-69% = High risk (multiple signals, active intervention needed)
   - <50% = Critical (likely to churn without major intervention)

## Renewal preparation
9. Build renewal preparation checklist:
```
  Renewal Prep Checklist
    [ ] Value summary prepared (ROI data, outcomes achieved)
    [ ] Stakeholder alignment confirmed (decision maker engaged)
    [ ] Health score reviewed (no unresolved red flags)
    [ ] Open support tickets resolved or escalated
    [ ] Pricing reviewed against market and usage
    [ ] Expansion opportunities identified
    [ ] Competitive positioning prepared
    [ ] Internal approval for pricing/terms obtained
    [ ] Renewal conversation scheduled with customer
```

## Pricing review
10. Review current pricing against:
    - Original contract terms
    - Usage growth (are they using more than contracted?)
    - Market rates (benchmark against similar customers)
    - Expansion opportunity (new seats, features, tiers)
    - Customer lifetime value
    - Strategic importance of account

## Renewal conversation guide
11. Provide talk track based on renewal status:

**Renewing (healthy, straightforward):**
- Lead with value summary
- Confirm continued alignment on success criteria
- Discuss growth opportunities
- Present renewal terms

**At risk (concerns exist):**
- Acknowledge known issues first
- Present resolution plan
- Show commitment to their success
- Discuss adjusted terms if needed
- Involve executive sponsor

**Expanding (opportunity to grow):**
- Lead with ROI data
- Present expansion business case
- Show what additional value looks like
- Propose expanded terms

## HARD GATE -- contract changes
12. Any contract modifications require explicit approval:
```
  ── APPROVAL REQUIRED ────────────────────────────────
  Contract change detected. This requires explicit approval.

  Change: {description of change}
  Impact: {financial impact}

  >> Approve  -- proceed with contract change
  >> Edit     -- modify the terms
  >> Reject   -- cancel the change
  ─────────────────────────────────────────────────────
```

13. In auto mode: STILL stop here -- contract changes are a hard gate

## Track and update
14. Update renewal status in RENEWALS.md:
    - Status: Renewing / Expanding / Contracting / Churning / Renewed / Churned
    - New ARR (if changed)
    - New term dates
    - Notes on negotiation

15. Update TIMELINE.md with renewal events
16. Update METRICS.md with GRR/NRR impact
17. Update LEARNINGS.md with renewal insights

18. Display:
```
  >> Next: /cs:check-in {ws} {customer} (post-renewal follow-up)
     Also: /cs:upsell {ws} {customer} (if expansion discussed)
     Also: /cs:qbr {ws} {customer} (schedule next QBR)
```
</process>
