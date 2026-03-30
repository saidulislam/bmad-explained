# BMAD Agents & Workflows: Complete Reference

> **Key concept:** Every agent listed below is an **AI persona** — not a person. A real person on your team activates an agent to help them do their job faster. Think of it as switching your AI assistant into a specialized mode.

---

## Agent Personas

Each agent has a name, a specialization, and a defined scope. When you activate an agent in Claude CLI, the AI adopts that persona's expertise, constraints, and communication style.

### Core Agents (BMad Method Module)

| Agent | Persona Name | Who Uses It (Human) | What It Does | Starter Prompt Samples |
|---|---|---|---|---|
| **PM Agent** | John | Product Manager | Drafts PRDs, structures acceptance criteria, validates user stories against business goals | [PM Agent prompts](prompts/pm-agent-prompts.md) — Create PRD, convert Jira Epics, strengthen acceptance criteria, scope negotiation |
| **Architect Agent** | Winston | Architect / Tech Lead | Generates architecture docs, validates tech decisions, defines component boundaries and security guardrails | [Architect Agent prompts](prompts/architect-agent-prompts.md) — Create architecture from PRD, ADRs, review proposals, security checklists |
| **Developer Agent** | Amelia | Developer | Implements stories against specs, generates code that respects architecture constraints, runs within validated guardrails | [Developer Agent prompts](prompts/developer-agent-prompts.md) — Implement from spec, generate tests, code review against specs, bug fixes |
| **SM Agent** | — | Scrum Master | Sprint planning, retrospectives, velocity tracking, workflow coordination | [SM Agent prompts](prompts/sm-agent-prompts.md) — Sprint planning, mid-sprint status, retrospectives, scope changes |
| **UX Designer Agent** | — | UI/UX Designer | Creates UX specs, validates design system compliance, defines component contracts | [UX Agent prompts](prompts/ux-agent-prompts.md) — UX spec from PRD, error states, component contracts, accessibility review |
| **Analyst Agent** | — | Business Analyst / PM | Conducts domain research, market research, technical research, generates project context | [Analyst Agent prompts](prompts/analyst-agent-prompts.md) — Domain research, competitive analysis, tech comparisons, stakeholder prep |

### Additional Agents (Extended Modules)

| Agent | Module | What It Does |
|---|---|---|
| **Test Architect** (TEA) | Test Architecture Module | Creates risk-based testing strategies, generates test plans from acceptance criteria |
| **Tech Writer** | BMM | Generates documentation from code and specs |
| **Quick Flow Solo Dev** | BMM | Streamlined agent for small, well-understood tasks — combines planning + implementation in one flow |
| **Brainstorming Coach** (Carson) | Creative Intelligence Suite | Facilitates structured brainstorming sessions |
| **Creative Problem Solver** | Creative Intelligence Suite | Applies lateral thinking frameworks to stuck problems |
| **Design Thinking Coach** | Creative Intelligence Suite | Guides teams through empathize → define → ideate → prototype → test |
| **Innovation Strategist** | Creative Intelligence Suite | Evaluates ideas against market viability and technical feasibility |

---

## Workflows by Phase

Workflows are the structured steps an agent follows. Each workflow has a defined input, a series of steps, and a specific output artifact.

### Phase 1: Discovery & Analysis *(Optional — skip if requirements are already clear)*

| Workflow | Command | What Happens | Output |
|---|---|---|---|
| **Brainstorming** | `bmad-brainstorming` | AI facilitates structured ideation with guided prompts | `brainstorming-report.md` |
| **Domain Research** | `bmad-domain-research` | Validates domain assumptions with structured research | Research findings |
| **Market Research** | `bmad-market-research` | Validates market assumptions, competitive landscape | Research findings |
| **Technical Research** | `bmad-technical-research` | Evaluates technical feasibility, compares approaches | Research findings |
| **Product Brief** | `bmad-product-brief` | Captures strategic vision in a concise format | `product-brief.md` |
| **PR/FAQ** | `bmad-prfaq` | Amazon-style "working backwards" — stress-tests concepts | `prfaq-{project}.md` |

