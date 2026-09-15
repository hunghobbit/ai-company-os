---
name: architecture-design
description: "Define technical architecture, interfaces, data models, dependencies, risks, and implementation boundaries after requirements are approved."
---

# Architecture Design

## Purpose

This skill defines the shared, multi-agent process for creating a technical architecture that satisfies approved requirements without implementing product code.

## Governing Authority

This skill is subordinate to the existing project governance hierarchy:

1. USER directive
2. AGENTS.md
3. .clinerules/
4. FOUNDATION.md
5. PROGRESS.md
6. docs/IMPLEMENTATION_LOG.md
7. docs/AI_COMPANY_OS_DESIGN_FREEZE.md
8. .github/skills/handoff-protocol/SKILL.md

It must not override governance.

## Scope

This skill applies to Phase 3 multi-agent skill creation only.

It must not:

- write production code
- change the frozen 8-role workflow
- redefine governance precedence
- create runtime orchestration or autonomous chaining
- change the Phase 1 handoff protocol

## Role Use

Primary users:

- Architect
- PM
- BA

## Inputs

- approved requirements
- PM phase/scope classification
- existing system context and constraints
- requirement artifacts and open questions

## Outputs

- architecture design
- interface contracts
- data model definitions
- implementation boundaries
- handoff package for Developer

## Required Process

1. Confirm the requirement set is approved.
2. Document the architecture intent.
3. Define interfaces, dependencies, and component boundaries.
4. Identify technical risks and open design questions.
5. Specify implementation boundaries for the current phase.
6. Prepare a handoff to Developer with the design package.

## Validation

Before the design is accepted:

- it is implementable within the approved phase
- interfaces are unambiguous
- dependencies are explicit
- the scope matches the frozen architecture and project governance

## Handoff

The Architecture Design output is transferred to Developer via the Phase 1 handoff protocol. This is a user-mediated review step, not autonomous execution.

## Forbidden Actions

- writing production code
- approving implementation quality without review
- unilaterally changing requirements
- inventing runtime behaviors not covered by the design freeze

## Deferred Questions

This skill preserves unresolved items such as parallel handoff handling, model guidance, and conflict resolution without converting them into new architecture decisions.
