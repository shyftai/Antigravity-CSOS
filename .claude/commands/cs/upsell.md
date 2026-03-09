---
name: cs:upsell
description: Expansion opportunity detection and execution -- signals, business case, guided conversation
argument-hint: "<workspace-name> <customer-name>"
---
<objective>
Detect and execute expansion opportunities. Verify health prerequisites, identify expansion signals, prepare business case, and guide the upsell conversation.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/defaults.md
@./.claude/csos/references/health-scoring.md
@./.claude/csos/references/BENCHMARKS.md
@./.claude/csos/references/playbooks.md
</execution_context>

<process>
1. Display mode header: `<< CS:OS // EXPANSION >>`
2. Parse workspace and customer from $ARGUMENTS
3. Load workspace context -- CUSTOMERS.md, HEALTH-SCORES.md, EXPANSION.md, METRICS.md, TIMELINE.md
4. Load playbooks for expansion process

## Health gate (mandatory)
5. Check customer health score before proceeding:
   - If health >= 80: proceed with expansion
   - If health 60-79: warn -- "Customer health is {score}. Address issues before expansion."
     - Show what needs fixing first
     - Suggest `/cs:health {ws} {customer}` to investigate
     - Ask CSM to confirm they want to proceed despite warning
   - If health < 60: BLOCK -- "Cannot pursue expansion. Customer health is {score} (RED)."
     - Redirect to `/cs:save {ws} {customer}`
     - Do not proceed under any circumstances

```
  ── HEALTH GATE ──────────────────────────────────────
  Health: {score}/100    Status: {GREEN/YELLOW/RED}

  {PASS: Proceeding with expansion analysis}
  {WARN: Health below threshold -- review before proceeding}
  {BLOCK: Health too low -- fix customer experience first}
  ─────────────────────────────────────────────────────
```

## Expansion signal detection
6. Scan for expansion indicators:

**Usage signals:**
- Approaching or exceeding contracted usage limits
- Team using product more broadly (new departments, use cases)
- Power users requesting advanced features
- API usage growing consistently
- Feature requests that map to higher-tier plans

**Business signals:**
- Company growing (hiring, funding, new offices)
- Team expanding (more potential users)
- New initiatives that align with product value
- Budget cycle timing favorable
- Positive ROI demonstrated

**Engagement signals:**
- Champion advocating internally
- Multiple stakeholders actively engaged
- Attending webinars, community events
- Requesting roadmap briefings
- Referring other teams to the product

**Timing signals:**
- Contract renewal approaching (bundle with renewal)
- Recently completed successful QBR
- Just achieved a major milestone
- New fiscal year/budget cycle
- Competitor contract expiring

7. Display signal assessment:
```
+----------------------------------------------------------+
|  EXPANSION ANALYSIS -- {Customer Name}                    |
+----------------------------------------------------------+

  Health: {score}    ARR: ${current}    Segment: {tier}

  Expansion Signals Detected
    ++ Usage at 95% of contracted limit        Strength: HIGH
    ++ Team grew from 15 to 28 employees       Strength: HIGH
    ++ Champion requested advanced features    Strength: MEDIUM
    ++ Positive ROI confirmed in last QBR      Strength: HIGH
    .. Budget cycle starts next month          Timing: GOOD

  Expansion Opportunity Score: {score}/100
```

## Business case preparation
8. Build the expansion business case:
```
  Business Case
    Current state:
      Plan: {current plan/tier}
      ARR:  ${current}
      Users: {current} of {contracted}

    Proposed expansion:
      Plan: {recommended plan/tier}
      ARR:  ${proposed}  (+${increase}, +{pct}%)
      Users: {proposed}
      New features: {list}

    ROI justification:
      Current ROI: {metrics from QBR/health data}
      Projected ROI with expansion: {projection}
      Payback period: {estimate}

    Competitive context:
      Alternative cost: ${competitor pricing if known}
      Switching cost: {high/medium/low}
```

## Conversation guide
9. Prepare the expansion conversation:

**Opening:**
- Reference recent success: "Since implementing {feature}, your team has {outcome}"
- Connect to their goals: "You mentioned wanting to {goal} -- here's how we can help"

**Discovery questions:**
- "How is the current solution working for the broader team?"
- "Are there other departments that could benefit?"
- "What capabilities would make the biggest difference next quarter?"

**Value bridge:**
- Connect expansion to their specific outcomes
- Show what similar customers achieved with expanded usage
- Present ROI projection

**Proposal:**
- Present options (good/better/best) rather than single proposal
- Include timeline for implementation
- Address potential objections

**Common objections and responses:**
- Budget: Show ROI payback period
- Timing: Propose phased rollout
- Need: Reference their own usage data and requests
- Risk: Offer pilot period or money-back guarantee

## Track opportunity
10. Record expansion opportunity in EXPANSION.md:
    - Customer name
    - Current ARR and proposed ARR
    - Expansion type (seats, tier, features)
    - Stage (identified, qualified, proposed, negotiating, closed)
    - Expected close date
    - Confidence level

11. Update TIMELINE.md with expansion activity
12. If team mode: sync to Supabase pipeline

13. Display:
```
  Expansion tracked in EXPANSION.md

  >> Next steps:
     1. Schedule expansion conversation with {champion}
     2. Prepare proposal with options
     3. Follow up within {timeframe}

  >> /cs:check-in {ws} {customer} (include expansion in agenda)
     /cs:qbr {ws} {customer} (present in next QBR)
     /cs:renewal {ws} {customer} (bundle with renewal)
```
</process>
