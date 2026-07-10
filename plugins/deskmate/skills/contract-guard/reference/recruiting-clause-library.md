# Recruiting Clause Library — Contract Guard source of truth

The domain IP behind Contract Guard. Each entry: what the clause is, where to look, default severity, the fair-market benchmark, why it hurts the recruiter, and ready-to-paste redline language.

**How the skill uses this:** after classifying the contract type, run the clauses tagged for that type. Rate severity off the *actual* language, using the default as a starting point. If a protective clause is **absent**, that is itself a flag (see "absence flags" at the end).

**US framing.** Benchmarks reflect US contingency-recruiting norms (fees as % of first-year base; at-will employment). Flag jurisdiction assumptions on every run.

Severity key: 🔴 High (can cost real money / open-ended risk) · 🟡 Medium (worth negotiating) · 🟢 Low (note it, usually fine).

---

## A. Money & when you get paid

### A1 — Fee-earning trigger 🔴
**Applies to:** MSA, placement agreement, subcontract.
**Look for:** the moment the fee is "earned" and the moment it's "payable." Phrases: "earned upon commencement," "upon the candidate's start date," "after completion of the probationary period," "invoiced upon acceptance."
**Fair benchmark:** fee earned on the candidate's **start date**, invoiced same day. "Earned after probation" or "payable only after 90 days employment" shifts months of risk onto you.
**Why it hurts:** ties your cash to the candidate surviving a probation you don't control. Combined with a long fall-off (B1), you can do the work and get paid nothing.
**Redline:**
> "The Fee is **earned on the Candidate's start date** and payable within [30] days of the start date, independent of any probationary period."

### A2 — Fee base 🔴
**Applies to:** MSA, placement agreement.
**Look for:** what the % is calculated on. "Annual salary," "first-year base," "total remuneration," "total compensation including bonus, commission, sign-on and equity," "CTC."
**Fair benchmark:** a clearly named base — most US contingency fees are a % of **first-year base salary**. Ambiguity ("total remuneration") is the risk, in either direction: it can shrink your fee (client argues base only) or expose you to clawback disputes.
**Why it hurts:** a 20% fee on a $120K base is $24K; if the client later argues the base excludes a $20K bonus you'd counted, you're arguing over $4K with no clear language.
**Redline:**
> "The Fee equals [20]% of the Candidate's **first-year annualised base salary**, excluding bonus, commission, equity and sign-on unless expressly stated."

### A3 — Payment terms / net window 🟡
**Applies to:** all.
**Look for:** "net 30 / 60 / 90," "within X days of invoice," late-payment interest, whether interest accrues.
**Fair benchmark:** **net-30**. Net-60 is a cash-flow drag for a solo shop; net-90 is a red flag. Late-payment interest should exist (statutory or ~1.5%/mo).
**Why it hurts:** you fronted the entire search cost. Net-90 means a quarter's wait, and without an interest clause there's no cost to the client paying late.
**Redline:**
> "Invoices are payable **net-30**. Overdue amounts accrue interest at 1.5% per month."

### A4 — Fee reduction / discount triggers 🟡
**Applies to:** MSA.
**Look for:** volume-discount language, "preferred rate on subsequent hires," MFN ("most favoured nation") clauses forcing you to match your lowest rate to any other client.
**Fair benchmark:** volume discounts are fine if *you* offered them; MFN clauses are not — they cap your pricing power across your whole book.
**Redline:** delete MFN language; scope any discount to named, agreed volume tiers.

---

## B. The fall-off / guarantee (the #1 money-loss clause)

### B1 — Refund vs. replacement 🔴
**Applies to:** MSA, placement agreement.
**Look for:** what happens if the candidate leaves within the guarantee window — "refund," "credit," "free replacement," "pro-rata refund."
**Fair benchmark:** **replacement-first** (you re-run the search) with a cash refund only if you can't fill it. A straight cash refund is the worst outcome for you.
**Why it hurts:** a full cash refund means you return money already earned and spent, with zero recourse. Replacement keeps the value in labour, not cash.
**Redline:**
> "If the Candidate leaves within the Guarantee Period, the Agency will provide **one replacement search at no additional fee**. A pro-rata cash refund applies only if the Agency cannot present a suitable replacement within [30] days."

