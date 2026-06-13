# SBI Hackathon 2026 — Idea Submission v3 (FINAL, compliance-clean)
# Keeps Rakshak's punch; fixes the landmines that a banking jury would catch.
#
# WHAT CHANGED FROM YOUR DRAFT (and why):
#  - Mule detection reframed: protects the customer as an UNWITTING VICTIM being
#    recruited as a mule. Removed any "warn before RBI blocks you" framing (that
#    reads as helping fraud evasion) and removed the claim of using RBI's
#    MuleHunter.AI database (it's confidential RBI infra you can't access).
#  - Credit Passport: no guaranteed rates/approvals. Always "eligible to APPLY,"
#    reviewed by a human banker (T3). This is both compliant and matches your own
#    governance design.
#  - Scam-Shield: dropped "voice-spoofing detection via Bhashini" (Bhashini is
#    translation/TTS, not a voice-biometrics engine). Kept behavioural-anomaly +
#    vendor-reputation warnings, which are buildable.
#  - Stats: "300M invisible borrowers" -> the citable TransUnion CIBIL figure
#    (~480M credit-unserved). Vague fraud/ROI numbers softened or labelled
#    illustrative so no judge can pull a thread.
#  - Scope honesty: platform vision = 4 agents; PROTOTYPE = 3 golden demo paths.
#    Rakshak's Credit Passport is the ONE Rakshak piece you'll build; Mule/Scam
#    are clearly "roadmap." Protects you in the prototype round.

**Theme dropdown:** Agentic AI & Emerging Tech
**Problem Statement dropdown:** Digital Engagement

---

## Field 1 — Project Title  [REQUIRED]
```
SBI Sahayak — A Governed Agentic AI Relationship Manager for Every Indian
```

---

## Field 2 — Team Details
```
Solo participant.
Uday Kumar Goel — B.Tech CSE student; independent builder (previously built SlotSync,
a B2B SaaS booking platform). Jind, Haryana, India.
Building the full prototype solo using Claude Code and the Antigravity IDE.
```

---

## Field 3 — Brief Description of the Idea  [REQUIRED]
```
SBI serves nearly 50 crore customers, but only a tiny fraction get a relationship
manager. Everyone else gets nothing between account opening and a problem — leading to
under 2 products per customer, crores of dormant accounts, billions in unclaimed
government benefits, and a service model that only reacts after a penalty has hit.

SBI Sahayak is a GOVERNED multi-agent AI platform that gives every customer a proactive
digital relationship manager. This submission focuses on "Disha", the Digital Engagement
agent, which reads a customer's transaction and UPI patterns (a persistent "Financial
Life Graph") to act on their financial life before they have to ask.

Disha's flagship capabilities:

1. LAKSHYA ENGINE (agentic auto-savings + gamification): Detecting a savings pattern
   from spending (e.g., frequent electronics browsing), Disha proposes a goal on
   WhatsApp — "Saving for a laptop? Shall I auto-sweep Rs.200 from your food-delivery
   spend toward it?" The customer explicitly opts in; at 50% progress she surfaces
   eligibility to APPLY for a relevant SBI offer (e.g., a low-fee electronics loan,
   subject to approval).

2. BILL SENSE: Monitors upcoming recurring obligations (LIC premium, EMI) and warns of
   a shortfall BEFORE a penalty, offering a one-tap transfer (customer-confirmed) from
   another of the customer's own accounts.

3. YOJANA FINDER: Auto-detects eligibility for government schemes (PMJJBY, Sukanya
   Samriddhi, APY, PM-Kisan) from the customer's profile and initiates enrollment
   in-chat or via a Bank Mitra kiosk.

4. RAKSHAK (protection + inclusion) — the platform's trust layer:
   - Credit Passport [the Rakshak feature we will prototype]: For India's ~480 million
     "credit-unserved" adults with no CIBIL history (TransUnion CIBIL), Rakshak builds an
     alternative-data profile from UPI consistency, bill-payment regularity and cash-flow
     stability, then surfaces whether the customer is likely ELIGIBLE TO APPLY for an SBI
     loan — which a human banker reviews and approves. Example: "You have no CIBIL score,
     but your payment record looks strong. You may be eligible to apply for an SBI loan —
     shall I start an application for a banker to review?" (No rate or approval is ever
     promised by the agent.)
   - Victim-Shield [roadmap]: Educates a customer who appears to be the UNWITTING victim
     of a mule-account recruitment scam (e.g., "someone asked you to receive and forward
     money for a commission") and routes them to the bank's official fraud-help channel.
     Aligned with the patterns RBI's MuleHunter.AI made industry-standard; it does NOT use
     RBI's confidential data and never helps anyone evade detection.
   - Scam-Shield [roadmap]: During a UPI payment, warns of a flagged-vendor or an unusual
     transaction pattern and lets the customer pause ("Reply STOP to hold this payment").

THE GOVERNANCE CORE — what makes this enterprise-grade, not a chatbot: every action Disha
proposes is validated by an independent JUDGE AGENT (a separate AI model) against banking
policy encoded as code, with autonomy tiers (auto / customer-confirm / human-approval),
an immutable audit trail, and kill switches (modelled on DBS Bank's PURE framework).
Concretely: when Disha attempts a Lakshya auto-sweep, the Judge Agent BLOCKS it because
Bill Sense sees an LIC premium due tomorrow — protecting the customer from a bounced-
payment fee. Safe, governed autonomy is the whole point. Any money movement is
customer-confirmed; any lending step is human-approved. The agent never moves money
silently and never promises credit.

Disha is the wedge into a broader platform (Swagat for acquisition, Guru for adoption +
a Bank Mitra co-pilot), but on its own it directly answers this theme: AI-driven
engagement that acts on customer behaviours, financial patterns, and life events — while
advancing SBI's financial-inclusion mandate.
```

