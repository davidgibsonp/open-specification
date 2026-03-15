# Open Specification

**A standard for defining software in written language.**

> "The entire history of software development has been a pursuit of abstraction — each
> major innovation a step away from the machine's native language and closer to human
> intent. Open Specification places written language at the top of this stack."

---

## The Idea

Traditional open source distributes code. Open Specification distributes **buildable knowledge**.

Instead of sharing a working application, you share the complete blueprint — the product
vision, the architecture, the functional requirements, and the phased roadmap — that
enables anyone (or any AI coding agent) to build their own implementation.

The specification is the product. The code is a downstream artifact.

This idea has always been aspirational. What makes it practical now is that large language
models can read natural language specifications and translate them directly into working
software. Written English (or any human language) is now a legitimate programming
abstraction — one that sits above compilers and runtimes, not instead of them.

## How It Works

An Open Specification project defines software through four documents:

| Document | Purpose | Question It Answers |
|----------|---------|-------------------|
| **PRODUCT.md** | Vision, users, success criteria | What are we building and why? |
| **ARCHITECTURE.md** | Components, relationships, design decisions | How is it structured? |
| **SPECIFICATION.md** | Functional requirements, interfaces, edge cases | What must it do? |
| **ROADMAP.md** | Phased milestones from v0.1 to v1.0 | In what order? |

These documents are technology-agnostic. They specify **outcomes and constraints**, not
implementation steps. The same specification can be built in Python, TypeScript, Go, or
any other language — the documents don't change, only the implementation does.

## The Ecosystem

Open Specification is a standard, not a tool. The ecosystem includes:

### This Repository — `open-specification`

The canonical home for the standard itself. Contains:

- **[OPENSPEC.md](OPENSPEC.md)** — The runtime methodology that defines how to build
  software from an Open Specification. This is the operating protocol: how specs become
  Issues, how Issues become code, how learnings compound back into the system.
- **[Writing Guide](docs/writing-guide.md)** — How to write effective specifications
- **[Issue Templates](.github/ISSUE_TEMPLATE/)** — Structured templates that bridge
  human intent and agent execution
- **[Examples](examples/)** — Well-written specifications you can reference

### Templates — `openspec-template-{language}`

GitHub Template Repositories that provide the harness infrastructure for building from
a specification. Each template includes a copy of OPENSPEC.md, language-specific CI/CD,
testing, linting, and verification tooling, plus the Issue templates from this repo.

