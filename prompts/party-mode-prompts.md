# Party Mode — Starter Prompts

## How Party Mode Actually Works in Practice

**Party Mode is not a meeting.** It's one person at their computer, in Claude CLI, activating multiple AI agent personas in a single conversation. There's no conference room, no calendar invite, no other people required.

### How to start

```
bmad-party-mode
```

That's it. The BMad Master orchestrator loads all relevant agent personas into your session. You then talk to them like you would in a room full of experts — except they all respond instantly.

### Who uses it and when

| Who | When | Why not just use a single agent? |
|---|---|---|
| **Architect** planning a new system | Before writing the Architecture Doc | You want the PM perspective on feasibility, the Dev perspective on implementation cost, and the QA perspective on testability — all at once |
| **PM** evaluating a feature request | Before committing to a PRD | You want the Architect to flag technical complexity, the UX Designer to flag usability concerns, and the Dev to estimate effort — before you promise anything to stakeholders |
| **Engineering Lead** triaging a production incident | During an active incident | You want the Dev to diagnose, the Architect to assess blast radius, the QA to identify regression risk, and the SM to plan the fix sprint — in one conversation |
| **Developer** stuck on a design decision | During implementation | You want the Architect to validate your approach, the QA to flag edge cases, and the PM to confirm it matches the acceptance criteria — without scheduling 3 meetings |

### What it looks like

```
You:       "We need to decide how to handle session management.
            Redis with JWT, or database-backed sessions?"

PM (John):      "From a product standpoint, we need fast login.
                 What's the latency difference?"

Architect (Winston): "JWT + Redis hybrid. JWT for stateless access tokens
                      (15-min TTL), Redis for refresh tokens. Here's why..."

Dev (Amelia):   "I can implement the hybrid approach in 2 days.
                 Pure DB sessions would take 3 because we'd need
                 connection pooling changes."

QA:             "With JWT, I need to test token expiry edge cases
                 and refresh races. Adding that to the test plan."

You:       "Winston, what about token revocation for SOC 2?"

Architect (Winston): "Good catch. We store a blacklist in Redis with
                      the same TTL as the access token..."
```

**You drive the conversation. You ask follow-ups. You push back. You decide.**

---

## Scenario 1: Architecture Decision — Before Writing the Architecture Doc

**Who starts this:** Architect or Engineering Lead
**When:** Phase 3 (Solutioning), before `bmad-create-architecture`

```
bmad-party-mode

I need to make a critical architecture decision before I write the
Architecture Doc for our User Authentication system.

PRD is here: @samples/01-prd-user-auth.md

The decision: Should we build authentication as a separate microservice
or as a module within our existing monolith?

Context:
- We have a Node.js/Express monolith serving 50K MAU
- Team of 4 backend developers
- SOC 2 compliance deadline in Q3 2026
- We plan to add OAuth, password reset, and admin features

I want each of you to weigh in from your perspective:

- PM: How does this affect our delivery timeline and the features
  promised to stakeholders?
- Architect: What are the infrastructure, deployment, and scaling
  implications of each approach?
- Developer: What's the realistic implementation effort for each?
  What are the gotchas our team will hit?
- QA: How does this affect our testing strategy? Which is easier
  to test and harder to break?

Don't just give me pros/cons lists. Tell me what you'd actually
recommend and why. Disagree with each other if you see it differently.
```

---

## Scenario 2: Sprint Planning — Prioritizing and Estimating Stories

**Who starts this:** Scrum Master or Engineering Lead
**When:** Phase 4, during sprint planning ceremony

```
bmad-party-mode

We're planning Sprint 13 and I need help prioritizing and estimating.

Here are the candidate stories (from the PM's prioritized backlog):
1. AUTH-04: OAuth Login (Google + GitHub) — 8 points estimated
2. AUTH-03: Password Reset flow — 3 points estimated
3. AUTH-06: Session timeout warning UI — 2 points estimated
4. AUTH-07: Audit logging for all auth events — 5 points estimated
5. INFRA-12: Redis cluster failover setup — 3 points estimated

Team capacity: 2 backend devs, 1 frontend dev, 15 working days total
Historical velocity: 18-22 points per sprint

I want each of you to weigh in:

- PM: Which of these are you hearing about from customers or
  stakeholders? What's the business priority order?
- Architect: Are there technical dependencies between these stories
  that affect the order? Does INFRA-12 need to happen before AUTH-04?
- Developer: Do you agree with the point estimates? Which stories
  have hidden complexity the estimates don't reflect?
- QA: Which stories have the highest test burden? Do we need to
  account for extra QA time on any of these?
- Scrum Master: Given velocity and capacity, what actually fits?
  What's the sprint goal?

Let's work through this together and come out with a committed sprint plan.
```

---

## Scenario 3: Design Review — Validating UX Before Development

**Who starts this:** UX Designer or PM
**When:** Phase 2 (Planning), after initial UX spec draft

