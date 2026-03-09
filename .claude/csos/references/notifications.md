# Notifications -- CS:OS

CS:OS can send Slack notifications for critical events using the Slack MCP integration. This is optional -- if Slack MCP is not connected, notifications are displayed inline only.

---

## Setup

1. Ensure Slack MCP is connected in Claude Code
2. Set the notification channel in `global/COLLABORATION.md`:
   ```
   ## Notifications
   slack_channel: #csos-alerts
   slack_enabled: true
   ```
3. Optionally set per-workspace channels in `workspace.config.md`:
   ```
   slack_channel: #customer-name-alerts
   ```

---

## Notification triggers

### Critical (always notify if Slack is connected)

| Event | Message format |
|-------|---------------|
| Churn risk detected | `[{workspace}] CHURN RISK: {customer} -- health dropped to {score}, {signal detected}` |
| Escalation needed | `[{workspace}] ESCALATION: {customer} -- {issue} -- severity: {level}` |
| Renewal at risk | `[{workspace}] RENEWAL RISK: {customer} -- ARR: ${amount} -- {days} days to renewal -- health: {score}` |
| Critical ticket unresolved | `[{workspace}] CRITICAL TICKET: {customer} -- open {days} days -- SLA breached` |
| Champion departure detected | `[{workspace}] CHAMPION LOSS: {customer} -- {name} has left -- immediate action needed` |

### Important (notify during active management)

| Event | Message format |
|-------|---------------|
| Health score drop | `[{workspace}] HEALTH DROP: {customer} -- {old_score} > {new_score} -- top factor: {dimension}` |
| NPS detractor received | `[{workspace}] NPS DETRACTOR: {customer} -- score: {score} -- "{comment preview...}"` |
| QBR due | `[{workspace}] QBR DUE: {customer} -- scheduled for {date} -- prep deadline: {date}` |
| Renewal process start | `[{workspace}] RENEWAL START: {customer} -- ARR: ${amount} -- {days} days to renewal` |
| Usage decline detected | `[{workspace}] USAGE DECLINE: {customer} -- {metric} down {pct}% over {period}` |

### Informational (optional -- enable per workspace)

| Event | Message format |
|-------|---------------|
| Check-in completed | `[{workspace}] CHECK-IN: {customer} -- completed -- next: {date}` |
| Onboarding milestone | `[{workspace}] ONBOARDING: {customer} -- milestone: {milestone} -- day {n}` |
| Expansion opportunity | `[{workspace}] EXPANSION: {customer} -- {type} -- est. value: ${amount}` |
| NPS promoter received | `[{workspace}] NPS PROMOTER: {customer} -- score: {score} -- advocacy candidate` |
| Health score improvement | `[{workspace}] HEALTH UP: {customer} -- {old_score} > {new_score} -- moved to {tier}` |

---

## How to send

When a notification trigger fires:

1. Check if `slack_enabled: true` in COLLABORATION.md
2. Determine the correct channel (workspace-specific or global)
3. Send via Slack MCP: `mcp__claude_ai_Slack__slack_send_message`
4. Format: plain text, no markdown formatting, keep under 200 characters
5. If Slack MCP is not available, display the notification inline with `!!` prefix

---

## User control

Users can configure notifications during onboarding or at any time:
- `slack_enabled: true/false` -- master toggle
- `notify_critical: true` -- churn risk, escalations, renewal risk
- `notify_important: true` -- health drops, NPS detractors, QBR due
- `notify_info: false` -- check-ins, milestones, expansion opportunities

Default: critical only.