**Example:** *Your PM wants to explore a new feature idea. They activate the Analyst Agent and run `bmad-brainstorming`. The agent asks structured questions, challenges assumptions, and produces a brainstorming report. If the idea has legs, the PM moves to Phase 2.*

### Phase 2: Planning *(PM + UX Designer — define what to build)*

| Workflow | Command | What Happens | Output |
|---|---|---|---|
| **Create PRD** | `bmad-create-prd` | Guides PM through structured requirements gathering — personas, requirements, acceptance criteria, scope boundaries | `PRD.md` |
| **Create UX Design** | `bmad-create-ux-design` | Generates UX spec with interaction patterns, component contracts, design system alignment | `ux-spec.md` |

**Example:** *PM activates the PM Agent and runs `bmad-create-prd`. The agent walks them through: "Who are the users? What problem are we solving? What does success look like?" The output is a structured PRD that becomes the single source of truth for the entire team.*

### Phase 3: Solutioning *(Architect + Senior Dev + PM/PO — define how to build it)*

| Workflow | Command | What Happens | Output |
|---|---|---|---|
| **Create Architecture** | `bmad-create-architecture` | Generates architecture doc with tech decisions, component boundaries, ADRs (Architecture Decision Records) | `architecture.md` |
| **Create Epics & Stories** | `bmad-create-epics-and-stories` | Breaks PRD requirements into implementable Epics and Stories with acceptance criteria | Epic files with stories |
| **Check Implementation Readiness** | `bmad-check-implementation-readiness` | Phase gate — validates that PRD, architecture, and stories are complete and consistent before dev begins | PASS / CONCERNS / FAIL |
| **Generate Project Context** | `bmad-generate-project-context` | Auto-generates project guidelines for AI agents (what goes into `CLAUDE.md`) | `project-context.md` |

**Example:** *Architect activates the Architect Agent and runs `bmad-create-architecture`, feeding it the PRD. The agent proposes a system design, asks clarifying questions ("Do you want JWT or session-based auth?"), and produces an architecture doc with explicit tech decisions and rationale. Then the team runs `bmad-check-implementation-readiness` — a gate check that flags any gaps before a single line of code is written.*

### Phase 4: Implementation *(Dev + QA — build and validate)*

| Workflow | Command | What Happens | Output |
|---|---|---|---|
| **Sprint Planning** | `bmad-sprint-planning` | Initializes sprint tracking, allocates stories to sprint | `sprint-status.yaml` |
| **Create Story** | `bmad-create-story` | Prepares the next story for implementation — pulls from Epic, links to specs | `story-[slug].md` |
| **Dev Story** | `bmad-dev-story` | **The main implementation workflow** — agent reads specs + architecture, generates code + tests | Working code + tests |
| **Code Review** | `bmad-code-review` | AI reviews generated code against architecture and specs | Approval or change requests |
| **Course Correct** | `bmad-correct-course` | Handles mid-sprint changes — re-routes plan without losing context | Updated plan |
| **Sprint Status** | `bmad-sprint-status` | Tracks progress against sprint goals | Status update |
| **Retrospective** | `bmad-retrospective` | Reviews what worked, what didn't, captures lessons | Lessons learned |

**Example:** *Developer activates the Developer Agent and runs `bmad-dev-story` for story AUTH-02 (User Login). The agent loads the PRD, Architecture Doc, and Technical Spec. It generates the Express route, bcrypt password validation, JWT issuance, Redis session storage, rate limiting logic, and error responses — all matching the spec exactly. Then the team runs `bmad-code-review` where the agent validates the output against architecture guardrails.*

### Quick Flow *(For small, well-understood tasks)*

