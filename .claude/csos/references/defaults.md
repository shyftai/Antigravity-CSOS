# CS:OS Defaults

Sensible defaults that apply out of the box. Every default can be overridden per workspace in the relevant file. If a workspace doesn't specify a value, use these.

---

## Health scoring defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Product usage weight | 30% | RULES.md `## Health scoring overrides` |
| Support health weight | 20% | RULES.md |
| Engagement weight | 20% | RULES.md |
| Business outcomes weight | 15% | RULES.md |
| Relationship weight | 15% | RULES.md |
| Healthy threshold | 80-100 | RULES.md |
| Stable threshold | 60-79 | RULES.md |
| At-risk threshold | 40-59 | RULES.md |
| Critical threshold | 0-39 | RULES.md |

## Onboarding defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Kickoff meeting | Within 48 hours of close | PLAYBOOKS.md |
| Time-to-value target | 14 days | PLAYBOOKS.md |
| Onboarding duration | 30/60/90 day milestones | PLAYBOOKS.md |
| Stakeholder mapping | Complete by day 7 | PLAYBOOKS.md |
| Training sessions | 2-3 within first 14 days | PLAYBOOKS.md |
| Go-live checkpoint | Day 14 | PLAYBOOKS.md |
| Success criteria definition | Before kickoff | PLAYBOOKS.md |
| Handoff from sales | Structured, within 24h of close | PLAYBOOKS.md |

## Check-in defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Standard accounts | Monthly | RULES.md |
| At-risk accounts | Bi-weekly | RULES.md |
| Critical accounts | Weekly | RULES.md |
| Enterprise accounts | Bi-weekly minimum | RULES.md |
| Check-in duration | 30 minutes | RULES.md |
| Prep time before check-in | 15 minutes | RULES.md |
| Follow-up email | Within 24 hours | RULES.md |

## QBR defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Frequency | Quarterly | RULES.md |
| Prep start | 2 weeks before QBR date | RULES.md |
| Deck draft ready | 1 week before | RULES.md |
| Internal review | 3 days before | RULES.md |
| Duration | 60 minutes | RULES.md |
| Attendees | CSM, champion, exec sponsor minimum | RULES.md |
| Follow-up actions | Documented within 24 hours | RULES.md |

## Renewal defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Renewal process start | 90 days before expiry | RULES.md |
| Early warning alert | 120 days before expiry | RULES.md |
| Renewal risk assessment | 90 days before | RULES.md |
| Commercial discussion | 60 days before | RULES.md |
| Contract sent | 30 days before | RULES.md |
| Escalation if unsigned | 14 days before | RULES.md |
| Auto-renewal notice | Per contract terms | RULES.md |

## NPS defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| First survey | 30 days post-onboarding | RULES.md |
| Second survey | 90 days | RULES.md |
| Third survey | 180 days | RULES.md |
| Ongoing frequency | Quarterly | RULES.md |
| Detractor follow-up | Within 24 hours | RULES.md (non-overridable) |
| Promoter follow-up | Within 1 week (advocacy ask) | RULES.md |
| Survey tool | Delighted or Typeform | TOOLS.md |

## Escalation defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Critical response time | 1 hour | RULES.md |
| High response time | 4 hours | RULES.md |
| Medium response time | 24 hours | RULES.md |
| Low response time | 72 hours | RULES.md |
| Critical escalation path | CSM > CS Manager > VP CS > CRO | RULES.md |
| High escalation path | CSM > CS Manager | RULES.md |
| Auto-escalate if no response | After 50% of SLA elapsed | RULES.md |

## Expansion defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Eligible when health score | >= 80 | RULES.md |
| Eligible when usage | >= 70% of entitlement | RULES.md |
| Upsell timing | After first value milestone | RULES.md |
| Cross-sell timing | After 90 days healthy | RULES.md |
| Seat expansion trigger | > 85% seat utilization | RULES.md |
| Expansion conversation owner | CSM introduces, AE closes | RULES.md |

## Workspace defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Execution mode | interactive | workspace.config.md |
| Collaboration mode | solo | workspace.config.md |
| Health check frequency | Weekly (portfolio), daily (critical) | workspace.config.md |
| Dashboard refresh | On load | workspace.config.md |

## Notification defaults

| Setting | Default | Override in |
|---------|---------|-------------|
| Slack notifications | Disabled | COLLABORATION.md |
| Critical alerts | Enabled (when Slack is on) | COLLABORATION.md |
| Important alerts | Enabled | COLLABORATION.md |
| Informational alerts | Disabled | COLLABORATION.md |

---

## How overrides work

1. CS:OS checks the workspace-level file first (e.g. RULES.md, PLAYBOOKS.md)
2. If the setting is specified there, use it
3. If not specified, fall back to these defaults
4. Non-overridable settings (marked above) always apply regardless of workspace config
5. Users can add a `## CS:OS overrides` section to any workspace file to change defaults
