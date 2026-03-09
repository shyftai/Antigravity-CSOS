---
name: cs:debrief
description: Post-churn or post-win analysis with root causes and process improvements
argument-hint: "<workspace> <customer-name> <outcome:churn|win|save>"
---
<objective>
Run a post-outcome analysis. Document what happened, identify root causes, extract learnings,
and recommend process improvements. Save insights to LEARNINGS.md for future reference.

Workspace, customer, and outcome: $ARGUMENTS

Outcome types:
- `churn` — Customer churned — why, what we missed, what to improve
- `win` — Customer expanded or renewed strongly — what worked
- `save` — Customer was at risk but saved — what intervention worked
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/BENCHMARKS.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // DEBRIEF >>`
2. Load workspace context and customer record
3. Load full customer timeline (all interactions, health changes, tickets, escalations)
4. Determine outcome type from $ARGUMENTS

## Phase 2: Build outcome timeline

1. Reconstruct the critical path — events that led to the outcome
2. For churn:
   - When did first warning signs appear?
   - What was health score trajectory?
   - Were there missed check-ins or QBRs?
   - When did champion leave (if applicable)?
   - What was the stated reason for leaving?
   - What was the real reason (based on data)?
3. For win:
   - What drove the expansion/renewal decision?
   - Which features/value drove the most impact?
   - Who were the internal champions?
   - What was the health score trajectory leading up?
   - Were there specific moments that cemented the decision?
4. For save:
   - What triggered the at-risk status?
   - What intervention was deployed?
   - What playbook was used (if any)?
   - How long did recovery take?
   - What was the health score recovery path?

## Phase 3: Root cause analysis

Display structured analysis:
```
  +-- DEBRIEF: {customer} — {OUTCOME} -------------+
  |                                                  |
  |  Customer:   {name}                              |
  |  ARR:        ${value}      Segment: {tier}       |
  |  Tenure:     {months} months                     |
  |  Outcome:    {churn/win/save}                    |
  |  Date:       {date}                              |
  |                                                  |
  |  ROOT CAUSES:                                    |
  |  1. {Primary cause — e.g., champion departed}    |
  |  2. {Contributing factor}                        |
  |  3. {Contributing factor}                        |
  |                                                  |
  |  CATEGORY:                                       |
  |  {Product / Service / Fit / Price / Champion /   |
  |   Competition / Acquired / Internal change}      |
  |                                                  |
  |  PREVENTABILITY:                                 |
  |  {Preventable / Partially preventable /          |
  |   Unpreventable}                                 |
  |                                                  |
  |  WARNING SIGNS (hindsight):                      |
  |  - {signal we could have caught earlier}         |
  |  - {signal we could have caught earlier}         |
  |                                                  |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 4: Extract learnings

1. Identify actionable learnings by category:
   - **Process:** What should we change in our CS process?
   - **Playbook:** Should we create/update a playbook for this scenario?
   - **Health model:** Should we adjust health score weights?
   - **Segmentation:** Was this customer in the right segment?
   - **Product feedback:** What product gaps contributed?
   - **Onboarding:** Were there onboarding gaps?
2. For each learning, assess confidence level (high/medium/low)
3. Check existing LEARNINGS.md — update confidence if pattern is confirmed, add new if novel

## Phase 5: Process improvements

1. Generate specific, actionable recommendations:
   - What early warning signal to add
   - What playbook to create or update
   - What health score component to adjust
   - What check-in cadence to change
   - What escalation trigger to add
2. For each recommendation, provide:
   - Priority (Urgent / High / Medium / Low)
   - Effort (Low / Medium / High)
   - Expected impact
3. Display for approval

## Phase 6: Save and update

1. Save debrief to debriefs/{customer}-{outcome}-{date}.md
2. Update LEARNINGS.md with new insights (tagged with source, confidence, date)
3. Update ROADMAP.md with action items from recommendations
4. Update segment/churn analysis data
5. Log in logs/decisions.md
6. Display completion:
```
---------------------------------------------------

  Debrief saved. {N} learnings added. {N} action items created.

  >> Next: /cs:metrics {workspace}
     Also: /cs:playbook {workspace}

---------------------------------------------------
```

</process>
</output>
