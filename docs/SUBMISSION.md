# Deskmate — submission & launch assets

Everything needed to submit Deskmate to the Anthropic community catalog and to launch it publicly. Keep this in sync with `plugin.json` / `README.md`.

**Status:** Submitted to the community catalog (clau.de/plugin-directory-submission) on **2026-07-10** — *pending review*. Launch/promotion is on hold until the catalog listing is accepted. Acceptance appears in `github.com/anthropics/claude-plugins-community` (nightly mirror).

---

## Community-catalog submission

**Plugin name:** Deskmate

**One-line description:**
> The back office for solo recruiters and small staffing shops — reviews contracts, chases overdue placement fees, and builds role kits from one shared record.

**Category:** Productivity / Business

**Keywords:** recruiting, staffing, contracts, placement fees, invoices, recruiter, agency, back-office

**Full description:**
> Deskmate handles the admin *around* the placement — the part that quietly costs recruiters money and time — without an ops team. It's not a sourcing tool or an ATS; it runs the desk.
>
> Contract Guard reviews a recruiting contract (client MSA, terms of business, placement/fee agreement, NDA, or subcontract) in plain English, flags the clauses recruiters actually lose money on — the fall-off/guarantee, fee-earning trigger, candidate ownership window, non-circumvent, uncapped indemnity — suggests redlines, and captures the agreed terms into a small **Deal Record**. Fee Chaser reads that Deal Record to know each client's real payment terms, so it chases only the fees that are *genuinely* overdue and drafts tone-matched reminders you approve before sending. Job Kit turns a client's req into a polished job description, a structured interview guide with a 1–5 scoring rubric, and an offer-letter template — priced up front against the same terms.
>
> The contract is understood once; every skill reads the shared record. Works from a file upload with zero connectors. US-framed. Not legal advice.

**Target users:** Solo/independent recruiters and small staffing agencies without a back-office or ops team.

**Example use cases (with prompts):**
1. **"What am I signing?"** — Upload a client MSA → *"any red flags?"* → plain-English summary, severity-rated flags, redlines, and a marked-up DOCX.
2. **"Who owes me money?"** — *"any overdue invoices?"* → only the fees actually past their real due date (skipping clients still within net terms), each with the right-toned reminder drafted.
3. **"Turn this req into a kit."** — Paste a rough role → *"polish this JD and build me an interview guide"* → candidate-facing JD, scored interview rubric, offer template, and the placement's expected fee computed.
4. **"Is this fee/rebate clause normal?"** — Ask about a clause → fair-market benchmark + redline language.

**What makes it different:**
> Most tools chase anything past the invoice date and review contracts generically. Deskmate is built on recruiting's actual money clauses and a shared Deal Record, so it's *precise* — it won't dun a client who's still within terms, and the fee it prices on a role is the exact fee it later chases.

---

## License & legal — form fields

**License type:**
> Deskmate Source-Available License 1.0 (proprietary source-available — commercial use permitted; no copying, redistribution, or resale). Full text: https://github.com/meenajainshah/deskmate-marketplace/blob/main/LICENSE

*Short form:* `Source-available (Deskmate Source-Available License 1.0 — not OSI-approved)`

**Privacy policy URL:** https://meenajainshah.github.io/deskmate-marketplace/privacy.html

> Note: the catalog leans toward OSI licenses (MIT/Apache). The source-available license is truthful but may lead to a decline. Install-by-slug works regardless.

---

## Launch blurbs (post once accepted)

**LinkedIn**
> Solo recruiters lose real money in the admin *around* the placement — not the sourcing. So I built **Deskmate**, a Claude plugin that runs the back office of a recruiting desk:
>
> 📄 **Contract Guard** — reviews a client MSA in plain English and flags the clauses that cost you money (fall-off, fee trigger, uncapped indemnity), then captures the terms.
> 💸 **Fee Chaser** — chases only the fees that are *actually* overdue per each client's real terms (a net-60 invoice at day 40 is left alone), with tone-matched reminders you approve.
> 📋 **Job Kit** — turns a client's rough req into a polished JD + interview rubric + offer template, priced against the same terms.
>
> One connected desk — the contract is understood once, and every skill reads from there. Zero connectors, works from a file upload.
>
> Try it 👉 https://meenajainshah.github.io/deskmate-marketplace/

**X / short**
> Built **Deskmate** — a Claude plugin that runs a recruiter's back office: reviews contracts, chases only the fees that are *genuinely* overdue, and builds role kits — all from one shared Deal Record. Zero connectors.
> 👉 https://meenajainshah.github.io/deskmate-marketplace/

---

## Links

- Home page: https://meenajainshah.github.io/deskmate-marketplace/
- Repo: https://github.com/meenajainshah/deskmate-marketplace
- Privacy: https://meenajainshah.github.io/deskmate-marketplace/privacy.html
- License: https://github.com/meenajainshah/deskmate-marketplace/blob/main/LICENSE
- Install: `/plugin marketplace add meenajainshah/deskmate-marketplace` then `/plugin install deskmate@deskmate-marketplace`
