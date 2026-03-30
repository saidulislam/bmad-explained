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

Read them in order. Notice how each one builds on the last, and how by the time you reach the Technical Spec, there is **zero ambiguity** about what the AI should generate.

### Why This Changes Everything

BMAD embraces the **Agent-as-Code paradigm**: agents, workflows, and guardrails are defined *as code* in your repo — versioned, reviewable, and auditable like any other artifact.

| Vibe-Coding | Spec-Driven (BMAD) |
|---|---|
| "Build a login page" | PRD defines requirements → Arch Doc sets guardrails → Tech Spec defines every detail |
| AI guesses requirements | AI reads approved requirements |
| AI invents architecture | AI follows reviewed architecture |
| QA reverse-engineers intent from code | QA tests against pre-defined acceptance criteria |
| Bugs found in production | Misalignment caught at spec review |

> **The core principle:** An AI agent should never generate code that hasn't been pre-validated against a spec.

---

## The Workflow: 4 Phases Mapped to Your Sprint Cycle

![BMAD Method: Spec-Driven AI Development Workflow](bmad/BMAD_Method.png)

| BMAD Phase | Sprint Activity | Key Output | Who Leads |
|---|---|---|---|
| **1. Analysis** | Sprint Planning / Backlog Refinement | PRD, validated user stories, personas | Product Manager + Business Analyst |
| **2. Planning** | Architecture & Design Sessions | Architecture doc, component boundaries, tech stack decisions | Architect + Engineering Leads |
| **3. Solutioning** | Pre-sprint technical design | Technical specs (API contracts, data models) co-authored with PM/PO to ensure business intent is preserved | Senior Devs + PM/PO + Architect |
| **4. Implementation** | Sprint execution | Production-ready code, generated against specs with AI agents | Developers + QA |

**How it fits:** Phases 1–3 front-load the thinking into **existing Scrum ceremonies** (refinement, planning, design spikes). Phase 4 is where developers use AI agents — but now those agents have the full spec context, not just a Jira title.

**Scale-Domain-Adaptive:** BMAD automatically adjusts planning depth to project complexity — a small utility gets a lightweight spec; a distributed system gets full architecture docs and API contracts. No one-size-fits-all overhead.

**The Orchestrator Agent:** A central coordinator manages handoffs between phases, routes tasks to the right specialized agent, tracks dependencies, and prevents workflow bottlenecks. Think of it as your AI Scrum Master that ensures no agent goes rogue.

---

## Role Impact: How BMAD Empowers Each Stakeholder

> **Important:** Every role below is a **real person on your team**. BMAD gives each person an **AI agent persona** — a specialized AI assistant that helps them do their job faster and more consistently. The human makes the decisions; the AI agent does the heavy lifting.

| Role (Human) | Their AI Agent Persona | How It Helps |
|---|---|---|
| **Product Manager** | **PM Agent** | Helps draft PRDs from your Epics/Stories, structures acceptance criteria in a format AI can execute against. Your work stays the same — the output just becomes machine-readable. |
| **Architect** | **Architect Agent** | Helps generate architecture docs, validate tech decisions, and set guardrails — *before a single line of code is written*. You make the calls; the agent documents and enforces them. |
| **Engineering Lead** | **Orchestrator Agent** | Coordinates agent handoffs across phases, tracks dependencies, flags blockers. You review structured specs instead of speculative AI output — shift-left quality. |
| **Developer** | **Developer Agent** | Receives validated specs + architecture docs via Claude CLI and generates code that respects your system design — not just the immediate prompt. You guide and review; the agent implements. |
| **UI/UX Designer** | **UX Agent** | Design specs and component contracts are captured in the planning phase, ensuring AI-generated frontend code aligns with your design system. |
| **UAT Tester** | **QA Agent** | Acceptance criteria from the PRD become test plans automatically. AI output is verifiable against documented expectations — no reverse-engineering what the code *should* do. |
| **Scrum Master** | **Orchestrator Agent** | Mirrors your coordination role — managing agent workflow discipline, phase gates, and handoffs across the sprint. |

**In short:** You're still the pilot. The AI agent is your co-pilot. BMAD is the flight plan that keeps both of you on course.

