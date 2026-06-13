# SBI Sahayak — 30-Day Prototype Roadmap

> **Status:** Idea-submission stage. Build starts only if shortlisted (top 10 announced 15 Jul 2026).
> Build window: **15 Jul – 14 Aug 2026** (30 days). Finalists announced 25 Aug.
> Solo build — Claude Code (backend/agents) + Antigravity IDE (frontend/demo).

---

## The rule: 3 golden paths built deep, not 10 features built shallow.

**Golden Path 1 — Hindi WhatsApp Lakshya flow**
Detect a savings pattern in synthetic UPI data → Disha proposes an opt-in goal on WhatsApp in Hindi via Bhashini → customer activates → Lakshya tracks progress.

**Golden Path 2 — The mic-drop (Judge Agent blocks the sweep)**
Disha attempts a scheduled Lakshya auto-sweep → Judge Agent detects an upcoming LIC premium via Bill Sense → BLOCKS the sweep with an explicit reason → shown live in the Langfuse audit panel. Safe, governed autonomy in one moment.

**Golden Path 3 — Credit Passport → eligible to apply**
Thin-file customer (no CIBIL) → Rakshak computes an explainable behavioural score from synthetic data → Disha surfaces "you may be eligible to apply" → routed to T3 human approval (never auto-approved). Inclusion, done safely.

*(Yojana Finder is a strong 4th path if time allows. Victim-Shield / Scam-Shield remain roadmap.)*

---

## Week-by-week plan

### Week 1 — Foundation (Days 1–7)
*Goal: everything else depends on this. Get it right before building agents.*

- **D1** — Repo layout (`app/ agents/ governance/ data/ rag/ llm/ demo/ evals/`). Write `llm/llm_client.py`: a single `complete(messages, model)` function wrapping the Claude API (default) and OpenAI API (judge), selected by env var. Tiny `__main__` test to confirm it works.
- **D2–3** — Synthetic data generator (`data/synth_generator.py`): 1,000 customer profiles × 12 months of UPI/bank history. Deliberately pattern the data: electronics browsing spend for Lakshya, farm-input purchases for PM-Kisan, LIC recurring debit for Bill Sense. **Critically:** create at least one customer whose balance covers either a Lakshya sweep OR an LIC premium — not both. That's the mic-drop setup.
- **D4** — Financial Life Graph feature extraction: from raw transactions compute per-customer signals (recurring_payments, salary_trend, category_spend, life_event_flags). Store in Postgres.
- **D5** — RAG pipeline (`rag/ingest.py` + `rag/retriever.py`): load SBI public product docs + government scheme rules into pgvector.
- **D6** — Disha v0 in plain Python (no LangGraph yet): take a customer's Life Graph + a question, call the model with RAG context, return a grounded answer.
- **D7** — Governance v0: `governance/policies.py` (10 encoded rules), `governance/audit.py` (append-only log). Internal demo #1: ask Disha → see response → see action logged.

### Week 2 — Engagement core + channels (Days 8–14)
*Goal: the 3 golden paths working end-to-end.*

- **D8** — Lakshya Engine: pattern detection → goal proposal flow. Explicit customer opt-in required before any sweep.
- **D9** — Bill Sense: recurring-payment detection + shortfall prediction. Wire to upcoming_payments table.
- **D10** — Yojana Finder: eligibility engine over synthetic profile + scheme rules from RAG. Encode 8–10 schemes.
- **D11** — Credit Passport (Rakshak): interpretable scoring function over behavioural features (payment regularity, cash-flow stability, bounce rate). Output is "eligible to apply" signal only — never a rate or approval promise.
- **D12** — Introduce LangGraph: refactor Disha into a small state graph (detect → reason → draft → governance node → respond). You understand the pieces now; LangGraph earns its place here.
- **D13** — Channel: WhatsApp Cloud API + Bhashini Hindi TTS. Wire one full golden path: WhatsApp message in → Disha → governed response in Hindi.
- **D14** — Internal demo #2 + fix list.

### Week 3 — Governance properly + prove it (Days 15–21)
*Goal: the differentiator. Most teams skip this entirely.*

- **D15–16** — Judge Agent (`governance/judge.py`): the second model validates every proposed action against policy-as-code. Pass/block/escalate. Returns a structured verdict + human-readable reason.
- **D17** — Autonomy tiers + kill switch UI: T1 auto, T2 customer-confirm, T3 human-approval. Per-agent kill switch toggle shown in the demo UI.
- **D18** — Live audit panel (Antigravity): a visible side panel showing each action → Judge verdict → outcome in real time. This is what wins bank judges — make it visible, not just logged.
- **D19–20** — Eval harness (`evals/`): 100 test conversations. Measure hallucination rate, containment rate, escalation accuracy. Report as real numbers in the pitch.
- **D21** — Tune based on eval results. Internal demo #3.

### Week 4 — Polish, video, pitch (Days 22–30)
*Non-coding week. Discipline matters here.*

- **D22–24** — Demo UI polish (Antigravity): clean WhatsApp/chat view, live audit panel, the 3 golden paths runnable on demand without breaking.
- **D25–26** — Record the demo video (max 3 min per the submission form). Use the 3-scene script: (1) Hindi Lakshya proposal, (2) Judge Agent blocks the sweep live, (3) Credit Passport → eligible to apply.
- **D27–28** — Pitch rehearsal: 5-minute script, timed, recorded. Fix anything that takes more than 30 seconds to explain.
- **D29–30** — Buffer + docs. Update README with real eval numbers + screenshots. Final commit. Submit.

---

## What NOT to build in the prototype

| Feature | Why deferred |
|---|---|
| Victim-Shield (mule awareness) | Roadmap — no confidential RBI data access in prototype |
| Scam-Shield (UPI intercept) | Roadmap — requires real-time payment pipeline |
| Guru (adoption agent) | Roadmap — focus is Disha/Rakshak |
| Swagat (acquisition agent) | Roadmap — demo a stub only |
| Live Bhashini voice full pipeline | If API is unstable, use cached Hindi audio — judges won't notice |
| Azure OpenAI | Nice-to-have swap for pitch credibility — not a blocker |

---

## Failure modes to avoid (solo)

- **Data rushed** → agents have nothing believable to detect; whole demo feels fake. Day 2–3 is the most important investment.
- **LangGraph too early** → fight the framework. Get plain Python working first (D6 before D12).
- **10 features at 60%** → 3 paths at 95% wins every time.
- **AI refactor breaks a working demo** → `git commit` after every working feature, no exceptions.
- **Week 4 turns into coding** → polish/video/pitch only. This is the discipline that separates finalists.
