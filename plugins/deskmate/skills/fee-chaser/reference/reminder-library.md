# Reminder Library — Fee Chaser source of truth

How to chase a fee without burning the client. The rung is chosen from **two axes**: how late the
fee is (aging bucket) and who the client is (payment history). Same amount of lateness gets a
different email from a reliable client than from a repeat offender.

**How the skill uses this:** for each *genuinely overdue* fee (see `placement-ledger-schema.md`),
pick the rung from the matrix, fill the template with ledger facts, and match the recruiter's voice.
Escalate on the *next* run using `last_reminder_rung` — never jump straight to firm on first contact
with a good client.

Golden rule: **the client is a future source of placements, not a debtor to win a fight with.**
Firm ≠ hostile. Never threaten interest, collections, or legal action the contract doesn't grant.

---

## The escalation ladder (rungs)

| Rung | Name | Tone | When |
|---|---|---|---|
| 0 | Soft heads-up | Friendly, pre-emptive | `due_soon` only, optional, reliable clients |
| 1 | Gentle nudge | "Probably slipped through" | 1–30 days late, first contact |
| 2 | Direct follow-up | Clear, specific, still warm | 31–60 late, or 2nd contact on a 1–30 |
| 3 | Firm reminder | Businesslike, cites terms/interest | 60+ late, or repeat-late client |
| 4 | Final notice before escalation | Formal, states next step | 60+ late after rung 3 ignored; **user-approved only** |

Move **one rung per contact**, not per day. Leave ~7 days between reminders (respect `last_reminder_date`).

## The matrix (aging × history → starting rung)

| Client history ↓ / Age → | 1–30 late | 31–60 late | 60+ late |
|---|---|---|---|
| `reliable` | Rung 1 | Rung 1→2 | Rung 2→3 |
| `average` / `unknown` | Rung 1 | Rung 2 | Rung 3 |
| `repeat_late` | Rung 1→2 | Rung 3 | Rung 3→4 |

Rung 4 always requires explicit user sign-off — it names a consequence.

---

## Wording rules

- **Lead with the facts, once:** candidate/role, invoice #, amount, original due date, days overdue.
  Pull every value from the ledger; invent nothing.
- **Make paying easy:** restate how to pay / offer to resend the invoice. Most late payment is
  friction, not refusal.
- **Interest only if earned:** mention late-payment interest *only* when the Deal Record's
  `late_interest` is set, and quote it exactly (e.g. "1.5% per month per our agreement").
- **One ask, one deadline:** a specific, near date ("by Friday the 18th") beats "ASAP."
- **Never** guilt-trip, threaten, cc the candidate, or reference collections/legal below rung 4.
- Match the recruiter's own voice if known; otherwise warm-professional.

---

## Templates (fill the {braces} from the ledger / Deal Record)

**Rung 0 — Soft heads-up** (due_soon, optional)
> Subject: Upcoming invoice {invoice_number} — {client_name}
> Hi {name}, quick heads-up that invoice {invoice_number} for {candidate}'s placement
> ({amount}) is due {due_date}. Happy to resend it if useful — thanks!

**Rung 1 — Gentle nudge** (1–30, first contact)
> Subject: Invoice {invoice_number} — {candidate} placement
> Hi {name}, just following up on invoice {invoice_number} ({amount}) for {candidate}'s
> placement, which was due {due_date}. Guessing it slipped through — could you let me know
> it's in the queue? Happy to resend. Thanks so much!

**Rung 2 — Direct follow-up** (31–60, or 2nd contact)
> Subject: Overdue: invoice {invoice_number} ({days_late} days) — {client_name}
> Hi {name}, invoice {invoice_number} for {candidate}'s placement ({amount}) is now
> {days_late} days past its {due_date} due date. Could you confirm the payment date, or flag
> anything holding it up? I'll resend the invoice alongside this. Appreciate it.

**Rung 3 — Firm reminder** (60+ or repeat-late)
> Subject: Payment required: invoice {invoice_number} — {days_late} days overdue
> Hi {name}, invoice {invoice_number} ({amount}) for {candidate}'s placement remains unpaid
> {days_late} days after its {due_date} due date. {interest_line} Please arrange payment by
> {deadline}, or let me know the specific date I can expect it. Thanks for sorting this out.
>   — where {interest_line} = "Per our agreement, overdue amounts accrue {late_interest}." only if late_interest is set; otherwise omit.

**Rung 4 — Final notice** (user-approved only)
> Subject: Final reminder before escalation — invoice {invoice_number}
> Hi {name}, despite previous reminders, invoice {invoice_number} ({amount}) for {candidate}'s
> placement is {days_late} days overdue. Please settle it by {deadline}. If payment isn't
> received, I'll need to escalate this per our agreement. I'd much rather resolve it directly —
> please get in touch.

---

## Grouping & cadence

- **Several overdue for one client** → one grouped email listing each invoice/amount/date, at the
  rung of the *most* overdue item. Don't send a client five separate emails.
- **Cadence** → one contact per client per ~7 days; escalate a rung each contact until paid or the
  user pauses/writes it off.
- Always log `last_reminder_date` + `last_reminder_rung` so the next run picks up where this left off.

---

## Anti-over-chasing rule

If nothing is genuinely overdue, **say so and send nothing**: *"Everything's within terms — no fees
to chase today."* Fee Chaser earns trust by *not* nagging clients who are paying on time. A tool
that fires reminders at on-time clients gets uninstalled — and costs the recruiter the relationship.
