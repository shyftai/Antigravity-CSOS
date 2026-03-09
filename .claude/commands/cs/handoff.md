---
name: cs:handoff
description: Sales to CS handoff -- receive deal context, map stakeholders, create customer record, trigger kickoff
argument-hint: "<workspace-name> <customer-name>"
---
<objective>
Execute a structured Sales-to-CS handoff. Receive deal context from the sales team or CRM, capture key stakeholders, success criteria, deal history, create the customer record, and trigger the kickoff workflow.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/onboarding-guide.md
@./.claude/csos/references/playbooks.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // HANDOFF >>`
2. Parse workspace and customer name from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, SEGMENTS.md, ONBOARDING.md

## Receive deal context
4. Check for incoming handoff data:
   - CRM record (HubSpot, Salesforce, Attio) via API if connected
   - GTM:OS handoff document if cross-OS handoff (context/handoffs/)
   - Manual intake if no automated source

5. If no automated data, run structured intake:
   Ask one block at a time:

**Block 1 -- Deal basics:**
- Company name and website
- Contract value (ARR/MRR)
- Contract term (months)
- Start date and renewal date
- Payment terms
- Plan/tier purchased

**Block 2 -- Why they bought:**
- Primary problem they're solving
- What success looks like (their words)
- Key evaluation criteria that won the deal
- Competitive alternatives they considered
- What made them choose us

**Block 3 -- Key stakeholders:**
- Executive sponsor (name, title, email)
- Champion / day-to-day contact (name, title, email)
- Technical lead (name, title, email)
- End users (names, roles)
- Decision maker for renewal
- Communication preferences per person

**Block 4 -- Deal history:**
- How long was the sales cycle?
- Key meetings and what was discussed
- Demos or trials completed
- Objections raised and how they were handled
- Promises or commitments made by sales
- Custom terms or special agreements

**Block 5 -- Risks and context:**
- Any concerns raised during evaluation
- Competing initiatives or priorities
- Technical constraints or requirements
- Integrations needed
- Timeline pressure or deadlines
- Political dynamics (supporters vs skeptics)

## Build handoff document
6. Generate the handoff record:
```
+----------------------------------------------------------+
|  HANDOFF -- {Customer Name}                               |
+----------------------------------------------------------+

  Company
    {Company Name}    {Industry}    {Size} employees
    Website: {url}
    Location: {timezone/region}

  Contract
    ARR: ${value}    Term: {months} months
    Plan: {tier}     Start: {date}    Renewal: {date}
    Special terms: {any custom agreements}

  ──────────────────────────────────────────────────────

  Why they bought
    Problem: {primary problem}
    Success criteria: {what success looks like}
    Winning factor: {why they chose us}
    Competitive context: {who else they evaluated}

  ──────────────────────────────────────────────────────

  Stakeholders
    Executive sponsor: {Name} -- {Title}
      {email} | {communication preference}
      Involvement level: {high/medium/low}

    Champion: {Name} -- {Title}
      {email} | {communication preference}
      Internal influence: {high/medium/low}

    Technical lead: {Name} -- {Title}
      {email} | {communication preference}

    End users: {count} planned
      {Names and roles if known}

  ──────────────────────────────────────────────────────

  Sales history
    Cycle length: {days}
    Key milestones:
      {date}  {event}
      {date}  {event}
      {date}  {event}

    Promises made:
      - {promise 1}
      - {promise 2}

    Concerns raised:
      - {concern 1}
      - {concern 2}

  ──────────────────────────────────────────────────────

  Onboarding context
    Technical requirements: {integrations, data migration, setup}
    Timeline expectations: {when they expect to be live}
    Training needs: {who needs training, complexity level}
    Known risks: {anything that could slow onboarding}

  ──────────────────────────────────────────────────────

  Recommended approach
    Segment: {suggested tier based on ARR and size}
    Onboarding type: {standard / accelerated / white-glove}
    Check-in cadence: {suggested frequency}
    First QBR: {suggested date}
    Key risk to watch: {highest priority concern}

----------------------------------------------------------
```

## Create customer record
7. Create or update customer entry in CUSTOMERS.md:
   - Company name, segment, ARR, contract dates
   - Key contacts with roles
   - Success criteria
   - Notes from handoff

8. Determine segment assignment:
   - Match against SEGMENTS.md criteria
   - Consider ARR, company size, strategic importance
   - Assign appropriate service level

## Set up tracking
9. Initialize customer tracking:
   - Set initial health score based on segment defaults (new customer baseline)
   - Create timeline entry for handoff received
   - Add to renewal tracking in RENEWALS.md
   - Create onboarding tracker stub

10. Flag promises and risks:
    - Add sales promises to customer record (these MUST be honored)
    - Add known risks to watchlist
    - If any promises seem unrealistic, flag for CSM review

## Trigger kickoff
11. Prepare for kickoff:
```
  Handoff complete. Customer record created.

  ── Handoff Quality Check ────────────────────────────
  [x] Contract details captured
  [x] Stakeholders mapped
  [x] Success criteria defined
  [x] Deal history documented
  [{check}] Risks identified and flagged
  [{check}] Promises documented for tracking

  Missing information:
    {list any gaps that need follow-up with sales}
  ─────────────────────────────────────────────────────
```

## Save and distribute
12. Save handoff document to context/handoffs/{customer-name}-handoff-{date}.md
13. Update TIMELINE.md
14. If team mode: sync to Supabase, notify assigned CSM
15. If Slack connected: offer to share handoff in CS channel

16. Display:
```
  Handoff saved: context/handoffs/{file}
  Customer added to CUSTOMERS.md
  Segment: {tier}    Health: {initial score}

  >> Next: /cs:kickoff {ws} {customer}
     Schedule kickoff within 48 hours of contract start.

     Also: /cs:onboard-customer {ws} {customer}
     Also: /cs:health {ws} {customer}
```
</process>
