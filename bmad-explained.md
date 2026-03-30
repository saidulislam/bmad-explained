# BMAD Method: Breakthrough Method for Agile AI-Driven Development

## Executive Summary

**BMAD** stands for **B**reakthrough **M**ethod for **A**gile AI-**D**riven Development.

In plain terms: it's a set of rules, templates, and AI agent personas that sit *on top of* your existing Agile Scrum process. Instead of letting AI write whatever it wants, BMAD makes sure every piece of generated code ties back to an approved requirement, a reviewed architecture, and clear acceptance criteria. **Think of it as giving your AI coding assistant a job description, a spec to follow, and a code review before it starts.**

---

## The "Why": From Vibe-Coding to Spec-Driven Development

### The Problem

Without a structured process, AI-assisted development drifts toward **"vibe-coding"** — you type a loose prompt like *"build me a login page"* and hope the AI figures out the rest. It often does produce something that *looks* right. But:

- **It guessed your requirements** — picked OAuth when you needed SAML, skipped rate limiting entirely
- **It invented an architecture** — used in-memory sessions when your team standardized on Redis
- **It hallucinated edge cases** — returns a 500 error on invalid credentials instead of a clean 401
- **Nobody can verify it** — there's no spec to test against, so QA is reverse-engineering intent from code

This is how teams end up with AI-generated code that passes a demo but fails in production.

### The Fix: Spec-Driven Development

**Spec-Driven Development** means one thing: **no code gets written until a specification exists that defines what to build and how to verify it's correct.**

BMAD enforces this through a chain of three artifacts, each created by the right person, each reviewed before the next begins:

| # | Artifact | Who Creates It | What It Answers | Why It Exists |
|---|---|---|---|---|
| 1 | **PRD** (Product Requirements Document) | **Product Manager** (PM Agent) | *What* are we building, *why*, and *what does "done" look like?* Includes business acceptance criteria for every requirement. | Without it, the AI guesses at requirements. With it, the agent knows exactly what's in scope, what's out, and how success is measured — **by the business, not the developer.** |
| 2 | **Architecture Doc** | **Architect** (Architect Agent) | *How* does it fit into our system? What tech stack, components, security patterns, and boundaries? | Without it, the AI makes its own architecture choices — maybe it picks MD5 when you require bcrypt, or builds a monolith when you need microservices. |
| 3 | **Technical Spec / Story** | **Senior Developer + PM/PO** (co-authored) | *Exactly how* do we implement the PM's requirements? API contracts, data models, error responses — the technical translation of business acceptance criteria. | Co-created so the dev defines *how* to build it while the PM/PO ensures *what's acceptable* is never lost in translation. Neither side works in isolation. |

**The handoff is non-negotiable:** PRD (with business acceptance criteria) feeds the Architecture Doc, Architecture Doc feeds the Technical Spec, PM/PO reviews the Technical Spec to confirm it represents their intent, and *only then* does the Developer Agent write code. No one grades their own homework.

### See It in Action

We've included **real sample artifacts** in the [`samples/`](samples/) folder so you can see exactly what these look like:

- [`01-prd-user-auth.md`](samples/01-prd-user-auth.md) — A Product Manager's PRD for a user authentication system
- [`02-architecture-user-auth.md`](samples/02-architecture-user-auth.md) — An Architect's system design with tech decisions, component boundaries, and security guardrails
- [`03-technical-spec-user-auth.md`](samples/03-technical-spec-user-auth.md) — A developer-ready technical spec with API contracts, data models, and test scenarios

Read them in order. Notice how each one builds on the last, and how by the time you reach the Technical Spec, there is **very little left for the AI to guess about.**

### The Before and After

| Without BMAD (Vibe-Coding) | With BMAD (Spec-Driven) |
|---|---|
| "Build a login page" → AI guesses everything | PRD defines requirements → Arch Doc sets guardrails → Tech Spec defines implementation details |
| AI picks its own architecture | AI follows your team's reviewed architecture |
| QA reverse-engineers intent from code | QA tests against pre-defined acceptance criteria |
| Bugs found in production or UAT | Misalignment caught at spec review, before code is written |

One more thing: BMAD stores all of this — agents, workflows, guardrails, specs — **as files in your repo**. They're versioned in Git, reviewable in PRs, and auditable like any other code. Nothing lives in someone's head or a Slack thread.

> **The core principle:** An AI agent should never generate code that hasn't been pre-validated against a spec.

---

## The Workflow: 4 Phases Mapped to Your Sprint Cycle

![BMAD Method: Spec-Driven AI Development Workflow](bmad/BMAD_Method.png)

