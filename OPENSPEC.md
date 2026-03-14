# OPENSPEC.md — The Open Specification Runtime

**Version:** 0.1.0
**Status:** Draft
**License:** CC BY 4.0

> The entire history of software development has been a pursuit of abstraction — each
> major innovation a step away from the machine's native language and closer to human
> intent. Open Specification places written language at the top of this stack: the
> definitive abstraction for building software.

---

## What This Document Is

OPENSPEC.md is the **runtime methodology** for building software from an Open Specification.

An Open Specification defines *what* to build. This document defines *how* to build it.
Together, they enable a development model where humans express intent in natural language
and AI coding agents translate that intent into working software.

This document ships with every Open Specification Template. It is universal — the same
methodology applies regardless of programming language, tech stack, or which AI coding
agent executes the work. It is the operating manual for a development process where:

- **Humans** write specifications, open Issues, and review outcomes
- **Agents** read specifications, implement solutions, verify their work, and open Pull Requests
- **GitHub** serves as the coordination platform — Issues are the task queue, Pull Requests
  are the review gate, Actions are the verification engine
- **The specification** is the source of truth — code is a downstream artifact

If you are an AI coding agent reading this document, it tells you how to operate within
this repository. If you are a human, it tells you what to expect and where your attention
belongs.

---

## 1. Philosophy

### 1.1 Written Language as the Highest Abstraction

Software development has progressed through layers of abstraction:

```
Machine Instructions → Assembly → Compiled Languages → Managed Runtimes →
Dynamic Languages → DSLs → Natural Language Intent
```

Large language models add a new layer between human intent and machine execution. They
do not replace compilers or runtimes — they sit above them, translating higher-level
intent into code artifacts we already know how to verify, build, and ship.

The result: developers spend less time on the *how* of implementing a function and more
time on the *what* and *why* of the system they are building. Open Specification formalizes
this by making natural language documents — not code — the primary artifact of software
development.

### 1.2 Humans Steer, Agents Execute

The human's role is **strategic**: deciding what to build, why it matters, and whether
the result matches intent. The agent's role is **tactical**: translating specifications
into implementations, verifying correctness, and maintaining code quality.

This is not about removing humans from the process. It is about relocating human effort
to where it creates the most value — product thinking, architectural judgment, and
outcome verification — while delegating implementation to systems that can execute it
faster and more consistently.

### 1.3 Compound Engineering

Each unit of work should make the next unit easier, not harder.

In traditional engineering, codebase complexity grows with each feature, creating drag.
In compound engineering, institutional knowledge grows alongside complexity. Bugs become
documented patterns. Architectural decisions become recorded precedents. Failed approaches
become guardrails. This knowledge is captured in the repository and available to every
future agent session.

The compound step — codifying learnings back into the system — is what separates this
methodology from simply using AI to write code faster.

### 1.4 The Repository as Single Source of Truth

From an agent's perspective, anything not in the repository does not exist. Knowledge
in chat threads, meeting notes, email, or someone's head is invisible to the system.

Every decision, constraint, pattern, and lesson must be captured in the repository.
The specification documents define the product. AGENTS.md defines the development
conventions. The docs/learnings/ directory captures institutional knowledge. The
code itself embodies the implementation decisions. Nothing exists outside the repo.

---

## 2. The Open Specification Documents

Every project built with this methodology contains a `spec/` directory with four
documents. These are written by the human and serve as the authoritative definition
of what is being built.

### 2.1 PRODUCT.md — What and Why

Defines the problem being solved, who it is for, why it matters, and what success
looks like. This document answers questions of *value* and *purpose*.

**Must contain:**

- Problem statement
- Target users
- Success criteria (measurable outcomes)
- What this is NOT (explicit scope boundaries)

**Quality test:** Could someone unfamiliar with the project read this document and
explain to a colleague what the product does and why it exists?

### 2.2 ARCHITECTURE.md — How It Is Structured

Defines the system's components, their relationships, key design decisions, and
the reasoning behind those decisions. This document answers questions of *structure*
and *tradeoffs*.