### B2 — Guarantee length & proration 🔴
**Applies to:** MSA, placement agreement.
**Look for:** the window (30/60/90/180 days) and whether the refund/credit **prorates** by days worked or is all-or-nothing.
**Fair benchmark:** **90 days**, **prorated** (candidate leaves day 45 of 90 → you owe ~half, not all). 180+ days or a full-refund cliff on day 89 is aggressive.
**Why it hurts:** a non-prorated 90-day cliff means a departure at day 88 costs you the entire fee even though the client got 3 months of work.
**Redline:**
> "The Guarantee Period is [90] days from start date. Any refund is **prorated** based on days worked (refund = Fee × (days remaining in period ÷ total period))."

### B3 — Guarantee void conditions 🟡
**Applies to:** MSA, placement agreement.
**Look for:** whether the guarantee survives events outside the candidate's control — layoff, restructure, role elimination, client non-payment, client-caused resignation.
**Fair benchmark:** guarantee is **void** if the departure isn't the candidate's own doing (redundancy, client breach, non-payment).
**Why it hurts:** without carve-outs, you owe a refund when the client lays the person off for budget reasons — a risk you can't underwrite.
**Redline:**
> "The Guarantee does not apply where the Candidate's departure results from redundancy, restructuring, role elimination, change of client circumstances, or the Client's breach (including late payment of the Fee)."

---

## C. Who owns the candidate

### C1 — Candidate ownership / source window 🔴
**Applies to:** MSA, placement agreement, subcontract.
**Look for:** a period during which a candidate you introduced "belongs" to you — "introduction," "for [12] months from the date of submission," "ownership period."
**Fair benchmark:** **6–12 months** from submission; if the client hires that candidate (any role) within the window, the fee is owed.
**Why it hurts (absence):** with no ownership window, a client can pass on your candidate, then hire them 4 months later for a different role and owe you nothing. This is the classic "backdoor hire."
**Redline:**
> "Where the Client (or an Affiliate) employs or engages a Candidate introduced by the Agency **within 12 months** of introduction, in any role, the full Fee is payable."

### C2 — Non-circumvent 🔴
**Applies to:** MSA, NDA, subcontract.
**Look for:** language stopping the client from going directly to your candidate/source to avoid the fee, and whether it covers **affiliates/subsidiaries**.
**Fair benchmark:** present, and explicitly extended to the client's affiliates, parent, and subsidiaries.
**Why it hurts:** without affiliate coverage, the candidate gets hired by the client's sister company and the introduction fee evaporates.
**Redline:**
> "The Client shall not circumvent the Agency by engaging any introduced Candidate directly or **through any Affiliate, parent, or subsidiary**. This survives termination for [12] months."

### C3 — Backdoor / onward-referral hire 🟡
**Applies to:** MSA.
**Look for:** whether the fee is still owed if the client refers your candidate to a third party who hires them.
**Fair benchmark:** fee owed on any hire traceable to your introduction, including onward referral.
**Redline:** extend C1 language to "or refers the Candidate to a third party who subsequently engages them."

---

## D. What they can make you do or eat

### D1 — Indemnification 🔴
**Applies to:** all.
**Look for:** you (agency) indemnifying the client — for "any losses arising from the Candidate," misrepresentation, negligence, right-to-work/background failures. Critically, whether it's **capped**.
**Fair benchmark:** narrow indemnity (your own fraud/gross negligence, or breach of your screening reps), **capped at the fee paid** for that placement.
**Why it hurts:** an uncapped indemnity for "any loss arising from the Candidate" can dwarf the fee — you're insuring the client against their own hire.
**Redline:**
> "The Agency's aggregate liability and indemnity obligations under this Agreement are **capped at the Fee paid for the relevant placement**, and exclude losses arising from the Candidate's performance once employed by the Client."

