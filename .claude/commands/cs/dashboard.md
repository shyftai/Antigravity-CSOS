---
name: cs:dashboard
description: Smart dashboard -- portfolio health, renewals, and what needs attention
argument-hint: "<workspace-name>"
---
<objective>
Analyze the full state of a CS workspace and surface what needs attention. Portfolio health distribution, renewal pipeline, at-risk customers, NPS trends, expansion pipeline, and support summary.

Workspace: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/BENCHMARKS.md
@./.claude/csos/references/defaults.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // DASHBOARD >>`
2. Load full workspace context -- all files
3. Scan and assess each area:

## Portfolio health distribution
4. Calculate health scores for all customers
5. Categorize into: Green (80+), Yellow (60-79), Red (<60)
6. Show distribution as visual chart:
```
+----------------------------------------------------------+
|  DASHBOARD -- {Workspace}                                 |
+----------------------------------------------------------+

  Portfolio Health
    Green (80+)     ████████████████  64%   (32 customers)
    Yellow (60-79)  ██████            24%   (12 customers)
    Red (<60)       ███               12%   (6 customers)

    Average health: {score}   Trend: {up/down/flat} vs last month
```

## Renewal pipeline
7. Show upcoming renewals by quarter:
```
  Renewal Pipeline
    This month    {n} renewals    ${value}    {risk assessment}
    Next month    {n} renewals    ${value}    {risk assessment}
    This quarter  {n} renewals    ${value}    {risk assessment}

    At-risk renewals: {n} worth ${value}
    Expansion in pipeline: {n} worth ${value}
```

## At-risk customers
8. List customers with health < 60 or active churn signals:
```
  At-Risk Customers ({n} total)
    !! {Customer-1}  Health: 42  Signal: Usage -60%      -- /cs:save {ws} {customer}
    !! {Customer-2}  Health: 55  Signal: Champion left    -- /cs:save {ws} {customer}
    !! {Customer-3}  Health: 38  Signal: Support spike    -- /cs:save {ws} {customer}
```

## NPS trend
9. Show NPS score over time:
```
  NPS Trend
    Current: {score}   Target: {target}   Trend: {direction}
    Promoters: {n} ({pct}%)   Passives: {n} ({pct}%)   Detractors: {n} ({pct}%)

    Last survey: {date}   Response rate: {pct}%
    Detractors needing follow-up: {n}
```

## Expansion pipeline
10. Show expansion opportunities:
```
  Expansion Pipeline
    Qualified:   {n} opportunities   ${value}
    In progress: {n} opportunities   ${value}
    Closed:      {n} this quarter    ${value}

    NRR: {pct}%   Target: {target}%
```

## Support summary
11. Show support ticket overview:
```
  Support Summary
    Open tickets: {n}   Avg resolution: {hours}h
    Escalations:  {n} active

    Customers with ticket spikes:
      {Customer-1}: {n} tickets this week (normal: {n})
```

## Context-aware alerts
12. Display alerts based on what needs attention:
```
  Needs attention
    !! 6 at-risk customers need save plans -- /cs:at-risk {ws}
    !! 3 renewals due in <30 days with no prep -- /cs:renewal {ws}
    !! 2 NPS detractors with no follow-up -- /cs:nps {ws} follow-up
    !! Onboarding customer past TTV target -- /cs:onboard-customer {ws} {customer}

  Looking good
    [x] No SLA breaches
    [x] NRR on track (108%)
    [x] Onboarding pipeline healthy
    [x] No executive escalations

  Key metrics
    GRR: {pct}%  (target: {target}%)    {status}
    NRR: {pct}%  (target: {target}%)    {status}
    NPS: {score} (target: {target})      {status}
    Avg health: {score}                  {status}

----------------------------------------------------------

  >> Recommended: /cs:at-risk {ws}
     Also: /cs:renewal {ws}

----------------------------------------------------------
```

13. Prioritize the "Recommended" action by urgency:
    - At-risk customers > renewal deadlines > escalations > NPS detractors > expansion > everything else
    - If nothing needs attention: "Portfolio healthy. Focus on expansion opportunities and proactive check-ins."

14. If learnings data reveals patterns worth surfacing, add a suggestion block:
```
  +-- INSIGHT -----------------------------------------+
  | Based on 8 churned customers this year:             |
  | Customers who skip Month 2 check-in churn at 3x    |
  | the rate of those who attend.                       |
  |                                                     |
  | 4 customers have not had Month 2 check-in.          |
  | >> Schedule these now? (y/n)                        |
  +----------------------------------------------------+
```
</process>
