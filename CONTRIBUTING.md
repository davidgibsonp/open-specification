# Contributing to Open Specification

Open Specification is an evolving standard. Contributions that improve the methodology,
clarify guidance, add examples, or expand the ecosystem are welcome.

## What Lives Here

This repository contains the **standard itself** — not code. Everything here is
documentation: the runtime methodology (OPENSPEC.md), the writing guide, issue
templates, and examples. Changes to this repo change how every project in the
ecosystem operates.

That means contributions should be deliberate. A typo fix is easy to merge. A change
to the GitOps Loop in OPENSPEC.md affects every project that references the runtime.
The bar for changes scales with their blast radius.

## How to Contribute

### Reporting Issues

If something in the standard is unclear, contradictory, or missing, open an Issue.
Describe what you expected to find, what you actually found (or didn't), and how it
affected your work. Concrete examples from real projects are more useful than abstract
suggestions.

### Proposing Changes

For changes to OPENSPEC.md, issue templates, or the writing guide:

1. **Open an Issue first.** Describe what you want to change and why. For significant
   changes, wait for discussion before writing a PR. For small clarifications, an
   Issue and PR can come together.

2. **Fork and branch.** Create a branch with a descriptive name. Make your changes.

3. **Open a Pull Request.** Reference the Issue. Explain the change and its rationale.
   For OPENSPEC.md changes, note which section is affected and whether this is a
   patch (clarification), minor (new capability), or major (breaking) change.

### Adding Examples

Example specifications in `examples/` are one of the best ways to contribute. A good
example:

- Covers a domain that isn't already represented
- Demonstrates spec-writing principles from the writing guide
- Passes the quality checklist (Immediate Start, Multiple Paths, Equivalence,
  Decision Clarity, Milestone tests)
- Includes all four documents (PRODUCT.md, ARCHITECTURE.md, SPECIFICATION.md, ROADMAP.md)

To add an example, create a subdirectory under `examples/` with a descriptive name
and include the four spec documents plus a brief README explaining why this is a
good example.

### Building Language Templates

New templates (`openspec-template-{language}`) are separate repositories, not part of
this one. If you're building a template for a new language:

- Include a copy of OPENSPEC.md pinned to a specific version
- Include the issue templates from this repo's `.github/ISSUE_TEMPLATE/`
- Follow the conventions described in OPENSPEC.md for directory structure, verification,
  and the bootstrap protocol
- Open an Issue here to get listed in the README's ecosystem table

## Writing Conventions

This is a documentation project. Quality of writing matters.

**Be concrete.** "Agents should verify their work" is vague. "Agents must run
`make pre-commit` before opening a Pull Request" is actionable.

**Prefer examples over explanation.** Show what a good spec looks like rather than
describing the properties of a good spec in the abstract.

**Keep it short.** Every sentence in OPENSPEC.md competes for attention with the
agent's actual task. If a sentence doesn't change behavior, it doesn't belong.

**Use present tense and active voice.** "The agent creates a branch" not "a branch
should be created by the agent."

**Specify, don't prescribe.** The standard defines outcomes and constraints, not
implementation steps. This principle applies to the standard itself — tell people
what good looks like, not exactly how to get there.

## Versioning

OPENSPEC.md follows semantic versioning:

- **Patch** (0.1.0 → 0.1.1): Typo fixes, clarifications that don't change meaning,
  improved examples
- **Minor** (0.1.0 → 0.2.0): New optional sections, additional issue templates,
  expanded guidance that doesn't break existing workflows
- **Major** (0.x → 1.0): Changes to required steps, renamed sections, altered
  document structure, anything that would require existing projects to update their
  workflow

CHANGELOG.md is updated with every release. Contributors should include a changelog
entry in their PR.

## Review Process

- **Typo and clarity fixes**: Reviewed and merged by a maintainer
- **Writing guide and examples**: Reviewed for quality and accuracy
- **Issue template changes**: Tested with at least one real project before merging
- **OPENSPEC.md changes**: Discussed in an Issue first, reviewed carefully for
  downstream impact, may require testing with an active template project

## Code of Conduct

Be respectful, be constructive, be specific. This is a project about clear
communication — model that in how you participate.

---

*Questions? Open a [Discussion](https://github.com/davidgibsonp/open-specification/discussions).*