| Workflow | Command | What Happens | Output |
|---|---|---|---|
| **Quick Dev** | `bmad-quick-dev` | All-in-one: clarify intent → plan → implement → review → present | `spec-*.md` + working code |

**Example:** *A developer needs to add a simple utility function. Instead of running the full 4-phase cycle, they run `bmad-quick-dev`. The agent clarifies what's needed, writes a mini-spec, implements it, self-reviews, and presents the result. Scale-Domain-Adaptive in action — small task, lightweight process.*

---

## Party Mode: How Real People Collaborate Through AI Agents

### What It Is

Party Mode (`bmad-party-mode`) loads **multiple AI agent personas into a single conversation** — like putting your whole AI team in one room. Instead of talking to one agent at a time, you talk to all of them at once.

### How It Actually Works

1. **You (a real human) start a Party Mode session** in Claude CLI
2. **The BMad Master orchestrator** loads the relevant agents — PM Agent, Architect Agent, Developer Agent, QA Agent, UX Agent, etc.
3. **You ask a question or raise a topic** — e.g., *"Should we use WebSockets or polling for real-time notifications?"*
4. **Each agent responds from their perspective:**
   - **Architect Agent (Winston):** *"WebSockets are the right call for our scale. Here's the infrastructure impact..."*
   - **Developer Agent (Amelia):** *"I agree on WebSockets, but we'll need to handle reconnection logic. Here's what that looks like..."*
   - **PM Agent (John):** *"From a product standpoint, the requirement is sub-second delivery. WebSockets meets that. But what's the fallback if the connection drops?"*
   - **QA Agent:** *"We'll need to test connection failures, reconnection, and message ordering. Adding that to the test plan..."*
5. **You push back, ask follow-ups, redirect** — it's a real conversation, not a one-shot answer
6. **The discussion continues** until you have alignment, then you move forward with the decision captured

### When to Use Party Mode

| Scenario | Why Party Mode Helps |
|---|---|
| **Complex architecture decisions** | Get engineering, product, and QA perspectives simultaneously instead of scheduling 3 separate meetings |
| **Sprint planning** | PM prioritizes, Architect estimates complexity, Dev flags dependencies — all in one conversation |
| **Incident post-mortems** | Analyze from technical, process, and product angles at once |
| **Design reviews** | UX, Dev, and Architect evaluate feasibility, usability, and maintainability together |
| **Tradeoff discussions** | When there's no obvious right answer and you need multiple viewpoints to decide |

### What Party Mode Is NOT

- It's **not autonomous agents working without you** — you're always driving the conversation
- It's **not a replacement for real team meetings** — it's a tool for one person to quickly get multi-perspective AI input
- It's **not agents talking to each other in the background** — every response is visible to you and directed by you

> **The analogy:** Imagine you could instantly summon your PM, Architect, Senior Dev, and QA lead into a room, ask them a question, and get all their perspectives in 30 seconds instead of scheduling a meeting next week. That's Party Mode.

---

## Summary: The Full Picture

```
Phase 1 (Optional)          Phase 2              Phase 3                Phase 4
Discovery & Analysis   →    Planning        →    Solutioning       →   Implementation

Brainstorming               Create PRD           Create Architecture    Sprint Planning
Domain Research             Create UX Design     Create Epics/Stories   Dev Story
Market Research                                  Readiness Check        Code Review
Technical Research                               Generate Context       Course Correct
Product Brief                                                           Sprint Status
PR/FAQ                                                                  Retrospective

         ↑                       ↑                     ↑                     ↑
    Analyst Agent           PM Agent +            Architect Agent +     Developer Agent +
                           UX Agent               PM/PO + Dev Agent     QA Agent

                    ← Party Mode available at any phase for multi-perspective decisions →
```

---

*For the full, up-to-date reference, see [docs.bmad-method.org](https://docs.bmad-method.org/) and the [BMAD-METHOD GitHub repo](https://github.com/bmad-code-org/BMAD-METHOD).*
