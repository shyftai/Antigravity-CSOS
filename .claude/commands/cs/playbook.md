---
name: cs:playbook
description: Success playbook management — browse, create, execute, and measure
argument-hint: "<workspace> [playbook-name]"
---
<objective>
Manage CS playbooks. Browse available playbooks, create custom ones, track execution
against active customers, and measure playbook effectiveness over time.

Workspace and playbook: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/playbook-library.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // PLAYBOOKS >>`
2. Load workspace context
3. Load playbooks/ directory for available playbooks
4. If playbook-name provided, jump to Phase 3 (execute)
5. If no playbook specified, show library (Phase 2)

## Phase 2: Browse playbook library

1. Display available playbooks grouped by category:
```
  +-- PLAYBOOK LIBRARY ----------------------------+
  |                                                 |
  |  Onboarding                                     |
  |    enterprise-onboard    14-day white-glove      |
  |    smb-onboard           7-day self-serve        |
  |    technical-onboard     Integration-focused     |
  |                                                 |
  |  Risk Mitigation                                |
  |    health-recovery       Score dropped below 60  |
  |    champion-loss         Key contact departed    |
  |    usage-decline         30-day usage drop >20%  |
  |    pre-renewal-save      At-risk renewal prep    |
  |                                                 |
  |  Expansion                                      |
  |    expansion-signal      Usage-triggered upsell  |
  |    multi-product         Cross-sell motion       |
  |    seat-expansion        User growth detected    |
  |                                                 |
  |  Lifecycle                                      |
  |    qbr-prep              Quarterly review prep   |
  |    annual-review         Year-end strategic rev  |
  |    exec-alignment        Exec sponsor engagement |
  |                                                 |
  |  Custom: {N} workspace-specific playbooks        |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+

  >> Select a playbook or type 'new' to create one
```

## Phase 3: Execute playbook

1. Load the selected playbook definition
2. Show playbook overview:
   - Trigger condition (what activates this playbook)
   - Steps with owners and timelines
   - Success criteria (what "done" looks like)
   - Expected health score impact
3. Select target customer(s) for execution
4. For each step, display:
   - Step description and owner
   - Suggested content (email templates, talk tracks, QBR slides)
   - Due date based on playbook timeline
5. Track step completion — mark steps done as they execute
6. Save execution record to logs/playbook-runs.md

## Phase 4: Create custom playbook

1. Display mode header: `<< CS:OS // NEW PLAYBOOK >>`
2. Collect playbook definition:
   - Name and category
   - Trigger condition (when should this fire?)
   - Target segment (which customers?)
   - Steps (action, owner, timeline, content template)
   - Success criteria
   - Health score impact (expected)
3. Save to playbooks/{name}.md
4. Log in logs/decisions.md

## Phase 5: Measure effectiveness

1. Pull all completed playbook runs from logs/playbook-runs.md
2. For each playbook type, calculate:
   - Times executed
   - Success rate (met success criteria)
   - Average health score change (before vs after)
   - Time to complete vs planned timeline
   - Churn rate of customers who went through playbook vs those who didn't
3. Display effectiveness dashboard:
```
  +-- PLAYBOOK EFFECTIVENESS ----------------------+
  |                                                 |
  |  Playbook         Runs  Success  Avg Health +/- |
  |  health-recovery    12    75%       +18          |
  |  champion-loss       4    50%       +8           |
  |  expansion-signal    8    63%       +5           |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```
4. Recommend playbook improvements based on data
5. Update LEARNINGS.md with playbook insights

</process>
</output>
