---
name: fee-chaser
description: >
  Chases unpaid placement fees — but only the ones that are actually overdue. Reads
  each client's Deal Record (from Contract Guard) to know the real payment terms, so a
  net-60 client at day 40 is left alone and a genuinely late invoice gets a tone-matched
  reminder. Use when the user asks "who owes me money," "chase unpaid fees," "any overdue
  invoices," "follow up on that placement fee," "is this invoice actually late," or "send
  a payment reminder." Works from a local ledger + Deal Records with zero connectors.
  Never sends or charges automatically. Not collections or legal advice.
allowed-tools: Read, Write, Bash
---

# Fee Chaser

Chase unpaid placement fees with precision: figure out what's *actually* overdue from each
client's agreed terms, rank it by what's worth chasing, and draft reminders matched to the
client and the aging — for the user to approve and send. Never dun a client who isn't late.

**The edge:** a generic reminder tool chases anything past the invoice date. Fee Chaser reads
the **Deal Record** — `payment_terms_days`, `fee_earned_on`, `late_interest` — so it knows a
net-60 invoice at day 40 is *on time*, and only chases fees the client genuinely owes now.

## Step 1 — Load the books

Read two things:

1. **Deal Records** — the per-client terms Contract Guard captured (see Contract Guard's
   `deal-record-schema.md`). These define, per client: when a fee is *earned*, the net window,
   and whether late interest applies.
2. **The placement ledger** — the outstanding fees, following `reference/placement-ledger-schema.md`.
   If no ledger exists yet, ask the user to paste or point to their open placements (client,
   candidate/role, fee amount, invoice #, invoice/earned date, anything paid). Accept a CSV or a
   pasted list; create the ledger from it so it's reusable next time.

If a fee has **no matching Deal Record**, don't guess the terms — flag it and ask (or assume the
recruiter's stated default) before treating it as late.

## Step 2 — Decide what's ACTUALLY overdue (the core)

For each open fee, resolve the real status from the client's Deal Record — never from the invoice
date alone:

- **`fee_earned_on`** sets when the clock starts: `acceptance` → offer accepted · `start_date` →
  candidate's first day · `post_probation` → after the guarantee/probation window. **If the fee
  isn't earned yet** (e.g. `post_probation` terms and the candidate is still inside the window),
  it is **not collectable** — do not chase it. Note it as pending.
- **Due date** = earned date + `payment_terms_days` (net-30/60/90). Use `date` math, don't eyeball it.
- **Status buckets** (as of today):
  - `not_yet_earned` — fee clock hasn't started · leave alone
  - `not_due` — within the net window · leave alone
  - `due_soon` — due within 7 days · optional soft heads-up only
  - `overdue` — past due, bucketed **1–30 / 31–60 / 60+** days late

**Do not chase `not_yet_earned`, `not_due`, or (by default) `due_soon`.** Chasing a client who is
still inside their agreed terms damages the relationship and is the fastest way to get Fee Chaser
switched off. Say plainly what's on track and why.

## Step 3 — Rank what's worth chasing

Order the truly-overdue fees by **exposure × age** (amount owed weighted by days late) so the user
works the biggest, oldest ones first. For each, pull the client's **payment history** from the
ledger (reliable payer vs. repeat-late) — this sets the tone in the next step, not just the order.

## Step 4 — Draft the reminders (tone-matched)

Load `reference/reminder-library.md`. Choose the escalation rung from the **aging bucket** and the
**client's history**, not a one-size email:

- a good client 3 days over → a light, assume-it-slipped nudge
- a repeat-late client 45 days over → firm, specific, and cite the late-payment interest **if and
  only if** the Deal Record's `late_interest` is set

Every draft states the facts from the ledger — candidate/role, invoice #, **amount**, original **due
date**, **days overdue** — and never invents numbers or threatens beyond the contract. Match the
recruiter's own voice where known. One draft per overdue fee (or one grouped email per client if
several are overdue for the same client).

## Step 5 — Review, then queue (never auto-send)

Present the drafts for approval. **Never send, charge, or issue anything automatically** — the user
sends (or a host mail/payments skill drafts it on request). On approval, mark the ledger row with
the **reminder date and rung** so the next run escalates instead of repeating the same email, and
so a client isn't pinged twice in a week. Record partial payments against the fee.

## Guardrails

- **Never auto-send or auto-charge.** Draft, then a human approves and sends.
- **Never chase a fee that isn't actually due** per the Deal Record — that precision is the point.
- **Late fees/interest only if the contract grants them** (`late_interest` present). Don't threaten
  interest, collections, or legal action the agreement doesn't support.
- **Use ledger values only** — never fabricate invoice numbers, amounts, or dates.
- Not collections or legal advice. For formal collections/legal escalation, hand back to the user.
- Store the ledger locally in the user's workspace; it holds fee amounts and client names — treat
  it as sensitive.

## Output shape

```
💸 Fee Chaser — {n} open fees · {x} actually overdue · ${total} at risk
✅ ON TRACK (not chasing)   {client — reason: within net-{d}, or fee not yet earned}
🔴 OVERDUE ({x})            {client · candidate · $amount · due {date} · {days}d late · bucket}
✉️ DRAFTS                   {one reminder per overdue fee, tone-matched}
→ Approve which to send? (all / pick / edit) — I never send on my own.
```

## Reference

- `reference/placement-ledger-schema.md` — the open-fee ledger: fields, how each links to a Deal
  Record, lifecycle, and how "actually overdue" is computed.
- `reference/reminder-library.md` — the escalation ladder: tone tiers by aging × history, wording
  rules, and ready-to-paste reminder templates.
