---
name: cs:qbr
description: QBR preparation and delivery -- metrics, deck outline, talking points, expansion recommendations
argument-hint: "<workspace-name> <customer-name>"
---
<objective>
Prepare and support delivery of a Quarterly Business Review for a customer. Pull metrics, create deck outline, define talking points, include health score, usage stats, ROI metrics, and expansion recommendations.

**HARD GATE: All customer-facing QBR materials require explicit approval before sharing.**

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/report-template.md
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/BENCHMARKS.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // QBR PREP >>`
2. Parse workspace and customer from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, HEALTH-SCORES.md, METRICS.md, TIMELINE.md, EXPANSION.md
4. Load report-template.md for QBR format
5. Run quality gates before proceeding

## Pre-QBR data collection
6. Gather all data for the review period (last quarter):

**Usage metrics:**
- Login frequency and trend
- Feature adoption (which features, how often)
- DAU/MAU ratio
- Key workflow completion rates
- Integration usage
- API call volume (if applicable)

**Support metrics:**
- Ticket volume and trend
- Average resolution time
- CSAT scores on tickets
- Open issues and their status
- Escalation history

**Business metrics:**
- ROI metrics (based on success criteria from kickoff)
- Time saved / efficiency gained
- Revenue impact (if measurable)
- Contract utilization (using what they're paying for?)

**Relationship metrics:**
- Meeting attendance rate
- Stakeholder engagement breadth
- NPS score and trend
- Feedback submitted

## QBR deck outline
7. Generate QBR structure:
```
+----------------------------------------------------------+
|  QBR OUTLINE -- {Customer Name} -- {Quarter}              |
+----------------------------------------------------------+

  SLIDE 1: Executive Summary
    - Relationship overview
    - Quarter highlights (top 3 wins)
    - Health score: {score} ({trend})
    - Key metric: {primary ROI metric}

  SLIDE 2: Usage & Adoption
    - Usage trend chart (quarterly view)
    - Feature adoption heatmap
    - Benchmark comparison vs similar customers
    - New features released this quarter

  SLIDE 3: Support & Service
    - Ticket volume and resolution metrics
    - CSAT trend
    - Notable resolved issues
    - Proactive improvements made

  SLIDE 4: Business Outcomes
    - ROI metrics aligned to success criteria
    - Value delivered this quarter
    - Customer-specific outcomes
    - Benchmarks vs industry

  SLIDE 5: Roadmap & Upcoming
    - Product roadmap highlights relevant to them
    - Planned improvements based on their feedback
    - Upcoming features they should know about

  SLIDE 6: Growth Opportunities
    - Expansion recommendations (if health GREEN)
    - Additional use cases for their team
    - Training opportunities
    - New features that unlock value

  SLIDE 7: Action Plan
    - Agreed next steps
    - Success criteria for next quarter
    - Meeting cadence adjustments
    - Owner assignments

----------------------------------------------------------
```

## Talking points
8. Generate talking points for each slide:
   - What to emphasize (wins, value delivered)
   - What to address proactively (known issues, gaps)
   - Questions to ask (discovery for expansion, satisfaction check)
   - Potential objections and responses

9. Flag sensitive topics:
   - Open escalations to address
   - Declining usage to explain
   - Missed milestones to acknowledge
   - Competitor mentions to handle

## Expansion recommendations
10. If health score >= 80:
    - Identify expansion signals (usage ceiling, team growth, new use cases)
    - Prepare expansion conversation framework
    - Include ROI projection for expanded usage
    - Suggest timing for expansion discussion

11. If health score < 80:
    - Focus QBR on value reinforcement and issue resolution
    - Do NOT include expansion slide
    - Add recovery plan to action items

## HARD GATE -- approval required
12. Display complete QBR package for review:
```
  ── APPROVAL REQUIRED ────────────────────────────────
  This is customer-facing material. Review before sharing.

  >> Approve  -- QBR deck is ready to present
  >> Edit     -- make changes (specify what)
  >> Reject   -- restart QBR prep with different approach
  ─────────────────────────────────────────────────────
```

13. Wait for explicit approval before finalizing
14. In auto mode: STILL stop here -- customer-facing materials are a hard gate

## Save and schedule
15. Save QBR document to context/qbrs/{customer-name}-{quarter}-{date}.md
16. Add QBR entry to TIMELINE.md
17. Update health score post-QBR (attendance and engagement)
18. Update LEARNINGS.md with QBR insights
19. Schedule next QBR based on segment cadence

20. Display:
```
  QBR prepared: context/qbrs/{file}

  >> Next: Present QBR to {customer}
     After: /cs:check-in {ws} {customer} (follow up on action items)
     Also:  /cs:upsell {ws} {customer} (if expansion discussed)
```
</process>
