# Changelog

All notable changes to the Open Specification standard are documented here.

This changelog tracks changes to OPENSPEC.md (the runtime), the issue templates,
the writing guide, and any other standard artifacts. It does not track changes to
individual specifications or template repositories.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
OPENSPEC.md follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [0.1.0] - 2026-03-14

### Added

- OPENSPEC.md v0.1.0 — initial draft of the runtime methodology
  - Philosophy: written language as highest abstraction, humans steer / agents execute,
    compound engineering, repository as single source of truth
  - GitOps Loop: Issue → Branch → Verify → PR → Review → Compound
  - Bootstrap Protocol: initializing a project from its specification
  - Agent Operating Model: principles, self-healing protocol, constraints
  - Verification Contract: standard checks agents must pass before requesting review
  - Compound Learning System: capturing and codifying institutional knowledge
  - Compatibility: agent-agnostic, ecosystem-compatible, language-independent
- Machine-parseable version marker: `<!-- openspec-version: 0.1.0 -->` on line 1
  - Enables automated version detection by downstream GitHub Actions
  - Documents automated and manual upgrade paths in Section 10.3
- GitHub Release workflow (`.github/workflows/release.yml`)
  - Triggers on `v*` tags
  - Verifies version consistency between tag, comment, and header
  - Creates GitHub Release with changelog content
- GitHub Issue Templates
  - Bootstrap: one-time project initialization from specification
  - Implementation: feature work, phase milestones, enhancements
  - Bug Fix: behavior deviating from specification
  - Compound Learning: codifying learnings back into the knowledge base
- README.md — orientation to the standard and ecosystem
- LICENSE — CC BY 4.0
