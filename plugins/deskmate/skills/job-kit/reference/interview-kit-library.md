# Interview Kit Library — Job Kit source of truth

The domain IP for turning a role's must-haves into a **structured, consistently-scored** interview.
Structured interviews (same questions, same rubric, every candidate) predict on-the-job success far
better than unstructured chats — and they give a solo recruiter a clean, comparable slate to hand
the client.

**How the skill uses this:** map each of the role's `must_haves` to a competency below, pull 2–3
questions, and attach the 1–5 anchor. Adapt wording to the role; don't ship the generic version.

Golden rule: **score the answer against the anchor, not against the last candidate.** A 3 is a 3
whether they interviewed first or fifth.

---

## Competency framework

Pick **4–6** competencies for the role — a mix of role-specific and cross-cutting. Every role
should include at least one of *ownership* and one of *communication*; the rest follow the must-haves.

| Competency | What it measures | Use for |
|---|---|---|
| **Technical/functional depth** | Real skill in the core of the role | every role — anchor to the must-haves |
| **Problem-solving** | How they reason through ambiguity | most roles |
| **Ownership & drive** | Do they push things over the line | every role |
| **Collaboration** | Works across people/teams | every role |
| **Communication** | Clear, appropriate to audience | every role |
| **Role-specific** | e.g. system design, client-facing, people-management | per req |

---

## Question bank (adapt, don't paste raw)

**Technical/functional depth**
- "Walk me through a piece of {domain} work you're proud of — what was the hard part, and what did *you* specifically do?"
- "Where does {core skill/tool} fall down, and how have you worked around it?"

**Problem-solving**
- "Tell me about a time the obvious solution was wrong. How did you find that out?"
- (live) "Here's a scoped problem from this role — think out loud; I care about the approach, not a perfect answer."

**Ownership & drive**
- "Describe something you shipped that nobody asked you to. Why did you take it on?"
- "A commitment was about to slip. What did you actually do?"

**Collaboration**
- "Tell me about a disagreement with a teammate on an approach. How did it resolve?"

**Communication**
- "Explain {technical concept from the role} to me as if I'm the hiring manager, not an engineer."

**Role-specific (examples)**
- *System design:* "Design {realistic system for this role}. Talk me through trade-offs."
- *Client-facing:* "A client is unhappy and partly right. Walk me through your first call."
- *People-management:* "How did you handle an underperformer? What changed?"

---

## Scoring anchors (attach a 1–5 to every competency)

Fill the {braces} per competency; give interviewers all five, or at least 1 / 3 / 5:

```
5 — {Clear, specific, senior-level evidence; taught the interviewer something}
4 — {Strong, concrete, minor gaps}
3 — {Solid and real, but generic or shallow in places}   ← the bar: 3 = hireable, not exciting
2 — {Vague, secondhand, or notably thin for the level}
1 — {No real evidence, or a red flag}
```

Sum or average across competencies; agree the pass bar with the client up front (commonly: no 1s on
a must-have competency, overall ≥ 3).

## Red flags (note, don't auto-reject)

- Can't give a *specific* example for a core must-have — only generalities.
- "We" for everything; never says what *they* did.
- Blames others for every failure; no ownership.
- Comp/level/scope mismatch they won't engage with.
- Inconsistent timeline or story vs. the CV.

## Interview loop (suggest, size to the role)

```
1. Recruiter screen (20–30m)  — motivation, must-haves at a glance, comp/location fit, sell
2. Deep-dive (45–60m)         — technical/functional depth + problem-solving, scored on the rubric
3. Final / team (30–45m)      — collaboration, ownership, hiring-manager fit
→ Debrief on the rubric, not on "feel." Fill the slate; recommend, don't decide for the client.
```

---

## Offer-letter scaffold (draft only — never send/sign)

```
[Client letterhead]

Dear {Candidate},
We're pleased to offer you the position of {title} at {client}, reporting to {manager}.

  • Start date:   {start_date}
  • Base salary:  {currency} {base} per year
  • {Bonus / equity / sign-on — only if agreed}
  • Location:     {location / remote}
  • Employment:   At-will (US) — {state jurisdiction assumption; adjust for non-US}

This offer is contingent on {background/reference checks, right-to-work, etc.}.
Please confirm by {date}.

Sincerely, {hiring manager}
```

- Pull comp from the Role Brief; **never invent** numbers.
- **Flag the guarantee window** from the Deal Record alongside the draft — that's the fall-off clock
  on the recruiter's fee once the candidate starts.
- The **client issues the offer.** Job Kit drafts; it does not send, sign, or submit.

---

## Anti-over-engineering rule

Match the kit to the role. A single mid-level backend req doesn't need eight competencies and a
five-round loop. Fewer, sharper questions with clear anchors beat an exhaustive script nobody follows.