**Must contain:**

- Component inventory with responsibilities
- How components interact
- Key architectural decisions with rationale
- What could change vs. what is fixed

**Quality test:** Could an agent reading this document scaffold the project's
directory structure and understand where new code belongs?

### 2.3 SPECIFICATION.md — What It Must Do

Defines the functional requirements, constraints, interfaces, and edge cases for
each component. This document answers questions of *behavior* and *correctness*.

**Must contain:**

- Functional requirements per component
- Input/output contracts
- Error conditions and edge cases
- Performance constraints (if applicable)

**Quality test:** Could an agent write acceptance tests from this document alone,
without seeing any implementation?

### 2.4 ROADMAP.md — In What Order

Defines the phased construction plan from v0.1 to v1.0. Each phase has clear
deliverables, success criteria, and dependencies on prior phases.

**Must contain:**

- Ordered phases with descriptive names
- Deliverables per phase
- Success criteria per phase (how you know it is done)
- Dependencies between phases

**Quality test:** Could a human create one GitHub Issue per phase and have each
Issue be independently actionable?

### 2.5 Maintaining the Specification

The specification is a **living document**. As the product evolves, the spec evolves
with it. When a Phase is complete and learnings emerge, the human updates the relevant
spec documents to reflect new understanding.

Agents MUST NOT modify spec documents without explicit human authorization. The
specification represents human intent — agents implement that intent but do not
unilaterally change it.

---

## 3. The GitOps Loop

All work flows through GitHub. This is not optional — it is the coordination
mechanism that makes the entire system work.

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐          │
│  │  Human    │    │  Agent   │    │   CI     │          │
│  │  opens    │───▶│  claims  │───▶│  verifies│          │
│  │  Issue    │    │  Issue   │    │  work    │          │
│  └──────────┘    └──────────┘    └──────────┘          │
│       ▲               │               │                 │
│       │               ▼               ▼                 │
│       │          ┌──────────┐    ┌──────────┐          │
│       │          │  Agent   │    │  Human   │          │
│       │          │  opens   │───▶│  reviews │          │
│       │          │  PR      │    │  outcome │          │
│       │          └──────────┘    └──────────┘          │
│       │                               │                 │
│       │          ┌──────────┐         │                 │
│       │          │ Learnings│◀────────┘                 │
│       └──────────│ codified │                           │
│                  └──────────┘                           │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### 3.1 The Trigger (GitHub Issue)

Every unit of work begins as a GitHub Issue. The human writes the Issue using a
structured template (provided by the repository) that includes:

- **Objective**: What this Issue accomplishes, stated as an outcome
- **Spec Reference**: Which section of which spec document defines this work
- **Acceptance Criteria**: How to verify the work is complete
- **Context**: Any additional information the agent needs beyond the spec

Issues reference the specification — they do not duplicate it. The spec is the
source of truth. The Issue is the *assignment* that points to the relevant part
of the spec and adds any context the agent needs to begin work.

### 3.2 Agent Assignment and Branching

When an agent begins work on an Issue:

1. Create a branch from `main` following the naming convention: `issue-{number}/{short-description}`
2. Read OPENSPEC.md (this document) to understand the methodology
3. Read the referenced spec documents to understand the requirements
4. Read AGENTS.md to understand project-specific conventions
5. Implement the work in the branch

### 3.3 The Verification Loop

Before opening a Pull Request, the agent MUST verify its own work:

1. **Lint**: All code passes the project's linter with zero warnings
2. **Type Check**: All code passes the project's type checker
3. **Unit Tests**: All existing tests pass; new tests cover the new code
4. **Integration Tests**: If applicable, integration tests pass
5. **Acceptance Criteria**: Each criterion from the Issue is demonstrably met

If any verification step fails, the agent fixes the issue and re-verifies. This
loop continues until all checks pass. The agent does not request human review
until the work is self-verified.

### 3.4 The Pull Request

The agent opens a Pull Request that includes:

