---
name: cs:health
description: Run health check on a customer or full portfolio -- scores, trends, actions
argument-hint: "<workspace-name> [customer-name]"
---
<objective>
Run a health check on a specific customer or the entire portfolio. Calculate scores across all dimensions, show trends, flag deterioration, and suggest actions.

Workspace and optional customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/BENCHMARKS.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/churn-signals.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // HEALTH CHECK >>`
2. Parse workspace and optional customer from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, HEALTH-SCORES.md, SEGMENTS.md, METRICS.md
4. Load health-scoring.md for scoring model
5. Load churn-signals.md for risk indicators

## Determine scope
6. If customer specified: run single-customer deep health check
7. If no customer: run portfolio-wide health scan

## Single customer health check
8. Calculate health score across all dimensions from health-scoring.md:

```
+----------------------------------------------------------+
|  HEALTH CHECK -- {Customer Name}                          |
+----------------------------------------------------------+

  Overall Health: {score}/100    Status: {GREEN/YELLOW/RED}
  Trend: {up/down/flat} ({change} pts since last check)
  Last check: {date}

  ── Dimension Scores ──────────────────────────────────
  Product Usage      {score}  ████████████████    {status}
    Login frequency:      {value} ({benchmark comparison})
    Feature adoption:     {value} ({benchmark comparison})
    DAU/MAU ratio:        {value} ({benchmark comparison})

  Engagement          {score}  ██████████████      {status}
    Meeting attendance:   {value}
    Email responsiveness: {value}
    Champion activity:    {value}
    Stakeholder depth:    {value}

  Support             {score}  ████████████        {status}
    Ticket volume:        {value} (trend: {direction})
    Avg resolution time:  {value}
    CSAT on tickets:      {value}
    Escalation history:   {value}

  Business            {score}  ██████████████████  {status}
    Contract value trend: {value}
    Payment status:       {value}
    Expansion history:    {value}
    Renewal likelihood:   {value}

  Relationship        {score}  ████████████████    {status}
    NPS score:            {value}
    Executive alignment:  {value}
    Multi-threading:      {value}
    Last QBR:             {value}

----------------------------------------------------------
```

## Trend analysis
9. Show health score history if multiple data points exist:
```
  Health Trend (last 6 months)
    Jan: 85  Feb: 82  Mar: 78  Apr: 75  May: 71  Jun: 68
                                                   vvv
    Warning: 4-month decline detected (-17 pts)
```

## Churn signal scan
10. Cross-reference churn-signals.md against customer data:
    - Usage decline (>20% drop)
    - Champion departure
    - Support ticket spike
    - Missed meetings (2+ consecutive)
    - Contract downgrade inquiry
    - Competitor mentions in tickets
    - Billing disputes
    - Reduced stakeholder engagement

11. For each signal detected:
```
  Active Churn Signals
    !! Usage declined 35% in 30 days         Severity: HIGH
    !! Champion {name} left the company       Severity: CRITICAL
    .. Support tickets up 2x this month       Severity: MEDIUM
```

## Action recommendations
12. Based on health score and signals, recommend specific actions:
    - RED (<60): Immediate save plan -- `/cs:save {ws} {customer}`
    - YELLOW (60-79): Proactive outreach -- `/cs:check-in {ws} {customer}`
    - GREEN (80+): Maintain and explore expansion -- `/cs:upsell {ws} {customer}`

13. Generate specific action items:
```
  Recommended Actions
    1. Schedule executive alignment call (champion left)
    2. Run product training refresh (usage declining)
    3. Review open support tickets with customer
    4. Prepare early renewal conversation (6 months out)
```

## Portfolio health check (no customer specified)
14. Run health scores for all customers:
```
  Portfolio Health Summary
    Total customers: {n}    Total ARR: ${value}

    GREEN (80+)     {n} customers    ${ARR}    {pct}% of portfolio
    YELLOW (60-79)  {n} customers    ${ARR}    {pct}% of portfolio
    RED (<60)       {n} customers    ${ARR}    {pct}% of portfolio

  Biggest movers (last 30 days)
    {Customer-1}   85 -> 92  (+7)   Reason: completed onboarding
    {Customer-2}   72 -> 58  (-14)  Reason: usage decline
    {Customer-3}   90 -> 82  (-8)   Reason: champion changed roles

  Attention required
    !! {Customer-A}  Health: 42  ${ARR}  -- /cs:save {ws} {customer}
    !! {Customer-B}  Health: 55  ${ARR}  -- /cs:at-risk {ws}
```

## Save results
15. Update HEALTH-SCORES.md with new scores and timestamps
16. Add health check entry to TIMELINE.md
17. Update LEARNINGS.md if patterns detected
18. Save detailed report to context/health/{customer-name or portfolio}-{date}.md

19. Display next steps:
```
  >> Next: /cs:at-risk {ws}
     Also: /cs:save {ws} {customer}
     Also: /cs:check-in {ws} {customer}
```
</process>
