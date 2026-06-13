# CLAUDE.md — Project context for future Claude Code sessions

## Project summary

**SBI Sahayak** is a governed multi-agent AI platform that turns SBI into a proactive digital relationship manager for every customer. It is a solo hackathon submission by Uday Goel for SBI Hackathon 2026 (Global Fintech Fest), entered under the **Digital Engagement** theme. The flagship agent, **Disha**, reads each customer's transaction and UPI patterns through a Financial Life Graph and acts on their financial life before they ask — life-event prediction, a Yojana Finder for government scheme eligibility + in-chat enrollment, and Bill Sense for shortfall warnings. Every agent action passes a governance layer (judge agent + policy-as-code + autonomy tiers + audit log + kill switch) before it reaches the customer.

## Status

Idea-submission stage. No application code is in the repo yet. Implementation begins **only if shortlisted on 15 July 2026**, and runs against the 30-day plan in [docs/roadmap.md](docs/roadmap.md).

## Planned stack

- **Backend:** Python + FastAPI
- **Agent orchestration:** LangGraph
- **Workflow automation:** n8n
- **Customer-agent LLM:** Azure OpenAI (GPT-4o)
- **Judge-agent LLM:** Anthropic Claude
- **Data + vectors:** PostgreSQL + pgvector
- **Voice (Indian languages):** Bhashini APIs
- **Messaging:** WhatsApp Cloud API
- **Build tooling:** Claude Code + Antigravity

## Naming conventions

- Customer-facing agents are named in Hindi/Sanskrit:
  - **Swagat** — onboarding.
  - **Guru** — financial literacy / Q&A.
  - **Disha** — proactive digital RM (the flagship).
- The governance validator is always called the **"judge agent"** — never "critic", "reviewer", or "guardrail agent".
- Autonomy tiers are written **T1 / T2 / T3** (inform / recommend / execute).
- The customer's behavioural data model is the **Financial Life Graph** (capitalised).

## Intended directory layout

Once the build starts, the repo will be structured as:

```
sbi-sahayak/
├── app/           # FastAPI service, channel adapters (WhatsApp, voice, app, Bank Mitra portal)
├── agents/        # LangGraph agents — swagat/, guru/, disha/, and domain/ (kyc, credit, fraud, scheme, product)
├── governance/    # Judge agent, policy-as-code rules, autonomy tiers, audit log, kill switch
├── data/          # Synthetic dataset generators, Financial Life Graph schema + migrations, RAG corpus loaders
└── docs/          # Architecture, roadmap, eval reports
```

## Data rules

- The prototype uses **synthetic customer data only**.
- **No real customer data and no live banking APIs** are connected at any point — not in dev, not in demos.
- Any sample numbers, names, or transactions in the repo are fabricated for illustration.
