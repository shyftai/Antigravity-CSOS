---
name: cs:status
description: Show workspace status and available commands
argument-hint: "[workspace-name]"
---
<objective>
Display the CS:OS banner, workspace status, and available commands.

Workspace: $ARGUMENTS (optional — if omitted, list all workspaces)
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
</execution_context>

<process>
1. Display the CS:OS startup banner

2. If no workspace specified:
   - List all workspaces in workspaces/ with name, status, customer count, and total ARR
   - Prompt: `>> Which workspace?`

3. If workspace specified:
   - Load workspace context
   - Display workspace header from ui-brand.md
   - Show loaded sources of truth: [x] for populated, [ ] for empty
     - SEGMENTS.md, PLAYBOOKS, HEALTH-MODEL.md, SLA.md
     - TOOLS.md, WORKFLOW.md, COSTS.md
     - workspace.config.md
   - Show customer portfolio summary:
     - Total customers, total ARR
     - Health distribution (healthy/neutral/at-risk/critical)
     - Upcoming renewals (next 30/60/90 days)
   - Show execution mode: interactive or auto (with indicator)
   - Show tool connection status: [x] for key present, [ ] for missing
   - Show active escalations and SLA breaches (if any)

4. Display available commands:

```
---------------------------------------------------

  CS:OS Commands

  Setup
    /cs:onboard        Onboard a new customer
    /cs:switch         Switch active workspace
    /cs:status         Show this command list
    /cs:collab         Collaboration setup (solo/team)

  Customer Management
    /cs:health         Customer health check and scoring
    /cs:check-in       Prep and run customer check-ins
    /cs:qbr            Quarterly business review prep
    /cs:timeline       Full customer journey timeline
    /cs:renewal        Renewal management and forecasting
    /cs:expansion      Expansion opportunity identification

  Support
    /cs:tickets        Ticket triage and SLA tracking
    /cs:escalation     Escalation management

  Strategy
    /cs:segments       Customer segmentation engine
    /cs:playbook       Success playbook management
    /cs:risk           At-risk customer identification

  Growth
    /cs:advocacy       Customer advocacy program
    /cs:referral       Referral program management
    /cs:nps            NPS survey and follow-up

  Reporting
    /cs:metrics        CS metrics dashboard
    /cs:report         Generate CS reports
    /cs:debrief        Post-churn/win/save analysis

  Feedback
    /cs:feedback       Submit feedback or report a bug

  Swarm (parallel agents)
    /cs:swarm health       Health checks across all customers
    /cs:swarm onboard      Process multiple onboardings
    /cs:swarm check-in     Prep check-ins for all scheduled
    /cs:swarm tickets      Triage ticket backlog in parallel
    /cs:swarm nps          Process NPS responses in parallel

---------------------------------------------------
```
</process>
</output>
