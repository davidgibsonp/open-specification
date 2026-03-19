# Ecosystem Roadmap

This document outlines the strategy for evolving the Open Specification ecosystem
from a single repository into a maintainable template system.

---

## Current State (Phase 1)

The Open Specification ecosystem consists of:

- **open-specification** — The runtime specification (OPENSPEC.md), issue templates,
  and supporting documentation
- **open-specification-python** — The first language-specific template, demonstrating
  Python project conventions

End users create new projects using GitHub's "Use this template" feature, which
creates an independent copy of the template repository.

---

## Phase 2: Copier-Based Template Extraction

**Trigger:** When a second language template (e.g., TypeScript, Go) is created.

**Goal:** Extract shared components into a base template that language-specific
templates can extend.

### Rationale

Creating a base template before multiple language templates exist would be
premature abstraction. The patterns that should be shared vs. language-specific
are only clear after implementing multiple templates.

### Planned Architecture

```
open-specification-template (base)
├── OPENSPEC.md
├── .github/ISSUE_TEMPLATE/
├── docs/learnings/
└── spec/
    ├── PRODUCT.md
    ├── ARCHITECTURE.md
    ├── SPECIFICATION.md
    └── ROADMAP.md

open-specification-python (extends base)
├── copier.yml (inherits from base)
├── AGENTS.md (Python conventions)
├── pyproject.toml
├── src/
└── tests/

open-specification-typescript (extends base)
├── copier.yml (inherits from base)
├── AGENTS.md (TypeScript conventions)
├── package.json
├── src/
└── tests/
```

### Copier Features to Leverage

- **Template inheritance:** Language templates extend the base template
- **Template variables:** Project name, author, license, etc.
- **Conditional files:** Include files based on user choices
- **Post-generation tasks:** Initialize git, run formatters, etc.

### Migration Path for Existing Projects

Projects created with "Use this template" before Phase 2 will not be affected.
They can optionally adopt Copier-based updates using `copier update`, but this
is not required.

---

## Phase 3: Community Template Process

**Trigger:** External contributors want to create templates for additional
languages or frameworks.

**Goal:** Establish a process for community-contributed templates that maintain
quality and consistency with the Open Specification methodology.

### Template Certification Requirements

1. **Extends base template:** Must use Copier to inherit from
   open-specification-template
2. **Complete harness:** Must include working CI, linting, testing, and
   verification scripts
3. **Documented AGENTS.md:** Must document language-specific conventions
4. **Bootstrap verified:** Must pass bootstrap with at least one sample
   specification
5. **Maintained:** Must have a designated maintainer who responds to issues

### Contribution Process

1. **Proposal:** Open an issue in open-specification describing the template
2. **Review:** Core team reviews for overlap with existing templates
3. **Development:** Create template in contributor's namespace
4. **Certification:** Core team reviews against certification requirements
5. **Adoption:** Template is linked from main README, optionally transferred
   to organization

### Governance

- Core team maintains the base template and certification requirements
- Language template maintainers have autonomy over language-specific decisions
- Breaking changes to base template require RFC process
- Abandoned templates are marked deprecated, not removed

---

## End User Experience

Throughout all phases, end users have a consistent experience:

1. **Find a template** — Browse templates linked from the main README
2. **Create a project** — Use GitHub "Use this template" or `copier copy`
3. **Write specification** — Fill in spec/ documents
4. **Bootstrap** — Open the Bootstrap issue
5. **Iterate** — Use Implementation and Bug Fix issues

The underlying template infrastructure is invisible to end users who just want
to build software with Open Specification.

---

## Timeline

| Phase | Trigger | Deliverables |
|-------|---------|--------------|
| 1 (Current) | — | Python template, "Use this template" workflow |
| 2 | Second language template | Base template, Copier integration |
| 3 | Community interest | Certification process, contributor guide |

This roadmap will be updated as the ecosystem evolves and we learn from real-world
usage.
