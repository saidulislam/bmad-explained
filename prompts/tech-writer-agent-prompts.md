# Tech Writer Agent — Starter Prompts

**Who uses this:** Technical Writer / Engineering Lead
**Module:** BMad Method (BMM)
**When to activate:** Phase 4 (Implementation) — after code is complete

---

## Starter Prompt: Generate API Documentation

```
Generate developer-facing API documentation for our Authentication endpoints.

Source artifacts:
- Technical Spec: @samples/03-technical-spec-user-auth.md
- Architecture Doc: @samples/02-architecture-user-auth.md
- Implementation: @src/routes/auth/

For each endpoint, document:
- Method + URL
- Description (what it does, when to use it)
- Request headers, body schema, and example
- Response schemas for all status codes (200, 400, 401, 403, 429)
- Authentication requirements (which endpoints need a token, which don't)
- Rate limiting rules
- Code examples (cURL + JavaScript fetch)

Format as OpenAPI 3.0 compatible markdown that we can convert to Swagger UI.
Include a "Quick Start" section showing the full register → login →
use token → refresh flow.
```

**Artifact delivered:** `docs/api/authentication.md`

---

## Starter Prompt: Generate Internal Runbook

```
Create an internal runbook for the Authentication system that our on-call
engineers can reference during incidents.

Source artifacts:
- Architecture Doc: @samples/02-architecture-user-auth.md
- Implementation: @src/services/authService.js

Include:
1. System overview (what components are involved, how they connect)
2. Health check endpoints and what they verify
3. Common failure scenarios and resolution steps:
   - Redis connection failure (sessions unavailable)
   - PostgreSQL connection failure (can't authenticate)
   - JWT signing key rotation
   - SendGrid outage (password reset emails not sending)
   - Rate limiter false positives (legitimate users locked out)
4. Key metrics to monitor (what dashboards, what thresholds trigger alerts)
5. Escalation path (who to contact for auth-specific issues)
6. How to manually disable/enable a user account in an emergency

Write for an engineer who may not have built this system — they need to
diagnose and fix issues at 3 AM.
```

**Artifact delivered:** `docs/runbooks/authentication-runbook.md`

---

## Starter Prompt: Generate User-Facing Help Articles

```
Create user-facing help articles for our authentication features.

Target audience: non-technical end users.

Articles needed:
1. "How to create your account"
2. "How to log in"
3. "I forgot my password"
4. "Login with Google or GitHub"
5. "Why is my account locked?"
6. "Why can't I log in? (Account disabled)"

For each article:
- Title (clear, searchable)
- Step-by-step instructions with numbered steps
- Screenshots placeholders (describe what the screenshot should show)
- Troubleshooting section (common issues + fixes)
- Related articles (link to others in this set)

Tone: friendly, simple, no jargon. Write at a 6th-grade reading level.
Assume the user has never used our product before.
```

**Artifact delivered:** `docs/help/` folder with individual articles

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