| Template | Language | Status |
|----------|----------|--------|
| [open-specification-python](https://github.com/davidgibsonp/open-specification-python) | Python | In Development |

Templates are where the work happens. You create a new repository from a template, write
your specification in the `spec/` directory, and start delegating work through GitHub Issues.

## The Runtime — OPENSPEC.md

**[Read the full runtime →](OPENSPEC.md)**

OPENSPEC.md is the operating protocol for Open Specification projects. It defines:

- **The GitOps Loop**: How specifications flow through Issues → Branches → Pull Requests →
  CI Verification → Human Review → Compound Learning
- **The Bootstrap Protocol**: How a new project initializes from its specification
- **The Agent Operating Model**: How AI coding agents work within the system — what they
  can do, what they must not do, and how they verify their own work
- **The Verification Contract**: The automated checks that must pass before a human
  sees a Pull Request
- **The Compound Learning System**: How institutional knowledge accumulates rather than
  technical debt

OPENSPEC.md ships with every template. It is universal — the same methodology regardless
of language, framework, or which AI coding agent does the work.

## Who This Is For

**Product thinkers who want to build software without writing code.** You define the
product. AI agents implement it. You review outcomes, not syntax.

**Developers who want to operate at a higher abstraction.** You write specifications
and open Issues instead of writing code directly. You review Pull Requests at the
product level — does this match what I intended? — not the implementation level.

**Teams exploring AI-native development.** Open Specification provides the structure
that turns ad-hoc AI coding into a repeatable, compounding process.

**Educators teaching software architecture.** The specification format forces students
to think about product design, system architecture, and phased delivery — skills that
matter more than syntax in an AI-augmented world.

## Core Principles

### Specify Outcomes, Not Implementation

A good specification says "Users must be able to search by keyword and receive results
ranked by relevance within 200ms." It does not say "Use Elasticsearch with a BM25
scoring function." The *what* and *why* are specified. The *how* is left to the builder.

### The Repository Is the Source of Truth

From an agent's perspective, anything not in the repository does not exist. Every
decision, constraint, pattern, and lesson is captured in the repo. Knowledge in chat
threads, meeting notes, or someone's head is invisible to the system.

### Compound, Don't Accumulate

Each unit of work should make the next unit easier. Bugs become documented patterns.
Architectural decisions become recorded precedents. Failed approaches become guardrails.
This knowledge lives in the repository and is available to every future session.

### Humans Steer, Agents Execute

The human's role is strategic: deciding what to build, defining success criteria, and
verifying outcomes match intent. The agent's role is tactical: reading specifications,
implementing solutions, verifying correctness, and capturing learnings.

## Writing Effective Specifications

The core principle: **specify outcomes and constraints, not implementation steps.**

### Quality Checklist

A complete specification passes these tests:

- **Immediate Start Test**: Can a builder begin working within 30 minutes of reading?
- **Multiple Paths Test**: Are there 2+ valid ways to implement each major component?
- **Equivalence Test**: Would different implementations be functionally compatible?
- **Decision Clarity Test**: Are architectural tradeoffs explained, not just stated?
- **Milestone Test**: Is v0.1 achievable in a focused session?
- **Agent Test**: Could an AI coding agent write acceptance tests from the specification
  alone, without seeing any implementation?

### Common Anti-Patterns

**Too prescriptive** — "Use React with Redux. Create a /components folder with
Header.tsx and Footer.tsx." Instead: "UI should update reactively when state changes.
State management should be predictable and debuggable."

**Too vague** — "Build a good user authentication system." Instead: "Users register
with email and password. Sessions persist for 30 days. Passwords require 8+ characters
with one number and one special character. Password reset via email."

**Implementation in disguise** — "Roadmap v0.1: Set up Express.js server, create
MongoDB schemas." Instead: "Roadmap v0.1: Single user can create, read, update, and
delete items. Data persists between sessions."

### What to Specify vs. What to Leave Open

| Specify This | Leave This Open |
|-------------|----------------|
| API contracts (inputs/outputs) | Programming language |
| Data relationships | Database choice |
| Performance targets | Algorithm details |
| Error conditions | UI framework |
| Security requirements | Folder structure |
| Feature behavior | Variable names |
| Success criteria | Library choices |

For comprehensive guidance, see the [Writing Guide](docs/writing-guide.md).

## Getting Started

### Starting a New Project

1. **Choose a template**: Create a new repository from
   [open-specification-python](https://github.com/davidgibsonp/open-specification-python)
   (or your language of choice)
2. **Rename your project** — run `bash scripts/rename_project.sh your_project_name` to
   replace placeholder naming with your project name
3. **Write your specification**: Fill in the four documents in `spec/` — start with
   PRODUCT.md, then ROADMAP.md, then ARCHITECTURE.md, then SPECIFICATION.md
4. **Open the Bootstrap Issue**: Use the Bootstrap issue template to initialize the
   project from your specification
5. **Review and merge**: An agent scaffolds the project; you review the result
6. **Delegate through Issues**: Open Issues for each phase or feature, agents implement
   them, CI verifies them, you review outcomes

### Creating a Standalone Specification

If you want to distribute a specification without an implementation template:

1. Create a repository with the four spec documents + README.md + LICENSE
2. Follow the writing guide for quality and completeness
3. License under CC BY 4.0 (or CC BY-SA 4.0 if you want modifications shared alike)
4. Builders choose their own language, tools, and implementation approach

## Contributing

Open Specification is an evolving standard. Contributions are welcome in these areas:

- **OPENSPEC.md improvements**: Clarifications, new patterns, better guidance
- **Issue template refinements**: Making templates more effective for human-agent
  collaboration
- **Writing guide expansions**: More examples, more anti-patterns, domain-specific advice
- **New language templates**: Building `openspec-template-{language}` for other ecosystems
- **Example specifications**: Well-written specs that others can learn from

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Versioning

OPENSPEC.md follows semantic versioning:

- **Major**: Breaking changes to the methodology
- **Minor**: New capabilities, expanded guidance
- **Patch**: Clarifications and minor improvements

Current version: **0.1.0** (Draft)

## License

The Open Specification standard, including OPENSPEC.md, writing guides, issue templates,
and all documentation in this repository, is licensed under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE).

You are free to use, adapt, and build upon this standard for any purpose, including
commercial use, as long as you provide attribution.

Implementations built from Open Specifications are not derivative works of the
specification. You own your implementation fully and may license it however you choose.

---

**Ready to build?** Start with a [template](https://github.com/davidgibsonp/open-specification-python),
write your specification, and let the agents handle the rest.
