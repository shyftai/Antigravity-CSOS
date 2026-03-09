---
name: cs:kickoff
description: Customer kickoff workflow -- agenda, success criteria, stakeholder mapping, 30/60/90 plan
argument-hint: "<workspace-name> <customer-name>"
---
<objective>
Run a structured kickoff for a new customer. Create the kickoff agenda, define success criteria, map stakeholders, set milestones, and build a 30/60/90 day plan.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/onboarding-guide.md
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/playbooks.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // KICKOFF >>`
2. Parse workspace and customer name from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, SEGMENTS.md, ONBOARDING.md, PLAYBOOKS.md
4. Load onboarding-guide.md for best practices

## Pre-kickoff prep
5. Check if customer record exists in CUSTOMERS.md
   - If exists: load contract details, segment, ARR, key contacts
   - If not: ask for essential details (company name, segment, ARR, contract start, renewal date)
6. Check for handoff document in context/handoffs/
   - If exists: pull deal context, stakeholder info, success criteria from sales
   - If not: note gap, ask CSM for deal context

## Stakeholder mapping
7. Map the customer's team:
   - **Executive sponsor** -- who owns the budget and strategic vision?
   - **Champion** -- who is the internal advocate and daily driver?
   - **Technical lead** -- who handles implementation and integration?
   - **End users** -- who are the primary users of the product?
   - **Decision maker for renewal** -- who signs off on renewal?

8. For each stakeholder, capture:
   - Name, title, email
   - Communication preference (email, Slack, phone)
   - Engagement level (high, medium, low)
   - Influence on renewal decision

## Success criteria definition
9. Define what success looks like for this customer:
   - **Business outcomes** -- what business problem are they solving?
   - **Key metrics** -- what numbers will prove value? (e.g., time saved, revenue generated, efficiency gained)
   - **Activation milestones** -- what usage milestones indicate adoption?
   - **Timeline** -- when do they expect to see results?
10. Validate success criteria against what the product can deliver
11. Flag any misaligned expectations early

## Kickoff agenda
12. Generate kickoff meeting agenda:
```
+----------------------------------------------------------+
|  KICKOFF AGENDA -- {Customer Name}                        |
+----------------------------------------------------------+

  1. Introductions (5 min)
     - CS team introduction
     - Customer team introduction and roles

  2. Align on goals (10 min)
     - Review why they purchased
     - Confirm success criteria
     - Agree on key metrics

  3. Onboarding overview (10 min)
     - Walk through onboarding timeline
     - Key milestones and checkpoints
     - Training plan

  4. Technical setup (10 min)
     - Integration requirements
     - Data migration plan
     - Technical prerequisites

  5. Communication cadence (5 min)
     - Check-in frequency
     - Preferred channels
     - Escalation process

  6. 30/60/90 day plan (10 min)
     - Review milestone plan
     - Assign owners and deadlines
     - Identify risks

  7. Q&A and next steps (10 min)
     - Open questions
     - Immediate action items
     - Schedule next check-in

----------------------------------------------------------
```

## 30/60/90 day plan
13. Build milestone plan based on segment and product:

**Day 1-30: Foundation**
- [ ] Technical setup complete
- [ ] Core integrations connected
- [ ] Initial data loaded/migrated
- [ ] Key users trained on basics
- [ ] First value milestone achieved
- [ ] Weekly check-in cadence established
- Target: Customer can use the product independently for core use case

**Day 31-60: Adoption**
- [ ] All planned users onboarded
- [ ] Advanced features introduced
- [ ] First business outcome measured
- [ ] Usage meets activation threshold
- [ ] Support channel established
- [ ] Bi-weekly check-in cadence
- Target: Customer sees measurable value from primary use case

**Day 61-90: Optimization**
- [ ] Full feature adoption across team
- [ ] ROI metrics collected and documented
- [ ] First QBR scheduled
- [ ] Expansion opportunities identified
- [ ] Customer can self-serve for common tasks
- [ ] Monthly check-in cadence (or per segment)
- Target: Customer is self-sufficient and seeing clear ROI

14. Adjust milestones based on:
    - Customer segment (Enterprise gets more touchpoints, SMB gets faster timeline)
    - Product complexity (complex products get longer onboarding)
    - Handoff notes (any concerns flagged by sales)

## Save and schedule
15. Save kickoff document to context/kickoffs/{customer-name}-kickoff-{date}.md
16. Create customer record in CUSTOMERS.md if not exists
17. Add kickoff entry to TIMELINE.md
18. Set initial health score based on segment defaults
19. Schedule first check-in based on cadence

20. Display summary:
```
  Kickoff ready: context/kickoffs/{file}

  >> Next: /cs:onboard-customer {ws} {customer}
     Also: /cs:check-in {ws} {customer} (schedule first check-in)
     Also: /cs:health {ws} {customer} (set baseline health)
```
</process>