BMAD ships with **12+ specialized agent personas** and **34+ structured workflows** covering the full lifecycle. For the complete list with examples, see [`bmad-agents-and-workflows.md`](bmad-agents-and-workflows.md).

**Party Mode** deserves special mention: it loads multiple AI agent personas into a single conversation — like putting your whole AI team in one room. **You (a real human) drive the discussion.** You ask a question like *"Should we use WebSockets or polling?"* and the PM Agent, Architect Agent, Developer Agent, and QA Agent each respond from their perspective — agreements, disagreements, tradeoffs — in seconds instead of scheduling four separate meetings. It's not agents working autonomously; it's one person getting multi-perspective AI input in real time. See [full Party Mode explanation](bmad-agents-and-workflows.md#party-mode-how-real-people-collaborate-through-ai-agents).

---

## Tooling Synergy: BMAD + Claude CLI + Opus 4.6

BMAD officially **recommends Claude Code** (Anthropic's CLI) as its primary IDE integration, and also supports Cursor and other AI coding assistants. Setup is one command:

```bash
npx bmad-method install
```

Here's how the synergy works:

- **Context management** — BMAD artifacts (PRDs, arch docs, technical specs) are stored as markdown in-repo. Claude CLI with Opus 4.6's extended context window ingests these as project knowledge via `CLAUDE.md` and file references, keeping the agent grounded across long sessions.
- **Agent personas** — BMAD defines 12+ specialized agent roles (Analyst, PM, Architect, Product Owner, Scrum Master, Developer, UX, QA, and more). In Claude CLI, these translate to structured system prompts and skills that constrain the agent's behavior to the current phase.
- **Guardrails in practice** — Checklist-driven validation at each phase gate, including **Adversarial Review** where agents stress-test each other's outputs before promotion. The Architect Agent reviews specs before the Developer Agent touches code.
- **Document sharding** — Project context is intelligently split across files so agents load only what they need, keeping within context limits even on large projects.
- **IDE integration** — Works in **VS Code** and **IntelliJ** via Claude CLI extensions, meeting developers where they already work.

> **The result:** Opus 4.6 generates code that is traceable to specs, constrained by architecture, and verifiable against acceptance criteria — not hallucinated from a one-line prompt.

---

## "But This Is More Work for Product" — Addressing the Elephant in the Room

**It's not.** Here's why.

### What Product Does Today (Without BMAD)

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
5. **No ambiguity. No "what did you mean?" No rework. No rolled cards.**

### The Math That Matters to Product

| Metric | Without BMAD | With BMAD |
|---|---|---|
| Clarification loops per story | 3–5 async rounds (hours to days each) | 1 co-authoring session (30 min) |
| "That's not what I meant" in sprint review | Common | Rare — PM confirmed intent in the Tech Spec |
| Cards rolled to next sprint due to rework | Frequent | Minimal — acceptance criteria verified before code gen |
| Implementation time (AI-assisted) | Fast but unpredictable — rework erases the speed | Fast *and* right the first time |
| **Epic cycle time** | **Weeks** (coding is fast, rework is slow) | **Days** (upfront clarity eliminates rework) |

### The Key Insight for Product

> **BMAD doesn't add work. It moves 30 minutes of your time from "answering Slack questions mid-sprint" to "one focused co-authoring session before sprint." The result: the AI builds it right the first time, and your Epic ships days faster.**

The PM's existing artifacts (Epics, Stories, acceptance criteria) *are* the BMAD inputs — just structured in a way that an AI agent can execute against without guessing. The PM Agent can even help generate the PRD from your existing Jira stories.

---

## The Bottom Line

| Without BMAD | With BMAD |
|---|---|
| "Generate a login page" → hope for the best | Spec-validated story → architecture-constrained implementation → verifiable output |
| AI hallucinates plausible but wrong code | AI follows documented guardrails and contracts |
| Rework discovered in code review or UAT | Misalignment caught at spec review, before code gen |
| No audit trail from requirement to code | Full traceability: PRD → Arch Doc → Tech Spec → Implementation |

**BMAD is not a replacement for Scrum. It is the missing process layer that makes AI-assisted development predictable, traceable, and production-ready.**

---

*Efficiency without Chaos.*
