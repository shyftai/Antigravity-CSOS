---
name: cs:today
description: Daily CS briefing -- what needs your attention right now
argument-hint: "<workspace-name>"
---
<objective>
Morning briefing. Scan the workspace, surface what needs action today, and prioritize it. Built for CSMs who want to know "what do I do right now?"

Workspace: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/BENCHMARKS.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // TODAY >>`
2. Load full workspace context -- all files
3. Check current date for relevant timing context

## Scan everything
4. Scan and categorize actions by urgency:

**Urgent (do now):**
- At-risk customers with health score drop in last 24h -- investigate immediately
- Escalations with SLA breach approaching -- respond now
- NPS detractor submitted in last 48h -- follow up today
- Renewal due within 7 days with no renewal plan -- act immediately
- Customer stakeholder change detected -- champion left, re-engage
- Support ticket spike (3x normal volume) for a customer -- investigate

**Today (do before end of day):**
- Scheduled check-ins today -- prep with `/cs:check-in`
- QBR scheduled this week -- prep with `/cs:qbr`
- Onboarding milestones due today -- verify completion
- Open escalations awaiting your response
- Customers with declining usage (3 consecutive days)
- Expansion opportunities flagged as ready
- Renewals due within 30 days -- start renewal prep

**This week (plan for it):**
- Renewals due within 60 days -- begin conversations
- Customers due for check-in (last contact >cadence threshold)
- NPS survey batch scheduled this week
- Health scores trending down but not yet critical
- Onboarding customers approaching time-to-value target
- QBRs to schedule for next month
- Advocacy candidates to engage (promoters with no recent ask)

5. Display the daily briefing:
```
+----------------------------------------------------------+
|  TODAY -- {Workspace} -- {date}                           |
+----------------------------------------------------------+

  Do now
    !! {Customer} health dropped to RED (was Yellow) -- /cs:health {ws} {customer}
    !! Escalation SLA breach in 2h: {Customer} -- /cs:escalation {ws} {customer}
    !! NPS detractor: {Customer} scored 3 -- /cs:nps {ws} follow-up

  Today
    >> Check-in with {Customer} at 2pm -- /cs:check-in {ws} {customer}
    >> {Customer} onboarding milestone due: Go-live -- /cs:onboard-customer {ws} {customer}
    >> Renewal prep: {Customer} renews in 25 days -- /cs:renewal {ws} {customer}
    >> Expansion ready: {Customer} health 92, usage +40% -- /cs:upsell {ws} {customer}

  This week
    .. QBR prep: {Customer} scheduled Thursday -- /cs:qbr {ws} {customer}
    .. 3 customers due for check-in -- /cs:check-in {ws}
    .. NPS survey batch: 15 customers scheduled -- /cs:nps {ws} send
    .. {Customer} health trending down (85 -> 78) -- monitor

  Portfolio pulse
    {Customer-1}   Enterprise   Health: 92   Renews: 45d   OK
    {Customer-2}   Mid-Market   Health: 67   Renews: 12d   AT RISK
    {Customer-3}   SMB          Health: 45   Renews: 90d   CRITICAL

  Summary
    {total} customers | {green} healthy | {yellow} watch | {red} at-risk
    {n} renewals this quarter | ${value} at risk

  All clear?
    {If nothing urgent: "Portfolio is healthy. Focus on expansion and proactive check-ins."}

----------------------------------------------------------
```

6. Recommend the single most important action:
```
  >> Start here: /cs:health {ws} {customer}
```

7. If role is set in workspace.config.md, adjust emphasis:
   - **CSM**: emphasize at-risk customers, check-ins, renewals
   - **CS Lead/Manager**: emphasize team portfolio summary, escalations, metrics
   - **Head of CS**: top-level metrics, GRR/NRR trend, board-level concerns
   - **Founder**: keep it simple -- top 3 actions only
   - **CS Ops**: emphasize process gaps, automation opportunities, data quality
</process>
