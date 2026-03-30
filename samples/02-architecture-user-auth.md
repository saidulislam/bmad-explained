# Architecture Doc: User Authentication System

**Author:** Architect (Architect Agent)
**Input:** [PRD: User Authentication System](01-prd-user-auth.md)
**Status:** Approved
**Date:** 2026-03-29

---

## System Context

```
┌─────────────┐     HTTPS      ┌─────────────┐      ┌──────────────┐
│   Browser /  │ ──────────────▶│   API        │─────▶│  PostgreSQL  │
│   Mobile App │◀────────────── │   Gateway    │      │  (users,     │
└─────────────┘   JWT Token     │   (Express)  │      │   sessions)  │
                                └──────┬───────┘      └──────────────┘
                                       │
                                ┌──────▼───────┐      ┌──────────────┐
                                │   Auth       │─────▶│  Redis       │
                                │   Service    │      │  (session    │
                                └──────┬───────┘      │   cache)     │
                                       │              └──────────────┘
                                ┌──────▼───────┐
                                │  Email       │
                                │  Service     │
                                │  (SendGrid)  │
                                └──────────────┘
```

## Key Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Auth tokens | JWT (RS256) | Stateless verification, industry standard, rotatable keys |
| Password hashing | bcrypt (cost 12) | Battle-tested, resistant to brute force |
| Session storage | Redis with 24h TTL | Fast lookup, auto-expiry, reduces DB load |
| OAuth provider | Passport.js | Proven library, supports Google + GitHub per PRD |
| Database | PostgreSQL | Already our primary store — no new infrastructure |

## Component Boundaries

| Component | Responsibility | Owns |
|---|---|---|
| **Auth Service** | Registration, login, token issuance, password reset | Business logic only |
| **API Gateway** | Route protection, token validation middleware | Request filtering |
| **User Repository** | CRUD operations on user/session tables | Data access only |
| **Email Service** | Verification and reset emails via SendGrid | Delivery only |

## Security Guardrails

- Passwords: minimum 8 chars, checked against HaveIBeenPwned top 1000
- Rate limiting: 5 failed login attempts per 15 min per IP
- Tokens: access token (15 min TTL), refresh token (7 day TTL, rotated on use)
- All secrets via environment variables — never hardcoded

## API Surface (High-Level)

| Endpoint | Method | Purpose |
|---|---|---|
| `/auth/register` | POST | Create account |
| `/auth/login` | POST | Issue tokens |
| `/auth/logout` | POST | Invalidate session |
| `/auth/refresh` | POST | Rotate access token |
| `/auth/forgot-password` | POST | Send reset email |
| `/auth/reset-password` | POST | Set new password |
| `/auth/oauth/:provider` | GET | Initiate OAuth flow |

## What This Doc Does NOT Cover

- API request/response schemas (see Technical Spec)
- UI/UX design (see Design Spec)
- Database migration scripts (implementation detail)

---

> **Why this matters for BMAD:** This is the Architect's guardrail document. When the Developer Agent later generates code, it *must* use bcrypt (not MD5), *must* use Redis for sessions (not in-memory), and *must* follow these component boundaries. Without this doc, the AI makes its own architecture choices — and they might contradict your security, performance, or infrastructure standards.
