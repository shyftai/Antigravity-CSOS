<ui_patterns>

Visual patterns for user-facing CS:OS output. All commands @-reference this file.

## Brand Color

CS:OS brand color is **blue** (ANSI 75).
- Use `\033[38;5;75m` to set blue text, `\033[0m` to reset
- Apply blue to: the CS:OS block-letter banner, mode headers (`<< CS:OS // MODE >>`), section titles in dashboards
- Use white/default for: body text, data values, box borders
- If terminal doesn't support color, display everything in plain white
- Never use orange (208/GTM:OS), teal (43/CONTENT:OS), green (34/FINANCE:OS), coral (203/HR:OS), violet (141/INVESTOR:OS), cyan (117/COMMUNITY:OS), or gold (220/FOUNDER:OS) as brand colors — those belong to other OS frameworks

## Startup Banner

Display once when CS:OS loads. Render the block letters in blue.

```
 ██████╗███████╗ ██╗  ██████╗ ███████╗
██╔════╝██╔════╝ ╚═╝ ██╔═══██╗██╔════╝
██║     ███████╗     ██║   ██║███████╗
██║     ╚════██║ ██╗ ██║   ██║╚════██║
╚██████╗███████║ ╚═╝ ╚██████╔╝███████║
 ╚═════╝╚══════╝      ╚═════╝ ╚══════╝
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  C S : O S
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Mode Headers

Use for workflow transitions. CS:OS uses angle brackets.

```
<< CS:OS // {MODE NAME} >>
```

**Mode names (uppercase, rendered in blue):**
- `ONBOARDING`
- `KICKOFF`
- `HEALTH CHECK`
- `QBR PREP`
- `RENEWAL`
- `AT-RISK`
- `SAVE PLAY`
- `UPSELL`
- `ADVOCACY`
- `SEGMENTATION`
- `TICKET TRIAGE`
- `ESCALATION`
- `HANDOFF`
- `CHECK-IN`
- `NPS`
- `METRICS`
- `TIMELINE`
- `PLAYBOOK`
- `REPORT`
- `DEBRIEF`
- `DASHBOARD`
- `FEEDBACK`

---

## Workspace Header

Show after loading a workspace. Always displayed before any task.

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  CUSTOMER:  {Name}                                          ┃
┃  SEGMENT:   {Enterprise / Mid-market / SMB}                 ┃
┃  HEALTH:    {score}/100    ARR: ${n}    RENEWAL: {date}     ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

---

## Approval Gates

When human decision is needed. Uses double borders.

**Interactive mode:**
```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  APPROVAL REQUIRED                                          ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛

{What is being approved}

>> Approve / Edit / Reject
```

**Auto mode:** Skip the gate — auto-approve and continue. Show a one-line confirmation instead:
```
>> Auto-approved: {what was approved}
```
Log the auto-approval in `logs/decisions.md` with timestamp and what was approved.

**Hard gates (always stop, even in auto mode):**
- Contract changes — always requires explicit approval
- Customer-facing communications — always requires explicit approval
- Escalations to leadership — always requires explicit approval
- Pricing/discount approvals — always requires explicit approval
- Account reassignment — always requires explicit approval

Hard gates always use the full approval gate format above, regardless of execution mode.

---

## Quality Gates

Run before every output. Compact inline format.

```
  -- QUALITY GATES -----------------------------------------
  [x] Health    [x] Segment    [x] Timeline
  [x] Playbook  [x] Risk       [x] NPS
  ---------------------------------------------------------
```

If a gate fails:
```
  -- QUALITY GATES -----------------------------------------
  [x] Health    [x] Segment    [ ] Timeline
  [x] Playbook  [x] Risk       [x] NPS
  ---------------------------------------------------------
  !! Timeline: renewal is 45 days out but no renewal playbook started
```

---

## Status Symbols

```
[x]  Passed / Complete
[ ]  Failed / Missing
[~]  Borderline / Needs review
>>   Action prompt — waiting for human input
!!   Warning or flag
--   Skipped / Not applicable
```

---

## Health Dashboard

Per-customer view:
```
  +- CUSTOMER HEALTH --------------------------------------+
  |                                                        |
  |  Product Usage     [GREEN]  Score: 85  DAU: 72%        |
  |  Support Health    [GREEN]  Score: 90  CSAT: 4.6       |
  |  Engagement        [AMBER]  Score: 65  Last: 12d ago   |
  |  Business Outcomes [GREEN]  Score: 82  ROI: 3.2x       |
  |  Relationship      [AMBER]  Score: 68  NPS: 7          |
  |                                                        |
  |  Overall: HEALTHY (78/100)                             |
  +--------------------------------------------------------+
```

Portfolio view:
```
  +- PORTFOLIO HEALTH -------------------------------------+
  |                                                        |
  |  Healthy (80+)     42 accounts   ████████████░░  68%   |
  |  Stable (60-79)    12 accounts   ████░░░░░░░░░░  19%   |
  |  At-risk (40-59)    6 accounts   ██░░░░░░░░░░░░  10%   |
  |  Critical (0-39)    2 accounts   █░░░░░░░░░░░░░   3%   |
  |                                                        |
  |  Portfolio avg: 76/100    ARR at risk: $240K           |
  +--------------------------------------------------------+
```

---

## At-Risk Display

```
  +- AT-RISK ACCOUNTS -------------------------------------+
  |                                                        |
  |  CRITICAL  2 accounts -- action today                  |
  |    Acme Corp        ARR: $120K  Health: 28  Renewal: 30d  |
  |    Beta Inc         ARR: $85K   Health: 35  Renewal: 45d  |
  |                                                        |
  |  HIGH      4 accounts -- action this week              |
  |  MEDIUM    6 accounts -- monitor                       |
  |                                                        |
  |  Total at risk: 12 of 62 (19.4%)                      |
  |  ARR at risk: $840K of $4.2M (20%)                    |
  +--------------------------------------------------------+
```

---

## Next Action Block

Always at end of a completed workflow.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  >> Next: {suggested next command}
     Also: {alternative command}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Escalation Display

```
  +- ESCALATION -------------------------------------------+
  |  Account:   {customer name}                            |
  |  Severity:  {CRITICAL / HIGH / MEDIUM / LOW}           |
  |  Issue:     {description}                              |
  |  Impact:    ARR: ${amount}  Health: {score}            |
  |                                                        |
  |  Escalation path:                                      |
  |    1. CSM action: {immediate step}                     |
  |    2. Manager review: {if needed}                      |
  |    3. Exec sponsor: {if critical}                      |
  |                                                        |
  |  Deadline: {response SLA}                              |
  +--------------------------------------------------------+
  >> Approve escalation? (y/n)
```

---

## Anti-Patterns -- What CS:OS never does

- Never use `GSD` prefix -- that is GSD's brand
- Never use orange color (ANSI 208) -- that is GTM:OS
- Never use teal (ANSI 43) -- that is CONTENT:OS
- Never use green (ANSI 34) -- that is FINANCE:OS
- Never use coral (ANSI 203) -- that is HR:OS
- Never use violet (ANSI 141) -- that is INVESTOR:OS
- Never use cyan (ANSI 117) -- that is COMMUNITY:OS
- Never use gold (ANSI 220) -- that is FOUNDER:OS
- Never use random emoji (no rockets, sparkles, stars)
- Never use `◆ ○` status dots -- CS:OS uses `[x] [ ] [~]`
- Never vary box widths within the same output
- Never skip the quality gate display on customer-facing output

</ui_patterns>
