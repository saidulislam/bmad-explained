# Architect Agent (Winston) — Starter Prompts

**Who uses this:** Architect / Tech Lead
**When to activate:** Phase 3 (Solutioning)
**Command:** `bmad-create-architecture`

---

## Starter Prompt: Create Architecture Doc from a PRD

```
I need to create an architecture document for our User Authentication System.

Here's the approved PRD: [link to or paste PRD]

Our existing stack:
- Backend: Node.js + Express
- Database: PostgreSQL 15
- Cache: Redis 7
- Hosting: AWS (ECS Fargate)
- CI/CD: GitHub Actions

Constraints:
- Must use our existing infrastructure — no new managed services
- Must meet SOC 2 compliance requirements
- p95 login latency must be under 500ms
- Team has experience with JWT but not session-based auth

Please generate an architecture document that includes:
- System context diagram (what talks to what)
- Key technology decisions with rationale (not just "we chose X" but "we chose X because Y")
- Component boundaries (what owns what)
- Security guardrails (hashing, token management, rate limiting)
- API surface (high-level endpoints)
- What this doc explicitly does NOT cover (leave to the Tech Spec)
```

---

## Starter Prompt: Architecture Decision Record (ADR)

```
We need to make a technology decision and I want it documented as an ADR
(Architecture Decision Record) so the team understands the "why" — not just
the "what."

Decision: How should we handle authentication tokens?

Options we're considering:
1. JWT with RS256 signing (stateless)
2. Opaque session tokens stored in Redis (stateful)
3. JWT + Redis hybrid (JWT for short-lived access, Redis for refresh tokens)

Context:
- We have 50K monthly active users, expecting 200K within 12 months
- We already run Redis for caching
- Our mobile app needs offline-capable token validation
- SOC 2 requires token revocation capability

For each option, help me evaluate:
- Pros and cons
- Security implications
- Infrastructure impact
- Scalability at our projected growth
- Recommendation with clear rationale
```

---

## Starter Prompt: Review a Developer's Proposed Architecture

```
A senior developer has proposed the following architecture for our auth service.
I need to review it as the Architect and identify any concerns before we proceed.

Their proposal:
- Express REST API with JWT (HS256) for auth tokens
- Passwords hashed with SHA-256 + salt
- Sessions stored in-memory using express-session
- Rate limiting via express-rate-limit middleware (in-memory store)
- Single PostgreSQL table for users, sessions, and audit logs

Our requirements (from the PRD):
- SOC 2 compliance
- 500ms p95 login latency
- Support for horizontal scaling (multiple instances behind a load balancer)
- Account lockout after 5 failed attempts

Please review this against our requirements and flag:
- Security concerns (with severity: critical / high / medium)
- Scalability concerns (what breaks when we add a second instance?)
- Architecture anti-patterns
- Specific recommendations for each concern
```

---

## Starter Prompt: Define Component Boundaries

```
We're designing a microservices boundary for our authentication system.
I want to avoid the common mistake of either:
(a) making everything one monolith, or
(b) over-splitting into too many services too early

Our auth system needs to handle:
- User registration and login
- Password reset
- OAuth (Google, GitHub)
- Session management
- Rate limiting
- Audit logging
- Admin account management

Help me define component boundaries:
- What should be a single service vs. separate services?
- What are the interfaces between them?
- Which components share a database vs. need their own?
- Where are the failure isolation boundaries?

Our current team is 4 backend developers. Factor team size into the recommendation.
```

---

## Starter Prompt: Security Guardrails Checklist

```
Before we move to implementation, I need a security guardrails checklist
for our auth system that the Developer Agent must follow.

Based on our architecture (JWT RS256, bcrypt, Redis sessions, PostgreSQL),
generate a checklist covering:

- Password storage requirements (algorithm, cost factor, constraints)
- Token management (signing, rotation, revocation, TTLs)
- Rate limiting thresholds
- Input validation rules
- Error response rules (what to reveal, what to hide)
- Logging rules (what to log, what to NEVER log)
- Secrets management (env vars, key rotation)
- OWASP Top 10 mitigations specific to auth

This checklist will be embedded in the Architecture Doc and the Developer Agent
must verify compliance before marking any story as complete.
```

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
