# Report Template -- CS:OS

Visual templates for customer success reports. Used by CS:OS reporting modes.

---

## Report types

- **Customer health report** -- individual account health snapshot
- **Portfolio health report** -- all accounts at a glance
- **QBR deck template** -- quarterly business review structure
- **Monthly CS metrics report** -- team and portfolio performance
- **Churn analysis report** -- why customers left, patterns, prevention
- **Expansion pipeline report** -- upsell/cross-sell opportunities
- **Board-level CS summary** -- exec summary for leadership

---

## Customer Health Report

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  CUSTOMER HEALTH -- {Customer Name}                            ┃
┃  Segment: {segment}    ARR: ${amount}    Renewal: {date}       ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

  +- Health Score -----------------------------------------------+
  |                                                              |
  |  Overall: {score}/100  [{GREEN/AMBER/RED/BLACK}]             |
  |                                                              |
  |  Product Usage      {score}/30  ████████████░░░░░░  {pct}%   |
  |  Support Health     {score}/20  ██████████████░░░░  {pct}%   |
  |  Engagement         {score}/20  ████████░░░░░░░░░░  {pct}%   |
  |  Business Outcomes  {score}/15  ██████████░░░░░░░░  {pct}%   |
  |  Relationship       {score}/15  ████████████░░░░░░  {pct}%   |
  |                                                              |
  +--------------------------------------------------------------+

  +- Key Metrics ------------------------------------------------+
  |                                                              |
  |  DAU/MAU:          {pct}%       Seat utilization: {pct}%     |
  |  Feature adoption: {pct}%       CSAT: {score}                |
  |  Open tickets:     {n}          NPS: {score}                 |
  |  Last login:       {date}       Last check-in: {date}        |
  |                                                              |
  +--------------------------------------------------------------+

  +- Risk Signals -----------------------------------------------+
  |                                                              |
  |  Active signals: {n}    Risk score: {score}/100              |
  |                                                              |
  |  {signal 1} -- {severity} -- {detail}                        |
  |  {signal 2} -- {severity} -- {detail}                        |
  |                                                              |
  +--------------------------------------------------------------+

  +- Timeline ---------------------------------------------------+
  |                                                              |
  |  Last QBR:        {date}    Next QBR: {date}                 |
  |  Last NPS:        {date}    Next NPS: {date}                 |
  |  Renewal date:    {date}    Days remaining: {n}              |
  |  Onboarding:      {complete / in progress}                   |
  |                                                              |
  +--------------------------------------------------------------+

  Recommendations:
  1. {action based on health data}
  2. {action based on risk signals}
  3. {action based on timeline}
```

---

## Portfolio Health Report

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  PORTFOLIO HEALTH -- {CSM Name / Team}                         ┃
┃  {Date}                                                        ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

  +- Summary ----------------------------------------------------+
  |                                                              |
  |  Total accounts:   {n}         Total ARR: ${amount}          |
  |  Avg health score: {score}     NRR: {pct}%                   |
  |                                                              |
  |  Healthy (80+)     {n}  ████████████████░░  {pct}%           |
  |  Stable (60-79)    {n}  ████████░░░░░░░░░░  {pct}%           |
  |  At-risk (40-59)   {n}  ████░░░░░░░░░░░░░░  {pct}%           |
  |  Critical (0-39)   {n}  ██░░░░░░░░░░░░░░░░  {pct}%           |
  |                                                              |
  +--------------------------------------------------------------+

  +- At-Risk Accounts -------------------------------------------+
  |                                                              |
  |  Customer            ARR       Health  Renewal  Top signal   |
  |  -------------------------------------------------------    |
  |  {customer-1}        ${amt}    {n}     {date}   {signal}     |
  |  {customer-2}        ${amt}    {n}     {date}   {signal}     |
  |  {customer-3}        ${amt}    {n}     {date}   {signal}     |
  |                                                              |
  |  ARR at risk: ${amount} ({pct}% of portfolio)                |
  |                                                              |
  +--------------------------------------------------------------+

  +- Renewals (next 90 days) ------------------------------------+
  |                                                              |
  |  Customer            ARR       Health  Days left  Status     |
  |  -------------------------------------------------------    |
  |  {customer-1}        ${amt}    {n}     {n}        {status}   |
  |  {customer-2}        ${amt}    {n}     {n}        {status}   |
  |                                                              |
  |  Renewal ARR (90d): ${amount}                                |
  |                                                              |
  +--------------------------------------------------------------+

  +- Expansion Pipeline -----------------------------------------+
  |                                                              |
  |  Opportunities: {n}    Pipeline value: ${amount}             |
  |  Weighted:      ${amount}                                    |
  |                                                              |
  +--------------------------------------------------------------+
```

