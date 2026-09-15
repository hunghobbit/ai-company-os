---
name: test-design
description: "Design validation checklists, test scenarios, acceptance criteria mappings, runtime validation plans, and validation handoff packages."
---

# Test Design

## Purpose

This skill defines the shared, multi-agent process for designing validation that checks implementation against requirements, architecture, and runtime behavior.

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

- replace runtime validation rules defined elsewhere
- create product code
- redesign the 8-role workflow
- create autonomous agent logic
- modify the handoff protocol

## Role Use

Primary users:

- QA
- Tester
- Developer

## Inputs

- requirements artifacts
- architecture design
- implementation state
- current validation rules from governance

## Outputs

- validation checklist
- test scenarios
- acceptance criteria mapping
- runtime validation plan
- handoff package for QA or Tester

## Required Process

1. Map requirements to verification checks.
2. Define what must be validated.
3. Document expected behavior and failure signals.
4. Identify runtime and integration scenarios.
5. Prepare the validation package for handoff.

## Validation

Before the validation design is accepted:

- test cases trace back to explicit requirements or architecture decisions
- failure indicators are reproducible
- runtime validation scope matches the approved phase

## Handoff

Validation outputs are passed using the Phase 1 handoff protocol. No automatic continuation is allowed.

## Forbidden Actions

- writing production code
- approving release without evidence
- inventing validation steps not supported by the project’s current rules
- bypassing the review workflow

## Deferred Questions

The skill leaves unresolved issues such as concurrency, simultaneous outputs, and detailed rejection flows as deferred governance questions rather than creating new operational rules.