| BMAD Phase | When It Happens | What Gets Produced | Who's Involved |
|---|---|---|---|
| **1. Analysis** | Before sprint — during backlog refinement or discovery | PRD with requirements, user stories, acceptance criteria | Product Manager + Business Analyst |
| **2. Planning** | Before sprint — during design sessions | Architecture doc, component boundaries, tech stack decisions | Architect + Engineering Leads |
| **3. Solutioning** | Before sprint — during technical design | Technical specs (API contracts, data models) co-authored with PM/PO | Senior Devs + PM/PO + Architect |
| **4. Implementation** | During the sprint | Working code + tests, generated against the specs from Phases 1–3 | Developers + QA |

**How it fits your current process:** Phases 1–3 happen in your **existing Scrum ceremonies** — backlog refinement, planning, design spikes. Nothing new to schedule. Phase 4 is sprint execution, same as today — except now the AI agent has the full spec context instead of just a Jira title.

**It scales to the task:** A small bug fix or utility gets a lightweight spec (or skips straight to Quick Flow). A complex distributed system gets full architecture docs and API contracts. BMAD adjusts — you don't apply the same overhead to every task.

**The Orchestrator Agent:** An AI coordinator that manages handoffs between phases — routes tasks to the right agent, tracks dependencies, and flags bottlenecks. Think of it as an AI assistant for your Scrum Master, keeping the workflow moving.

---

## Role Impact: How BMAD Empowers Each Stakeholder

> **Important:** Every role below is a **real person on your team**. BMAD gives each person an **AI agent persona** — a specialized AI assistant that helps them do their job faster and more consistently. The human makes the decisions; the AI agent does the heavy lifting.

| Role (Human) | Their AI Agent Persona | How It Helps |
|---|---|---|
| **Product Manager** | **PM Agent** | Helps draft PRDs from your Epics/Stories, structures acceptance criteria in a format AI can execute against. Your work stays the same — the output just becomes machine-readable. |
| **Architect** | **Architect Agent** | Helps generate architecture docs, validate tech decisions, and set guardrails — *before a single line of code is written*. You make the calls; the agent documents and enforces them. |
| **Engineering Lead** | **Orchestrator Agent** | Coordinates agent handoffs across phases, tracks dependencies, flags blockers. You review structured specs instead of speculative AI output — catching problems earlier, not in code review. |
| **Developer** | **Developer Agent** | Receives validated specs + architecture docs via Claude CLI and generates code that respects your system design — not just the immediate prompt. You guide and review; the agent implements. |
| **UI/UX Designer** | **UX Agent** | Design specs and component contracts are captured in the planning phase, ensuring AI-generated frontend code aligns with your design system. |
| **UAT Tester** | **QA Agent** | Acceptance criteria from the PRD become test plans automatically. AI output is verifiable against documented expectations — no reverse-engineering what the code *should* do. |
| **Scrum Master** | **Orchestrator Agent** | Mirrors your coordination role — managing agent workflow discipline, phase gates, and handoffs across the sprint. |

**In short:** You're still the pilot. The AI agent is your co-pilot. BMAD is the flight plan that keeps both of you on course.

BMAD ships with **12+ specialized agent personas** and **20+ structured workflows** covering the full lifecycle. For the complete list with examples, see [`bmad-agents-and-workflows.md`](bmad-agents-and-workflows.md).

