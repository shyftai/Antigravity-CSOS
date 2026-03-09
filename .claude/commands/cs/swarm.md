---
name: cs:swarm
description: Run CS operations with parallel agent swarm for high-volume work
argument-hint: "<workspace> <operation> [options]"
---
<objective>
Run a CS operation using parallel agent swarms. Orchestrator splits work into batches,
spawns agents, collects results, presents unified output for review.

Operation and workspace: $ARGUMENTS

Available operations:
- `health` — Run health checks across all customers in parallel
- `onboard` — Process multiple customer onboardings
- `check-in` — Prep check-ins for all scheduled customers
- `tickets` — Triage ticket backlog in parallel
- `nps` — Process NPS responses and follow-ups in parallel
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/sla-tiers.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // SWARM >>`
2. Parse operation type from $ARGUMENTS
3. Load workspace context — all source-of-truth files
4. Display workspace header

## Phase 2: Scope the work

Based on operation type, identify the full workload:

**health:**
- Load all customer records from customers/
- Count total customers to health-check
- Display: "{N} customers to health-check across {batches} batches"

**onboard:**
- Load pending onboarding queue
- Count new customers to onboard
- Display: "{N} customers to onboard across {batches} batches"

**check-in:**
- Load check-in schedule from WORKFLOW.md
- Identify all customers due for check-in this week
- Display: "{N} check-ins to prep across {batches} batches"

**tickets:**
- Pull open ticket backlog from support tool
- Count total unprocessed tickets
- Display: "{N} tickets to triage across {batches} batches"

**nps:**
- Pull unprocessed NPS responses
- Count total responses needing follow-up
- Display: "{N} NPS responses to process across {batches} batches"

## Phase 3: Spawn agents

Split workload into batches (10-15 items per batch).

For each batch, spawn an agent with:
```
Agent(
  subagent_type="general-purpose",
  prompt="
    You are a CS:OS swarm agent. Your job is to {operation} for a batch of customers.

    RULES:
    - Draft only — never send messages or update external tools
    - Follow health scoring model exactly
    - Return structured results — one entry per customer
    - Flag anything uncertain as [~] for manual review

    WORKSPACE CONTEXT — read these files:
    - SEGMENTS: {workspace}/SEGMENTS.md
    - HEALTH-MODEL: {workspace}/HEALTH-MODEL.md
    - SLA: {workspace}/SLA.md
    - WORKFLOW: {workspace}/WORKFLOW.md
    {additional context files as needed}

    YOUR BATCH:
    {batch data — customer records, tickets, or NPS responses}

    OUTPUT FORMAT:
    Return a markdown table with one entry per customer/item.
    Include: customer name, action taken, result, flags, recommended next step.
  ",
  description="{operation} batch {N}"
)
```

Display spawning indicator:
```
  << CS:OS // SWARM >>

  Spawning {N} agents...
    [~] Agent 1: customers 1-12
    [~] Agent 2: customers 13-24
    [~] Agent 3: customers 25-36
```

Run agents in parallel where independent. Wait for all to complete.

## Phase 4: Collect and merge results

As each agent completes, update display:
```
    [x] Agent 1: customers 1-12   — 12 complete, 1 flag
    [x] Agent 2: customers 13-24  — 11 complete, 2 flags
    [~] Agent 3: customers 25-36
```

When all complete, merge results into unified output.

Display swarm results summary:
```
  +-- SWARM RESULTS -------------------------------+
  |                                                 |
  |  Agents spawned:     {N}                        |
  |  Items processed:    {total}                    |
  |  Completed:          {count}                    |
  |  Flagged:            {count} (need review)      |
  |  Errors:             {count}                    |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 5: Review and act

1. Show flagged items first — these need manual review
2. Show summary of results by priority:
   - Critical items (escalations, SLA breaches, churn risk)
   - Action items (follow-ups needed, playbooks to trigger)
   - Informational (healthy customers, resolved items)
3. After review:
```
  >> Options:
     1. Review all {N} results individually
     2. Approve clean results, review flagged only
     3. Export all to reports/ for offline review
```

## Phase 6: Save and log

- Save results to appropriate locations (health scores, check-in notes, ticket triage, etc.)
- Log swarm run in logs/decisions.md:
  - Date, operation type, agent count, batch sizes
  - Items processed, flags raised
- Display next action:
```
---------------------------------------------------

  >> Next: {context-appropriate suggestion}

---------------------------------------------------
```

</process>
</output>
