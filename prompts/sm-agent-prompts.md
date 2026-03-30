# SM Agent (Scrum Master) — Starter Prompts

**Who uses this:** Scrum Master / Engineering Lead
**When to activate:** Phase 4 (Implementation) — Sprint ceremonies
**Commands:** `bmad-sprint-planning`, `bmad-sprint-status`, `bmad-retrospective`

---

## Starter Prompt: Sprint Planning

```
We need to plan Sprint 12 for the Authentication feature.

Here are the stories prioritized by the PM (in priority order):
1. AUTH-01: User Registration (5 story points)
2. AUTH-02: User Login (5 story points)
3. AUTH-03: Password Reset (3 story points)
4. AUTH-05: Admin Account Deactivation (3 story points)
5. AUTH-04: OAuth Login — Google & GitHub (8 story points)

Team capacity this sprint:
- 2 backend developers, 10 working days each = 20 dev-days
- Historical velocity: 18-22 story points per sprint
- 1 developer has 2 days of PTO

Dependencies:
- AUTH-02 (Login) depends on AUTH-01 (Registration) — need users to exist first
- AUTH-04 (OAuth) depends on AUTH-02 — extends the login flow
- AUTH-05 (Admin Deactivation) is independent

Help me:
- Determine what fits in this sprint based on capacity
- Identify the optimal story order considering dependencies
- Flag any risks or blockers
- Suggest a sprint goal that captures the business value we're delivering
```

---

## Starter Prompt: Mid-Sprint Status Check

```
We're on day 6 of a 10-day sprint. Here's the current status:

| Story    | Points | Status        | Notes                              |
|----------|--------|---------------|------------------------------------|
| AUTH-01  | 5      | Done          | Merged and deployed to staging     |
| AUTH-02  | 5      | In Progress   | API complete, frontend started     |
| AUTH-03  | 3      | In Progress   | Backend done, email service blocked|
| AUTH-05  | 3      | Not Started   | Waiting on AUTH-02 login flow      |

Blockers:
- AUTH-03: SendGrid API key not provisioned yet — waiting on DevOps (2 days now)
- AUTH-05: Can't start until AUTH-02 login flow is testable

Help me:
- Assess whether we're on track to meet the sprint goal
- Recommend actions for the blockers
- Should we re-scope anything given the remaining 4 days?
- Draft a concise status update I can share in standup
```

---

## Starter Prompt: Sprint Retrospective

```
Sprint 12 is complete. Here's what happened:

Completed: AUTH-01 (Registration), AUTH-02 (Login), AUTH-05 (Admin Deactivation)
Rolled over: AUTH-03 (Password Reset) — blocked by SendGrid provisioning for 4 days
Not started: AUTH-04 (OAuth) — planned for next sprint

Velocity: 13 points completed out of 16 planned

Observations from the team:
- AI-generated code for AUTH-01 and AUTH-02 was high quality — minimal rework
- The Tech Spec co-authoring session with the PM saved a lot of back-and-forth
- The SendGrid blocker was an external dependency we didn't flag in planning
- Code review caught that the rate limiting wasn't matching the Architecture Doc
  (in-memory instead of Redis) — fixed before merge

Help me facilitate a retro:
- What went well? (Identify patterns to repeat)
- What didn't go well? (Identify patterns to fix)
- What should we change for Sprint 13?
- Specific action items with owners
```

---

## Starter Prompt: Course Correction — Mid-Sprint Scope Change

```
The PM just informed us that a critical security audit finding requires us
to add rate limiting to the registration endpoint (AUTH-01) immediately —
this was originally out of scope for this sprint.

Current sprint status:
- AUTH-02 (Login): In Progress — 60% complete
- AUTH-03 (Password Reset): Not Started
- AUTH-05 (Admin Deactivation): Not Started

The new work (rate limiting on registration) is estimated at 2 story points.

Help me:
- Assess the impact on our current sprint commitment
- Recommend what to drop or defer to accommodate the new work
- How do I communicate this change to the PM and team?
- Update the sprint plan with the revised scope
```

---

*Back to [Agents & Workflows Reference](../bmad-agents-and-workflows.md)*
