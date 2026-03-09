---
name: cs:check-in
description: Customer check-in prep -- contact history, tickets, usage trends, agenda, talking points
argument-hint: "<workspace-name> <customer-name>"
---
<objective>
Prepare for a regular customer check-in. Load contact history, recent support tickets, usage trends, prepare an agenda, and suggest talking points.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // CHECK-IN PREP >>`
2. Parse workspace and customer from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, HEALTH-SCORES.md, TIMELINE.md, SEGMENTS.md
4. Run quality gates before proceeding

## Customer context snapshot
5. Display current state:
```
+----------------------------------------------------------+
|  CHECK-IN PREP -- {Customer Name}                         |
+----------------------------------------------------------+

  Health: {score}/100 ({status})    ARR: ${value}
  Segment: {tier}    Renewal: {date} ({n} days)
  Last check-in: {date} ({n} days ago)
  Cadence: {frequency} (segment default: {default})

  Key contacts:
    {Name} -- {Title} (Champion)      Last contact: {date}
    {Name} -- {Title} (Exec sponsor)  Last contact: {date}
    {Name} -- {Title} (Technical)     Last contact: {date}
```

## Recent history review
6. Pull recent activity:
```
  Recent Timeline (last 30 days)
    {date}  {event type}  {description}
    {date}  {event type}  {description}
    {date}  {event type}  {description}

  Support Tickets (open / recent)
    #{id}  {subject}    Status: {open/resolved}    CSAT: {score}
    #{id}  {subject}    Status: {open/resolved}    CSAT: {score}

  Usage Trends
    Logins:          {trend} ({change}% vs last period)
    Feature usage:   {trend} ({key features})
    Active users:    {count} of {total} ({pct}%)
```

## Previous check-in action items
7. Pull action items from last check-in:
```
  Previous Action Items
    [x] {Item 1} -- completed {date}
    [x] {Item 2} -- completed {date}
    [ ] {Item 3} -- still open (assigned: {owner})
    [ ] {Item 4} -- overdue by {n} days
```

## Generate check-in agenda
8. Build agenda based on customer state:
```
  Suggested Agenda (30 min)

  1. Relationship check (5 min)
     - How are things going? Any changes on your end?
     - Open items from last meeting

  2. Usage review (5 min)
     - {Usage trend observation -- positive or concern}
     - Feature spotlight: {underused feature relevant to them}

  3. Support review (5 min)
     - {Open ticket status if any}
     - {Resolved issues acknowledgment}
     - Any unlogged concerns?

  4. Roadmap preview (5 min)
     - {Upcoming features relevant to them}
     - {Beta invitations if applicable}

  5. Strategic alignment (5 min)
     - {Connect to their business goals}
     - {Upcoming milestones or events}

  6. Next steps and action items (5 min)
     - {Proposed actions}
     - Schedule next check-in
```

## Talking points
9. Generate context-aware talking points:

**If health is GREEN:**
- Lead with value recognition
- Explore expansion opportunities
- Ask about new team members or use cases
- Request feedback for roadmap

**If health is YELLOW:**
- Acknowledge any known issues upfront
- Focus on resolution and support
- Ask about unstated concerns
- Reinforce commitment to their success

**If health is RED:**
- This should be a save conversation, not a check-in
- Suggest `/cs:save {ws} {customer}` instead
- If proceeding: focus entirely on issue resolution

**If renewal within 90 days:**
- Include renewal conversation prep
- Review contract terms and usage
- Begin expansion/renewal discussion

**If NPS detractor:**
- Address detractor feedback directly
- Show actions taken since their feedback
- Ask what would change their score

10. Flag topics to avoid:
    - Don't discuss expansion if health is below 80
    - Don't ignore open escalations
    - Don't bring up competitor topics unless customer raised them
    - Don't over-promise on roadmap

## Save and track
11. Save check-in prep to context/check-ins/{customer-name}-{date}.md
12. After the meeting, prompt for:
    - Meeting notes summary
    - Action items with owners
    - Next check-in date
    - Health score adjustment (better/worse/same)
13. Update TIMELINE.md with check-in event
14. Update HEALTH-SCORES.md if engagement data changed

15. Display:
```
  Check-in prep saved: context/check-ins/{file}

  >> After the meeting:
     Update notes: /cs:check-in {ws} {customer} --notes
     Log timeline: automatically recorded

  >> Also: /cs:health {ws} {customer}
     Also: /cs:qbr {ws} {customer} (if QBR due soon)
```
</process>
