# CLAUDE.md — SBI Sahayak Project Context

> Read this at the start of every Claude Code session before writing any code.
> This file is the single source of truth for project conventions, scope, and constraints.

---

## Project summary

**SBI Sahayak** is a governed multi-agent AI platform that acts as a proactive digital
relationship manager for SBI customers. It is a submission for SBI Hackathon 2026
(Global Fintech Fest), theme: Digital Engagement.

**Builder:** Uday Kumar Goel — solo, using Claude Code (backend/agents) + Antigravity (frontend/demo).
**Status:** Idea-submission stage until 15 Jul 2026. Prototype build starts only if shortlisted.

---

## The core idea in one paragraph

Disha, the Digital Engagement agent, reads a persistent "Financial Life Graph" (a
PostgreSQL database of synthetic transaction/UPI patterns per customer) and acts on the
customer's financial life before they ask. Four capabilities: Lakshya Engine (agentic
auto-savings + gamification), Bill Sense (predict shortfalls before penalties), Yojana
Finder (detect government-scheme eligibility and enroll in-chat), and Rakshak (Credit
Passport for thin-file customers + fraud-awareness shields). Every action Disha proposes
is validated by an independent Judge Agent (a different model) against policy-as-code
before it reaches the customer. The mic-drop demo: Disha tries a Lakshya sweep → Judge
Agent blocks it because Bill Sense sees an LIC premium due tomorrow.

---

## Agents and naming conventions

| Name | Role | Notes |
|---|---|---|
| **Disha** | Digital Engagement agent | Core submission; runs Lakshya, Bill Sense, Yojana, Rakshak |
| **Swagat** | Customer Acquisition | Conversational onboarding, KYC orchestration |
| **Guru** | Digital Adoption | Contextual coaching, Bank Mitra co-pilot |
| **Rakshak** | Protection + Inclusion | Credit Passport (prototype), Victim-Shield, Scam-Shield (roadmap) |
| **Judge Agent** | Governance validator | MUST be a different model than the customer agents |

**Domain logic modules** (inside Disha):
- `lakshya` — savings pattern detection + auto-sweep goals + gamification
- `bill_sense` — recurring-payment prediction + shortfall warning
- `yojana_finder` — government scheme eligibility detection + enrollment
- `credit_passport` — alternative-data credit scoring for thin-file customers

**Governance components:**
- `judge_agent` — independent model cross-validation
- `policy_engine` — policy-as-code rules (Python functions)
- `audit_log` — append-only, never UPDATE/DELETE
- Autonomy tiers: `T1` auto · `T2` customer-confirm · `T3` human-approval

---

## Planned directory layout (use from build day 1)

```
sbi-sahayak/
  app/                # FastAPI entrypoint + API routes
  agents/
    disha.py          # Lakshya + Bill Sense + Yojana + Rakshak orchestration
    swagat.py         # Acquisition agent (future)
    guru.py           # Adoption agent (future)
  governance/
    judge.py          # Judge Agent — DIFFERENT model from customer agents
    policies.py       # Policy-as-code rule engine
    audit.py          # Append-only audit log
  data/
    schema.sql        # Full PostgreSQL schema (Financial Life Graph)
    synth_generator.py # Synthetic dataset: 1,000 users × 12 months
  domain/
    lakshya.py
    bill_sense.py
    yojana_finder.py
    credit_passport.py
  rag/
    ingest.py         # Load SBI docs + scheme rules into pgvector
    retriever.py
  llm/
    llm_client.py     # Swappable model client — read provider from env var
  demo/               # Antigravity frontend / demo UI lives here
  evals/              # 100 test conversations + scoring harness
  docs/
    architecture.mmd  # Mermaid diagram
    roadmap.md
  CLAUDE.md           # This file
  README.md
  requirements.txt
  .env.example
  .gitignore
```

---

## Tech stack

