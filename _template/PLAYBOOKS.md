# Playbooks

Workspace-specific playbook overrides and custom playbooks. These extend or replace the default CS:OS playbooks.

## Active playbooks

| Playbook | Trigger | Owner | Last updated |
|----------|---------|-------|-------------|
| Onboarding | New customer signed | CSM | — |
| At-risk intervention | Health score < 60 | CSM + CS Lead | — |
| Renewal | 90-120 days before renewal | CSM | — |
| Expansion | Usage > 80% or champion request | CSM | — |
| Executive escalation | Health score < 40 or churn signal | CS Lead | — |
| Reactivation | Usage drop > 50% in 14 days | CSM | — |
| QBR | Quarterly cadence | CSM | — |

---

## Onboarding playbook

**Trigger:** New customer contract signed
**Duration:** {30 / 60 / 90} days depending on segment
**Owner:** CSM (or onboarding manager for Enterprise+)

| Day | Action | Owner | Done |
|-----|--------|-------|------|
| 0 | Internal handoff from Sales (notes, goals, stakeholders) | AE > CSM | [ ] |
| 1 | Welcome email with onboarding timeline | CSM | [ ] |
| 3 | Kickoff call (goals, success criteria, stakeholders, timeline) | CSM | [ ] |
| 7 | Technical setup confirmed, integrations live | CSM + Support | [ ] |
| 14 | Training session 1 — core workflows | CSM | [ ] |
| 21 | Training session 2 — advanced features | CSM | [ ] |
| 30 | 30-day check-in (adoption metrics, blockers, feedback) | CSM | [ ] |
| 45 | Success plan review — on track to first value? | CSM | [ ] |
| 60 | Go-live confirmed, transition to steady-state cadence | CSM | [ ] |
| 90 | First QBR (Enterprise+ only) | CSM | [ ] |

---

## At-risk intervention playbook

**Trigger:** Health score drops below 60 OR manual flag
**Escalation:** CS Lead notified immediately
**Timeline:** 14-day intervention window

| Day | Action | Owner | Done |
|-----|--------|-------|------|
| 0 | Identify root cause (usage data, support tickets, engagement gaps) | CSM | [ ] |
| 0 | Internal alert — CS Lead + executive sponsor (if applicable) | CSM | [ ] |
| 1 | Outreach to primary contact — empathy-first, diagnose not sell | CSM | [ ] |
| 3 | Save plan created (specific actions, owners, timeline) | CSM + CS Lead | [ ] |
| 5 | Executive-to-executive outreach (Strategic/Enterprise only) | CS Lead | [ ] |
| 7 | Progress check — are planned actions happening? | CSM | [ ] |
| 14 | Status assessment — saved / still at risk / lost | CSM + CS Lead | [ ] |

---

## Renewal playbook

**Trigger:** {90-180} days before renewal date (segment-dependent)
**Owner:** CSM

| Step | Action | Timeline | Done |
|------|--------|----------|------|
| 1 | Internal renewal prep — usage data, health, expansion opportunity | T-120 days | [ ] |
| 2 | Renewal sentiment check with champion | T-90 days | [ ] |
| 3 | QBR with value realization data | T-75 days | [ ] |
| 4 | Commercial conversation — pricing, terms, expansion | T-60 days | [ ] |
| 5 | Proposal sent | T-45 days | [ ] |
| 6 | Negotiation / procurement | T-30 days | [ ] |
| 7 | Contract signed | T-14 days | [ ] |
| 8 | Post-renewal kickoff — next period goals | T+7 days | [ ] |

---

## Expansion playbook

**Trigger:** Usage consistently above 80%, champion request, or new use case identified
**Owner:** CSM (co-sell with AE if applicable)

| Step | Action | Owner | Done |
|------|--------|-------|------|
| 1 | Document expansion signal and evidence | CSM | [ ] |
| 2 | Validate with champion — is there budget and need? | CSM | [ ] |
| 3 | Build business case with ROI from current usage | CSM | [ ] |
| 4 | Present proposal to economic buyer | CSM + AE | [ ] |
| 5 | Commercial negotiation | AE | [ ] |
| 6 | Contract amendment signed | AE | [ ] |
| 7 | Onboard new seats/features/modules | CSM | [ ] |

---

## Custom playbooks

Add workspace-specific playbooks below as needed.

### {Custom playbook name}

**Trigger:** {what triggers this playbook}
**Owner:** {role}

| Step | Action | Owner | Done |
|------|--------|-------|------|
| 1 | — | — | [ ] |