### D2 — Liability cap 🔴
**Applies to:** all.
**Look for:** a cap on total liability; absence of one; carve-outs.
**Fair benchmark:** liability **capped at fees paid**; only fraud/wilful misconduct excluded from the cap.
**Why it hurts:** no cap = open-ended exposure for a business with no legal team.
**Redline:** add a liability cap at fees paid if none exists.

### D3 — Off-limits / non-solicit of placed candidates 🟡
**Applies to:** MSA, subcontract.
**Look for:** you agreeing not to recruit *out of* the client, or not to re-place candidates you placed there — and the **scope** (whole company vs. specific team) and **duration**.
**Fair benchmark:** limited to **candidates you actually placed**, for a **defined period** (e.g. 12 months). "Never solicit anyone at the entire company, forever" is over-broad.
**Why it hurts:** an over-broad off-limits sterilises a whole company from your future sourcing.
**Redline:**
> "The Agency agrees not to solicit **Candidates it placed with the Client** for [12] months following their placement. This does not extend to the Client's other employees or to candidates who approach the Agency independently."

### D4 — Exclusivity 🟡
**Applies to:** MSA, placement agreement.
**Look for:** whether you're sole agency or contingent among several; whether exclusivity is **paid** (retainer) or free.
**Fair benchmark:** exclusivity is fine **if compensated** (retainer or engagement fee). Free, one-sided exclusivity that also lets the client hire through other channels is a trap.
**Redline:** either add a retainer for exclusivity, or convert to non-exclusive/contingent.

### D5 — Candidate data / PII handling 🟢
**Applies to:** all.
**Look for:** obligations you accept for handling candidate personal data — CCPA/CPRA (California) references, data-transfer, breach-notification duties.
**Fair benchmark:** reasonable, mutual data terms. Note (don't alarm) any one-sided data-liability you're accepting.
**Redline:** make breach/data obligations mutual and proportionate.

---

## E. Generic business clauses (run on every contract in addition to A–D)

- 🟡 **Auto-renewal + short cancellation window** — evergreen term with a narrow opt-out (e.g. must cancel 90 days before renewal).
- 🟡 **Unilateral change rights** — client can change terms/rates without your consent.
- 🟡 **Assignment** — client can assign the contract (and your obligations) without consent.
- 🟢 **IP / work product** — usually minor for recruiting, but check any broad IP-transfer language.
- 🟢 **Governing law & venue** — flag if it's an inconvenient/foreign jurisdiction.
- 🟢 **Termination** — how either side exits; notice period; survival of fee obligations post-termination (should survive — ties to C1/C2).

---

## Absence flags (flag what's *missing*)

A fair recruiting contract should contain these; if a scan doesn't find them, flag the gap — don't invent language:
- No **candidate ownership window** (C1) → 🔴 backdoor-hire exposure.
- No **non-circumvent** (C2) → 🔴 fee can be avoided directly.
- No **liability cap** (D2) → 🔴 open-ended exposure.
- No **guarantee void conditions** (B3) → 🟡 you may owe refunds for client-caused departures.
- No **late-payment interest** (A3) → 🟡 nothing deters slow payment.

---

## Anti-over-flagging rule

A fair, balanced contract should return a short flag list or none. **Do not manufacture flags to look thorough.** If clauses A–D are present and reasonable, say so plainly: *"This is a balanced agreement — nothing here needs pushback."* A tool that cries wolf gets uninstalled.

---

## Fields this library feeds into the Deal Record

When terms are agreed, these extracted values populate the Deal Record (see `deal-record-schema.md`): fee % (A2), fee base (A2), payment terms/trigger (A1, A3), guarantee length + type + proration (B1, B2), ownership window (C1), non-circumvent term (C2), exclusivity/off-limits (D3, D4), key dates (E).