**Party Mode** deserves special mention: it loads multiple AI agent personas into a single conversation — like putting your whole AI team in one room. **You (a real human) drive the discussion.** You ask a question like *"Should we use WebSockets or polling?"* and the PM Agent, Architect Agent, Developer Agent, and QA Agent each respond from their perspective — agreements, disagreements, tradeoffs — in seconds instead of scheduling four separate meetings. It's not agents working autonomously; it's one person getting multi-perspective AI input in real time. See [full Party Mode explanation](bmad-agents-and-workflows.md#party-mode-how-real-people-collaborate-through-ai-agents).

---

## "But This Is More Work for Product" — Let's Talk About It

This is the first question your product team will ask. Here's the honest answer.

### What Product Does Today

1. PM creates an **Epic** in Jira
2. PM writes **User Stories** with business rules and acceptance criteria
3. Tech team creates **tech-specific stories** from those
4. Dev starts coding...
5. Dev hits ambiguity → Slack message to PM → PM responds hours later → dev context-switches
6. Repeat step 5 three to five more times per story
7. Code review reveals a misunderstood requirement → rework
8. Sprint review: "That's not what I meant" → card rolls to next sprint
9. UAT finds edge cases nobody discussed → more rework

**The real cycle time killer isn't missing specs — it's the back-and-forth that happens because the specs weren't clear enough for the person (or AI) writing the code.**

### What Product Does With BMAD

1. PM creates an **Epic** in Jira *(same as today)*
2. PM writes **User Stories with acceptance criteria** in a structured PRD template *(same work, better format — the AI PM Agent can even help draft it)*
3. PM sits with Senior Dev for a **30-minute Tech Spec co-authoring session** — Dev translates business criteria into technical implementation, PM confirms intent in real-time *(this replaces days of async Slack back-and-forth)*
4. AI agent receives PRD + Architecture Doc + Tech Spec → generates implementation
5. **Dramatically less ambiguity. Fewer "what did you mean?" moments. Significantly less rework. Fewer rolled cards.**

**Steps 1 and 2 are identical.** Step 3 is new but replaces the 3–5 rounds of Slack clarifications that happen today anyway — it just moves them from scattered and async to one focused 30-minute session. Steps 4 and 5 are where the speed comes from.

### The Numbers

**BMAD does not change your sprint cadence.** A 2-week sprint is still 2 weeks. What changes is the **throughput inside each sprint** and how many sprints an Epic takes to complete.

| Metric | Today | With BMAD | Why the Difference |
|---|---|---|---|
| Clarification loops per story | 3–5 async rounds (hours to days each) | 1 co-authoring session (30 min) | Questions answered upfront, not mid-sprint |
| "That's not what I meant" in sprint review | Common | Rare | PM co-authored the spec, not just reviewed it after the fact |
| **Story cycle time** (ready → done) | 3–5 days (coding + clarification + rework) | 1–2 days (AI generates against clear spec) | The AI agent has the full spec — it isn't guessing |
| **Stories completed per sprint** | 4–6 (rework eats capacity) | 6–10 (less rework = more throughput) | Time not spent on back-and-forth becomes more delivered stories |
| Sprint rollover rate | 20–40% of stories roll | Under 10% | Specs are validated before implementation — fewer surprises |
| **Epic cycle time** | 3–4 sprints / 6–8 weeks | 1–2 sprints / 2–4 weeks | **This is the number product teams care about** |

**The sprint stays the same length. You deliver more per sprint with less waste.** An Epic that used to span 3–4 sprints can close in 1–2 — not because the sprint is shorter, but because you're not losing capacity to rework and clarification loops.

### The Key Insight for Product

> **BMAD doesn't add work or change your sprint cadence. It moves 30 minutes of your time from "answering Slack questions mid-sprint" to "one focused co-authoring session before sprint." The result: higher throughput per sprint, fewer rolled cards, and Epics that close in fewer sprints.**

Your existing artifacts (Epics, Stories, acceptance criteria) *are* the BMAD inputs — just structured in a way that an AI agent can execute against without guessing. The PM Agent can even help generate the PRD from your existing Jira stories.

---

## How It Works With Our Tools

BMAD officially **recommends Claude Code** (Anthropic's CLI) as its primary IDE integration. It also supports Cursor and other AI coding assistants. Setup is one command:

```bash
npx bmad-method install
```

Here's what that gives you:

- **Specs live in your repo** — PRDs, architecture docs, and technical specs are stored as markdown files alongside your code. Claude CLI reads them via `CLAUDE.md` references, so the AI agent always has the full project context — not just the current prompt.
- **Agent personas are pre-configured** — When you activate the PM Agent or Architect Agent, Claude CLI loads a structured system prompt that constrains the AI to that role. It won't go off-script.
- **Phase gates catch problems early** — Before the Developer Agent writes code, the Architect Agent reviews the specs. Agents can challenge each other's outputs (called Adversarial Review) — like a built-in peer review before implementation.
- **Large projects stay manageable** — Project context is split across files so the AI loads only what it needs for the current task, even on large codebases.
- **Works where you work** — **VS Code** and **IntelliJ** via Claude CLI extensions. No new tools to learn.

---

## The Bottom Line

**BMAD is not a replacement for Scrum.** It's the missing layer between your existing Agile process and AI-assisted development.

Without it, AI coding is fast but unpredictable — you get speed but lose control. With BMAD, AI coding is fast *and* constrained — every piece of generated code traces back to an approved requirement, a reviewed architecture, and testable acceptance criteria.

**What you get:**
- **Traceability** — PRD → Architecture Doc → Technical Spec → Code. Every decision is documented.
- **Accountability** — PM owns requirements, Architect owns guardrails, Dev owns implementation. No one grades their own homework.
- **Speed with confidence** — AI generates code faster, and the specs make sure it generates the *right* code.

---

*Spec-driven development for predictable AI-assisted outcomes.*
