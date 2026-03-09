# CS:OS — The Customer Success Operating System

> Turn Claude Code into a full customer success engine. Win them. Keep them. Grow them.

CS:OS is a Claude Code plugin that runs your entire customer success workflow — from sales handoff to onboarding, health monitoring, QBR delivery, churn prevention, expansion, renewal, and advocacy. It connects to your CS stack via API, enforces quality at every step, and never upsells an unhappy customer.

**Built for:** CSMs, CS leaders, VP of Customer Success, founders, and agencies managing customer portfolios.

---

## Install

### Prerequisites
You need [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed:
```
npm install -g @anthropic-ai/claude-code
```

### Get started
```
git clone https://github.com/shyftai/CSOS.git
cd CSOS
claude
```

That's it. CS:OS boots automatically — shows the banner, scans your connected tools, and asks which workspace to load. No config files to edit, no build step.

### Connect your tools
CS:OS works with your existing tools. Two ways to connect:

**MCP servers (recommended)** — Claude can use these tools directly with full capabilities:
- [Slack](https://slack.com) — notifications and team alerts
- [Intercom](https://intercom.com) — customer messaging and support
- [Zendesk](https://zendesk.com) — ticket management and support

Add MCP servers to your Claude Code settings — CS:OS detects them automatically on boot.

**API keys** — add to `.env` for tools that connect via API:
```
cp .env.example .env
# add your keys (HubSpot, Stripe, ChurnZero, Vitally, etc.)
```

You don't need all tools to start. CS:OS works with whatever you have and tells you what's missing.

### First run
When CS:OS boots, run:
```
/cs:onboard my-portfolio
```
It asks your role (CSM, CS Leader, VP CS, Founder, or Agency), walks you through setup, and creates your workspace. Then you're ready to manage customers.

---

## What it looks like

When you open CS:OS in Claude Code, this is what you see.

### Boot sequence
```
 ██████╗███████╗ ██╗  ██████╗ ███████╗
██╔════╝██╔════╝ ╚═╝ ██╔═══██╗██╔════╝
██║     ███████╗     ██║   ██║███████╗
██║     ╚════██║ ██╗ ██║   ██║╚════██║
╚██████╗███████║ ╚═╝ ╚██████╔╝███████║
 ╚═════╝╚══════╝      ╚═════╝ ╚══════╝
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  C S : O S                                   v1.0.0
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  Win them. Keep them. Grow them.
                                        by Shyft AI

  ┌─ SYSTEM ──────────────────────────────────────────┐
  │                                                    │
  │  Workspaces:  acme-saas                            │
  │  Mode:        solo                                 │
  │  Execution:   interactive                          │
  │                                                    │
  │  MCP servers:                                      │
  │  [x] Slack            [x] Intercom                  │
  │  [ ] Zendesk                                       │
  │                                                    │
  │  API keys:                                         │
  │  [x] HubSpot          [ ] Salesforce                │
  │  [x] Stripe           [x] ChurnZero                │
  │  [ ] Vitally          [ ] Gainsight                 │
  │                                                    │
  │  2 MCP servers · 3 API keys · 4 missing            │
  │                                                    │
  └────────────────────────────────────────────────────┘

  >> Which workspace are we loading?
```

### Workspace loaded
```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  WORKSPACE: Acme SaaS                                      ┃
┃  ACCOUNTS:  47        ARR: $2.4M       NRR: 112%           ┃
┃  HEALTH:    38 green · 6 amber · 3 red                     ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

### Quality gates — every action is checked
```
  ── QUALITY GATES ──────────────────────────────────
  [x] Health      [x] Segment     [x] Timeline
  [x] Playbook    [x] Risk        [x] NPS
  ─────────────────────────────────────────────────
```

### Customer health monitoring
```
  ┌─ PORTFOLIO HEALTH ─────────────────────────────────┐
  │                                                     │
  │  Overall        [GREEN]   Score: 78/100              │
  │  Enterprise     [GREEN]   12 accounts · avg 82       │
  │  Mid-market     [AMBER]   20 accounts · avg 71       │
  │  SMB            [GREEN]   15 accounts · avg 76       │
  │                                                     │
  │  At-risk: 3     Renewals (30d): 5     NPS: 42        │
  └─────────────────────────────────────────────────────┘
```

### Nothing ships without your approval
```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃  APPROVE QBR DECK?                              ┃
┃  Customer: Acme Corp (Enterprise)               ┃
┃  Period: Q1 2026                                ┃
┃  Health: GREEN (82/100)                         ┃
┃                                                  ┃
┃  >> approve / reject / edit                      ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

---

## How it works

```
  ┌──────────────────────────────────────────────────────────┐
  │  HANDOFF ─── KICKOFF ─── ONBOARD ─── ADOPT              │
  │                    │                                     │
  │                HEALTH                                    │
  │                    │                                     │
  │     ┌──────────────┼──────────────┐                      │
  │     ▼              ▼              ▼                      │
  │   CHECK-IN       QBR          SUPPORT                    │
  │     │              │              │                      │
  │     ▼              ▼              ▼                      │
  │  EXPAND ──── UPSELL ──── ADVOCACY                        │
  │                    │                                     │
  │     ┌──────────────┼──────────────┐                      │
  │     ▼              ▼              ▼                      │
  │  RENEW        REFERRAL        NPS                        │
  │                    │                                     │
  │           REPORT + LEARN                                 │
  └──────────────────────────────────────────────────────────┘
```

Every action is checked against these sources of truth before anything happens:

| File | What it controls |
|------|-----------------|
| **CUSTOMERS.md** | Customer roster, key details, contract info |
| **SEGMENTS.md** | Tier definitions, segment rules |
| **HEALTH-SCORES.md** | Health model, current scores, trends |
| **PLAYBOOKS.md** | Lifecycle playbooks for every stage |
| **ONBOARDING.md** | Onboarding process, milestones |
| **RENEWALS.md** | Renewal pipeline and tracking |
| **EXPANSION.md** | Expansion opportunities |
| **NPS.md** | Survey results and sentiment |
| **ESCALATIONS.md** | Active escalations |
| **TIMELINE.md** | Complete interaction history |
| **METRICS.md** | KPIs, targets, benchmarks |

If the health score hasn't been checked, the action doesn't proceed.

---

## The customer success lifecycle

**1. Handoff** → `/cs:handoff` receives new customers from sales with full context — deal notes, stakeholders, expectations, success criteria. Nothing falls through the cracks.

**2. Kickoff** → `/cs:kickoff` prepares and runs the kickoff call — agenda, introductions, success plan, timeline, and next steps. Sets the relationship up right from day one.

**3. Onboard** → `/cs:onboard-customer` manages the onboarding journey — milestones, training sessions, integration setup, go-live. Tracks time-to-value obsessively.

**4. Adopt** → Health monitoring begins. Usage tracking, feature adoption, stakeholder engagement. The goal is deep product adoption before the first renewal.

**5. Health** → `/cs:health` continuously monitors customer health scores. Proactive outreach on amber. Immediate action on red. Pattern detection across the portfolio.

**6. Expand** → `/cs:upsell` identifies expansion opportunities based on usage patterns, feature gaps, and growth signals. Only when health is green.

**7. Renew** → Renewal tracking starts 90 days out. Risk assessment, stakeholder alignment, value documentation. No last-minute scrambles.

**8. Advocate** → `/cs:advocacy` converts successful customers into advocates — case studies, referrals, reviews, speaking opportunities.

---

## Key features

### Customer health scoring
Multi-dimensional health scoring across usage, engagement, support, relationship, and business metrics. Configurable weights per segment. Trend analysis with predictive churn indicators. Automated alerts when scores drop.

### Lifecycle management
Full lifecycle orchestration from sales handoff through onboarding, adoption, expansion, renewal, and advocacy. Each stage has defined milestones, playbooks, and success criteria.

### Churn prevention
Proactive churn detection using declining usage, missed meetings, stakeholder changes, support ticket spikes, and NPS drops. Automated save playbooks with escalation paths. Post-churn analysis feeds learnings.

### QBR engine
Automated QBR preparation — usage analytics, ROI calculations, success metrics, product roadmap alignment, expansion recommendations. Generates presentation-ready decks. Tracks QBR outcomes and action items.

### Expansion detection
Pattern-based expansion identification — usage approaching limits, new use case adoption, growing team size, positive NPS trends. Warm handoff to sales when timing is right.

### Renewal management
90-day renewal pipeline with risk scoring. Stakeholder mapping for multi-threaded relationships. Value documentation for renewal justification. Early warning system for at-risk renewals.

### NPS management
Survey deployment, response tracking, promoter/passive/detractor segmentation. Close-the-loop workflows for detractors. Trend analysis across segments and cohorts.

### Support integration
Ticket volume monitoring per account. Escalation detection. Repeat issue identification. Support health feeds into overall customer health score.

### Sales-to-CS handoff
Structured handoff template capturing deal context, stakeholder map, expectations, success criteria, and known risks. Nothing gets lost in transition.

### Daily briefing
`/cs:today` scans everything and tells you what needs attention right now. At-risk accounts, upcoming renewals, overdue check-ins, open escalations, NPS detractors.

### Learnings system
CS:OS learns from every churn, every expansion, every QBR. Patterns are documented, playbooks are refined, predictions improve. Updated after every debrief, loaded before every session.

### Parallel processing (Swarm)
Spin up parallel agents for batch health assessments, portfolio-wide renewal prep, and large-scale QBR generation.

---

## Smart defaults, full control

CS:OS ships with sensible defaults for everything:

- **Health:** 5-dimension scoring (usage, engagement, support, relationship, business), red/amber/green thresholds
- **Check-ins:** weekly for enterprise, bi-weekly for mid-market, monthly for SMB
- **QBRs:** quarterly for enterprise, semi-annual for mid-market, annual for SMB
- **Renewals:** 90-day tracking window, 60-day action plan, 30-day escalation
- **Onboarding:** 30-day target for SMB, 60-day for mid-market, 90-day for enterprise
- **Escalation SLAs:** critical 2hr, high 4hr, medium 24hr, low 48hr

**Every default is overridable per workspace.** Add overrides in the relevant workspace file. If you don't override, the defaults just work.

---

## All commands

### Start
| Command | What it does |
|---------|-------------|
| `/cs:today` | Daily CS briefing — what needs attention now |
| `/cs:dashboard` | Full portfolio dashboard with health, renewals, metrics |

### Setup
| Command | What it does |
|---------|-------------|
| `/cs:onboard` | Create a new workspace — guided setup |
| `/cs:segments` | Define or update customer segments and tiers |
| `/cs:playbook` | Create or update success playbooks |

### Customer lifecycle
| Command | What it does |
|---------|-------------|
| `/cs:kickoff` | Prepare and run customer kickoff |
| `/cs:onboard-customer` | Manage customer onboarding journey |
| `/cs:check-in` | Prepare and run customer check-in |
| `/cs:qbr` | Prepare and deliver quarterly business review |

### Health
| Command | What it does |
|---------|-------------|
| `/cs:health` | Customer health check — scores, trends, alerts |
| `/cs:at-risk` | Detect and manage at-risk customers |
| `/cs:save` | Execute churn save playbook |
| `/cs:nps` | NPS survey management and analysis |

### Growth
| Command | What it does |
|---------|-------------|
| `/cs:upsell` | Identify and manage expansion opportunities |
| `/cs:advocacy` | Customer advocacy program — case studies, references |
| `/cs:referral` | Customer referral program management |

### Operations
| Command | What it does |
|---------|-------------|
| `/cs:tickets` | Support ticket triage and tracking |
| `/cs:escalation` | Manage escalations and resolution |
| `/cs:handoff` | Sales-to-CS handoff management |
| `/cs:timeline` | Customer interaction timeline |

### Review
| Command | What it does |
|---------|-------------|
| `/cs:metrics` | Key CS metrics dashboard |
| `/cs:report` | Generate CS performance reports |
| `/cs:debrief` | Post-churn or post-expansion retrospective |
| `/cs:feedback` | Submit feedback, report a bug, or request a feature |

### Collaboration
| Command | What it does |
|---------|-------------|
| `/cs:collab` | Team collaboration and shared state setup |

### Scale
| Command | What it does |
|---------|-------------|
| `/cs:swarm` | Run CS operations with parallel agents |

---

## Supported tools

CS:OS connects to your existing customer success stack. Use what you have — skip what you don't. Every tool is optional.

| Category | Tools |
|----------|-------|
| **CRM** | HubSpot, Salesforce |
| **CS Platforms** | ChurnZero, Vitally, Gainsight |
| **Support** | Intercom, Zendesk |
| **Billing** | Stripe |
| **Communication** | Slack |
| **Analytics** | Mixpanel, Amplitude |

---

## Workspaces

Each workspace is fully isolated — its own customers, health scores, playbooks, renewals, and metrics. A workspace can be:

- A SaaS product portfolio
- A business unit
- A customer segment
- A client (for CS agencies)
- Any customer portfolio that deserves its own context

---

## Notifications (optional)

Connect Slack to get real-time alerts:
- At-risk customer detected (health score red)
- Renewal due within 30 days
- Escalation raised to leadership
- NPS detractor identified
- Customer churned
- Expansion closed

Configure in COLLABORATION.md. Works via Slack MCP.

---

## Team mode (optional)

By default CS:OS runs in **solo mode** — all state lives in markdown, no database needed.

For teams, enable **team mode** with Supabase:

1. Create a Supabase project
2. Add keys to `.env`
3. Run `/cs:collab setup`

Adds: shared health score tracking, escalation queue, renewal pipeline, handoff coordination, approval audit trail, activity feed. Falls back to files automatically if Supabase is unreachable.

---

## Repo structure

```
CSOS/
├── CLAUDE.md                  <- Entrypoint for Claude Code
├── CSOS.md                    <- All rules and behaviour
├── CHANGELOG.md               <- Version history
├── .env.example               <- API key template
├── _template/                 <- Workspace template (copied on onboard)
├── workspaces/                <- One folder per workspace
├── global/                    <- Cross-workspace standards
│   ├── RULES-GLOBAL.md        <- Global CS rules
│   └── COLLABORATION.md       <- Solo/team mode config
├── .claude/
│   ├── commands/cs/           <- Slash commands (/cs:*)
│   └── csos/references/       <- System references
│       ├── ui-brand.md         <- Visual system
│       ├── defaults.md         <- All overridable defaults
│       ├── health-scoring.md   <- Health score model
│       ├── playbooks.md        <- Success playbooks
│       ├── onboarding-guide.md <- Onboarding best practices
│       ├── churn-signals.md    <- Churn indicator patterns
│       ├── BENCHMARKS.md       <- Industry benchmarks
│       ├── report-template.md  <- Report formats
│       ├── notifications.md    <- Slack alert config
│       └── tool-pricing.md     <- Per-unit costs
```

---

## Feedback

Found a bug? Want a feature? Run `/cs:feedback` inside Claude Code, or open an issue on this repo.

---

## License

MIT — Built by [Shyft AI](https://shyft.ai)
