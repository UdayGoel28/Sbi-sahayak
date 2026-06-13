# SBI Sahayak — 30-Day Build Roadmap

The prototype build kicks off if the idea is shortlisted on **15 July 2026**. The plan below assumes a solo build (Uday Goel) using Claude Code + Antigravity, with synthetic data throughout.

---

## Week 1 — Foundation

- Generate a synthetic customer dataset (~10k profiles: demographics, transactions, UPI history, salary credits, EMIs, bills).
- Design the **Financial Life Graph** schema on PostgreSQL + pgvector — accounts, transactions, life-events, scheme-eligibility facts, embeddings of merchant/category context.
- Stand up the FastAPI service, LangGraph orchestrator skeleton, and a single end-to-end "hello world" path: channel → orchestrator → agent → reply.
- Load the RAG corpus: central + select state government schemes, SBI product fact-sheets, RBI customer-service guidelines.

## Week 2 — Engagement core (Disha)

- Build **Disha** as a LangGraph agent reading the Financial Life Graph.
- Implement **Yojana Finder**: eligibility rules + LLM justification + in-chat enrollment flow over WhatsApp Cloud API.
- Implement **Life-Event Prediction**: detectors for job change, salary jump, new dependent, medical spend, business inflow.
- Implement **Bill Sense**: cash-flow forecaster that flags shortfalls ahead of scheduled debits.
- Wire **Bhashini** for Hindi (and one regional) voice in/out.

## Week 3 — Govern + evals

- Build the **judge agent** (Claude) as an independent validator that scores every proposed Disha action.
- Codify **policy-as-code**: RBI disclosure rules, consent, product-eligibility, tone, language constraints.
- Implement **autonomy tiers** T1/T2/T3 and the **immutable audit log** (hash-chained).
- Implement the **kill switch** (global / per-channel / per-tier).
- Build an eval harness: 50+ scripted scenarios covering happy paths, mis-eligibility, hostile prompts, and consent violations.

## Week 4 — Polish + pitch

- **Bank Mitra co-pilot** tablet UI: customer summary, eligible schemes, next-best-action.
- Record the three golden-path demos (below) end-to-end.
- Build the pitch deck and a 3-minute submission video.
- Final hardening: rate limits, observability, README polish, architecture diagram exports.

---

## Demo Golden Paths

Three demos that judges will see in the final video.

### 1. Hindi WhatsApp onboarding (Swagat)
A new customer messages SBI on WhatsApp in Hindi. Swagat greets them, collects KYC fields conversationally, verifies via the KYC agent, and opens a basic savings account — all in Hindi, all under 3 minutes, with consent captured at each step.

### 2. Yojana Finder enrollment (Disha)
Disha notices a customer's transaction pattern matches Sukanya Samriddhi eligibility (girl-child-related spend, age bracket, no existing SSA). It proactively messages the customer in their language, explains the scheme in one paragraph, answers two follow-up questions via the RAG-grounded Product agent, and enrolls them on the spot once they say yes.

### 3. Governed loan offer with live judge approval (Disha + Governance)
Disha drafts a pre-approved personal-loan offer based on a salary jump it detected. Before the offer is sent, the **judge agent's verdict is shown on screen live**: policy checks, tone check, autonomy-tier verdict (T2 — needs customer confirm), audit-log entry. Only then does the offer reach WhatsApp. A second variant shows the judge **blocking** an over-aggressive offer, and the kill switch disabling the loan-offer capability with one click.
