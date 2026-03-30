# Analyst Agent — Starter Prompts

**Who uses this:** Business Analyst / Product Manager
**When to activate:** Phase 1 (Discovery & Analysis)
**Commands:** `bmad-domain-research`, `bmad-market-research`, `bmad-technical-research`, `bmad-brainstorming`

---

## Starter Prompt: Domain Research

```
I'm building an authentication system and need to understand the compliance
and security landscape before writing the PRD.

Research the following:
1. SOC 2 requirements for user authentication — what specifically must we implement?
2. OWASP authentication best practices (2024-2025) — what's the current standard?
3. Common authentication pitfalls that lead to security breaches
4. Password policy recommendations (NIST 800-63B vs. traditional complexity rules)

For each area, provide:
- Key requirements or recommendations
- How it impacts our system design
- What we MUST do vs. what's nice to have
- Any recent changes or trends (e.g., NIST now says DON'T require special characters)

I'll use this research to inform the acceptance criteria in our PRD.
```

---

## Starter Prompt: Market Research — Competitive Auth Patterns

```
Before designing our auth UX, I want to understand what users already expect
from authentication flows in 2025-2026.

Research how the following products handle authentication:
1. GitHub (developer-focused)
2. Notion (productivity SaaS)
3. Stripe (developer + business)
4. Linear (project management)

For each product, analyze:
- Registration flow (steps, required fields, verification method)
- Login flow (options offered: email, OAuth, magic link, passkeys)
- Password reset experience
- Error messaging patterns (what they reveal vs. hide)
- Time-to-first-login (how fast can a new user get in?)

Summarize:
- Common patterns across all four (what users now expect as baseline)
- Differentiators (what's unique or innovative)
- Recommendations for our implementation based on these patterns
```

---

## Starter Prompt: Technical Research — Auth Approach Comparison

```
We need to choose our authentication approach before the Architect starts
the Architecture Doc.

Compare the following approaches for our context:
1. Traditional email/password + JWT
2. Passwordless (magic links)
3. Passkeys (WebAuthn)
4. OAuth-only (no local passwords)

Our context:
- B2C product with 50K MAU, growing to 200K
- Users range from non-technical consumers to developers
- Mobile app + web app
- SOC 2 compliance required
- Team of 4 backend developers, moderate auth experience

For each approach, evaluate:
- User experience (friction, speed, familiarity)
- Security posture
- Implementation complexity for our team size
- Infrastructure requirements
- Migration path (can we start with one and evolve to another?)
- Industry trend (growing, stable, or declining adoption?)

Recommend an approach with a clear rationale tied to our specific context.
```

---

## Starter Prompt: Structured Brainstorming

```
We're exploring adding authentication to our currently open-access platform.
Before I commit to a specific approach, I want to brainstorm broadly.

Starting question: "How should we introduce authentication without
alienating our existing users who are accustomed to open access?"

Guide me through a structured brainstorming session:
1. Start with divergent thinking — generate as many approaches as possible,
   including unconventional ones
2. Then converge — evaluate each against our constraints:
   - Must not break existing user workflows
   - Must meet SOC 2 by Q3 2026
   - Must be implementable by a 4-person backend team in 2 sprints
3. Identify the top 2-3 approaches worth exploring further
4. For each finalist, list the key assumptions we'd need to validate

Challenge my assumptions along the way. If I'm anchored on a particular
approach too early, push back.
```

---

## Starter Prompt: Stakeholder Impact Analysis

```
We're about to introduce mandatory authentication to a platform that
currently has open access. I need to prepare for the stakeholder
conversations.

Stakeholders and their likely concerns:
- CEO: "Will this slow down user growth?"
- Head of Sales: "Will this add friction to the trial experience?"
- Engineering Lead: "How much maintenance overhead is this?"
- Legal/Compliance: "Does this get us to SOC 2?"
- Customer Support: "Are we going to get flooded with 'I can't log in' tickets?"

For each stakeholder:
- Anticipate their top 2-3 objections
- Prepare a data-backed response or mitigation
- Identify what they need to see in the PRD to feel confident
- Suggest how to frame the change as a benefit, not a burden

I'll use this to prepare for the kickoff meeting before writing the PRD.
```

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
