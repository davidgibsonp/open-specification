# Writing Guide

*How to write effective Open Specifications.*

> **Status**: This guide is under development. The essentials are covered in the
> [README](../README.md#writing-effective-specifications). This document will expand
> with more examples, domain-specific advice, and lessons learned from real projects.

---

## The Core Principle

**Specify outcomes and constraints, not implementation steps.**

Your job is to define what success looks like and what boundaries exist, then trust
the builder — human or agent — to find their own path.

## Document-by-Document Guidance

### PRODUCT.md — Start Here

This is the most important document. If you can only write one, write this one.

**What it answers:** What problem are we solving? For whom? Why does it matter?
What defines success?

**How to write it:**

1. Start with the problem, not the solution. Describe the pain point or opportunity
   in concrete terms.
2. Define your users. Who are they? What do they need? What do they currently do
   instead?
3. Write success criteria that are measurable. "Users can do X" is better than
   "the system supports X." "Response time under 200ms" is better than "fast."
4. Define what this is NOT. Explicit scope boundaries prevent scope creep and
   help agents stay focused.

**Quality test:** Could someone unfamiliar with your project explain to a colleague
what the product does and why it exists, after reading only this document?

### ROADMAP.md — Write This Second

Break the journey from nothing to v1.0 into phases. Each phase should be
independently valuable — if you stopped after Phase 2, you'd still have something
useful.

**How to write it:**

1. Phase 1 should be the smallest possible thing that works. Not a skeleton —
   something a user could actually use, even if limited.
2. Each phase builds on the previous one. Don't plan phases that require
   rearchitecting what came before.
3. Success criteria per phase should be verifiable. "Can create and retrieve 10
   items" is verifiable. "Basic CRUD works" is not.
4. Keep it to 3-5 phases. More than that and you're over-planning.

**Quality test:** Could a human create one GitHub Issue per phase, and have each
Issue be independently actionable?

### ARCHITECTURE.md — Write This Third

Define the pieces and how they connect. This is where you make the structural
decisions that shape everything downstream.

**How to write it:**

1. List every component with its single responsibility.
2. Define how components communicate (APIs, events, shared state, etc.).
3. For each significant decision, explain the tradeoff. "We chose X over Y
   because Z" is more valuable than "We use X."
4. Identify what's fixed vs. what could change. Fixed constraints are guardrails.
   Flexible decisions are opportunities.

**Quality test:** Could an agent scaffold the project's directory structure and
understand where new code belongs, after reading only this document?

### SPECIFICATION.md — Write This Last

The detailed functional requirements. This is the most technical document but
it should still describe *behavior*, not *implementation*.

**How to write it:**

1. For each component from ARCHITECTURE.md, define what it must do.
2. Specify inputs, outputs, and error conditions for each interface.
3. Include edge cases — what happens with empty input? Invalid data? Concurrent
   access? Network failure?
4. Define performance constraints where they matter.

**Quality test:** Could an agent write acceptance tests from this document alone,
without seeing any implementation?

## Common Mistakes

**Writing the spec after the code.** The spec should drive the code, not
document it. If you write the code first, you'll unconsciously constrain the
spec to match your implementation choices.

**Confusing detail with quality.** A 50-page spec is not better than a 10-page
spec. The best spec is the shortest document that passes all the quality tests.

**Specifying technology choices.** "Use PostgreSQL" belongs in AGENTS.md (project
conventions), not in the specification. The spec says "data must persist across
restarts and support concurrent access." The implementation decides how.

**Forgetting to update the spec.** The spec is a living document. When requirements
change, update the spec first, then open Issues that reference the updated sections.
Stale specs are worse than no specs — they actively mislead agents.

---

*This guide will grow with examples and lessons learned from real projects.*
