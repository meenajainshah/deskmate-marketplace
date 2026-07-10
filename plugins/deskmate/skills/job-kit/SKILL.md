---
name: job-kit
description: >
  Turns a client's rough req into a full working kit for the role: a polished, candidate-facing
  job description, a structured interview guide with a 1–5 scoring rubric, and an offer-letter
  template — all tied to the client's Deal Record so the role is priced (expected fee) and its
  guarantee clock is known before you start. Use when the user says "polish this JD," "write a
  job description," "build an interview guide," "make a scoring rubric," "draft an offer letter,"
  "new req from a client," or "help me work this role." Works from an uploaded/pasted req with
  zero connectors. Drafts only — never sends or signs. Not legal or HR advice.
allowed-tools: Read, Write
---

# Job Kit

Take a client's role and hand back everything you need to run it: a clean JD, a structured
interview guide + rubric, and an offer template — each tied to the client's terms.

**The edge:** Job Kit reads the **Deal Record** Contract Guard captured, so every role is
**priced up front** (`fee_pct` × `fee_base` = expected fee) and you know the **guarantee window**
you'll be on the hook for the moment the candidate starts — before you've sourced a single person.

## Step 1 — Intake the role

Read the client's **Deal Record** (terms). Take the raw req — uploaded, pasted, or a link.
Identify the client and link `deal_record_id`.

- **Price it now.** Compute and state the expected fee: `fee_pct` × `fee_base` of the target
  first-year base (ask the target comp if the req doesn't give it). The recruiter should know what
  the role is worth in the first minute.
- **Surface the guarantee.** Note the client's `guarantee_days` / `guarantee_type` — that's the
  fall-off clock you inherit once the hire starts.
- If there's **no Deal Record** for this client, you can still build the kit — but flag that fee
  and guarantee are unknown until terms are captured (send them to Contract Guard).
- If the req is thin, **interview the user** for the essentials (title, level, must-haves, comp
  range, location/remote, hiring manager, timeline). Don't fabricate requirements.

## Step 2 — Polish the JD

Turn the req into a clean, candidate-facing spec:

- crisp **title**; a one-paragraph *what the role is and why it matters*;
- **5–8 core responsibilities** (outcomes, not a wish list);
- **must-haves vs. nice-to-haves, clearly separated** — inflated must-haves shrink the pipeline and
  screen out good people; be honest about what's truly required;
- **comp range + location/remote**; a short, genuine sell of the team/mission.

Flag anything **missing or unrealistic** (e.g. "10 years" of a 6-year-old framework, a senior scope
at a junior band). Keep the client's employer voice — not generic filler.

## Step 3 — Interview guide + scoring rubric

Load `reference/interview-kit-library.md`. Build a **structured** guide mapped to the must-haves:

- **4–6 competencies**, each with 2–3 questions drawn from (and adapted to) the library;
- a **1–5 scoring anchor per competency** — spell out what a 1, a 3, and a 5 answer look like, so
  candidates are compared on the same bar, not on vibes;
- a **red-flag list** and a suggested **interview loop** (screen → deep-dive → final).

Structured and consistent scoring is faster *and* more defensible — and it's what lets a solo
recruiter present a clean, comparable slate to the client.

## Step 4 — Offer template

Draft an **offer-letter scaffold** tied to the agreed comp (title, base, start date, key terms).
Pull the client's **guarantee window** from the Deal Record and note it prominently — that's the
clock that decides whether your fee sticks. **Never send or sign** — export a draft for the
client/candidate to issue. Note the US at-will assumption where relevant (state jurisdiction).

## Step 5 — Save the Role Brief

Capture the role into a **Role Brief** following `reference/role-brief-schema.md` (client,
`deal_record_id`, title, comp, must-haves, **expected fee**, **guarantee window**, status). When the
candidate starts, the brief **spawns a placement-ledger row** for Fee Chaser, with the fee computed
from the Deal Record — so the fee you *priced* here becomes the fee you *chase* there. One role,
understood once, carried across the whole desk.

## Guardrails

- **Draft only** — never send, sign, or submit a JD or offer. The user/client issues it.
- **Don't invent** requirements, comp, or candidate facts. Missing info gets flagged, not filled in.
- **Don't inflate the req** — separate must-haves from nice-to-haves; over-speccing costs candidates.
- **Same rubric for every candidate** — structured, equal scoring is the point.
- **US framing** for at-will/offer norms; state the jurisdiction assumption. Not legal or HR advice —
  the client's counsel owns the final offer.

## Output shape

```
📋 Job Kit — {role} @ {client}   expected fee ~{$X}   guarantee {n}d {type}
📝 JOB DESCRIPTION        {polished, candidate-facing spec}
🎤 INTERVIEW GUIDE        {competencies · questions · 1–5 anchors · red flags · loop}
📄 OFFER TEMPLATE (draft) {scaffold + guarantee note}
→ Want these as files / a DOCX? Save the Role Brief so the desk can track it?
```

## Reference

- `reference/role-brief-schema.md` — the Role Brief: fields, how it links to the Deal Record and
  spawns a placement-ledger row on hire, and the expected-fee computation.
- `reference/interview-kit-library.md` — the competency framework, question bank, 1–5 scoring
  anchors, red flags, interview-loop patterns, and offer-letter scaffold.