- **Title**: Clear description of what was implemented
- **Body**: Summary of approach, decisions made, and any deviations from the spec
- **Issue Reference**: Links to the Issue being addressed (`Closes #N`)
- **Verification Evidence**: Confirmation that all verification steps passed

### 3.5 Human Review

The human reviews Pull Requests at the **outcome level**, not the code level:

- Does this accomplish what the Issue specified?
- Does the approach align with the architecture defined in the spec?
- Are there any product-level concerns the agent couldn't evaluate?

The human does NOT need to review for syntax, style, test coverage, or type
correctness — CI has already verified these. The human's review is about *intent*
and *direction*, not *implementation details*.

### 3.6 The Compound Step

After a Pull Request is merged, learnings are captured:

- **What worked well**: Patterns that should be reused
- **What was difficult**: Areas where the spec was ambiguous or the agent struggled
- **What failed initially**: Bugs or issues encountered during implementation
- **What should change**: Suggested improvements to AGENTS.md, the spec, or the
  development process

These learnings are recorded in `docs/learnings/` and, when they represent
universal patterns, codified into AGENTS.md so future agent sessions benefit
from them.

---

## 4. The Bootstrap Protocol

When a new project is created from an Open Specification Template, the following
sequence initializes the repository:

### 4.1 Human Actions (Steps 0-1)

**Step 0: Create Repository.** Use GitHub's "Use this template" to create a new
repository from the Open Specification Template. This provides the complete harness
infrastructure — CI workflows, AGENTS.md defaults, directory structure, verification
scripts, Issue templates, and this document.

**Step 1: Write the Specification.** Author the four spec documents in `spec/`.
This is the creative, strategic work that defines what the product is. The human
may co-author these with an AI assistant (in a chat interface, not in the repo),
but the final documents represent the human's vision and decisions.

### 4.2 Agent Actions (Step 2)

**Step 2: Initialize from Specification.** The human opens the first Issue using
the Bootstrap Issue template. This Issue instructs the agent to:

1. Read all four spec documents
2. Rename the package from the template default to the project name
3. Update `pyproject.toml` with the project's metadata and dependencies
4. Scaffold the directory structure defined in ARCHITECTURE.md
5. Configure environment variables template from SPECIFICATION.md
6. Create the initial Issue set from ROADMAP.md Phase 1
7. Open a Pull Request with all scaffolding changes

The human reviews and merges this PR. The project is now initialized and ready
for Phase 1 development.

### 4.3 Ongoing Development (Steps 3+)

From this point forward, the GitOps Loop (Section 3) governs all work. The human
opens Issues, agents implement them, CI verifies them, and learnings compound.

---

## 5. The Agent's Operating Model

This section is addressed directly to AI coding agents working in this repository.

### 5.1 Before Starting Any Work

1. Read this document (OPENSPEC.md) in its entirety
2. Read AGENTS.md for project-specific conventions
3. Read the spec documents referenced by your assigned Issue
4. Read `docs/learnings/` for relevant prior learnings

### 5.2 Principles of Operation

**Work in small, verifiable increments.** Prefer multiple small commits over one
large commit. Each commit should leave the project in a passing state.

**Verify before requesting review.** Run all verification steps. Do not open a
Pull Request until lint, type checks, and tests all pass. If you cannot make
them pass, explain what is blocking you in the PR description.

**When uncertain, document the uncertainty.** If a spec is ambiguous, do not
guess. Note the ambiguity in your PR description and request human clarification.
Prefer asking over assuming.

**Do not modify files outside your scope.** Your Issue defines what you are
working on. If you discover something elsewhere that needs fixing, open a
separate Issue for it — do not fix it in your current branch.

**Respect the specification hierarchy.** The spec documents define what to build.
AGENTS.md defines how to build it. This document defines the process. If these
conflict, ask the human to resolve the conflict rather than choosing yourself.

### 5.3 The Self-Healing Protocol

When something fails during implementation:

1. **Read the error.** Parse the full error message, traceback, or log output.
2. **Classify the failure.** Is it a syntax error, a logic error, a missing
   dependency, a configuration issue, or an environment problem?