---

## QBR Deck Template

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  QUARTERLY BUSINESS REVIEW -- {Customer Name}                  ┃
┃  {Quarter} {Year}                                              ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

  SECTION 1: Partnership Overview
  - Relationship timeline and milestones
  - Team and stakeholder map
  - Support summary (tickets, CSAT, resolution time)

  SECTION 2: Success Plan Progress
  - Goals set last QBR vs current status
  - Metrics: {goal 1} -- {baseline} > {current} (target: {target})
  - Metrics: {goal 2} -- {baseline} > {current} (target: {target})
  - Blockers and how they were resolved

  SECTION 3: Product Usage & Adoption
  - Usage trends (DAU/MAU, feature adoption, seat utilization)
  - Top used features
  - Underutilized features with value potential
  - Usage vs peers/benchmarks

  SECTION 4: ROI & Value Delivered
  - Quantified value: {metric} = ${amount} saved/gained
  - Qualitative wins: {team efficiency, process improvement}
  - Customer quotes or feedback

  SECTION 5: Roadmap & What's Next
  - Relevant upcoming features
  - New use cases to explore
  - Training opportunities

  SECTION 6: Goals for Next Quarter
  - Goal 1: {description} -- metric: {metric} -- target: {value}
  - Goal 2: {description} -- metric: {metric} -- target: {value}
  - Goal 3: {description} -- metric: {metric} -- target: {value}

  SECTION 7: Open Discussion
  - Customer feedback and concerns
  - Partnership improvement ideas
  - Any changes in business priorities
```

---

## Monthly CS Metrics Report

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  MONTHLY CS METRICS -- {Month Year}                            ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

  +- Retention --------------------------------------------------+
  |  GRR:  {pct}%  (target: {pct}%)   {trend arrow}             |
  |  NRR:  {pct}%  (target: {pct}%)   {trend arrow}             |
  |  Logo: {pct}%  (target: {pct}%)   {trend arrow}             |
  +--------------------------------------------------------------+

  +- Health Distribution ----------------------------------------+
  |  Healthy:  {n} ({pct}%)   vs last month: {+/-n}             |
  |  Stable:   {n} ({pct}%)   vs last month: {+/-n}             |
  |  At-risk:  {n} ({pct}%)   vs last month: {+/-n}             |
  |  Critical: {n} ({pct}%)   vs last month: {+/-n}             |
  +--------------------------------------------------------------+

  +- Activity ---------------------------------------------------+
  |  Check-ins completed:    {n} of {n} scheduled ({pct}%)       |
  |  QBRs delivered:         {n}                                 |
  |  NPS surveys sent:       {n}   Responses: {n} ({pct}%)      |
  |  Escalations:            {n}   Resolved: {n}                 |
  |  Onboardings active:     {n}   Completed: {n}               |
  +--------------------------------------------------------------+

  +- Expansion --------------------------------------------------+
  |  Expansion revenue:      ${amount}                           |
  |  Opportunities opened:   {n}    Closed: {n}                  |
  |  Pipeline value:         ${amount}                           |
  +--------------------------------------------------------------+

  +- Churn/Contraction -----------------------------------------+
  |  Churned accounts:       {n}    ARR lost: ${amount}          |
  |  Downgraded accounts:    {n}    ARR reduced: ${amount}       |
  |  Save attempts:          {n}    Saved: {n} ({pct}%)          |
  +--------------------------------------------------------------+
```

