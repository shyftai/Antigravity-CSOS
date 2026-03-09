# CS Rules

Workspace-specific rules governing customer success operations. Override defaults as needed.

## Escalation rules

### Health-based escalation
- **Score drops below 60:** CSM creates intervention plan, notifies CS Lead within 24h
- **Score drops below 40:** CS Lead engaged, executive sponsor looped in within 48h
- **Score drops below 25:** CRO/CEO notified, war room initiated
- **Any 20+ point drop in 14 days:** Automatic escalation regardless of absolute score

### Support-based escalation
- **3+ open tickets for same customer:** CSM notified for proactive outreach
- **Escalated ticket (P1/P2):** CSM notified immediately, joins support thread
- **Executive complaint:** CS Lead takes point, CSM supports

### Renewal-based escalation
- **Renewal at risk (30 days out, no signature):** CS Lead engaged
- **Renewal at risk (14 days out, no signature):** VP CS engaged
- **Customer requests downgrade:** CSM + CS Lead review before processing

## Communication cadence

| Segment | Check-in | QBR | Health review | Renewal outreach |
|---------|----------|-----|---------------|-----------------|
| Strategic | Weekly | Monthly | Weekly | T-180 days |
| Enterprise | Bi-weekly | Quarterly | Bi-weekly | T-120 days |
| Mid-Market | Monthly | Quarterly | Monthly | T-90 days |
| SMB | Automated monthly | Bi-annual | Automated | T-60 days |

### Response time SLAs (CS team, not support)
- **Customer email:** Acknowledge within 4 business hours
- **Meeting request:** Respond within 1 business day
- **Escalation from support:** Engage within 2 hours
- **Executive request:** Same business day

## Health thresholds

These override the defaults in HEALTH.md for this workspace.

| Signal | Default weight | Workspace override | Notes |
|--------|---------------|-------------------|-------|
| Product usage | 30% | —% | — |
| Support health | 15% | —% | — |
| Engagement | 20% | —% | — |
| Contract signals | 15% | —% | — |
| Outcome achievement | 20% | —% | — |

## Expansion criteria

### Qualified expansion signals
- Usage consistently above 80% of license for 30+ days
- Customer requests additional features or modules
- New department or team expressing interest
- Champion advocates for expansion internally
- Contract includes usage-based pricing and usage is growing

### Expansion disqualifiers
- Health score below 70 (fix health first)
- Open P1/P2 support tickets
- Unresolved escalation in last 30 days
- Customer explicitly said "not now" in last 90 days

## Churn prevention rules
- Never process a cancellation without CSM conversation (minimum 1 call attempt)
- All churned customers get exit interview (survey or call)
- Churned customers enter 90-day winback sequence if eligible
- Log churn reason in CUSTOMERS.md and LEARNINGS.md

## Data hygiene
- Health scores updated minimum weekly (automated) or after every meaningful interaction (manual)
- CUSTOMERS.md updated after every status change
- Success plans reviewed at every QBR
- Renewal dates verified 180 days out
- Contact information validated quarterly
