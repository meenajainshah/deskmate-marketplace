---
name: contract-guard
description: >
  Reviews recruiting contracts in plain English and flags the clauses that cost
  recruiters money. Use when the user uploads or mentions a client MSA, terms of
  business, placement/fee agreement, candidate offer letter, NDA, or subcontract,
  or says "review this contract," "what am I signing," "any red flags," "check the
  payment terms," or "is this fee/rebate clause normal." Works from a file upload
  with zero connectors. Not legal advice.
allowed-tools: Read, Bash
---

# Contract Guard

Review a recruiting contract: explain it plainly, flag the risky clauses with severity,
suggest redlines, and capture the agreed terms into a Deal Record the rest of Deskmate reads.

**Always end every review with:** "This is not legal advice — have an attorney review before signing."

## Step 1 — Load & classify

Read the uploaded PDF/DOCX. Detect the contract type, because the checklist differs:

- **Client MSA / Terms of Business** — governs all placements
- **Placement / fee agreement** — one-role version
- **Candidate offer letter** — client↔candidate (you're reviewing it)
- **NDA / non-circumvent**
- **Subcontract / MSP agreement** — you as sub to another agency

State the detected type and invite correction: *"This looks like a client Terms of Business — tell me if it's something else."* If the file isn't a contract (e.g. a resume), say so and ask for the right file. Don't hallucinate a review.

## Step 2 — Plain-English summary

Three short paragraphs: what the deal does (who / what / fee / term) · what the recruiter must do · what they get and how they exit.

## Step 3 — Red-flag list

Load `reference/recruiting-clause-library.md` and run the clauses tagged for the detected type, **plus** the generic clauses on every contract. Rate each off the actual language:

🔴 High (can cost real money / open-ended risk) · 🟡 Medium (worth negotiating) · 🟢 Low (note it)

Format each flag:
```
{🔴/🟡/🟢} {Clause} — {what it says in plain English} — {why it hurts you as the recruiter} — Fix: {redline}
```

The clauses that matter most for recruiters (full detail + fair benchmarks + redline language in the library): fee-earning trigger, fee base, payment terms, the fall-off/guarantee (refund-vs-replacement, length, proration, void conditions), candidate ownership window, non-circumvent, indemnity, liability cap, off-limits, exclusivity.

**Flag what's missing.** If a protective clause is absent (no ownership window, no non-circumvent, no liability cap), flag the absence — see "Absence flags" in the library. Don't invent language that isn't there.

**Don't over-flag.** A fair, balanced contract should return a short list or none. If clauses are present and reasonable, say so plainly: *"This is a balanced agreement — nothing here needs pushback."* A tool that cries wolf gets uninstalled.

## Step 4 — Redlines + export

Produce specific edits:
```
§{section}: DELETE "{original}" / INSERT "{suggested}"  — Reason: {one line}
```
Offer a marked-up DOCX (the host `docx` skill can build it). Never overwrite the original file — export a new one. Never sign, send, or modify any DocuSign envelope.

## Step 5 — Capture the Deal Record

Once terms are agreed (or from the reviewed draft), extract the key values into a per-client Deal Record following `reference/deal-record-schema.md` (fee %, fee base, payment terms/trigger, guarantee, ownership window, non-circumvent, exclusivity/off-limits, key dates). The contract is read once; the rest of Deskmate reads the record, never the PDF. Record any absence flags in `open_flags` so the risk is remembered, not dropped.

## Guardrails

- Not legal advice — caveat every output.
- Never sign / send / modify the original or a DocuSign envelope.
- Never overwrite the original file.
- US framing (at-will, CCPA, USD); state that jurisdiction assumptions are US.
- Store the Deal Record locally with extracted terms only unless the user opts to keep full text.

## Output shape

```
📄 Contract Guard — {type}
WHAT THIS IS      {3-paragraph summary}
🚩 RED FLAGS ({n}: {x} high, {y} medium)   {flags}
✏️ SUGGESTED REDLINES   {§ edits}
→ Want a marked-up DOCX? (yes / where to save)
⚠️ Not legal advice — have an attorney review before signing.
```

## Reference

- `reference/recruiting-clause-library.md` — the clause-by-clause IP: what to look for, fair benchmark, why it hurts, redline language.
- `reference/deal-record-schema.md` — the Deal Record fields, lifecycle, and which downstream skill reads each.
