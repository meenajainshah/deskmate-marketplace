# Deskmate

**The back office for solo recruiters and small staffing shops.** Deskmate doesn't find candidates — you've got tools for that. It handles the admin *around* the placement that quietly costs you money and time.

## v1 — Contract Guard

Upload a recruiting contract (client MSA, terms of business, placement/fee agreement, candidate offer letter, NDA, or subcontract) and get:

- a plain-English summary of what you're signing,
- severity-rated red flags focused on the clauses recruiters actually lose money on — the fall-off/guarantee, the fee-earning trigger, candidate ownership windows, non-circumvent, uncapped indemnity,
- suggested redlines with ready-to-paste language,
- an optional marked-up DOCX to send back.

Works from a file upload with **zero connectors**. US-framed (at-will, USD, CCPA). **Not legal advice** — always review with an attorney before signing.

> **Marked-up DOCX export — dependencies.** The optional redlined-DOCX output (Word tracked changes + comments) is produced through the host `docx` skill, whose default path uses Node (`docx-js`), and `pandoc`/LibreOffice for reading and rendering. On machines without those installed, Contract Guard falls back to a dependency-free builder (Python standard library `zipfile` + hand-authored OOXML) that produces the same tracked-change DOCX; only the optional visual render (PDF/image preview) is skipped. No install steps are required for the review itself — the DOCX is only generated on request.

Contract Guard also captures the agreed terms into a small **Deal Record** that later Deskmate skills read, so the contract is understood once and never re-opened.

## v2 — Fee Chaser

The first skill to read the Deal Record. Point it at your open placements and it tells you what's *actually* overdue — reading each client's real payment terms, so a net-60 invoice at day 40 is left alone and a genuinely late one gets chased.

- resolves the real due date from the client's terms (`fee_earned_on` + `payment_terms_days`), not the invoice date,
- ranks the truly-overdue fees by exposure × age,
- drafts **tone-matched reminders** — gentle for a reliable client who's a few days late, firm (citing contractual interest, if any) for a repeat-late one,
- **never sends or charges automatically** — you approve every reminder,
- tracks each nudge so the next run escalates instead of repeating.

Run `/deskmate:fee-chaser` or ask "who owes me money?" / "any overdue invoices?".

## v3 — Job Kit

Turn a client's rough req into a full working kit for the role, tied to the same Deal Record:

- a polished, candidate-facing **job description** (must-haves vs. nice-to-haves, honest and un-inflated),
- a **structured interview guide + 1–5 scoring rubric** mapped to the must-haves, so candidates are compared on the same bar,
- an **offer-letter template** (draft only — never sent or signed),
- **priced up front**: reads `fee_pct` × `fee_base` to show the expected fee, and surfaces the guarantee window you'll inherit on hire.

When the role is filled, its **Role Brief** spawns the placement-ledger row Fee Chaser chases — so the fee you priced is the fee you collect. Run `/deskmate:job-kit` or ask "polish this JD" / "build me an interview guide."

## Roadmap

Cash forecast · dual-pipeline CRM cleanup · Monday/Friday desk briefs.

## Install

```
/plugin marketplace add meenajainshah/deskmate-marketplace
/plugin install deskmate@deskmate-marketplace
```

> The marketplace repo is **private**. To install, your GitHub account must have access and be authenticated (`gh auth login`).

Then run `/deskmate:contract-guard` or just upload a contract and ask "any red flags?".

## Usage

```
/deskmate:contract-guard
```

Or upload a contract and say "review this" / "what am I signing?" / "check the payment terms."

---

© iView Labs. Deskmate provides informational contract analysis, not legal advice.
