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

| Role | BMAD Superpower |
|---|---|
| **Product Manager** | Defines the PRD **and owns all acceptance criteria** — the PM decides what "done" looks like, not the developer. Reviews Technical Specs before implementation to confirm intent is preserved |
| **Architect** | Uses the **Architect Agent** persona to set technical guardrails, define component boundaries, and validate architecture *before a single line of code is written* |
| **Engineering Lead** | Reviews structured specs instead of reviewing speculative AI output — shift-left quality |
| **Developer** | Feeds validated specs + architecture docs into Claude CLI; gets code that respects the system design, not just the immediate prompt |
| **UI/UX Designer** | Design specs and component contracts are captured in the planning phase, ensuring AI-generated frontend code aligns with the design system |
| **UAT Tester** | Acceptance criteria are baked into specs from Phase 1 — test plans write themselves; AI output is verifiable against documented expectations |
| **Scrum Master** | The **Orchestrator Agent** mirrors the SM role — coordinating agent handoffs, managing dependencies, and enforcing workflow discipline across all phases |

BMAD ships with **12+ specialized agent personas** and **34+ structured workflows** covering the full lifecycle. In **Party Mode**, multiple agents collaborate in a single session — e.g., Architect + Developer + QA reviewing a design simultaneously — enabling rapid, multi-perspective feedback loops.

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