```
bmad-party-mode

I've drafted a UX spec for the login and registration flow and I need
the team to review it before we move to implementation.

UX Spec: @ux-spec.md

Here's the flow I'm proposing:
- Single page with tabs: "Log in" (default) | "Sign up"
- Email + password fields with inline validation
- "Forgot password?" link below password field
- OAuth buttons (Google, GitHub) below the form with "or continue with" divider
- Mobile: same layout, stacked vertically

I want feedback from each perspective:

- PM: Does this flow match the acceptance criteria in the PRD?
  Are we missing any user scenario?
- Architect: Are there any technical constraints that make this
  flow difficult? (e.g., tabbed auth vs. separate pages for OAuth redirect handling)
- Developer: How long to implement this? Any components we don't
  have in our design system that would need to be built?
- QA: What are the edge cases in this flow? (tab switching mid-form,
  OAuth redirect failures, password manager autofill behavior)
- UX Designer: Challenge my own design — what would you improve
  about the error states, loading states, or accessibility?

Be critical. I'd rather fix problems now than after it's built.
```

---

## Scenario 4: Production Incident Triage

**Who starts this:** Engineering Lead or on-call engineer
**When:** During an active incident

```
bmad-party-mode

INCIDENT: Users are reporting intermittent login failures.
About 15% of login attempts are returning 500 errors since 2:30 PM.

What we know so far:
- Error logs show "ECONNREFUSED" from the Redis connection
- Redis cluster shows one node in FAIL state
- PostgreSQL is healthy, no connection issues
- No deployments in the last 24 hours
- Affected users: ~7,500 of 50K MAU

I need immediate input:

- Architect: What's the blast radius? Is this only affecting login
  or are other services using this Redis cluster? Should we failover
  or can we recover the node?
- Developer: Can we implement a quick fallback? If Redis is down,
  can we temporarily issue stateless JWTs without the session cache?
  What's the code change and how fast can we ship it?
- QA: If we push an emergency fix, what's the minimum test we need
  to run before deploying? What regression risks should we watch for?
- PM: We need to draft a customer communication. How should we frame
  this? What's the SLA impact?
- Scrum Master: We're mid-sprint. How do we accommodate this
  unplanned work? What gets deferred?

Let's triage this NOW. Start with containment, then root cause,
then remediation plan.
```

---

## Scenario 5: Retrospective — What Went Wrong and What to Improve

**Who starts this:** Scrum Master
**When:** End of sprint

```
bmad-party-mode

Sprint 12 retrospective. Here's what happened:

Completed: AUTH-01 (Registration), AUTH-02 (Login), AUTH-05 (Admin Deactivation)
Rolled: AUTH-03 (Password Reset) — blocked by SendGrid API key for 4 days
Velocity: 13/16 points (81%)

Notable events:
- AI-generated code for AUTH-01 was merged with zero rework
- AUTH-02 needed 2 rounds of revision because the Tech Spec didn't
  cover the "account locked" error message format — PM and Dev had
  different assumptions
- The SendGrid blocker was known on Day 2 but not escalated until Day 6
- Code review caught rate limiting using in-memory store instead of
  Redis (per Architecture Doc) — fixed before merge

I want each of you to reflect:

- PM: Where did the spec fall short? What would you add to the
  PRD or Tech Spec co-authoring session to prevent the AUTH-02 issue?
- Architect: The in-memory rate limiting violation — how did that
  slip past the Architecture Doc? Should we add automated checks?
- Developer: What helped you move fast? What slowed you down?
  Was the AI agent effective or did you fight with it?
- QA: Were the test scenarios in the Tech Spec sufficient?
  What would you add for next sprint?
- Scrum Master: How do we prevent the 4-day blocker escalation
  delay? What process change do you recommend?

Give me concrete action items with owners, not generic "communicate better."
```

---

## Scenario 6: Feature Feasibility — Before Committing to Stakeholders

**Who starts this:** PM or Business Analyst
**When:** Phase 1 (Discovery), before writing a PRD

```
bmad-party-mode

The CEO wants to know if we can add "Sign in with Apple" to our auth
system by end of Q2. Before I commit to anything, I need a quick
feasibility check.

What we have today:
- Email/password login (shipped)
- Google + GitHub OAuth (in progress, Sprint 13)
- Node.js + Express backend, Passport.js for OAuth

Questions I need answered:

- Architect: How different is Apple Sign In from Google/GitHub OAuth?
  Can we reuse the Passport.js patterns or is it a fundamentally
  different flow? (I've heard Apple requires special handling for
  email relay and token verification)
- Developer: Realistically, how many story points? Can one developer
  do this in a single sprint alongside other work?
- PM: Is there user demand data for Apple Sign In? What percentage
  of our users are on Apple devices? Is this a "nice to have" or a
  "customers are asking for it"?
- QA: What's the test surface? Can we test this in CI or does it
  require a physical Apple device / developer account?
- UX Designer: Where does the Apple button go in our current login
  layout? Apple has strict branding guidelines — does our design
  system accommodate that?

I need a GO / NOT YET / NO recommendation with a rough timeline
I can bring back to the CEO.
```

---

## Tips for Effective Party Mode Sessions

1. **Start with context** — paste or reference the relevant artifacts (PRD, Arch Doc, code) so all agents have the same information
2. **Ask for disagreement** — explicitly say "disagree with each other if you see it differently" — otherwise agents tend to be agreeable
3. **Drive the conversation** — don't just ask one question and accept the answers. Push back, ask follow-ups, redirect
4. **Name specific agents** — "Winston, what about the security implications?" gets better results than a generic question
5. **End with a decision** — Party Mode is for decisions, not discussion. Close with "Based on this, here's what we're doing..."
6. **Keep sessions focused** — one topic per session. Don't mix sprint planning with architecture review

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
