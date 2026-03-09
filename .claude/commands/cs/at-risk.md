---
name: cs:at-risk
description: Detect at-risk customers -- churn signals, risk scoring, save play recommendations
argument-hint: "<workspace-name>"
---
<objective>
Scan all customers for churn risk indicators. Score and prioritize at-risk accounts. Recommend appropriate save plays from playbooks.

Workspace: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/churn-signals.md
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/playbooks.md
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/BENCHMARKS.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // AT-RISK DETECTION >>`
2. Load workspace context -- CUSTOMERS.md, HEALTH-SCORES.md, SEGMENTS.md, PLAYBOOKS.md
3. Load churn-signals.md for signal definitions and weights

## Full portfolio scan
4. For each customer, check all churn signal categories:

**Usage signals:**
- Login frequency decline (>30% drop over 30 days)
- Feature adoption regression (stopped using previously active features)
- DAU/MAU ratio below segment threshold
- API call volume declining
- Key workflow abandonment

**Engagement signals:**
- Missed 2+ consecutive check-ins
- Email response time increasing
- QBR declined or postponed
- Reduced stakeholder participation in meetings
- No product feedback in 90+ days

**Relationship signals:**
- Champion left the company
- Executive sponsor changed
- Key stakeholder unresponsive for 30+ days
- New decision maker not yet engaged
- Contract owner changed

**Support signals:**
- Ticket volume spike (3x normal)
- Repeat issues on same topic
- Escalation filed in last 30 days
- CSAT scores declining
- Unresolved critical ticket >SLA

**Business signals:**
- Requested contract review before renewal
- Asked about data export or migration
- Mentioned competitors in communications
- Payment delays or disputes
- Budget cuts announced
- Downsized team using the product

**NPS signals:**
- Detractor score (0-6)
- Score dropped 3+ points since last survey
- Passive trending toward detractor

## Risk scoring
5. For each customer with 1+ signals, calculate risk score:
   - Weight signals by severity (from churn-signals.md)
   - Factor in ARR (higher ARR = higher priority)
   - Factor in renewal proximity (closer renewal = higher urgency)
   - Factor in segment (enterprise churn is costlier)

6. Display at-risk report:
```
+----------------------------------------------------------+
|  AT-RISK CUSTOMERS -- {Workspace}                         |
+----------------------------------------------------------+

  {n} customers flagged | ${total ARR} at risk

  ── CRITICAL (act today) ──────────────────────────────
  1. {Customer}    Health: 35    ARR: ${value}    Renews: {date}
     Signals: Champion left, usage -55%, escalation open
     Save play: Executive re-engagement (playbooks.md)
     >> /cs:save {ws} {customer}

  2. {Customer}    Health: 42    ARR: ${value}    Renews: {date}
     Signals: Competitor mentioned, QBR declined, NPS detractor
     Save play: Value reinforcement + executive call
     >> /cs:save {ws} {customer}

  ── HIGH (act this week) ──────────────────────────────
  3. {Customer}    Health: 58    ARR: ${value}    Renews: {date}
     Signals: Usage declining, missed 2 check-ins
     Save play: Proactive outreach + product training
     >> /cs:check-in {ws} {customer}

  ── WATCH (monitor closely) ───────────────────────────
  4. {Customer}    Health: 68    ARR: ${value}    Renews: {date}
     Signals: Stakeholder change, support tickets up
     Save play: Relationship rebuilding
     >> /cs:health {ws} {customer}

----------------------------------------------------------
```

## Prioritization matrix
7. Show prioritized action list:
```
  Priority Actions
    1. {Customer} -- call executive sponsor TODAY (${ARR} at risk)
    2. {Customer} -- schedule emergency QBR this week
    3. {Customer} -- send value summary before renewal conversation
    4. {Customer} -- schedule re-engagement check-in
    5. {Customer} -- monitor for 2 more weeks, then reassess
```

## Trend analysis
8. Compare current at-risk list to previous scan:
   - New additions to at-risk list
   - Customers who improved (moved off at-risk)
   - Customers who worsened (moved up in severity)

9. Show portfolio risk trend:
```
  Risk Trend (last 3 months)
    At-risk count:  12 -> 10 -> 8    Improving
    ARR at risk:    ${value} -> ${value} -> ${value}
    Save rate:      {pct}% (benchmark: {pct}%)
```

## Save and alert
10. Update HEALTH-SCORES.md with risk flags
11. Add at-risk entries to TIMELINE.md
12. If team mode: sync to Supabase escalation queue
13. If Slack connected: send alert for CRITICAL customers

14. Display next steps:
```
  >> Start here: /cs:save {ws} {most critical customer}
     Also: /cs:health {ws} (full portfolio health check)
     Also: /cs:renewal {ws} (review renewal pipeline)
```
</process>
