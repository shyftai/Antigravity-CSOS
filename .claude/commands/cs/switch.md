---
name: cs:switch
description: Switch active workspace and reload all context
argument-hint: "<workspace-name>"
---
<objective>
Switch to a different workspace. Unload current context, load new workspace, display summary.

Workspace: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // SWITCHING >>`
2. Confirm the target workspace exists in workspaces/
3. If not found, list available workspaces and prompt for selection
4. Load all source-of-truth files from the new workspace:
   - SEGMENTS.md, HEALTH-MODEL.md, SLA.md
   - TOOLS.md, WORKFLOW.md, COSTS.md
   - workspace.config.md
   - customers/ directory (index all customer records)
   - context/INDEX.md (then read priority files)
5. Check .env for active tool API keys
6. Display workspace header:
```
+----------------------------------------------------------+
|  WORKSPACE: {Name}                                        |
|  CUSTOMERS: {N}            ARR: ${total}                  |
|  STATUS:    {active/paused}  TOOLS: {tool list}           |
+----------------------------------------------------------+
```
7. Show context summary:
   - Customer portfolio size and health distribution
   - Upcoming renewals (next 30 days)
   - Open escalations
   - Active playbook executions
   - CSM assignments
   - Tool connections ready
   - Any missing keys or configuration gaps

8. Confirm: `>> Ready. What would you like to do?`
</process>
</output>
