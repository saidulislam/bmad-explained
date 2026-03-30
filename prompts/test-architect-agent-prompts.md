# Test Architect Agent (TEA) — Starter Prompts

**Who uses this:** QA Lead / UAT Tester
**Module:** Test Architecture Module
**When to activate:** Phase 3 (Solutioning) and Phase 4 (Implementation)

---

## Starter Prompt: Create a Risk-Based Test Strategy

```
I need a risk-based test strategy for our User Authentication System.

Artifacts to reference:
- PRD: @samples/01-prd-user-auth.md
- Architecture Doc: @samples/02-architecture-user-auth.md

Risk areas to evaluate:
- Security (authentication bypass, credential stuffing, injection attacks)
- Data integrity (user records, session state, audit logs)
- Performance (login latency under load, rate limiting effectiveness)
- Availability (Redis failure, database failover, OAuth provider outage)
- Compliance (SOC 2 requirements for auth)

For each risk area, generate:
- Risk level (Critical / High / Medium / Low)
- Test types needed (unit, integration, e2e, security, performance, chaos)
- Coverage priority (test this first vs. test this later)
- Specific test scenarios with expected outcomes
- Tools recommended (Jest, Playwright, k6, OWASP ZAP, etc.)

Output a test strategy document I can share with the team and use to
generate specific test plans per story.
```

**Artifact delivered:** `test-strategy.md`

---

## Starter Prompt: Generate Test Plan from Acceptance Criteria

```
Generate a detailed test plan for story AUTH-02 (User Login).

Business acceptance criteria (from PRD — PM-owned):
- Session token issued, user redirected to dashboard within 500ms
- After 5 failed attempts in 15 min, user is locked out with clear message
- Deactivated user sees "Account disabled. Contact support."

Technical spec: @samples/03-technical-spec-user-auth.md

For each acceptance criterion, generate:
- Test case ID
- Test type (unit / integration / e2e / security)
- Preconditions (test data setup)
- Steps to execute
- Expected result (exact response codes, messages, behavior)
- Edge cases to cover
- Priority (P0 = must pass for release, P1 = should pass, P2 = nice to have)

Also generate:
- Negative test cases (what should NOT happen)
- Security-specific tests (injection, token manipulation, session hijacking)
- Performance test scenario (login under 100 concurrent users)
```

**Artifact delivered:** `test-plan-AUTH-02.md`

---

## Starter Prompt: Automate E2E Test Generation

```
Based on the UX spec and technical spec for the login flow, generate
Playwright end-to-end tests.

User flow:
1. Navigate to /login
2. Enter email and password
3. Click "Log in"
4. Verify redirect to /dashboard
5. Verify user name displayed in header

Error flows to test:
- Wrong password → see "Invalid email or password" inline error
- 5 failed attempts → see lockout message with countdown
- Disabled account → see "Account disabled. Contact support."

Generate Playwright tests that:
- Use page object pattern (LoginPage, DashboardPage)
- Include data-testid selectors (from UX component contracts)
- Run against our staging environment
- Are independent (each test seeds and cleans its own data)
- Include screenshots on failure for debugging
```

**Artifact delivered:** `tests/e2e/auth-login.spec.ts`

---

## Starter Prompt: Pre-Release Quality Gate

```
We're about to release the Authentication feature. Run a quality gate check.

Review the following against the test strategy:
- Test results: @test-results/auth-suite.json
- Coverage report: @coverage/lcov-report/index.html
- Security scan: @security/zap-report.json

Check:
1. Are all P0 test cases passing?
2. Is code coverage above our 80% threshold for auth-critical paths?
3. Are there any open security findings (Critical or High)?
4. Were all acceptance criteria from the PRD exercised in tests?
5. Were performance tests run? Did login meet the 500ms p95 target?

Output a GO / NO-GO recommendation with:
- Summary of findings
- Any gaps that must be addressed before release
- Any risks the team should accept knowingly (with justification)
```

**Artifact delivered:** `release-quality-gate.md` (GO / NO-GO)

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