---

## Field 4 — Proposed Solution / Business Model / Commercial Potential
```
WHAT IT IS
A governed agent operating layer SBI plugs its existing systems into (CRM, KYC,
transaction data) — not a bolt-on chatbot. Agents reason over a persistent Financial
Life Graph, so they have real context and memory instead of one-off prompts.

WHY IT WINS FOR SBI
- SBI publicly committed to agentic AI in 2025. This hands them the GOVERNED architecture
  to scale it safely — the Judge Agent is the difference between a pilot and production.
- Built India-first: vernacular voice via Bhashini (Govt of India), and an assisted mode
  that turns Bank Mitras / CSP kiosks into AI-augmented relationship managers — a channel
  no consumer chatbot addresses.
- Rakshak's Credit Passport aligns with the industry shift to alternative-data scoring for
  thin-file borrowers, and with RBI's broader fraud-prevention push (e.g., MuleHunter.AI,
  now live across 20+ banks).

BUSINESS MODEL / COMMERCIAL POTENTIAL
- B2B licence to SBI (replicable across PSU banks), priced per active customer per year,
  plus a setup/integration fee.
- Illustrative value per 1 crore active users (directional, to be validated in a pilot):
  - ~Rs.1,500 Cr/yr in service-cost savings (high query containment).
  - ~Rs.400 Cr/yr revenue uplift (better-targeted, consented product suggestions).
  - Credit Passport opens a large new, responsibly-underwritten lending segment among the
    ~480M credit-unserved adults — incremental loan-book growth with human-approved risk.
- Beyond ROI: measurable financial inclusion (scheme enrollments, reactivated dormant
  accounts, healthier savings behaviour) — aligned with SBI's public mandate.
- IP retained by me per hackathon rules; SBI may pilot/commercialise via licence.

COMPETITIVE DIFFERENTIATION
- Most teams will demo "savings nudges." We pair that with GOVERNED autonomy (a real
  Judge Agent that blocks unsafe actions live) and INCLUSIVE CREDIT for thin-file Indians.
- The moat is architecture, not the model: persistent Financial Life Graph + policy-as-code
  governance + the assisted Bank Mitra channel — none of which a stateless chatbot has.
- India-first: UPI-pattern intelligence + Bhashini vernacular + government-scheme integration.
```

