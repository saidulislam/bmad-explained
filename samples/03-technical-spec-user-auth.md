# Technical Spec: AUTH-02 — User Login

**Author:** Senior Developer (Developer Agent) + Architect review
**Input:** [PRD](01-prd-user-auth.md) → [Architecture Doc](02-architecture-user-auth.md)
**Story:** As a returning user, I want to log in with my email and password so I can access my dashboard.
**Status:** Ready for Implementation
**Date:** 2026-03-29

---

## Acceptance Criteria

- [ ] User can submit email + password to `/auth/login`
- [ ] Valid credentials return an access token (JWT, 15 min TTL) and refresh token (7 day TTL)
- [ ] Invalid credentials return `401` with generic error (no info leakage)
- [ ] Account locked after 5 failed attempts in 15 min — returns `429`
- [ ] Deactivated accounts return `403` with message "Account disabled. Contact support."
- [ ] Login event logged with timestamp, IP, and user agent (no password logged)
- [ ] p95 response time < 500ms

## API Contract

### Request

```
POST /auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "s3cureP@ss!"
}
```

### Response — Success (200)

```json
{
  "accessToken": "eyJhbG...",
  "refreshToken": "dGhpcyBpcyBh...",
  "expiresIn": 900,
  "user": {
    "id": "uuid-here",
    "email": "user@example.com",
    "name": "Jane Doe"
  }
}
```

### Response — Invalid Credentials (401)

```json
{
  "error": "Invalid email or password."
}
```

### Response — Rate Limited (429)

```json
{
  "error": "Too many login attempts. Try again in 15 minutes."
}
```

### Response — Account Disabled (403)

```json
{
  "error": "Account disabled. Contact support."
}
```

## Data Model

```sql
-- users table (existing, relevant columns)
CREATE TABLE users (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email       VARCHAR(255) UNIQUE NOT NULL,
  password    VARCHAR(255) NOT NULL,  -- bcrypt hash
  name        VARCHAR(255),
  is_active   BOOLEAN DEFAULT true,
  created_at  TIMESTAMPTZ DEFAULT now(),
  updated_at  TIMESTAMPTZ DEFAULT now()
);

-- login_attempts (new table for rate limiting)
CREATE TABLE login_attempts (
  id          SERIAL PRIMARY KEY,
  email       VARCHAR(255) NOT NULL,
  ip_address  INET NOT NULL,
  attempted_at TIMESTAMPTZ DEFAULT now(),
  success     BOOLEAN NOT NULL
);

CREATE INDEX idx_login_attempts_email_time
  ON login_attempts (email, attempted_at);
```

## Implementation Notes

- Use `bcrypt.compare()` for password verification (per Architecture Doc — cost factor 12)
- Store session in Redis with key `session:{userId}` and 24h TTL
- JWT signed with RS256 using key from `AUTH_PRIVATE_KEY` env variable
- Rate limiting: query `login_attempts` for count in last 15 min before allowing attempt
- Never return whether an email exists or not — always "Invalid email or password"

## Test Scenarios

| Scenario | Input | Expected |
|---|---|---|
| Valid login | Correct email + password | 200, tokens returned |
| Wrong password | Correct email, wrong password | 401, generic error |
| Non-existent email | Unknown email | 401, same generic error |
| 6th failed attempt | 5 prior failures in 15 min | 429, rate limit error |
| Deactivated account | Valid creds, `is_active=false` | 403, disabled message |
| SQL injection attempt | `' OR 1=1 --` as email | 401, parameterized query prevents injection |
| Missing fields | No password field | 400, validation error |

---

> **Why this matters for BMAD:** This is what the AI agent actually codes against. Every field, every status code, every edge case is defined. The Developer Agent doesn't guess what a 401 response looks like — it's right here. The UAT Tester doesn't invent test cases — they're pre-defined. And the Architect already signed off that this follows the security guardrails. **This is how you eliminate hallucinated code.**
