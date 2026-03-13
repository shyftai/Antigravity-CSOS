# CS:OS Swarm Architecture

Parallel agent execution for customer success operations. Use when a task can be split across accounts, tickets, or customer segments.

---

## When to Swarm

| Scenario | Agents | Why Parallel |
|----------|--------|-------------|
| Bulk ticket triage | 1 per batch of 20 | Each ticket is independent |
| Multi-account health check | 1 per account | Each account is standalone |
| Churn risk assessment (cohort) | 1 per segment | Segments have different patterns |
| CSAT/NPS response analysis | 1 per batch of 50 | Pattern matching is parallelizable |
| Knowledge base audit | 1 per category | Categories are independent |
| Onboarding pipeline review | 1 per cohort | Each cohort is standalone |

---

## Agent Types

| Color | Role | Typical Task |
|-------|------|-------------|
| **magenta** | Research | Customer sentiment analysis, churn pattern research, competitive support benchmarking |
| **cyan** | Review / Verification | Ticket quality audit, SLA compliance check, response accuracy review |
| **green** | Execution | Template updates, macro creation, auto-response drafting |
| **red** | Issues / Escalation | Escalation triage, complaint root cause analysis, SLA breach investigation |
| **yellow** | Strategy / Synthesis | CSAT trend reports, churn analysis summaries, QBR preparation |
| **blue** | Integration | CRM sync, helpdesk data pull, cross-platform ticket reconciliation |

---

## Batch Sizing

| Operation | Max per Agent | Reason |
|-----------|--------------|--------|
| Ticket triage | 20 tickets | Quick categorization, low complexity |
| Account health check | 5 accounts | Need to review usage data, tickets, and engagement |
| Churn risk scoring | 10 accounts | Requires multi-signal analysis |
| Response drafting | 10 responses | Quality degrades with volume |
| Knowledge base articles | 5 articles | Each needs accuracy verification |
| QBR preparation | 1 account | Deep analysis, multiple data sources |

---

## Wave Structure

### Example: Quarterly Business Review Prep

```
Wave 1: Data Collection (parallel)
  → blue Integration: pull usage metrics from product analytics
  → blue Integration: pull ticket history from helpdesk
  → blue Integration: pull billing data from Stripe
  → magenta Research: competitive landscape updates

Wave 2: Analysis (parallel, depends on Wave 1)
  → yellow Strategy: account health scorecard
  → red Issues: open issue summary and risk assessment
  → cyan Review: SLA compliance report

Wave 3: Synthesis (depends on Wave 2)
  → yellow Strategy: QBR deck and talking points
  → green Execution: action item proposals
```

### Example: Churn Prevention Sprint

```
Wave 1: Identify (parallel)
  → magenta Research: usage decline signals (batch 1-50)
  → magenta Research: usage decline signals (batch 51-100)
  → red Issues: open escalation review

Wave 2: Score & Prioritize (depends on Wave 1)
  → cyan Review: risk scoring and prioritization
  → yellow Strategy: intervention recommendations

Wave 3: Act (depends on Wave 2)
  → green Execution: outreach drafts for at-risk accounts
  → blue Integration: update CRM with risk scores
```

---

## Safety Rules

1. **Never auto-close tickets** — all closures require human review
2. **Never send customer communications** without approval
3. **Never delete conversation history** — archive only
4. **PII handling** — agents must not expose customer PII in summaries
5. **Escalation paths** — never downgrade an escalation without confirmation
6. **Financial operations** — refunds and subscription changes always require human approval
