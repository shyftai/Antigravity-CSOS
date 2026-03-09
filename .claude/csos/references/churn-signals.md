# Churn Signals -- CS:OS

Patterns that indicate a customer may churn. Use this during health checks, at-risk detection, and renewal prep.

---

## Product signals

| Signal | Severity | Threshold | Decay |
|--------|----------|-----------|-------|
| Usage decline (week-over-week) | HIGH | >20% drop for 2+ weeks | Resets if usage recovers |
| Feature abandonment | MEDIUM | Key feature unused for 30+ days | -1 severity per week of re-use |
| Login frequency drop | HIGH | <50% of previous 30-day avg | Resets at normal frequency |
| Seat utilization decline | MEDIUM | Drops below 50% of licensed seats | Resets when seats re-activate |
| API call volume drop | MEDIUM | >30% decline over 14 days | Resets at normal volume |
| Export activity spike | HIGH | 3x normal export volume | One-time signal, review within 7d |
| Downgrade inquiry | CRITICAL | Any request to reduce plan | Does not decay |
| Integration disconnected | MEDIUM | Core integration removed | Resets when reconnected |

---

## Support signals

| Signal | Severity | Threshold | Decay |
|--------|----------|-----------|-------|
| Ticket volume spike | HIGH | >2x normal monthly volume | Resets after 2 normal weeks |
| Escalation frequency | HIGH | 2+ escalations in 30 days | -1 per 30 days without escalation |
| CSAT decline | MEDIUM | Score drops below 3.5 | Resets when score >4.0 |
| Repeated same issue | HIGH | Same ticket category 3+ times | Resets when root cause fixed |
| Unresolved critical ticket | CRITICAL | Open >5 business days | Resets when resolved |
| "Cancel" or "alternative" in ticket | CRITICAL | Any mention | Does not decay |
| Support satisfaction survey skip | LOW | 3+ consecutive surveys skipped | Resets on response |

---

## Engagement signals

| Signal | Severity | Threshold | Decay |
|--------|----------|-----------|-------|
| Meeting no-shows | HIGH | 2+ consecutive no-shows | Resets after attended meeting |
| Email non-response | MEDIUM | No reply to 3+ emails over 21 days | Resets on response |
| Champion departure | CRITICAL | Champion leaves company or role | Does not decay (requires new champion) |
| Exec sponsor change | HIGH | Sponsor leaves or is reassigned | -1 when new sponsor engaged |
| QBR decline | HIGH | Customer declines QBR | Resets when QBR accepted |
| Reduced meeting attendees | MEDIUM | Fewer stakeholders attending | Resets at normal attendance |
| NPS detractor response | HIGH | NPS score 0-6 | Resets when score improves to 7+ |
| Community/event disengagement | LOW | Stops attending after previous participation | Resets on re-engagement |

---

## Business signals

| Signal | Severity | Threshold | Decay |
|--------|----------|-----------|-------|
| Budget cuts announced | CRITICAL | Customer communicates budget reduction | Does not decay |
| Company reorg | HIGH | Leadership or team restructure | -1 per month if no impact |
| Competitor evaluation | CRITICAL | Customer mentions evaluating alternatives | Does not decay |
| Contract dispute | CRITICAL | Billing dispute or legal issue raised | Resets when resolved |
| Merger/acquisition | HIGH | Customer being acquired or merging | Evaluate in 30 days |
| Layoffs at customer | HIGH | Customer company doing layoffs | Evaluate impact on team |
| Payment delays | MEDIUM | Invoice >30 days overdue | Resets when paid |
| ROI questions | MEDIUM | Customer asks to justify cost | Resets after ROI review |

---

## Composite risk score calculation

Each signal contributes to a composite churn risk score (0-100):

| Severity | Points per active signal |
|----------|------------------------|
| CRITICAL | 25 |
| HIGH | 15 |
| MEDIUM | 8 |
| LOW | 3 |

**Score ranges:**

| Risk score | Level | Action |
|------------|-------|--------|
| 0-15 | Low risk | Standard monitoring |
| 16-35 | Moderate risk | Increase check-in cadence, investigate |
| 36-60 | High risk | Activate save playbook, escalate to CS Manager |
| 61-100 | Critical risk | Immediate exec intervention, daily monitoring |

**Rules:**
- Signals stack -- multiple signals add together
- Cap at 100 (not cumulative beyond max)
- Any single CRITICAL signal = minimum 25 (always at least "moderate risk")
- Two CRITICAL signals = minimum 50 (always "high risk")

---

## Signal-to-action mapping

| Signal detected | Immediate action | Owner |
|----------------|-----------------|-------|
| Usage decline >20% | Send usage report, schedule call | CSM |
| Champion departure | Identify new contact, schedule intro | CSM |
| Competitor evaluation | Exec escalation, ROI review | CSM + Manager |
| Ticket volume spike | Review tickets, assign dedicated support | CSM + Support |
| Export spike | Check-in call to understand intent | CSM |
| NPS detractor | Follow-up within 24h | CSM |
| Budget cuts | ROI justification, right-size discussion | CSM + AE |
| Contract dispute | Loop in leadership and legal | CS Manager |
| Meeting no-shows | Try alternate channels (phone, LinkedIn) | CSM |
| Downgrade inquiry | Value review, explore alternatives | CSM + AE |

---

## Early warning thresholds

Configure these to get alerts before signals become critical:

| Metric | Yellow alert | Red alert |
|--------|-------------|-----------|
| Usage trend | -10% week-over-week | -20% week-over-week |
| Login frequency | -25% vs 30-day avg | -50% vs 30-day avg |
| CSAT score | Drops below 4.0 | Drops below 3.5 |
| Time since last login | 14 days | 30 days |
| Time since last response | 10 days | 21 days |
| Open support tickets | 3+ open simultaneously | 5+ or any critical |
| Seat utilization | Below 70% | Below 50% |
| NPS | Passive (7-8) after being promoter | Detractor (0-6) |

**Yellow alerts:** Add to next check-in agenda, monitor.
**Red alerts:** Trigger immediate outreach, flag in dashboard.
