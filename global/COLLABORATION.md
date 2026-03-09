# Collaboration Mode

## Current mode
**Mode:** solo

## Notifications
slack_channel: #csos-alerts
slack_enabled: false
notify_critical: true
notify_important: true
notify_info: false

---

## Solo mode (default)
All state lives in markdown files. No database needed. One CSM per workspace.

## Team mode (optional)
Shared state syncs via Supabase. Requires SUPABASE_URL and SUPABASE_ANON_KEY in .env.

### Enables
- Real-time health score tracking across the CS team
- Shared escalation queue (no double-handling)
- Live renewal pipeline across CSMs
- Handoff coordination between sales and CS
- Approval audit trail (who approved what when)
- Activity feed (who did what when)

### Setup
1. Create a Supabase project
2. Add SUPABASE_URL and SUPABASE_ANON_KEY to .env
3. Run `/cs:collab setup`

### Rules
- **Dual-write:** In team mode, always write to both Supabase AND the local markdown file. Markdown is the cache. Supabase is the source of truth.
- **Fallback:** If Supabase is unreachable, fall back to file-based mode for that operation. Warn the user. Never block work because of a connection issue.