---

## Field 5 — Technology Stack Details
```
Agents & reasoning:
- Claude API as the default customer-agent model (Disha + the platform agents).
- An independent, DIFFERENT model (e.g., GPT-4o-class) as the "Judge Agent" for genuine
  cross-validation — not one model checking itself.

Orchestration:
- Python + FastAPI backend.
- LangGraph for agent state management + routing (Disha <-> domain logic <-> Judge).
- n8n for business workflows (Lakshya sweep, Bill Sense alerts, Yojana enrollment).

Language / voice (India-first):
- Bhashini APIs (Govt of India) for vernacular ASR/TTS in Hindi + other Indian languages.
  (Used for language access — not as a fraud/biometric engine.)
- Azure Speech as a Hindi fallback.

Channels:
- WhatsApp Cloud API (primary engagement channel).
- Web UI for desktop customers.
- Bank Mitra kiosk simulator for rural/assisted mode.

Data layer:
- PostgreSQL for the Financial Life Graph (customers, accounts, transactions, Lakshya
  goals, Bill Sense upcoming payments, scheme eligibility, Credit Passport features,
  governance audit).
- pgvector for RAG over SBI product docs + scheme rules (PMJJBY, Sukanya Samriddhi, APY,
  PM-Kisan).
- 100% SYNTHETIC dataset: 1,000 simulated users x 12 months of UPI/bank history.
  No real customer data, no live banking APIs, and NO access to any confidential
  regulator database — a deliberate, honest de-risking choice for the prototype.

Credit Passport (alternative-data scoring) — prototype approach:
- An interpretable scoring function over synthetic behavioural features (payment
  regularity, cash-flow stability, bounce rate, income consistency). Kept transparent and
  explainable for the demo rather than a black-box model; output is an "eligible to apply"
  signal for a human banker, never an automated lending decision.

Governance & observability:
- Policy-as-code rule engine (RBI / UDAAP / KYC constraints encoded as Python rules).
- Autonomy tiers: auto (informational) / customer-confirm (money movement) /
  human-approval (any lending or account-restriction step).
- Immutable audit log (every action + Judge verdict + reason).
- Kill switch (DBS PURE-inspired).
- Langfuse for live agent traces shown during the demo.

Built solo with Claude Code (backend/agents) and Antigravity IDE (frontend/demo).
```

---

## Field 6 — Process Flow / Architecture
```
ENGAGEMENT FLOW (the governed loop):
1. Customer transacts normally (UPI, salary, bills) -> Financial Life Graph updates.
2. Disha reasons over the graph: detects a savings pattern (Lakshya), an upcoming
   shortfall (Bill Sense), a scheme match (Yojana Finder), or a credit-eligibility
   signal (Rakshak Credit Passport).
3. Disha drafts a proposed action (goal nudge, sweep, alert, enrollment, "eligible to
   apply" prompt).
4. GOVERNANCE INTERCEPT: the Judge Agent (a separate model) validates against policy-as-code:
   - Informational  -> auto-delivered.
   - Money movement (sweep, transfer) -> customer-confirm required.
   - Lending / account restriction -> human (banker) approval required.
   - Fails policy / unsafe -> BLOCKED with an explicit reason
     (e.g., "LIC premium due tomorrow — auto-sweep would risk a bounced-payment fee").
5. Approved action delivered via WhatsApp / voice (Bhashini) / kiosk in the customer's
   language.
6. Every step written to an immutable audit trail (shown live via Langfuse in the demo).

CREDIT PASSPORT FLOW (inclusion, fully human-gated):
1. Customer has no CIBIL history. Rakshak computes an explainable score from synthetic
   behavioural features (payment regularity, cash-flow stability, bounce rate).
2. Judge Agent checks the action is framed as "eligible to apply" only — no rate, no
   guarantee, no auto-approval.
3. Disha surfaces: "You may be eligible to apply for an SBI loan — start an application
   for a banker to review?"  -> routed to human approval (T3).

LAYERED ARCHITECTURE (top to bottom):
- CHANNELS: WhatsApp Cloud API | Web UI | Bhashini Voice | Bank Mitra kiosk
- ORCHESTRATOR / AGENT FABRIC: LangGraph (state + routing) | n8n (workflows) | memory
- CUSTOMER AGENTS: Swagat (acquire) | Guru (adopt) | Disha (engage) | Rakshak (protect + include)
- DOMAIN LOGIC: Lakshya Engine | Bill Sense | Yojana Finder | Credit Passport | Product (RAG)
- GOVERNANCE LAYER: Judge Agent (separate model) + policy-as-code + autonomy tiers
                    + immutable audit + kill switch
- DATA LAYER: Financial Life Graph (PostgreSQL) + RAG (pgvector) + synthetic data

(A full Mermaid architecture diagram is in the uploaded idea deck and the GitHub README.)
```

