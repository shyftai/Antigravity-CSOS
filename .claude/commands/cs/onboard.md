---
name: cs:onboard
description: Onboard a new customer success workspace with structured intake interview
argument-hint: "<workspace-name>"
---
<objective>
Onboard a new CS workspace through a structured intake interview. Create the folder structure, ask questions in blocks, and populate all source-of-truth files.

Workspace name: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/onboarding-guide.md
</execution_context>

<process>
1. Display the CS:OS startup banner from CSOS.md
2. Display mode header: `<< CS:OS // ONBOARDING >>`
3. Create workspace folder by copying _template/ to workspaces/$ARGUMENTS/

## Block 0 -- Role selection (always first)
4. Ask: "What's your role?"
   - **CSM** -- I manage a book of business, run QBRs, and handle renewals
   - **CS Lead/Manager** -- I oversee a CS team and need portfolio visibility
   - **Head of CS** -- I need strategy, forecasting, and team performance
   - **Founder** -- I'm doing CS myself, just get me running
   - **CS Ops** -- I build processes, automation, and reporting infrastructure
5. Save role to workspace.config.md
6. Adjust onboarding path based on role

## Collaboration mode (after role)
7. Ask: "Are you working solo or with a team?"
   - **Solo** (default) -- everything stays in local files, no setup needed
   - **Team** -- shared state via Supabase: real-time health scores, shared escalation queue, live renewal pipeline, handoff coordination, activity feed

   Role-based defaults:
   - **CSM** -- ask (depends on team size)
   - **CS Lead/Manager** -- suggest team mode (needs visibility into CSM activities)
   - **Head of CS** -- strongly suggest team mode (portfolio-wide visibility required)
   - **Founder** -- default solo (unless they have a CS team)
   - **CS Ops** -- suggest team mode (building infrastructure for the team)

   If **Team** selected:
   a. Check .env for SUPABASE_URL, SUPABASE_ANON_KEY, SUPABASE_SERVICE_KEY
   b. If keys present -- test connection, confirm tables exist, set mode to `team` in COLLABORATION.md
   c. If keys missing -- show setup steps:
      ```
      1. Create a free Supabase project at supabase.com
      2. Run the migration: supabase/migrations/001_initial_schema.sql
      3. Copy your project URL and keys to .env
      4. Run /cs:collab setup to connect
      ```
   d. Ask: "Want to set this up now or skip and add it later?"
   e. If skip -- set mode to `solo`, note in workspace.config.md that team mode is pending

   If **Solo** selected:
   - Set mode to `solo` in COLLABORATION.md
   - Skip Supabase setup entirely

## Execution mode (after collaboration)
8. Ask: "How should I handle approvals?"
   - **Interactive** (default) -- I'll confirm each major decision before proceeding
   - **Auto** -- I'll auto-approve and keep moving. Only stops for customer-facing communications, contract changes, escalations to leadership, pricing/discount approvals, and account reassignment.

   Role-based defaults:
   - **CSM** -- default interactive (customer-facing work needs precision)
   - **CS Lead/Manager** -- suggest auto (needs efficiency across portfolio)
   - **Head of CS** -- default interactive (strategic decisions)
   - **Founder** -- suggest auto (they want to move fast)
   - **CS Ops** -- default interactive (process design needs review)

   Save to workspace.config.md as `**Execution mode:** auto` or `**Execution mode:** interactive`

9. Ask if they want Slack notifications (works in both modes if Slack MCP connected):
   - If Slack MCP detected -- "Want alerts for at-risk customers, renewals due, escalations, and NPS detractors in Slack?"
   - If not detected -- skip

## Block 1 -- Product and customer success definition
10. Ask: "What product/service do your customers use? What does success look like for them?"
    - Product name, type, and core value proposition
    - What outcome means a customer is "successful"
    - Key activation events (what makes a customer sticky)
    Save to workspace.config.md

## Block 2 -- Customer segments
11. Ask: "How are your customers segmented?"
    - Segment tiers: Enterprise, Mid-Market, SMB, or custom tiers
    - ARR ranges per segment
    - Customer count per segment
    - Service level differences (touch model per tier)
    Save to SEGMENTS.md

