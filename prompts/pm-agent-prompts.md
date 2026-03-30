# PM Agent (John) — Starter Prompts

**Who uses this:** Product Manager
**When to activate:** Phase 1 (Discovery) and Phase 2 (Planning)
**Command:** `bmad-create-prd`

---

## Starter Prompt: Create a PRD from Scratch

```
I need to create a PRD for a new feature: [User Authentication System].

Here's what I know so far:
- We need email/password registration and login
- We need OAuth support for Google and GitHub
- Admins need to be able to deactivate accounts
- We have a SOC 2 compliance deadline in Q3 2026
- This replaces our current "no auth" state — users currently access everything anonymously

Target users: end users (consumers), internal admins
Tech stack: Node.js, Express, PostgreSQL, Redis (already in use)

Please walk me through creating a structured PRD with:
- Problem statement
- Business goals
- User personas
- Requirements with acceptance criteria
- Out of scope items
- Success metrics
```

---

## Starter Prompt: Convert Existing Jira Epic into a PRD

```
I have an existing Jira Epic with user stories that I need to convert into a BMAD-structured PRD.

Here's what I have today:

Epic: "User Authentication"
- Story 1: As a user, I want to register with email and password
- Story 2: As a user, I want to log in and be redirected to my dashboard
- Story 3: As a user, I want to reset my password if I forget it
- Story 4: As a user, I want to log in with Google or GitHub
- Story 5: As an admin, I want to deactivate a user account

These stories have basic acceptance criteria in Jira but they're informal.

Please help me restructure this into a formal PRD with:
- Clear problem statement (why are we building this?)
- Business-level acceptance criteria that I (the PM) own
- Defined scope boundaries (what's in, what's explicitly out)
- Measurable success metrics

I want the acceptance criteria to be specific enough that a developer — or an AI agent — cannot misinterpret them.
```

---

## Starter Prompt: Validate and Strengthen Acceptance Criteria

```
I've drafted acceptance criteria for our login feature but I want to make sure
they're airtight — specific enough for AI-assisted development with no room
for guessing.

Here's what I have:

AUTH-02: Users can log in with email + password
- Acceptance: "User logs in and sees dashboard"

Help me strengthen this. I need criteria that:
- Define exact user-visible behavior (what do they see, when, where?)
- Cover failure scenarios (wrong password, locked account, disabled account)
- Include measurable thresholds (latency, retry limits)
- Are written from the business/user perspective, not the technical perspective
- Leave zero ambiguity for the developer or AI agent implementing this
```

---

## Starter Prompt: Scope Negotiation — What's In vs. Out

```
My stakeholders want everything in the auth system for v1:
- Email/password login
- OAuth (Google, GitHub, Apple, Microsoft)
- Multi-factor authentication (SMS + authenticator app)
- SSO/SAML for enterprise clients
- Biometric login (fingerprint, Face ID)
- Passwordless magic links

Help me structure a scope recommendation:
- What's realistic for a v1 MVP that meets our SOC 2 deadline (Q3 2026)?
- What should be explicitly deferred to Phase 2?
- How do I frame this for stakeholders so they understand the tradeoff
  between shipping fast and shipping everything?

I need a clear "In Scope / Out of Scope" section I can put in the PRD.
```

---

## Starter Prompt: Write User Personas

```
I need to define user personas for our authentication system PRD.

Our platform serves:
- Individual consumers who sign up to use our product
- Team admins who manage their organization's users
- Internal support staff who handle account issues
- Developers who integrate via our API

For each persona, help me define:
- Who they are (role, technical level)
- What they need from the auth system
- What frustrates them about typical auth experiences
- What "success" looks like for them

These personas will drive the acceptance criteria, so they need to be
specific and actionable — not generic marketing profiles.
```

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
