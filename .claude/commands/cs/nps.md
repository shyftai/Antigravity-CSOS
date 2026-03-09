---
name: cs:nps
description: NPS survey management -- schedule, track, follow up detractors, activate promoters
argument-hint: "<workspace-name> [action]"
---
<objective>
Manage NPS surveys end-to-end. Schedule survey batches, track scores, follow up with detractors (priority), activate promoters for advocacy, and show NPS trends.

Actions: send | results | follow-up | trend | promoters

Workspace and optional action: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/BENCHMARKS.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // NPS >>`
2. Parse workspace and optional action from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, NPS.md, HEALTH-SCORES.md, SEGMENTS.md
4. If no action specified, show NPS overview dashboard

## NPS overview dashboard (default)
5. Display current NPS state:
```
+----------------------------------------------------------+
|  NPS -- {Workspace}                                       |
+----------------------------------------------------------+

  Current NPS: {score}    Target: {target}    Status: {on/off track}

  Distribution
    Promoters (9-10):   ████████████████  {pct}%   ({n} customers)
    Passives (7-8):     ████████          {pct}%   ({n} customers)
    Detractors (0-6):   ███               {pct}%   ({n} customers)

  Trend (last 4 quarters)
    Q1: {score}    Q2: {score}    Q3: {score}    Q4: {score}
    Direction: {improving / declining / stable}

  Segment breakdown
    Enterprise:   NPS {score}   ({n} responses)
    Mid-Market:   NPS {score}   ({n} responses)
    SMB:          NPS {score}   ({n} responses)

  Action needed
    !! {n} detractors with no follow-up -- /cs:nps {ws} follow-up
    >> {n} promoters available for advocacy -- /cs:nps {ws} promoters
    .. Next survey batch: {date} ({n} customers)

----------------------------------------------------------
```

## Send surveys (action: send)
6. Prepare survey batch:
   - Select customers due for NPS survey (based on cadence from defaults)
   - Exclude: customers surveyed within cooldown period
   - Exclude: customers with active escalations (bad timing)
   - Exclude: customers in first 30 days of onboarding (too early)
   - Exclude: customers with renewal in <14 days (sensitive timing)

7. Display batch for review:
```
  Survey Batch -- {date}
    {n} customers selected

    Sending to:
      {Customer-1}   {Segment}   Last survey: {date}   Health: {score}
      {Customer-2}   {Segment}   Last survey: {date}   Health: {score}
      {Customer-3}   {Segment}   Last survey: {date}   Health: {score}

    Excluded:
      {Customer-A}   Reason: Active escalation
      {Customer-B}   Reason: Surveyed 45 days ago (cooldown: 90)
      {Customer-C}   Reason: Onboarding (Day 22)

    >> Send batch? (y/n)
```

8. Record survey send in NPS.md and TIMELINE.md

## View results (action: results)
9. Display recent survey results:
```
  Recent Results (last 30 days)
    {Customer-1}   Score: 9   Promoter    "{verbatim feedback}"
    {Customer-2}   Score: 4   Detractor   "{verbatim feedback}"
    {Customer-3}   Score: 8   Passive     "{verbatim feedback}"

    Response rate: {pct}% ({n} of {total})
    Batch NPS: {score}
```

## Follow up with detractors (action: follow-up) -- PRIORITY
10. List all detractors needing follow-up:
```
  Detractor Follow-up Queue
    !! {Customer-1}   Score: 3   "{feedback}"
       Health: {score}   ARR: ${value}   Renewal: {date}
       Suggested action: {based on feedback and health}

    !! {Customer-2}   Score: 5   "{feedback}"
       Health: {score}   ARR: ${value}   Renewal: {date}
       Suggested action: {based on feedback and health}
```

11. For each detractor, prepare follow-up approach:
    - Acknowledge their feedback specifically (reference their words)
    - Show what you're doing about their concern
    - Schedule a call within 48 hours
    - Assign owner for resolution
    - Set follow-up cadence until resolved

12. Generate follow-up email template:
    - Personal, not templated feel
    - Reference their specific feedback
    - Propose concrete next step
    - Include CSM direct contact info

## Activate promoters (action: promoters)
13. List promoters available for advocacy:
```
  Promoter Activation
    {Customer-1}   Score: 10   Last ask: {date or "never"}
       Potential: Case study, referral, review
    {Customer-2}   Score: 9    Last ask: {date or "never"}
       Potential: Reference call, testimonial

    Activation ideas:
      - Request G2/Capterra review
      - Invite to case study interview
      - Ask for referral introduction
      - Invite to customer advisory board
      - Feature in customer spotlight
```

14. Track advocacy asks to avoid over-asking:
    - Max 1 ask per quarter per promoter
    - Rotate ask types
    - Always deliver value before asking

## Trend analysis (action: trend)
15. Display NPS trend analysis:
```
  NPS Trend Analysis
    12-month trend:  {monthly scores}
    Segment trends:  {per-segment direction}
    Correlation:     NPS vs churn rate, NPS vs expansion rate

    Insights:
      - {Pattern 1: e.g., "Detractors who receive follow-up within 48h improve to Passive 60% of the time"}
      - {Pattern 2: e.g., "Enterprise NPS 15pts higher than SMB -- investigate SMB experience"}
```

## Save and update
16. Update NPS.md with all new data
17. Update HEALTH-SCORES.md (NPS affects health score)
18. Update TIMELINE.md with NPS events
19. Update LEARNINGS.md if patterns detected
20. If Slack connected: alert for new detractors

21. Display:
```
  >> Next: /cs:nps {ws} follow-up (detractors first)
     Also: /cs:health {ws} (update health scores)
     Also: /cs:nps {ws} promoters (activate advocates)
```
</process>
