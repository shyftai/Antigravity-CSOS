# Health Scoring

Customer health scoring configuration. Overrides defaults when workspace-specific thresholds are needed.

## Health score weights

Total must equal 100%.

| Signal | Weight | Source | Description |
|--------|--------|--------|-------------|
| Product usage | 30% | {analytics tool} | DAU/MAU ratio, feature adoption, login frequency |
| Support health | 15% | {support tool} | Open ticket volume, resolution time, escalation rate |
| Engagement | 20% | {CS platform / manual} | Meeting attendance, email response rate, champion activity |
| Contract signals | 15% | {CRM} | Renewal date proximity, multi-year vs month-to-month, payment history |
| Outcome achievement | 20% | {CS platform / manual} | Success plan progress, ROI realized, goals met |

## Health thresholds

| Score range | Label | Color | Action required |
|-------------|-------|-------|-----------------|
| 80-100 | Healthy | Green | Standard cadence, identify expansion |
| 60-79 | Monitor | Yellow | Increase touchpoints, investigate dips |
| 40-59 | At-risk | Orange | Escalate to CS lead, create save plan |
| 0-39 | Critical | Red | Executive sponsor engagement, daily monitoring |

## Score overrides

Manual overrides when automated scoring misses context.

| Customer | Auto Score | Override Score | Reason | Override By | Date |
|----------|-----------|---------------|--------|------------|------|
| — | — | — | — | — | — |

## Signal definitions

### Product usage scoring
- **High (9-10):** DAU/MAU > 40%, using 70%+ of licensed features
- **Medium (5-8):** DAU/MAU 15-40%, using 40-70% of licensed features
- **Low (1-4):** DAU/MAU < 15%, using < 40% of licensed features
- **Critical (0):** No logins in 14+ days

### Support health scoring
- **High (9-10):** < 2 open tickets, no escalations, CSAT > 4.5
- **Medium (5-8):** 2-5 open tickets, CSAT 3.5-4.5
- **Low (1-4):** 5+ open tickets or 1+ escalation, CSAT < 3.5
- **Critical (0):** Unresolved escalation, executive complaint

### Engagement scoring
- **High (9-10):** Attends QBRs, responds within 24h, champion actively advocating
- **Medium (5-8):** Attends some meetings, responds within 48h
- **Low (1-4):** Misses meetings, slow responses, champion disengaged
- **Critical (0):** Ghost account, no response in 30+ days

## Health trend tracking

| Customer | 30d ago | 60d ago | 90d ago | Current | Trend |
|----------|---------|---------|---------|---------|-------|
| — | — | — | — | — | {improving / stable / declining} |