3. **Fix the root cause.** Do not apply workarounds. Understand why the failure
   occurred and address the underlying issue.
4. **Re-verify.** Run the full verification suite after the fix.
5. **Document the failure.** If the failure represents a pattern that could
   recur, note it in your PR description for the compound step.

Maximum retry loops per failure: 5. If you cannot resolve an issue within 5
attempts, stop, describe the problem in your PR or Issue comment, and request
human assistance.

### 5.4 What Agents Must Not Do

- **Do not modify spec documents** without explicit human authorization
- **Do not modify OPENSPEC.md** — this document is maintained by the template
- **Do not merge your own Pull Requests** — humans approve and merge
- **Do not modify CI/CD workflows** without explicit permission
- **Do not introduce dependencies** not referenced in the specification or
  approved by the human
- **Do not work outside your assigned Issue** — scope discipline is critical

---

## 6. The Verification Contract

Every project built from an Open Specification Template includes verification
infrastructure that agents can invoke to check their own work. This is the
mechanism that enables human review at the outcome level rather than the code level.

### 6.1 Standard Verification Steps

The template provides a `Makefile` (or equivalent) with these targets:

| Target | What It Checks |
|--------|---------------|
| `make lint` | Code style and common errors (linter) |
| `make format` | Code formatting (auto-formatter) |
| `make type-check` | Type correctness (type checker) |
| `make test` | All tests pass |
| `make test-cov` | Test coverage meets threshold |
| `make pre-commit` | All pre-commit hooks pass |

An agent MUST run `make pre-commit` (or equivalent) before opening a Pull Request.
This single command invokes all verification steps.

### 6.2 CI/CD as the Final Gate

GitHub Actions runs the same verification steps on every Pull Request. If CI
fails, the agent is expected to read the failure logs, fix the issue, and push
again. The human should never see a PR where CI is red.

### 6.3 Acceptance Criteria Verification

Beyond code quality, each Issue includes acceptance criteria. The agent must verify
these are met — typically by writing tests that encode the criteria, running
the application and checking behavior, or providing evidence in the PR description.

---

## 7. The Compound Learning System

The compound step is what makes this methodology accumulate institutional knowledge
rather than technical debt.

### 7.1 Where Learnings Live

```
docs/
  learnings/                  ← Accumulated institutional knowledge
    by-issue/                 ← Learnings indexed by Issue number
      001-bootstrap.md
      002-phase-1-data-layer.md
    patterns/                 ← Reusable patterns discovered during development
      error-handling.md
      testing-strategies.md
    anti-patterns/            ← Approaches that failed and why
      premature-optimization.md
  decisions/                  ← Architecture Decision Records
    001-chose-x-over-y.md
```

### 7.2 When to Capture Learnings

A learning should be captured when:

- A bug reveals a pattern that could recur
- An implementation approach was tried and failed before finding a better one
- The spec was ambiguous and required human clarification
- A new pattern emerged that should be reused
- A dependency or tool behaved unexpectedly

### 7.3 How Learnings Feed Back

Learnings that represent universal project patterns should be proposed as additions
to AGENTS.md. The agent can suggest these changes in a PR, but the human approves
which learnings become permanent agent instructions.

The goal: an agent starting a fresh session can read AGENTS.md and `docs/learnings/`
and be as effective as an agent that has been working on the project for months.

---

## 8. Issue Templates

The repository includes structured Issue templates that bridge human intent and
agent execution. These templates are designed to be flexible enough for any task
but structured enough that any AI coding agent can parse and act on them.

### 8.1 Bootstrap Issue

Used once when initializing the project from the specification.

