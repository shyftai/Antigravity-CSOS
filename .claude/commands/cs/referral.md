---
name: cs:referral
description: Customer referral program management and tracking
argument-hint: "<workspace>"
---
<objective>
Manage the customer referral program. Track referral requests, warm introductions,
and conversion from referral to opportunity to closed-won revenue.

Workspace: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // REFERRALS >>`
2. Load workspace context and customer portfolio
3. Load REFERRALS.md (referral program tracker)
4. Load ADVOCACY.md for cross-reference with advocacy program

## Phase 2: Identify referral sources

1. Filter customers eligible for referral asks:
   - Health score >= 75
   - NPS score >= 8
   - Active for 3+ months
   - Achieved documented value/ROI
   - No open escalations
2. Prioritize by:
   - Network value (customer's industry connections)
   - Relationship depth (exec sponsor engaged)
   - Prior referral history (repeat referrers)
   - Recent positive interaction (QBR win, expansion, support resolution)
3. Display referral candidates with context

## Phase 3: Request referral

1. Select customer to ask for referral
2. Choose referral type:
   - **Warm introduction** — customer introduces prospect directly
   - **Name drop permission** — use customer's name in outreach
   - **Co-marketing** — joint webinar, blog post, event
   - **Internal referral** — introduction to another department/BU
3. Draft referral request:
   - Personalized ask based on customer's success
   - Specific target profile (who would benefit)
   - What the customer gets (program benefits, credits, swag)
4. Display draft for approval:
```
  +-- REFERRAL REQUEST PREVIEW --------------------+
  |                                                 |
  |  To:       {customer contact}                   |
  |  Type:     {warm intro / name drop / etc.}      |
  |  Ask:      {specific request}                   |
  |  Benefit:  {what they get}                      |
  |                                                 |
  |  {draft message}                                |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
  >> Approve and send? (y/n)
```

## Phase 4: Track referral pipeline

1. Display referral pipeline:
```
  +-- REFERRAL PIPELINE ---------------------------+
  |                                                 |
  |  Stage           Count    Revenue Potential      |
  |  Requested         {N}    -                      |
  |  Intro made        {N}    -                      |
  |  Meeting booked    {N}    ${value}               |
  |  Opportunity       {N}    ${value}               |
  |  Closed-won        {N}    ${value}               |
  |  Declined          {N}    -                      |
  |                                                 |
  |  Conversion rate: {request to intro}%            |
  |  Win rate: {intro to closed-won}%                |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```
2. Show individual referral status with aging
3. Flag stale referrals (intro made > 14 days, no follow-up)

## Phase 5: Measure program impact

1. Calculate referral program metrics:
   - Total referrals requested vs received
   - Referral-sourced pipeline value
   - Referral-sourced closed revenue
   - Average deal size (referral vs non-referral)
   - Average sales cycle (referral vs non-referral)
   - Top referring customers
2. Calculate program ROI
3. Update LEARNINGS.md with referral insights
4. Suggest next actions:
```
---------------------------------------------------

  >> Next: /cs:advocacy {workspace}
     Also: /cs:metrics {workspace}

---------------------------------------------------
```

</process>
</output>
