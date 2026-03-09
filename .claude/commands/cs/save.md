---
name: cs:save
description: Execute a churn save play -- identify reason, select playbook, guide through steps
argument-hint: "<workspace-name> <customer-name>"
---
<objective>
Execute a churn save play for an at-risk customer. Identify the churn reason, select the appropriate playbook, guide through save steps, and track the outcome.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/playbooks.md
@./.claude/csos/references/churn-signals.md
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // SAVE PLAY >>`
2. Parse workspace and customer from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, HEALTH-SCORES.md, PLAYBOOKS.md, TIMELINE.md
4. Load customer's full history -- timeline, health, support tickets, NPS

## Assess the situation
5. Display current customer state:
```
+----------------------------------------------------------+
|  SAVE PLAY -- {Customer Name}                             |
+----------------------------------------------------------+

  Health: {score}/100 ({status})    ARR: ${value}
  Segment: {tier}    Renewal: {date} ({n} days)
  CSM: {name}    Since: {start date}

  Active churn signals:
    !! {Signal 1} -- {severity}
    !! {Signal 2} -- {severity}
    .. {Signal 3} -- {severity}

  Recent timeline:
    {date}  {event}
    {date}  {event}
    {date}  {event}
```

## Identify churn reason
6. Analyze signals and history to determine primary churn driver:
   - **Value gap** -- customer not seeing expected ROI
   - **Product fit** -- product doesn't meet their needs
   - **Support failure** -- unresolved issues eroding trust
   - **Relationship gap** -- lost champion, no executive alignment
   - **Competitor** -- actively evaluating alternatives
   - **Budget/business** -- budget cuts, downsizing, reorganization
   - **Onboarding failure** -- never fully adopted the product

7. Ask CSM to confirm or adjust the assessment:
   "Based on the signals, this looks like a **{reason}** situation. Does that match your read?"

## Select save playbook
8. Match churn reason to playbook from PLAYBOOKS.md:

**Value gap playbook:**
- Step 1: Pull usage data and ROI metrics
- Step 2: Build a value summary showing actual outcomes
- Step 3: Schedule executive meeting to realign on success criteria
- Step 4: Create a 30-day value acceleration plan
- Step 5: Offer success resources (training, consulting, dedicated support)

**Product fit playbook:**
- Step 1: Document specific feature gaps
- Step 2: Check product roadmap for planned features
- Step 3: Identify workarounds or alternative workflows
- Step 4: Escalate to product team with customer context
- Step 5: Offer early access to beta features if applicable

**Support failure playbook:**
- Step 1: Review all open and recent tickets
- Step 2: Assign dedicated support engineer
- Step 3: Schedule a service recovery call with customer
- Step 4: Create a resolution plan with timeline
- Step 5: Implement proactive monitoring for this account

**Relationship gap playbook:**
- Step 1: Identify new stakeholders and decision makers
- Step 2: Research new contacts (LinkedIn, internal notes)
- Step 3: Request warm introduction from remaining contacts
- Step 4: Schedule executive-to-executive alignment call
- Step 5: Rebuild multi-threading plan

**Competitor playbook:**
- Step 1: Identify which competitor and why
- Step 2: Build competitive comparison (honest, not dismissive)
- Step 3: Highlight switching costs and integration depth
- Step 4: Offer exclusive terms or features
- Step 5: Schedule executive discussion on long-term partnership

**Budget/business playbook:**
- Step 1: Understand the scope of budget impact
- Step 2: Offer flexible pricing or contract restructuring
- Step 3: Show ROI to justify continued investment
- Step 4: Propose a reduced tier rather than full churn
- Step 5: Set a check-in cadence for when budget recovers

## Execute the play
9. Walk through each step of the selected playbook
10. For each step, provide:
    - What to do (specific action)
    - What to say (talk track / email template)
    - What to prepare (documents, data, materials)
    - Success criteria (how to know this step worked)

11. Track progress:
```
  Save Play Progress -- {Playbook Name}
    [x] Step 1: {description}     Completed {date}
    [x] Step 2: {description}     Completed {date}
    [ ] Step 3: {description}     Due: {date}
    [ ] Step 4: {description}     --
    [ ] Step 5: {description}     --
```

## Track outcome
12. After save play completes, record result:
    - **Saved** -- customer retained, crisis resolved
    - **Downgraded** -- customer stayed but reduced contract
    - **Churned** -- customer left despite intervention
    - **Pending** -- save play in progress

13. If saved or downgraded:
    - Update health score (should be improving)
    - Schedule follow-up check-in in 2 weeks
    - Add to watchlist for 90 days
    - Update LEARNINGS.md with what worked

14. If churned:
    - Record churn reason and contributing factors
    - Document what was tried and what failed
    - Update LEARNINGS.md with anti-learnings
    - Schedule post-mortem debrief

## Save and update
15. Save save play record to context/saves/{customer-name}-{date}.md
16. Update TIMELINE.md
17. Update HEALTH-SCORES.md
18. Update PLAYBOOKS.md if new learnings warrant playbook changes

19. Display:
```
  Save play tracked: context/saves/{file}

  >> Next: /cs:check-in {ws} {customer} (follow-up in 2 weeks)
     Also: /cs:health {ws} {customer} (monitor recovery)
     Also: /cs:at-risk {ws} (check remaining at-risk customers)
```
</process>
