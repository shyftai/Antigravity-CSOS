---
name: cs:segments
description: Customer segmentation engine with service level management
argument-hint: "<workspace> [action]"
---
<objective>
Define, update, and analyze customer segments. Set service levels per segment, analyze
segment health, and identify segment-level trends and anomalies.

Workspace and action: $ARGUMENTS

Available actions:
- `view` — Show current segmentation and health (default)
- `define` — Create or update segment definitions
- `analyze` — Deep segment health analysis with trends
- `rebalance` — Re-evaluate customer segment assignments
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/sla-tiers.md
@./.claude/csos/references/BENCHMARKS.md
</execution_context>

<process>

## Action: view (default)

1. Display mode header: `<< CS:OS // SEGMENTS >>`
2. Load SEGMENTS.md from workspace
3. Display segment overview:
```
  +-- SEGMENT OVERVIEW ----------------------------+
  |                                                 |
  |  Strategic    {N} customers   ${ARR}   Health: {avg}  |
  |  Enterprise   {N} customers   ${ARR}   Health: {avg}  |
  |  Mid-market   {N} customers   ${ARR}   Health: {avg}  |
  |  SMB          {N} customers   ${ARR}   Health: {avg}  |
  |                                                 |
  |  Total:       {N} customers   ${total ARR}      |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```
4. Show service level summary per segment (touch cadence, QBR frequency, CSM ratio)
5. Flag segments with declining average health

## Action: define

1. Display mode header: `<< CS:OS // SEGMENT DEFINITION >>`
2. Show current segment criteria or defaults:
   - Strategic: ARR > $500K or executive-sponsored
   - Enterprise: ARR $100K-$500K
   - Mid-market: ARR $25K-$100K
   - SMB: ARR < $25K
3. Allow custom segment criteria (ARR thresholds, industry, use case, etc.)
4. Define service levels per segment:
   - Touch cadence (weekly/biweekly/monthly/quarterly)
   - QBR frequency (monthly/quarterly/biannual)
   - CSM ratio (1:5 / 1:15 / 1:30 / 1:50+tech-touch)
   - Response SLA (1h / 4h / 8h / 24h)
   - Onboarding type (white-glove / guided / self-serve)
5. Save to SEGMENTS.md
6. Log changes in logs/decisions.md

## Action: analyze

1. Display mode header: `<< CS:OS // SEGMENT ANALYSIS >>`
2. For each segment, calculate:
   - Average health score and distribution
   - NRR (net revenue retention) for segment
   - Churn rate (logo and revenue)
   - Average TTV (time to value)
   - Expansion rate
   - Support ticket volume per customer
   - NPS distribution
3. Compare against BENCHMARKS.md
4. Identify segment-level trends:
   - Health score trend (30/60/90 day)
   - Churn acceleration or deceleration
   - Expansion pipeline by segment
5. Flag anomalies:
   - SMB customer behaving like Enterprise (upgrade candidate)
   - Enterprise customer with SMB-level engagement (risk)
   - Segment with disproportionate support load
6. Display analysis with actionable recommendations

## Action: rebalance

1. Display mode header: `<< CS:OS // SEGMENT REBALANCE >>`
2. Re-evaluate each customer against current segment criteria
3. Identify customers that should move segments:
   - ARR growth crossed threshold
   - Usage patterns changed
   - Strategic importance shifted
4. Show proposed changes:
```
  PROPOSED SEGMENT CHANGES:
  {Customer} — Mid-market -> Enterprise (ARR grew to $120K)
  {Customer} — Enterprise -> Strategic (exec sponsor added)
  {Customer} — SMB -> Mid-market (ARR grew to $30K)

  >> Apply changes? (y/n)
```
5. On approval, update customer records and adjust service levels
6. Log in logs/decisions.md

</process>
</output>