## Block 3 -- Current customer roster
12. Ask: "Tell me about your current customers"
    - Top 10-20 customers with: name, segment, ARR, renewal date, health (gut feel), CSM owner
    - Or import from CSV/CRM if available
    Save to CUSTOMERS.md

## Block 4 -- Health scoring model
13. Ask: "What are your key health indicators?"
    - Product usage (login frequency, feature adoption, DAU/MAU)
    - Engagement (meeting attendance, email responsiveness, champion activity)
    - Support (ticket volume, severity, resolution satisfaction)
    - Business (contract value trend, expansion history, payment status)
    - Custom dimensions (industry-specific metrics)
    - If unsure, use defaults from health-scoring.md
    Save to HEALTH-SCORES.md

## Block 5 -- Onboarding process
14. Ask: "What does your onboarding process look like today?"
    - Standard onboarding milestones and timeline
    - Time-to-value target (days from signed contract to first value)
    - Training requirements and completion criteria
    - Technical setup steps
    - Go-live criteria
    Save to ONBOARDING.md

## Block 6 -- Playbooks
15. Ask: "What playbooks do you run today?"
    - Onboarding playbook (steps, timeline, success criteria)
    - At-risk/save playbook (triggers, interventions, escalation path)
    - Expansion playbook (signals, qualification, approach)
    - QBR playbook (frequency, format, content)
    - Renewal playbook (timeline, process, negotiation)
    - If unsure, use defaults from playbooks.md
    Save to PLAYBOOKS.md

## Block 7 -- Tools and integrations
16. Ask: "What tools do you use for customer success?"
    - CRM (HubSpot, Salesforce, Attio)
    - CS platform (Gainsight, Vitally, ChurnZero, Totango)
    - Support (Zendesk, Intercom, Freshdesk)
    - Billing (Stripe, Chargebee, Recurly)
    - Communication (Slack, email)
    - Analytics (Mixpanel, Amplitude, Pendo)
    Save to workspace.config.md tools section

## Block 8 -- Metrics and targets
17. Ask: "What are your CS KPIs and targets?"
    - GRR (Gross Revenue Retention) target
    - NRR (Net Revenue Retention) target
    - NPS target
    - Churn rate target
    - Time-to-value target
    - Expansion revenue target
    - If unsure, use industry defaults from BENCHMARKS.md
    Save to METRICS.md

## Block 9 -- Churn and risk
18. Ask: "What are the most common reasons customers churn?"
    - Top churn reasons (rank ordered)
    - Known churn signals (what precedes churn)
    - Current save rate (% of at-risk customers retained)
    - Escalation process (who gets involved, when)
    Save to PLAYBOOKS.md churn section

## Finalize
19. For any field the user skips or doesn't know yet, use defaults from defaults.md
20. Write all answers into respective files
21. Check .env for required API keys and MCP servers
22. If team mode: run initial sync to Supabase
23. Display workspace header with loaded context

## Role-based next steps
24. Suggest next actions based on role:

**CSM:**
- `/cs:today $ARGUMENTS` -- see what needs attention today
- `/cs:health $ARGUMENTS` -- run health check on your portfolio
- `/cs:at-risk $ARGUMENTS` -- identify at-risk customers

**CS Lead/Manager:**
- `/cs:dashboard $ARGUMENTS` -- portfolio overview
- `/cs:metrics $ARGUMENTS` -- team performance metrics
- `/cs:at-risk $ARGUMENTS` -- at-risk customers across team

**Head of CS:**
- `/cs:dashboard $ARGUMENTS` -- strategic overview
- `/cs:metrics $ARGUMENTS` -- CS organization metrics
- `/cs:report $ARGUMENTS` -- board-ready CS report

**Founder:**
- `/cs:today $ARGUMENTS` -- daily briefing
- `/cs:health $ARGUMENTS` -- quick health check
- `/cs:dashboard $ARGUMENTS` -- see everything at a glance

**CS Ops:**
- `/cs:segments $ARGUMENTS` -- refine segmentation
- `/cs:playbook $ARGUMENTS` -- build playbooks
- `/cs:metrics $ARGUMENTS` -- set up reporting
</process>
