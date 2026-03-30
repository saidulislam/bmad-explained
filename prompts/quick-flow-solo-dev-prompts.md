# Quick Flow Solo Dev Agent — Starter Prompts

**Who uses this:** Developer (for small, well-understood tasks)
**Module:** BMad Method (BMM)
**When to activate:** Any time — bypasses the full 4-phase cycle
**Command:** `bmad-quick-dev`

---

## Starter Prompt: Small Feature — End to End

```
Quick dev task: Add a "Remember Me" checkbox to the login form.

Context:
- Current login flow: @src/routes/auth/login.js
- Frontend login page: @src/pages/Login.tsx
- Architecture Doc: @samples/02-architecture-user-auth.md

Requirements:
- Add a "Remember me" checkbox to the login form
- When checked: set refresh token TTL to 30 days (instead of default 7 days)
- When unchecked: keep current 7-day refresh token TTL
- Store the preference in the JWT claims so the refresh endpoint knows
- No changes to the access token TTL (stays at 15 min)

This is small enough to skip the full PRD → Arch → Spec cycle.
Plan it, implement it, write tests, and self-review — all in one flow.
```

**Artifact delivered:** `spec-remember-me.md` + working code + tests

---

## Starter Prompt: Bug Fix — Quick Turnaround

```
Quick fix: The logout endpoint returns 200 but doesn't actually
invalidate the Redis session.

Current code: @src/services/authService.js (logout method)

Expected behavior (from Tech Spec):
- POST /auth/logout should delete the Redis session key
- Return 200 with { "message": "Logged out successfully" }
- Subsequent requests with the old access token should still work
  (JWT is stateless) but refresh should fail (session gone)

What's happening:
- The Redis DEL command is called but with wrong key format
- Using "session:{email}" instead of "session:{userId}"

Fix this, add a regression test, and confirm the fix matches the spec.
```

**Artifact delivered:** Code fix + regression test

---

## Starter Prompt: Utility Function

```
Quick dev: Create a password strength validator utility.

Requirements:
- Minimum 8 characters
- Check against top 1000 common passwords (from HaveIBeenPwned list)
- Return a strength score: weak / fair / strong
- Return specific feedback messages ("Add a number", "Too common", etc.)

This will be used by the registration endpoint but is a standalone utility.
Put it in src/utils/passwordStrength.js with full unit tests.

No PRD needed — this is a well-defined utility with clear inputs and outputs.
```

**Artifact delivered:** `src/utils/passwordStrength.js` + `tests/utils/passwordStrength.test.js`

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
