# Health Scoring Model -- CS:OS

Weighted scoring model for measuring customer health. Produces a 0-100 score per account.

---

## Score components

| Component | Weight | Max points | What it measures |
|-----------|--------|------------|-----------------|
| Product usage | 30% | 30 | How actively the customer uses the product |
| Support health | 20% | 20 | Quality of the support relationship |
| Engagement | 20% | 20 | Customer participation and responsiveness |
| Business outcomes | 15% | 15 | Whether the customer is achieving their goals |
| Relationship | 15% | 15 | Strength of the human relationship |

**Total: 100 points**

---

## Product usage (0-30)

| Factor | Points | Criteria |
|--------|--------|----------|
| DAU/MAU ratio | 0-10 | 10 = >60%, 7 = 40-60%, 4 = 20-40%, 0 = <20% |
| Feature adoption | 0-8 | 8 = using >80% of entitled features, 4 = 50-80%, 0 = <50% |
| Usage trend | 0-6 | 6 = growing, 3 = stable, 0 = declining |
| Seat utilization | 0-4 | 4 = >85% seats active, 2 = 50-85%, 0 = <50% |
| Login frequency | 0-2 | 2 = daily, 1 = weekly, 0 = monthly or less |

---

## Support health (0-20)

| Factor | Points | Criteria |
|--------|--------|----------|
| CSAT score | 0-6 | 6 = >4.5, 4 = 4.0-4.5, 2 = 3.0-4.0, 0 = <3.0 |
| Ticket volume trend | 0-4 | 4 = stable/decreasing, 2 = slight increase, 0 = spiking |
| Escalation frequency | 0-4 | 4 = none in 90d, 2 = 1 in 90d, 0 = 2+ in 90d |
| Time to resolution | 0-3 | 3 = within SLA, 1 = near SLA, 0 = exceeding SLA |
| Open critical tickets | 0-3 | 3 = none, 1 = 1, 0 = 2+ |

---

## Engagement (0-20)

| Factor | Points | Criteria |
|--------|--------|----------|
| Meeting attendance | 0-6 | 6 = attends all, 3 = attends most, 0 = no-shows |
| Email responsiveness | 0-4 | 4 = responds <24h, 2 = responds <72h, 0 = non-responsive |
| QBR participation | 0-4 | 4 = exec + team attend, 2 = team only, 0 = declines QBR |
| Training completion | 0-3 | 3 = team certified, 1 = partial, 0 = no training |
| Community participation | 0-3 | 3 = active in community/events, 1 = occasional, 0 = none |

---

## Business outcomes (0-15)

| Factor | Points | Criteria |
|--------|--------|----------|
| ROI achievement | 0-6 | 6 = exceeding targets, 3 = on track, 0 = not tracking |
| Success plan progress | 0-4 | 4 = ahead of plan, 2 = on track, 0 = behind/no plan |
| Value realization | 0-3 | 3 = documented value, 1 = anecdotal, 0 = no evidence |
| Expansion signals | 0-2 | 2 = requesting more, 1 = open to discussion, 0 = no interest |

---

## Relationship (0-15)

| Factor | Points | Criteria |
|--------|--------|----------|
| Champion strength | 0-5 | 5 = strong internal advocate, 3 = supportive, 0 = no champion |
| Exec sponsor access | 0-4 | 4 = regular exec engagement, 2 = occasional, 0 = no access |
| Multi-threading | 0-3 | 3 = 3+ contacts engaged, 2 = 2 contacts, 0 = single-threaded |
| NPS score | 0-3 | 3 = promoter (9-10), 2 = passive (7-8), 0 = detractor (0-6) |

---

## Score ranges

| Range | Label | Color | Action |
|-------|-------|-------|--------|
| 80-100 | Healthy | GREEN | Maintain cadence, explore expansion, request advocacy |
| 60-79 | Stable | AMBER | Monitor closely, increase engagement, address gaps |
| 40-59 | At-risk | RED | Activate save playbook, escalate internally, increase cadence |
| 0-39 | Critical | BLACK | Immediate intervention, exec escalation, daily monitoring |

---

## Automatic actions by health level

**Healthy (80-100):**
- Standard check-in cadence (monthly)
- Eligible for expansion conversations
- Eligible for advocacy asks (reference, case study, review)
- Include in promoter programs

**Stable (60-79):**
- Increase check-in cadence to bi-weekly
- Investigate declining dimensions
- Create targeted improvement plan
- Alert CSM of any further decline

**At-risk (40-59):**
- Activate at-risk save playbook
- Bi-weekly check-ins minimum
- Internal escalation to CS Manager
- Notify account team (AE, SE if applicable)
- Block expansion conversations

**Critical (0-39):**
- Immediate exec escalation
- Weekly check-ins minimum
- Daily internal monitoring
- VP/CRO notification
- Dedicated save plan with timeline
- Block all non-essential outreach

---

## How to override weights per workspace

During onboarding or at any time, the user can customize health scoring. Add a `## Health scoring overrides` section to the workspace's RULES.md.

Example override in RULES.md:
```
## Health scoring overrides
- Product usage weight: 40% (instead of 30%)
- Engagement weight: 10% (instead of 20%)
- Add custom factor: "API usage" = +5 points under product usage
- Healthy threshold: 75 (instead of 80)
- Ignore relationship component (all accounts single-threaded)
```

If no overrides exist in the workspace RULES.md, use this default model as-is.