---

## Churn Analysis Report

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  CHURN ANALYSIS -- {Period}                                    ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

  +- Summary ----------------------------------------------------+
  |  Accounts churned:  {n}       ARR lost: ${amount}            |
  |  Logo churn rate:   {pct}%    Revenue churn rate: {pct}%     |
  +--------------------------------------------------------------+

  +- Churn by Reason --------------------------------------------+
  |                                                              |
  |  Value not realized    {n}  ████████████████░░  {pct}%       |
  |  Product gaps          {n}  ██████████░░░░░░░░  {pct}%       |
  |  Support issues        {n}  ██████░░░░░░░░░░░░  {pct}%       |
  |  Budget/cost           {n}  ████░░░░░░░░░░░░░░  {pct}%       |
  |  Champion loss         {n}  ███░░░░░░░░░░░░░░░  {pct}%       |
  |  Competitor            {n}  ██░░░░░░░░░░░░░░░░  {pct}%       |
  |  Other                 {n}  █░░░░░░░░░░░░░░░░░  {pct}%       |
  |                                                              |
  +--------------------------------------------------------------+

  +- Prevention Analysis ----------------------------------------+
  |                                                              |
  |  Preventable churns:     {n} of {total} ({pct}%)             |
  |  Avg days from signal:   {n} days before churn               |
  |  Save attempts made:     {n}    Success rate: {pct}%         |
  |                                                              |
  |  Top missed signals:                                         |
  |  1. {signal} -- seen in {n} of {total} churns               |
  |  2. {signal} -- seen in {n} of {total} churns               |
  |                                                              |
  +--------------------------------------------------------------+

  Recommendations:
  1. {data-backed prevention recommendation}
  2. {process improvement}
  3. {product feedback to share with eng}
```

---

## Expansion Pipeline Report

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  EXPANSION PIPELINE -- {Period}                                ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

  +- Pipeline Summary -------------------------------------------+
  |                                                              |
  |  Open opportunities:  {n}       Pipeline: ${amount}          |
  |  Weighted pipeline:   ${amount}  Avg deal size: ${amount}    |
  |                                                              |
  |  By type:                                                    |
  |    Upsell:         {n}  ${amount}                            |
  |    Cross-sell:     {n}  ${amount}                            |
  |    Seat expansion: {n}  ${amount}                            |
  |                                                              |
  +--------------------------------------------------------------+

  +- Opportunities ----------------------------------------------+
  |                                                              |
  |  Customer          Type       Value    Health  Stage         |
  |  -------------------------------------------------------    |
  |  {customer-1}      Upsell     ${amt}   {n}     {stage}      |
  |  {customer-2}      Seats      ${amt}   {n}     {stage}      |
  |  {customer-3}      Cross-sell ${amt}   {n}     {stage}      |
  |                                                              |
  +--------------------------------------------------------------+
```

---

## Board-Level CS Summary

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  CUSTOMER SUCCESS -- EXECUTIVE SUMMARY                         ┃
┃  {Period}                                                      ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

  KEY METRICS
  GRR: {pct}%    NRR: {pct}%    NPS: {score}    Avg Health: {score}

  WINS
  - {win 1 with dollar impact}
  - {win 2 with dollar impact}

  RISKS
  - {risk 1 with ARR at stake}
  - {risk 2 with ARR at stake}

  ASKS
  - {resource or support needed from leadership}
```

---

## Notes

- All reports use the CS:OS box style from ui-brand.md
- Render in blue for headers, white for data
- Include benchmark comparisons from BENCHMARKS.md where relevant
- Highlight metrics that are above or below benchmarks with [GREEN] or [RED]
- Reports can be exported as markdown files to `reports/`
