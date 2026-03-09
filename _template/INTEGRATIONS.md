# Integrations

Connected tool configuration, field mappings, sync settings, and webhook URLs.

## Connected tools status

| Tool | Category | Status | Last sync | Sync frequency | Notes |
|------|----------|--------|-----------|---------------|-------|
| {CRM} | CRM | {connected / not configured} | — | {real-time / hourly / daily} | — |
| {CS Platform} | CS Platform | {connected / not configured} | — | — | — |
| {Support} | Support | {connected / not configured} | — | — | — |
| {Billing} | Billing | {connected / not configured} | — | — | — |
| {Analytics} | Product analytics | {connected / not configured} | — | — | — |

## CRM field mappings

### Inbound (CRM > CS:OS)

| CRM field | CS:OS field | Sync rule | Notes |
|-----------|------------|-----------|-------|
| Account Name | Customer | Always | — |
| ARR / ACV | ARR | Always | — |
| Renewal Date | Renewal Date | Always | — |
| Account Owner | CSM | Always | — |
| Industry | Segment metadata | On create | — |
| Employee Count | Segment metadata | On create | — |

### Outbound (CS:OS > CRM)

| CS:OS field | CRM field | Sync rule | Notes |
|------------|-----------|-----------|-------|
| Health score | {custom field} | Daily | Numeric 0-100 |
| Health label | {custom field} | Daily | Healthy/Monitor/At-risk/Critical |
| Last CSM touchpoint | {custom field} | On update | Date of last meaningful interaction |
| Expansion signal | {custom field} | On detection | Boolean or text |
| Churn risk | {custom field} | On detection | Boolean or text |

## CS platform configuration

### Health score sync
- **Source:** {CS:OS calculated / platform native}
- **Override behavior:** {CS:OS overrides platform / platform overrides CS:OS / manual merge}
- **Sync field:** {field name}

### Playbook triggers
| Playbook | Trigger source | Trigger condition | Notes |
|----------|---------------|-------------------|-------|
| At-risk | Health score | Score < 60 | — |
| Renewal | Renewal date | T-{90/120} days | — |
| Onboarding | Deal stage | Closed Won | — |
| Expansion | Usage data | Usage > 80% for 30d | — |

## Support tool integration

### Ticket sync
- **Sync tickets to CS:OS:** {yes / no}
- **Escalation alerts:** {Slack / email / CS platform}
- **CSAT feed:** {automatic / manual}

### Alert rules
| Condition | Alert to | Channel | Priority |
|-----------|----------|---------|----------|
| P1 ticket opened | CSM + CS Lead | {Slack / email} | Immediate |
| 3+ open tickets (same account) | CSM | {Slack / email} | High |
| CSAT < 3 | CSM | {Slack / email} | High |
| Escalation | CS Lead | {Slack / email} | Immediate |

## Billing integration

### Revenue sync
- **ARR source:** {billing tool / CRM / manual}
- **Expansion tracking:** {automatic from billing / manual}
- **Churn detection:** {auto-cancel alert / manual}

## Webhook URLs

| Webhook | URL | Events | Status |
|---------|-----|--------|--------|
| {name} | {URL} | {events triggered} | {active / inactive} |

## API keys and credentials

Store credentials securely. Reference locations here, never store actual keys.

| Tool | Credential location | Last rotated | Rotation schedule |
|------|-------------------|-------------|-------------------|
| {CRM} | {vault / env var / settings} | — | {quarterly / annual} |
| {CS Platform} | — | — | — |
| {Support} | — | — | — |
