---
name: cs:onboard-customer
description: Track customer onboarding -- milestones, adoption, training, time-to-value
argument-hint: "<workspace-name> <customer-name>"
---
<objective>
Track and manage a customer's onboarding journey. Monitor milestones, training completion, feature adoption, and time-to-value. Show progress dashboard and flag blockers.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/onboarding-guide.md
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // ONBOARD CUSTOMER >>`
2. Parse workspace and customer name from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, ONBOARDING.md, SEGMENTS.md, HEALTH-SCORES.md
4. Load customer's kickoff doc if exists (context/kickoffs/)

## Load onboarding state
5. Check for existing onboarding tracker in context/onboarding/{customer-name}/
   - If exists: load current state, show progress
   - If not: create new tracker from ONBOARDING.md template

## Onboarding progress dashboard
6. Display current onboarding status:
```
+----------------------------------------------------------+
|  ONBOARDING -- {Customer Name}                            |
+----------------------------------------------------------+

  Status: {In Progress / At Risk / Complete}
  Started: {date}    Target TTV: {date}    Days elapsed: {n}
  Segment: {tier}    ARR: ${value}

  ── Phase 1: Foundation (Day 1-30) ────────────────────
  [x] Contract signed                          Day 1    DONE
  [x] Kickoff meeting completed                Day 3    DONE
  [x] Technical setup initiated                Day 5    DONE
  [ ] Core integrations connected              Day 10   DUE
  [ ] Initial data loaded                      Day 12   --
  [ ] Key users trained (basic)                Day 15   --
  [ ] First value milestone                    Day 25   --

  Progress: ████████░░░░░░░░░░░░  40%

  ── Phase 2: Adoption (Day 31-60) ─────────────────────
  [ ] All users onboarded                      Day 35   --
  [ ] Advanced features introduced             Day 40   --
  [ ] First business outcome measured          Day 50   --
  [ ] Usage meets activation threshold         Day 55   --

  Progress: ░░░░░░░░░░░░░░░░░░░░   0%

  ── Phase 3: Optimization (Day 61-90) ─────────────────
  [ ] Full feature adoption                    Day 65   --
  [ ] ROI metrics documented                   Day 75   --
  [ ] First QBR scheduled                      Day 80   --
  [ ] Expansion opportunities identified       Day 85   --

  Progress: ░░░░░░░░░░░░░░░░░░░░   0%

----------------------------------------------------------
```

## Milestone management
7. Ask what to update:
   - **Complete a milestone** -- mark as done, record actual date
   - **Add a milestone** -- add custom milestone to the plan
   - **Flag a blocker** -- record what's blocking progress
   - **Update notes** -- add context to a milestone
   - **View full status** -- show detailed progress report

## Feature adoption tracking
8. Track feature adoption if product usage data is available:
```
  Feature Adoption
    Core features:     ████████████████  80%   (4/5 adopted)
    Advanced features: ████              20%   (1/5 adopted)
    Integrations:      ██████████        50%   (2/4 connected)

    Not yet adopted:
      - {Feature 1} -- recommended for their use case
      - {Feature 2} -- drives ROI for similar customers
```

## Training completion
9. Track training status:
```
  Training Status
    {User 1} -- {Role}    ████████████████████  Complete
    {User 2} -- {Role}    ████████████          60%
    {User 3} -- {Role}    ████                  20%
    {User 4} -- {Role}    ░░░░░░░░░░░░░░░░░░░░  Not started
```

## Time-to-value tracking
10. Calculate and display TTV metrics:
```
  Time-to-Value
    Target TTV:   {n} days (segment default: {n})
    Elapsed:      {n} days
    Status:       {On track / At risk / Exceeded}
    First value:  {achieved / not yet}

    Benchmark: Similar customers reach TTV in {n} days avg
```

## Risk detection
11. Flag onboarding risks:
    - Milestone overdue by >5 days
    - Training stalled (no progress in 7 days)
    - Key user not engaged (no login in 7 days)
    - Technical blocker unresolved for >3 days
    - Executive sponsor not involved after kickoff
    - Customer responsiveness declining

12. If risks detected, suggest interventions:
    - Escalate to executive sponsor
    - Schedule hands-on training session
    - Offer technical support engagement
    - Adjust timeline and re-set expectations

## Save and update
13. Save onboarding state to context/onboarding/{customer-name}/tracker.md
14. Update TIMELINE.md with milestone completions
15. Update health score -- onboarding progress affects health
16. If onboarding complete, trigger graduation:
    - Update customer status in CUSTOMERS.md
    - Schedule first regular check-in
    - Set up QBR cadence based on segment

17. Display next steps:
```
  >> Next: Complete milestone "{next milestone}"
     Also: /cs:check-in {ws} {customer}
     Also: /cs:health {ws} {customer}
```
</process>
