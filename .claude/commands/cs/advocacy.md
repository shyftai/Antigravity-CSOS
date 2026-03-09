---
name: cs:advocacy
description: Customer advocacy program — references, case studies, reviews, and program tracking
argument-hint: "<workspace> [customer-name]"
---
<objective>
Manage the customer advocacy program. Identify promoters, request references and case studies,
track advocacy pipeline, and measure program impact on retention and expansion.

Workspace and customer: $ARGUMENTS
</objective>

<execution_context>
@./.claude/csos/references/ui-brand.md
@./.claude/csos/references/health-scoring.md
</execution_context>

<process>

## Phase 1: Initialize

1. Display mode header: `<< CS:OS // ADVOCACY >>`
2. Load workspace context and customer portfolio
3. Load ADVOCACY.md (advocacy program tracker)
4. If customer-name provided, show that customer's advocacy status
5. If no customer specified, show program overview

## Phase 2: Identify promoters

1. Filter customers eligible for advocacy:
   - NPS score 9-10 (promoter)
   - Health score >= 80
   - Customer for 6+ months
   - No open P0/P1 tickets
   - No active escalations
2. Rank by advocacy potential:
   - Brand recognition (well-known company = higher value)
   - Use case relevance (matches target ICP = higher value)
   - Relationship strength (exec sponsor engaged = higher value)
   - Prior advocacy participation
3. Display eligible promoters:
```
  +-- ADVOCACY CANDIDATES -------------------------+
  |                                                 |
  |  Customer       NPS  Health  Segment   Status   |
  |  {name}          10    92    Enterprise  New     |
  |  {name}           9    85    Mid-market  Active  |
  |  {name}          10    88    Strategic   Asked   |
  |                                                 |
  |  Eligible: {N}   Active advocates: {N}          |
  |                                                 |
  +--  --  --  --  --  --  --  --  --  --  --  -- --+
```

## Phase 3: Request advocacy

For a selected customer, choose advocacy type:
1. **Reference call** — willing to speak with prospects
   - Draft reference request email
   - Track availability and preferences (industry, use case, format)
2. **Case study** — published success story
   - Draft case study request with outline
   - Define key metrics to highlight
   - Track approval process (customer review, legal, marketing)
3. **G2/Capterra review** — public review
   - Draft review request with direct link
   - Track completion
4. **Speaking engagement** — conference, webinar, podcast
   - Draft speaking invitation
   - Define topic and format
5. **Logo permission** — use logo on website/materials
   - Draft logo permission request
   - Track legal approval

Display draft for approval before sending.

## Phase 4: Track advocacy pipeline

1. Show advocacy pipeline by stage:
```
  ADVOCACY PIPELINE:
  Identified:    {N} customers
  Requested:     {N} customers
  In progress:   {N} (awaiting content/approval)
  Completed:     {N} advocacy assets
  Declined:      {N} (with reasons)
```
2. Show completed advocacy assets:
   - Reference calls completed this quarter
   - Case studies published
   - Reviews posted
   - Speaking engagements done
3. Track advocacy freshness (references older than 12 months need refresh)

## Phase 5: Measure program impact

1. Calculate program metrics:
   - Total advocacy assets produced
   - Reference call conversion rate (prospect to customer)
   - Case study influence on pipeline
   - Review site rating trend
   - Advocate retention rate vs non-advocate
   - Advocate expansion rate vs non-advocate
2. Display impact dashboard
3. Update LEARNINGS.md with advocacy insights
4. Suggest next actions:
```
---------------------------------------------------

  >> Next: /cs:referral {workspace}
     Also: /cs:health {workspace} {customer}

---------------------------------------------------
```

</process>
</output>