| Layer | Choice | Notes |
|---|---|---|
| Customer agents | Claude API (`claude-sonnet-4-6`) | Default — easy access, no approval wait |
| Judge Agent | OpenAI API (GPT-4o-mini) | Must be a DIFFERENT provider/model |
| Orchestration | LangGraph + n8n | LangGraph for agent graphs; n8n for workflows |
| Backend | Python + FastAPI | |
| Language / voice | Bhashini APIs | ASR/TTS — not a biometrics engine |
| Channels | WhatsApp Cloud API, web UI | IVR via Twilio (demo only) |
| Database | PostgreSQL 16 + pgvector | Financial Life Graph + RAG |
| Observability | Langfuse | Show live traces in the demo |
| Frontend/demo | Antigravity IDE | |

**Model client pattern:** `llm/llm_client.py` exposes a single `complete(messages, model)`
function. Provider is selected by `LLM_PROVIDER` env var (`anthropic` or `openai`).
Everything else imports from this — never hardcode a provider elsewhere.

---

## Data rules — non-negotiable

- **100% synthetic data.** Never use real customer data. Never call live banking APIs.
- **No access to confidential regulator databases** (e.g., RBI's MuleHunter.AI data).
- Synthetic generator must produce *detectable patterns*:
  - Some customers with electronics/food-delivery spend → Lakshya signal
  - Some with upcoming LIC premium + low balance → Bill Sense shortfall
  - At least one customer where a Lakshya sweep + LIC premium compete for the same
    balance → the mic-drop demo scenario
  - Some with farm-input purchases / girl-child / age < 40 → Yojana Finder signals
  - Some with no CIBIL proxy (no credit-category transactions) → Credit Passport signal
- Seed the database so the mic-drop scenario is deterministic (not left to chance).

---

## Governance rules — enforce in every agent

- Every proposed action must be written to `agent_actions` table before delivery.
- Judge Agent validation must run before any action reaches the customer.
- Autonomy tier must be set at action creation and respected:
  - T1 (informational) → auto-deliver after Judge approves
  - T2 (money movement) → hold; require explicit customer confirmation
  - T3 (lending, account restriction) → hold; require human banker approval
- The agent NEVER promises a loan rate, approval, or specific credit amount.
- The agent NEVER moves money without an explicit customer opt-in.
- The agent NEVER claims to use RBI/MuleHunter data.
- `governance_audit` is append-only — no UPDATE or DELETE ever.

---

## Build order (dependency order — follow this)

1. `llm/llm_client.py` — foundation; everything depends on this
2. `data/schema.sql` + `data/synth_generator.py` — every demo depends on data
3. `governance/policies.py` + `governance/audit.py` — governance v0
4. `domain/bill_sense.py` + `domain/lakshya.py` (plain Python first, no LangGraph)
5. `governance/judge.py` — introduce the second model
6. Refactor into LangGraph state graph (only after plain Python version works)
7. `domain/yojana_finder.py` + `domain/credit_passport.py`
8. Channel integration (WhatsApp / web)
9. `evals/` harness — run before any demo recording

**Introduce LangGraph only at step 6** — get plain Python working first to avoid
fighting the framework while the core logic is still forming.

---

## The three golden demo paths (optimise for these)

1. **Hindi WhatsApp Lakshya flow:** Disha detects electronics saving pattern →
   proposes goal on WhatsApp in Hindi → customer opts in → first sweep runs.
2. **The mic-drop:** Disha attempts a daily sweep → Judge Agent blocks it because
   Bill Sense sees LIC premium due tomorrow → shown live in Langfuse audit panel.
3. **Credit Passport:** thin-file customer → explainable score computed →
   "you may be eligible to apply" → routed to human approval (T3).

---

## Scope discipline

**Prototype (build in 30 days):** Lakshya Engine, Bill Sense, Yojana Finder,
Credit Passport (Rakshak), Judge Agent, governance audit panel.

**Roadmap only (do NOT build in prototype):** Victim-Shield, Scam-Shield,
Swagat full KYC flow, Guru adoption coaching.

If a feature isn't in the prototype list, it goes on a roadmap slide — not in code.
Building out-of-scope features before the three golden paths are solid is the #1
failure mode for solo hackathon builds.

---

## Key dates

- Idea submission deadline: **30 Jun 2026, 11:59 PM IST**
- Top 10 shortlisted: **15 Jul 2026**
- Prototype build window: **15 Jul – 14 Aug 2026** (30 days)
- Finalists announced: **25 Aug 2026**
- Winners at GFF: **9-11 Sep 2026**
