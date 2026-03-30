# Developer Agent (Amelia) — Starter Prompts

**Who uses this:** Developer
**When to activate:** Phase 4 (Implementation)
**Command:** `bmad-dev-story`

---

## Starter Prompt: Implement a Story from Tech Spec

```
Implement story AUTH-02: User Login.

Read the following artifacts before writing any code:
- PRD: @samples/01-prd-user-auth.md
- Architecture Doc: @samples/02-architecture-user-auth.md
- Technical Spec: @samples/03-technical-spec-user-auth.md

Requirements:
- Implement POST /auth/login endpoint per the API contract in the Tech Spec
- Use bcrypt (cost factor 12) for password verification per Architecture Doc
- Store session in Redis with key session:{userId} and 24h TTL
- Sign JWT with RS256 using AUTH_PRIVATE_KEY env variable
- Implement rate limiting: 5 failed attempts per 15 min per IP → return 429
- Return exact error responses defined in the Tech Spec (401, 403, 429)
- NEVER return whether an email exists — always "Invalid email or password"

Generate:
- Route handler
- Service layer (business logic)
- Repository layer (data access)
- Input validation middleware
- Unit tests covering all scenarios in the Tech Spec test table
```

---

## Starter Prompt: Implement with Existing Codebase Context

```
I need to implement the user login endpoint (AUTH-02) in our existing codebase.

Here's our project structure:
- src/routes/ — Express route definitions
- src/services/ — Business logic layer
- src/repositories/ — Database access (using Knex.js)
- src/middleware/ — Express middleware (auth, validation, rate-limiting)
- src/utils/ — Shared utilities
- tests/ — Jest test files mirroring src/ structure

Conventions to follow:
- We use async/await, not callbacks
- Error handling uses our custom AppError class in src/utils/errors.js
- All routes go through the validation middleware before hitting the handler
- We use Joi for request validation schemas
- Database queries use our existing Knex instance from src/db/connection.js

Read @src/routes/health.js and @src/services/userService.js for examples
of our patterns before generating code.

Implement AUTH-02 following these existing patterns. Do not introduce new
libraries or patterns that differ from what's already in the codebase.
```

---

## Starter Prompt: Generate Tests from Acceptance Criteria

```
Generate a complete test suite for the POST /auth/login endpoint.

Use the test scenarios defined in the Technical Spec:

| Scenario                | Input                        | Expected           |
|------------------------|------------------------------|---------------------|
| Valid login            | Correct email + password      | 200, tokens returned |
| Wrong password         | Correct email, wrong password | 401, generic error   |
| Non-existent email     | Unknown email                 | 401, same generic error |
| 6th failed attempt     | 5 prior failures in 15 min   | 429, rate limit error |
| Deactivated account    | Valid creds, is_active=false  | 403, disabled message |
| SQL injection attempt  | ' OR 1=1 -- as email         | 401, parameterized query prevents injection |
| Missing fields         | No password field             | 400, validation error |

Testing requirements:
- Framework: Jest + Supertest
- Use our test database (not mocks) for integration tests
- Seed test data in beforeAll, clean up in afterAll
- Each test should be independent — no shared state between tests
- Assert on exact status codes and response body shapes from the Tech Spec
- Include both unit tests (service layer) and integration tests (full HTTP request)
```

---

## Starter Prompt: Code Review Against Specs

```
Review the following implementation of POST /auth/login against our specs.

Artifacts to check against:
- Architecture Doc: @samples/02-architecture-user-auth.md
- Technical Spec: @samples/03-technical-spec-user-auth.md

Code to review: @src/routes/auth/login.js, @src/services/authService.js

Check for:
1. Does the implementation match every API contract in the Tech Spec?
   (request/response shapes, status codes, error messages)
2. Does it follow every Architecture Doc decision?
   (bcrypt cost 12, Redis sessions, JWT RS256, rate limiting thresholds)
3. Does it satisfy every business acceptance criteria from the PRD?
4. Security: OWASP Top 10 compliance, no info leakage, parameterized queries
5. Are there any cases handled in the code that AREN'T in the spec?
   (feature creep)
6. Are there any spec requirements NOT handled in the code? (gaps)

Flag issues as: CRITICAL / HIGH / MEDIUM / LOW with specific line references.
```

---

## Starter Prompt: Fix a Bug Against the Spec

```
Bug report: Users with deactivated accounts are getting a generic 401 error
instead of the 403 with "Account disabled. Contact support." message.

Per the Technical Spec (AUTH-02), the expected behavior is:
- Deactivated accounts (is_active=false) → 403 with message
  "Account disabled. Contact support."
- Invalid credentials → 401 with "Invalid email or password."

The current code in @src/services/authService.js checks is_active AFTER
password validation instead of BEFORE returning the generic 401.

Fix this bug:
- Check is_active flag after email lookup but before password comparison
- Return the exact 403 response defined in the Tech Spec
- Add a test case that catches this regression
- Do not change any other behavior
```

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
