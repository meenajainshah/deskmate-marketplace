# Role Brief — Schema

The record of a role the desk is working. It sits between the **Deal Record** (client terms, one
per contract) and the **placement ledger** (fees owed, one per hire): a Role Brief is one **open
requisition**, priced against the client's terms, that becomes a ledger row when it's filled.

One record per **role/req**. Links to exactly one Deal Record via `deal_record_id` (the contract
governing that client's placements). Job Kit writes it; the desk view reads it; on placement it
spawns a placement-ledger row for Fee Chaser.

---

## Fields

| Field | Type | Allowed / example | Notes |
|---|---|---|---|
| `role_id` | string | `role_acme_be_2026_07` | system |
| `deal_record_id` | string\|null | `dr_acme_2026_v1` · null | **join** to client terms; null if no Deal Record yet (flagged) |
| `client_name` | string | "Acme Corp" | |
| `title` | string | "Senior Backend Engineer" | |
| `level` | enum | `junior` · `mid` · `senior` · `staff` · `lead` | |
| `location` | string | "Remote (US)" · "Ahmedabad, hybrid" | |
| **Comp & fee** | | | |
| `comp_min` / `comp_max` | number | 140000 / 170000 | first-year base range |
| `comp_target` | number\|null | 155000 | used to price the fee; ask if unknown |
| `currency` | string | "USD" | from the Deal Record |
| `expected_fee` | number\|null | 31000 | **computed** = `fee_pct` × `fee_base`(comp_target); null if terms unknown |
| **The role** | | | |
| `must_haves` | list | ["5y backend", "Go or Java", "distributed systems"] | drive the rubric |
| `nice_to_haves` | list | ["fintech", "k8s"] | never gate on these |
| `guarantee_days` | int\|null | 90 | copied from Deal Record `guarantee_days` |
| `guarantee_type` | enum\|null | `replacement` · `cash_refund` · `credit` | the fall-off clock you inherit on hire |
| **State** | | | |
| `status` | enum | `open` · `interviewing` · `offer` · `placed` · `closed` | lifecycle |
| `candidate` | string\|null | "J. Smith" | set when placed |
| `start_date` | date\|null | 2026-09-01 | set when placed → starts the fee/guarantee clocks |
| `created` | date | 2026-07-10 | system |
| `notes` | string | "HM wants to close by Sept" | free text |

---

## Computing the expected fee

```
if deal_record_id and comp_target:
        base = comp_target if Deal Record fee_base == first_year_base else <resolve per fee_base>
        expected_fee = round(fee_pct/100 * base)      # or fee_flat if the Deal Record is a flat fee
else:
        expected_fee = null      # flag: capture terms (Contract Guard) and/or target comp
```

State the expected fee at intake — it tells the recruiter what the role is worth before sourcing.

---

## Lifecycle

```
open ──▶ interviewing ──▶ offer ──▶ placed ──(candidate starts)──▶ [spawns placement-ledger row]
   └───────────────────────────────▶ closed (role pulled / filled elsewhere)
```

- **placed → ledger:** when `status = placed` and `start_date` is set, create a placement-ledger
  row (see Fee Chaser's `placement-ledger-schema.md`) with `deal_record_id`, `client_name`,
  `candidate`, `fee_amount = expected_fee`, and `fee_earned_on` / `payment_terms_days` copied from
  the Deal Record. The clocks Fee Chaser runs on all start here.
- **closed** roles are retained (not deleted) — they feed fill-rate and client-history stats.

---

## How it links to the rest of Deskmate

- **Contract Guard → Deal Record** gives the terms Job Kit prices against (`fee_pct`, `fee_base`,
  `guarantee_*`). Never re-open the contract.
- **Job Kit** owns the Role Brief: the JD, rubric, and offer draft attach to it; it computes
  `expected_fee` and carries the guarantee window.
- **Fee Chaser** picks up where a placed Role Brief leaves off — the fee priced here becomes the
  ledger row chased there.
- **Desk view (future)** reads open Role Briefs for pipeline value (sum of `expected_fee`) and
  guarantee clocks on recent placements.

## Storage & privacy

- One set of Role Briefs per user, stored in the user's own Deskmate workspace.
- Holds client names, comp, and candidate names — treat as sensitive; never transmit to third parties.
