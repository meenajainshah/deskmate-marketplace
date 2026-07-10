# Placement Ledger — Schema

The list of money owed to the desk. Where the **Deal Record** holds the *terms* (one per client
contract), the **placement ledger** holds the *invoices* (one row per placement fee). Fee Chaser
joins the two: the fee row says *how much and since when*; the client's Deal Record says *when
it's actually due*.

One row per **placement fee**. A row links to exactly one Deal Record (the contract it was placed
under) via `deal_record_id`. The ledger is the desk's accounts-receivable — Fee Chaser reads and
updates it; a future desk/cash-forecast view reads it too.

---

## Fields

| Field | Type | Allowed / example | Notes |
|---|---|---|---|
| `placement_id` | string | `pl_acme_jsmith_2026_03` | system |
| `deal_record_id` | string | `dr_acme_2026_v1` | **join key** to the Deal Record (terms) |
| `client_name` | string | "Acme Corp" | |
| `candidate` | string | "J. Smith" | who was placed |
| `role` | string | "Senior Backend Engineer" | |
| **Money** | | | |
| `fee_amount` | number | 24000 | the invoice value (from `fee_pct` × base, or `fee_flat`) |
| `currency` | string | "USD" | from the Deal Record |
| `amount_paid` | number | 0 · 12000 | partial payments accumulate here |
| **The clock** | | | |
| `fee_earned_on` | enum | `acceptance` · `start_date` · `post_probation` | copied from Deal Record `fee_earned_on` |
| `earned_date` | date\|null | 2026-06-01 · null | the date the clock actually starts; null if not earned yet |
| `invoice_number` | string\|null | "INV-1042" · null | null until invoiced |
| `invoice_date` | date\|null | 2026-06-01 | when invoiced |
| `payment_terms_days` | int | 30 · 60 · 90 | copied from Deal Record; defines the net window |
| `due_date` | date | 2026-07-01 | **computed** = earned/invoice date + terms (see below) |
| **State** | | | |
| `status` | enum | `not_yet_earned` · `not_due` · `due_soon` · `overdue` · `paid` · `written_off` | computed each run |
| `days_late` | int | 0 · 12 · 47 | computed; 0 unless overdue |
| `last_reminder_date` | date\|null | 2026-07-05 | when last chased |
| `last_reminder_rung` | int | 0–4 | escalation level last used (see reminder-library) |
| `client_payment_history` | enum | `reliable` · `average` · `repeat_late` · `unknown` | sets reminder tone |
| `notes` | string | "promised payment by 15th" | free text |

---

## Computing "actually overdue" (the core logic)

```
if fee_earned_on == post_probation and today < end of guarantee/probation window:
        status = not_yet_earned            # clock hasn't started — do NOT chase
        earned_date = null
else:
        earned_date = (acceptance | start_date | probation-end date, per fee_earned_on)
        due_date    = earned_date + payment_terms_days       # net window from the Deal Record
        if today <= due_date - 7:   status = not_due         # comfortably within terms
        elif today <= due_date:     status = due_soon         # within 7 days of due
        else:                        status = overdue
                                     days_late = today - due_date
                                     bucket = 1-30 | 31-60 | 60+
```

**Only `overdue` rows are chased by default.** `not_yet_earned` / `not_due` are reported as "on
track" and left alone; `due_soon` gets at most an optional soft heads-up.

If a fee row has **no `deal_record_id`** (placed before Contract Guard captured terms), Fee Chaser
can't compute the due date — flag it and ask the user for the terms (or the recruiter's default)
rather than assuming.

---

## Lifecycle

```
not_yet_earned ──(fee earned)──▶ not_due ──▶ due_soon ──▶ overdue ──(payment)──▶ paid
                                                              │
                                                              └──(uncollectable)──▶ written_off
```

- Partial payment: `amount_paid` rises; status stays `overdue` until `amount_paid >= fee_amount`.
- `paid` and `written_off` rows are retained (not deleted) — they feed `client_payment_history`
  for future tone decisions and the desk's cash history.

---

## How it links to the rest of Deskmate

- **Contract Guard** produces the **Deal Record** (`deal_record_id`, terms). Fee Chaser copies
  `fee_earned_on` and `payment_terms_days` from it onto each fee row and reads `late_interest`
  for reminder wording. The contract is never re-opened.
- **Fee Chaser** owns the ledger: sets `status`/`days_late`/`due_date`, records reminders and
  payments.
- **Desk / cash forecast (future)** reads `fee_amount`, `amount_paid`, `due_date` to project
  incoming cash and show what's at risk.

## Storage & privacy

- One ledger per user, stored in the user's own Deskmate workspace (local / their account).
- Holds fee amounts and client names — treat as sensitive; never transmit to third parties.