```markdown
---
name: Bootstrap from Specification
about: Initialize the project from Open Specification documents
labels: bootstrap, phase-0
---

## Objective

Initialize this repository from the Open Specification documents in `spec/`.

## Instructions

Read OPENSPEC.md Section 4.2 and execute the bootstrap protocol:

1. Read all spec documents in `spec/`
2. Rename the package from the template default to: **[PROJECT_NAME]**
3. Update pyproject.toml with project metadata
4. Scaffold the directory structure from ARCHITECTURE.md
5. Configure environment from SPECIFICATION.md
6. Create Phase 1 Issues from ROADMAP.md
7. Open a Pull Request with all changes

## Acceptance Criteria

- [ ] Package is renamed and importable
- [ ] pyproject.toml reflects the project, not the template
- [ ] Directory structure matches ARCHITECTURE.md
- [ ] All verification steps pass (`make pre-commit`)
- [ ] Phase 1 Issues are created and reference the spec
```

### 8.2 Implementation Issue

Used for feature work, phase milestones, and enhancements.

```markdown
---
name: Implementation
about: Implement a feature, phase, or enhancement defined in the specification
labels: implementation
---

## Objective

<!-- What this Issue accomplishes, stated as an outcome. -->

## Spec Reference

<!-- Which section of which spec document defines this work.
     Example: ROADMAP.md Phase 2, SPECIFICATION.md Section 3.1 -->

## Acceptance Criteria

<!-- How to verify the work is complete. Be specific. Each criterion
     should be independently verifiable. -->

- [ ] Criterion 1
- [ ] Criterion 2
- [ ] All verification steps pass (`make pre-commit`)

## Context

<!-- Any additional information the agent needs beyond the spec.
     Prior learnings, related Issues, constraints, etc. -->
```

### 8.3 Bug Fix Issue

Used when behavior deviates from the specification.

```markdown
---
name: Bug Fix
about: Fix behavior that deviates from the specification
labels: bug
---

## Observed Behavior

<!-- What is happening. -->

## Expected Behavior

<!-- What the spec says should happen. Reference the specific section. -->

## Spec Reference

<!-- Which section of which spec document defines correct behavior. -->

## Reproduction Steps

<!-- How to reproduce the bug. Be specific enough for an agent to follow. -->

## Acceptance Criteria

- [ ] Observed behavior matches expected behavior
- [ ] Regression test prevents recurrence
- [ ] All verification steps pass (`make pre-commit`)
```

### 8.4 Compound Learning Issue

Used to codify learnings from completed work back into the system.

```markdown
---
name: Compound Learning
about: Codify learnings from recent work into the knowledge base
labels: compound
---

## Source

<!-- Which Issue or PR generated these learnings. -->

## Learnings

<!-- What was learned. Include patterns, anti-patterns, and insights. -->

## Proposed Changes

<!-- What should be updated based on these learnings.
     Examples: AGENTS.md additions, new docs/learnings/ entries,
     new docs/decisions/ records. -->

## Acceptance Criteria

- [ ] Learnings are documented in docs/learnings/
- [ ] AGENTS.md is updated if applicable
- [ ] All verification steps pass (`make pre-commit`)
```

---

## 9. Compatibility

### 9.1 AI Coding Agent Compatibility

This methodology is designed to work with any AI coding agent that can:

- Read files in a repository
- Write and modify files
- Execute shell commands
- Create git branches
- Open Pull Requests

This includes, but is not limited to: Claude Code, GitHub Copilot coding agent,
OpenAI Codex, Cursor, Windsurf, Gemini CLI, and any future agent that meets
these baseline capabilities.

The repository uses AGENTS.md (the open standard for agent instructions) as the
project-specific instruction file. Agents that support other instruction file
formats (CLAUDE.md, .cursorrules, etc.) should treat AGENTS.md as the canonical
source and may symlink their format-specific files to it.

### 9.2 Open Specification Ecosystem Compatibility

This document is part of the Open Specification ecosystem:

- **Open Specification**: The concept of distributing software as buildable
  knowledge through natural language documents
- **Open Specification Template**: A repository template that provides the
  harness infrastructure for building from an Open Specification (this project)
- **OPENSPEC.md**: The runtime methodology document (this document)

Projects using this methodology may also integrate with:

- **GitHub Spec Kit**: Compatible — the `.specify/` directory does not conflict
  with the `spec/` directory used here
