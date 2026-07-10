# Deal Record — Schema

The small piece of shared state that makes Deskmate a pipeline instead of three tools. Contract Guard writes it once per client contract; Fee Chaser, Job Kit, and the desk view read it. **Nothing re-opens the contract PDF** — everything reads this record.

One record per **client contract** (not per placement). A client with a renewed/amended contract gets a new **version** of the same record (old versions retained for placements made under them).

---

## Fields

| Field | Type | Allowed / example values | Written from (clause) | Read by |
|---|---|---|---|---|
| `record_id` | string | `dr_acme_2026_v1` | system | all |
| `client_name` | string | "Acme Corp" | header | all |
| `contract_type` | enum | `msa` · `placement_agreement` · `subcontract` · `nda` | classify step | all |
| `status` | enum | `draft` · `live` · `archived` | lifecycle | all |
| `version` | int | 1, 2, … | on re-review | all |
| **Fee** | | | | |
| `fee_pct` | number | 20 (percent) | A2 | Job Kit, desk |
| `fee_base` | enum | `first_year_base` · `total_comp` · `ctc` · `unspecified` | A2 | Job Kit, desk |
| `fee_flat` | number\|null | e.g. 15000 (if flat fee, not %) | A2 | Job Kit, desk |
| **Payment** | | | | |
| `fee_earned_on` | enum | `acceptance` · `start_date` · `post_probation` | A1 | Fee Chaser |
| `payment_terms_days` | int | 30 · 60 · 90 | A3 | **Fee Chaser** (defines "late") |
| `late_interest` | string\|null | "1.5%/mo" · null | A3 | Fee Chaser |
| **Guarantee / fall-off** | | | | |
| `guarantee_days` | int | 30 · 90 · 180 | B2 | desk (guarantee clock) |
| `guarantee_type` | enum | `replacement` · `cash_refund` · `credit` | B1 | desk, risk warnings |
| `guarantee_prorated` | bool | true / false | B2 | desk |
| `guarantee_void_conditions` | bool | true (carve-outs present) / false | B3 | desk |
| **Ownership** | | | | |
| `ownership_window_months` | int\|null | 12 · 6 · null (absent = flagged) | C1 | backdoor-hire check |
| `non_circumvent` | bool | true / false | C2 | backdoor-hire check |
| `non_circumvent_covers_affiliates` | bool | true / false | C2 | backdoor-hire check |
| **Restrictions** | | | | |
| `exclusivity` | enum | `exclusive_paid` · `exclusive_unpaid` · `non_exclusive` | D4 | sourcing guardrail |
| `off_limits_scope` | enum | `placed_only` · `whole_company` · `none` | D3 | sourcing guardrail |
| `off_limits_months` | int\|null | 12 · null | D3 | sourcing guardrail |
| `liability_capped` | bool | true / false | D2 | risk summary |
| **Dates** | | | | |
| `effective_date` | date | 2026-07-01 | E | desk |
| `renewal_date` | date\|null | 2027-07-01 | E | desk (renewal nudge) |
| `expiry_date` | date\|null | null (evergreen) | E | lifecycle |
| `auto_renew` | bool | true / false | E | desk (renewal nudge) |
| **Provenance** | | | | |
| `source_file` | string | "acme-msa-signed.pdf" | system | audit |
| `reviewed_on` | date | 2026-07-10 | system | audit |
| `open_flags` | list | unresolved red flags at signing | review | risk summary |
| `full_text_stored` | bool | false (default) / true (user opt-in) | user choice | privacy |

**Absence handling:** where a field maps to a clause that was missing (e.g. `ownership_window_months: null`, `non_circumvent: false`), the corresponding **absence flag** from the clause library is recorded in `open_flags` — so the risk is remembered, not silently dropped.

---

## Example instance

```yaml
record_id: dr_acme_2026_v1
client_name: Acme Corp
contract_type: msa
status: live
version: 1

fee_pct: 20
fee_base: first_year_base
fee_flat: null

fee_earned_on: start_date
payment_terms_days: 30
late_interest: "1.5%/mo"

guarantee_days: 90
guarantee_type: replacement
guarantee_prorated: true
guarantee_void_conditions: true

ownership_window_months: 12
non_circumvent: true
non_circumvent_covers_affiliates: true

exclusivity: non_exclusive
off_limits_scope: placed_only
off_limits_months: 12
liability_capped: true

effective_date: 2026-07-01
renewal_date: 2027-07-01
expiry_date: null
auto_renew: true

source_file: acme-msa-signed.pdf
reviewed_on: 2026-07-10
open_flags: []
full_text_stored: false
```

---

## Lifecycle

```
draft ──(contract agreed/signed)──▶ live ──(expiry or termination)──▶ archived
                                      │
                                      └──(renewal / amendment)──▶ new version (v2), old kept
```

- **draft** — created at first review of an unsigned contract; terms provisional. Not yet read by Fee Chaser/Job Kit for live billing.
- **live** — contract in force. Authoritative source for all downstream skills.
- **archived** — contract ended, but **retained**. Ownership windows (`ownership_window_months`) and non-circumvent terms often outlive the contract, so archived records still answer "am I still owed a fee if they hire this candidate now?" Never hard-deleted by the system.
- **versioning** — a renewal/amendment creates `v(n+1)` in `live`; the prior version drops to `archived` but remains linked, so placements made under old terms still resolve against the terms that applied then.

---

## How each skill reads it

- **Fee Chaser** → `payment_terms_days` + `fee_earned_on` to decide whether an invoice is *actually* overdue (a "late" net-60 client isn't late at day 40); `late_interest` for reminder wording.
- **Job Kit / desk** → `fee_pct` + `fee_base` to compute a placement's expected fee; `guarantee_days`/`_type` to show the guarantee clock on active placements.
- **Sourcing guardrails (future)** → `off_limits_scope`, `exclusivity` to warn before sourcing out of a restricted account.
- **Backdoor-hire check** → `ownership_window_months` + `non_circumvent` to answer "is a fee still owed?" even after archive.
- **Desk renewal nudge** → `renewal_date` + `auto_renew` to warn before an evergreen contract silently renews.

---

## Storage & privacy

- One record per contract, stored in the **user's own Deskmate workspace** (local / their account) — not a shared cloud store.
- **Extracted terms only by default.** `full_text_stored: false` unless the user opts in to keep the source contract text.
- The source document is **never re-transmitted** by downstream skills — they read fields, not files.
- State this in the listing. Recruiters guard client contract data closely; "we keep the terms, not the contract, and only on your machine" is a trust feature, not fine print.

---

## Build order note

Build this schema **before Fee Chaser** — Fee Chaser's core logic ("is this invoice actually late?") depends on reading `payment_terms_days` and `fee_earned_on` from here. Contract Guard is the producer; Fee Chaser is the first consumer.
