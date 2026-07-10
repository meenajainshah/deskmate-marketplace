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

Contract Guard also captures the agreed terms into a small **Deal Record** that later Deskmate skills (Fee Chaser, Job Kit) read, so the contract is understood once and never re-opened.

## Roadmap

Fee Chaser (chase unpaid placement fees) · Job Kit (JD polish + interview guide + scoring rubric + offer template) · cash forecast · dual-pipeline CRM cleanup · Monday/Friday desk briefs.

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
