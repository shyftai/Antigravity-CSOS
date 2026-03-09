---
name: cs:report
description: Generate CS reports — customer, portfolio, board-level, or churn analysis
argument-hint: "<workspace> [report-type] [customer-name]"
---
<objective>
Generate CS reports. Types: individual customer report, portfolio report, board-level summary,
churn analysis. Load report templates and format for the target audience.
HARD GATE on customer-facing reports.

Workspace, report type, and customer: $ARGUMENTS

Report types:
- `customer` — Individual customer health and engagement report
- `portfolio` — Full portfolio overview for CS leadership
- `board` — Board-level CS summary with key metrics
- `churn` — Churn analysis with root causes and trends
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/report-template.md
@./.claude/csos/references/BENCHMARKS.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // REPORT >>`
2. Load workspace context and customer data
3. Determine report type (default: portfolio)
4. Load report-template.md for formatting
5. Load BENCHMARKS.md for comparison data

## Phase 2: Generate report by type

### Customer report (requires customer-name)
1. Load full customer record, timeline, health history
2. Generate sections:
   - Customer overview (ARR, segment, contract dates, key contacts)
   - Health score with trend and component breakdown
   - Recent interactions (last 90 days)
   - Support ticket summary
   - Product adoption and usage metrics
   - Expansion history and pipeline
   - Risk factors and mitigation actions
   - Success milestones achieved
   - Upcoming: renewal date, scheduled QBR, planned actions

### Portfolio report
1. Load all customer records
2. Generate sections:
   - Portfolio summary (total customers, ARR, avg health)
   - Segment breakdown with health by segment
   - At-risk customers (health < 60) with action plans
   - Expansion pipeline and forecast
   - Churn/contraction this period
   - Upcoming renewals (next 90 days) with health status
   - CSM workload distribution
   - Top wins and saves this period
   - Key action items

### Board report
1. Aggregate portfolio-level metrics
2. Generate sections:
   - Executive summary (1 paragraph)
   - Key metrics table: NRR, GRR, NPS, logo churn, revenue churn
   - Benchmark comparison
   - Quarter-over-quarter trend
   - Notable wins (new logos, expansions, advocacy)
   - Notable losses (churn, contraction) with root causes
   - Strategic initiatives and progress
   - Forecast: next quarter outlook
   - Resource needs

### Churn analysis
1. Load all churned customers from period
2. Generate sections:
   - Churn summary (logos, ARR, rate)
   - Root cause distribution (product, price, service, fit, champion loss, acquired)
   - Churn by segment, tenure, CSM
   - Leading indicators (health score trend before churn)
   - Preventability assessment (preventable vs unpreventable)
   - Patterns and themes
   - Recommendations for churn reduction

## Phase 3: HARD GATE — Customer-facing reports

**If report type is `customer` and intended for external sharing:**
```
  !! HARD GATE — CUSTOMER-FACING REPORT !!

  This report will be shared with: {customer name}

  Checklist:
  [ ] No internal-only metrics exposed
  [ ] No other customer names visible
  [ ] No internal commentary or risk flags
  [ ] Formatting is clean and professional
  [ ] All data points are accurate and current

  >> Approve for external sharing? (y/n)
  >> Type APPROVE to confirm.
```

Do NOT finalize customer-facing reports without explicit confirmation.

## Phase 4: Format and save

1. Format report using report-template.md standards
2. Strip all internal references and CS:OS-specific language
3. Save to reports/{type}-{date}.md (or reports/{customer}-{date}.md)
4. Display completion:
```
---------------------------------------------------

  Report saved to reports/{filename}.md

  >> Next: /cs:metrics {workspace}
     Also: /cs:debrief {workspace} {customer}

---------------------------------------------------
```

</process>
</output>
