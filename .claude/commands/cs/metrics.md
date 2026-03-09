---
name: cs:metrics
description: CS metrics dashboard with benchmarks and trend analysis
argument-hint: "<workspace>"
---
<objective>
Display comprehensive CS metrics dashboard. Show NRR, GRR, NPS, CSAT, TTV, expansion rate,
churn rates, health distribution, and CSM workload. Compare against industry benchmarks.

Workspace: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/BENCHMARKS.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // METRICS >>`
2. Load workspace context and full customer portfolio
3. Load BENCHMARKS.md for industry comparison
4. Load historical metrics from metrics/ directory

## Phase 2: Revenue metrics

Calculate and display:
```
  +-- REVENUE METRICS -----------------------------+
  |                                                 |
  |  Net Revenue Retention (NRR)                    |
  |    Current:   {value}%    Benchmark: {bench}%   |
  |    Trend:     {direction} ({delta} vs last Q)   |
  |                                                 |
  |  Gross Revenue Retention (GRR)                  |
  |    Current:   {value}%    Benchmark: {bench}%   |
  |    Trend:     {direction} ({delta} vs last Q)   |
  |                                                 |
  |  Expansion Revenue                              |
  |    This quarter:  ${value}                      |
  |    Rate:          {value}% of starting ARR      |
  |    Benchmark:     {bench}%                      |
  |                                                 |
  |  Contraction                                    |
  |    This quarter:  ${value}                      |
  |    Rate:          {value}%                      |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 3: Customer metrics

```
  +-- CUSTOMER METRICS ----------------------------+
  |                                                 |
  |  Logo Churn Rate                                |
  |    Current:   {value}%    Benchmark: {bench}%   |
  |    Logos lost: {N} this quarter                  |
  |    ARR lost:   ${value}                         |
  |                                                 |
  |  Revenue Churn Rate                             |
  |    Current:   {value}%    Benchmark: {bench}%   |
  |                                                 |
  |  Time to Value (TTV)                            |
  |    Median:    {days} days  Benchmark: {bench}    |
  |    By segment: Ent {d}, Mid {d}, SMB {d}        |
  |                                                 |
  |  Onboarding Completion Rate                     |
  |    Current:   {value}%                          |
  |    Avg time:  {days} days                       |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 4: Satisfaction metrics

```
  +-- SATISFACTION --------------------------------+
  |                                                 |
  |  NPS                                            |
  |    Score:       {value}    Benchmark: {bench}    |
  |    Promoters:   {N} ({pct}%)                    |
  |    Passives:    {N} ({pct}%)                    |
  |    Detractors:  {N} ({pct}%)                    |
  |    Response rate: {pct}%                        |
  |                                                 |
  |  CSAT                                           |
  |    Score:       {value}    Benchmark: {bench}    |
  |    Responses:   {N} this period                 |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 5: Health distribution

```
  +-- HEALTH DISTRIBUTION -------------------------+
  |                                                 |
  |  90-100  ||||||||||||||||   {N} ({pct}%)        |
  |  70-89   ||||||||||         {N} ({pct}%)        |
  |  50-69   |||||             {N} ({pct}%)         |
  |  30-49   |||               {N} ({pct}%)         |
  |  0-29    |                 {N} ({pct}%)         |
  |                                                 |
  |  Average: {score}   Median: {score}             |
  |  Trending: {up/down/flat} vs last period        |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 6: CSM workload

```
  +-- CSM WORKLOAD --------------------------------+
  |                                                 |
  |  CSM            Customers  ARR       Avg Health |
  |  {name}            {N}    ${value}     {score}  |
  |  {name}            {N}    ${value}     {score}  |
  |  {name}            {N}    ${value}     {score}  |
  |  Unassigned        {N}    ${value}     {score}  |
  |                                                 |
  |  Flags:                                         |
  |  [!] {name} — overloaded ({N} > target {max})   |
  |  [!] {N} customers unassigned                   |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 7: Trends and recommendations

1. Show 3-month trend for each key metric
2. Flag metrics below benchmark (red), at benchmark (yellow), above (green)
3. Identify correlations (e.g., low TTV correlates with higher NRR)
4. Generate top 3 recommendations based on metrics
5. Save snapshot to metrics/snapshot-{date}.md
6. Suggest next actions:
```
---------------------------------------------------

  >> Next: /cs:report {workspace} portfolio
     Also: /cs:segments {workspace} analyze

---------------------------------------------------
```

</process>
</output>