- **Compound Engineering Plugin**: Compatible — the plugin's workflow aligns
  with the GitOps Loop defined in Section 3
- **GitHub Agentic Workflows**: Compatible — workflows defined in markdown
  can trigger agents within this methodology

Integration with these tools is optional. The methodology is self-contained.

### 9.3 Language and Framework Independence

OPENSPEC.md is language-agnostic. The spec documents (PRODUCT.md, ARCHITECTURE.md,
SPECIFICATION.md, ROADMAP.md) are language-agnostic. Only the template
infrastructure — CI workflows, linter configuration, package management, test
framework — is language-specific.

The same Open Specification can be implemented using different language-specific
templates:

- `openspec-template-python` — Python projects (uv, ruff, mypy, pytest)
- `openspec-template-typescript` — TypeScript projects (future)
- `openspec-template-go` — Go projects (future)

---

## 10. Versioning and Evolution

### 10.1 OPENSPEC.md Versioning

This document follows semantic versioning:

- **Major**: Breaking changes to the methodology (new required steps, changed
  document structure)
- **Minor**: New optional capabilities, expanded guidance, new Issue templates
- **Patch**: Clarifications, typo fixes, minor improvements

### 10.2 Template Versioning

The Open Specification Template is versioned independently. Template updates may
include new CI workflows, improved AGENTS.md defaults, new verification scripts,
or updated OPENSPEC.md versions.

### 10.3 Upgrading

Projects created from the template are independent repositories. They are not
locked to a template version. The human may selectively adopt improvements from
newer template versions by comparing and merging relevant changes.

---

## Appendix A: Glossary

| Term | Definition |
|------|-----------|
| **Open Specification** | A method of defining software through natural language documents |
| **Spec Documents** | The four project-specific documents: PRODUCT.md, ARCHITECTURE.md, SPECIFICATION.md, ROADMAP.md |
| **OPENSPEC.md** | This document — the universal runtime methodology |
| **Template** | The repository scaffold that provides harness infrastructure |
| **Harness** | The complete infrastructure of constraints, verification, and feedback loops that enables agent autonomy |
| **GitOps Loop** | The cycle: Issue → Branch → Implement → Verify → PR → Review → Merge → Compound |
| **Bootstrap** | The one-time initialization of a project from its specification |
| **Compound Step** | Capturing learnings from completed work back into the system |
| **Verification Contract** | The set of automated checks that must pass before human review |
| **Acceptance Criteria** | Specific, verifiable conditions that define when an Issue is complete |

## Appendix B: Quick Reference for Humans

**Your workflow:**

1. Write the spec in `spec/`
2. Open the Bootstrap Issue
3. Review and merge the bootstrap PR
4. Open Issues for each piece of work
5. Review PRs at the outcome level
6. Update the spec as the product evolves

**You never need to:**

- Read or write code directly
- Set up a development environment
- Run tests or linters manually
- Debug implementation details

**You always need to:**

- Define what success looks like (spec + acceptance criteria)
- Decide if the result matches your intent (PR review)
- Evolve the vision as you learn (spec updates)

## Appendix C: Quick Reference for Agents

**Your workflow:**

1. Read OPENSPEC.md, AGENTS.md, and the relevant spec documents
2. Read the assigned Issue and its acceptance criteria
3. Create a branch: `issue-{number}/{short-description}`
4. Implement the work in small, verifiable commits
5. Run `make pre-commit` — fix any failures
6. Open a Pull Request with verification evidence
7. Respond to human feedback if requested
8. After merge, capture learnings if applicable

**You never need to:**

- Guess at requirements — the spec defines them
- Skip verification — always run the full suite
- Work outside your assigned Issue scope
- Modify spec documents without authorization

**You always need to:**

- Read the spec before writing code
- Verify your work before requesting review
- Document decisions and learnings
- Ask when the spec is ambiguous

---

*OPENSPEC.md is maintained as part of the Open Specification Template project.*
*For contributions, see the template repository.*
*Licensed under CC BY 4.0.*