---

## Field 7 — Upload Your Idea Deck  [OPTIONAL — UPLOAD IT]
```
Upload: SBI_Sahayak_Idea_Deck.pptx
```
Suggested slides (if you refresh the deck to match v3):
1. Title + tagline ("A relationship manager for every Indian")
2. Problem (50 cr customers, RM gap, dormant accounts, unclaimed benefits)
3. Solution overview (Disha + Lakshya / Bill Sense / Yojana / Rakshak; governed)
4. Lakshya Engine flow (pattern -> opt-in goal -> gamified milestone)
5. Bill Sense + Yojana Finder (prevent penalties; enroll in schemes)
6. Rakshak (Credit Passport for the ~480M credit-unserved; Victim/Scam-Shield = roadmap)
7. Governance Core (Judge Agent + autonomy tiers + audit + kill switch) — the mic-drop
8. Architecture (5 layers, Mermaid)
9. Impact (illustrative; clearly labelled)
10. Why SBI wins (agentic-AI alignment; alt-data credit; RBI fraud-prevention context)
11. 30-day prototype plan (3 golden demo paths)
12. Solo builder + IP retained

---

## Field 8 — Demo Video Link  [OPTIONAL — SKIP]
```
Leave blank. Not expected at idea stage; won't affect shortlisting.
```

---

## Field 9 — GitHub Repository Link  [OPTIONAL — ADD IT]
```
https://github.com/udaygoel28/sbi-sahayak
```
Push before submitting. Repo should contain the README (with Mermaid diagram), the
schema, the architecture file, and the 30-day plan. Code files can be stubs at idea stage.

---

## THE 3 GOLDEN DEMO PATHS (what you actually build in 30 days if shortlisted)
1. Hindi WhatsApp Lakshya flow: detect savings pattern -> propose goal -> customer opts in.
2. The mic-drop: Disha attempts a sweep -> Judge Agent BLOCKS it (LIC premium tomorrow) ->
   shown live in the Langfuse audit panel.
3. Credit Passport: thin-file customer -> explainable score -> "eligible to apply" ->
   routed to human approval.
(Yojana Finder is a strong 4th if time allows. Victim-Shield / Scam-Shield stay roadmap.)

---

## SUBMISSION CHECKLIST
- [ ] Theme = Agentic AI & Emerging Tech
- [ ] Problem statement = Digital Engagement
- [ ] Fields 1 + 3 (REQUIRED) pasted
- [ ] Fields 4, 5, 6 pasted
- [ ] Deck uploaded (refresh to v3 scope if you can)
- [ ] GitHub repo pushed + public + linked
- [ ] Demo video skipped
- [ ] SUBMIT before 30 Jun 2026, 11:59 PM IST

## IF A JUDGE PROBES — be ready to say:
- "Where's the 480M figure from?" -> TransUnion CIBIL credit-unserved study.
- "Do you use RBI's MuleHunter data?" -> No. We align with public fraud-pattern thinking;
  we never access confidential regulator data. Victim-Shield protects unwitting victims.
- "Does the agent approve loans / move money on its own?" -> Never. Money movement is
  customer-confirmed; lending is human-approved. The Judge Agent enforces this.
- "Is the ROI real?" -> Illustrative and directional, to be validated in a pilot.
