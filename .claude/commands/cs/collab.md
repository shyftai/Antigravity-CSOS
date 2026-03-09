---
name: cs:collab
description: Set up or manage collaboration mode (solo/team)
argument-hint: "<action>"
---
<objective>
Manage CS:OS collaboration mode. Set up Supabase connection, check status, invite users,
or sync local data to the shared database.

Action: $ARGUMENTS

Available actions:
- `setup` — Connect Supabase for team mode
- `status` — Check collaboration connection
- `invite` — Invite a team member
- `sync` — Sync local files to Supabase
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/collaboration.md
</execution_context>

<process>

## Action: setup
1. Display mode header: `<< CS:OS // COLLABORATION SETUP >>`
2. Check .env for SUPABASE_URL and SUPABASE_ANON_KEY
3. If missing, show what needs to be added to .env and stop
4. Test connection to Supabase (simple query)
5. Check if CS:OS tables exist (query information_schema)
6. If tables missing, show the migration command:
   `Run supabase/migrations/001_csos_schema.sql in your Supabase SQL editor`
7. If tables exist, update global/COLLABORATION.md to `mode: team`
8. Display connection status:
```
+-------------------------------------------+
|  COLLABORATION — CONNECTED                 |
+-------------------------------------------+
|  Mode:       team                          |
|  Supabase:   connected                     |
|  Tables:     {n} ready                     |
|  Users:      {n} registered                |
|  Workspaces: {n} synced                    |
+-------------------------------------------+
```

## Action: status
1. Display mode header: `<< CS:OS // COLLABORATION STATUS >>`
2. Read global/COLLABORATION.md for current mode
3. If solo: show "Running in solo mode. Run /cs:collab setup to enable team mode."
4. If team: test connection, show status dashboard, show active users per workspace
5. Show sync status:
   - Last sync timestamp
   - Records pending sync
   - Any sync conflicts

## Action: invite
1. Display mode header: `<< CS:OS // INVITE USER >>`
2. Must be in team mode — if solo, redirect to setup
3. Ask for: email, display name, role (cs-lead/csm/support/viewer), workspace(s)
4. Define role permissions:
   - **cs-lead:** Full access, can approve escalations and reports
   - **csm:** Manage assigned customers, run playbooks, create reports
   - **support:** Ticket triage, escalation creation, view customer records
   - **viewer:** Read-only access to dashboards and reports
5. Create user in Supabase auth (or show manual invite link)
6. Add workspace_members entries with role
7. Log in activity_feed

## Action: sync
1. Display mode header: `<< CS:OS // SYNC TO SUPABASE >>`
2. Must be in team mode
3. Ask which workspace to sync (or sync all)
4. Read local files and push to Supabase:
   - Customer records → customers table
   - Health scores → health_scores table
   - Escalations → escalations table
   - Playbook runs → playbook_executions table
   - Tickets → tickets table
   - NPS responses → nps_responses table
5. Show sync summary: records created/updated per table
6. Log sync in activity_feed
7. Display completion:
```
---------------------------------------------------

  Sync complete. {N} records updated.

  >> Next: /cs:status {workspace}

---------------------------------------------------
```

</process>
</output>
