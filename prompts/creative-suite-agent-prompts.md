# Creative Intelligence Suite — Agent Starter Prompts

This file covers the four agents in the **Creative Intelligence Suite (CIS)** module.
These agents are used in **Phase 1 (Discovery)** for ideation, problem-solving, and
innovation — before requirements are written.

---

## Brainstorming Coach (Carson)

**Who uses this:** Anyone leading an ideation session
**When to activate:** Phase 1 — when you need to generate ideas, not evaluate them

### Starter Prompt: Feature Ideation Session

```
I need to brainstorm feature ideas for our authentication system beyond
the basic login/register flow.

Context:
- We're a B2C platform with 50K MAU, growing to 200K
- Competitors offer: passwordless login, passkeys, social login, magic links
- Our users range from non-technical consumers to developers
- We have a SOC 2 compliance requirement

Run a structured brainstorming session:
1. Warm-up: Generate 15-20 ideas in 2 minutes — no filtering, no judgment
2. Categorize: Group them into themes (security, convenience, delight, enterprise)
3. Wild cards: Give me 3 unconventional ideas nobody in the industry is doing
4. Dot voting: Help me evaluate each against impact (user value) vs. effort
5. Shortlist: Identify the top 5 worth exploring further

Push me to think beyond the obvious. Challenge any idea I anchor on too quickly.
```

**Artifact delivered:** `brainstorming-report.md`

---

## Creative Problem Solver

**Who uses this:** Anyone stuck on a hard problem
**When to activate:** When the obvious solutions aren't working

### Starter Prompt: Solve a UX Friction Problem

```
We have a problem: our registration conversion rate is only 40%.
Users start the signup form but don't complete it.

What we know:
- The form has 5 fields: name, email, password, confirm password, terms checkbox
- Analytics shows 60% drop-off happens at the password field
- Users on mobile drop off more than desktop (70% vs. 50%)
- Competitors like Notion have 85%+ conversion with simpler flows

I've already considered:
- Reducing to 3 fields (name, email, password) — team says we need confirm password
- Adding a password strength meter — didn't move the needle in A/B test
- Social login only — PM says we need email/password as a baseline

Apply lateral thinking frameworks to find solutions I haven't considered:
- Reverse the problem: What if we made signup HARDER? What does that reveal?
- Analogy: How do other industries handle "registration" (hotels, gyms, apps)?
- Constraint removal: If we could change ONE thing about our tech stack, what?
- First principles: Why do users need passwords at all?

Give me 3 non-obvious solutions with a hypothesis for each.
```

**Artifact delivered:** `creative-solutions-report.md`

---

## Design Thinking Coach

**Who uses this:** Product Manager / UX Designer
**When to activate:** Phase 1 — when you need to deeply understand the user before building

### Starter Prompt: Empathy Mapping for Auth UX

```
Guide me through a Design Thinking exercise for our authentication experience.

I want to redesign our login/registration flow and I need to start with
empathy — understanding what users actually feel, not what I assume.

Phase 1 — Empathize:
- Help me build an empathy map for our 3 user personas:
  (a) First-time consumer user
  (b) Returning power user
  (c) Admin managing team accounts
- For each: What do they think, feel, say, and do during authentication?
- What are their pain points that they won't say out loud?

Phase 2 — Define:
- From the empathy maps, help me write 3 "How Might We" statements
  (e.g., "How might we make first-time users feel safe sharing their email?")

Phase 3 — Ideate:
- For each HMW statement, generate 5 solution ideas

Phase 4 — Prototype:
- Pick the top idea from each HMW and describe a low-fidelity prototype
  (what would we test with real users?)

Phase 5 — Test:
- Write a usability test script I can use with 5 real users
```

**Artifact delivered:** `design-thinking-report.md` (empathy maps, HMW statements, prototype descriptions, test script)

---

## Innovation Strategist

**Who uses this:** Product Manager / Business Analyst
**When to activate:** Phase 1 — when evaluating whether an idea is worth pursuing

### Starter Prompt: Evaluate an Innovation Opportunity

```
We're considering adding passkey support (WebAuthn) to our authentication
system. Before we commit engineering resources, I need a strategic evaluation.

Evaluate this opportunity against:

1. Market readiness:
   - What % of users have passkey-capable devices today?
   - Which competitors have shipped passkeys? How's adoption?
   - Is this a "table stakes" feature or a differentiator?

2. Technical feasibility:
   - How much effort for our 4-person backend team?
   - What infrastructure changes are needed?
   - Can we ship this incrementally (alongside password auth) or is it all-or-nothing?

3. Business impact:
   - Will this reduce support tickets (password resets)?
   - Will this improve our security posture for SOC 2?
   - Will this affect our registration conversion rate (positive or negative)?

4. Timing:
   - Is now the right time, or should we wait for broader adoption?
   - What's the cost of waiting 6 months?

Give me a GO / WAIT / PASS recommendation with clear reasoning.
```

**Artifact delivered:** `innovation-assessment-passkeys.md` (GO / WAIT / PASS with strategic rationale)

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
