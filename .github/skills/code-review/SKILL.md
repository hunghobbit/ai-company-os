---
name: code-review
description: "Review implementation changes for correctness, security, architecture alignment, conventions, scope, and explicit approval or rework decisions."
---

# Code Review

## Purpose

This skill defines the shared, multi-agent process for reviewing implementation quality, scope alignment, and architecture correctness before approval.

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

- modify production code
- replace governance review and approval
- create product features
- bypass the Phase 1 handoff protocol
- invent new workflow steps beyond the frozen architecture

## Role Use

Primary users:

- Code Reviewer
- PM
- Developer

## Inputs

- actual code diff
- architecture design
- requirements and acceptance criteria
- test results and runtime findings

## Outputs

- review report
- approval or requested-changes decision
- rework handoff to Developer
- PM approval handoff if valid

## Required Process

1. Review the actual diff rather than assumptions.
2. Evaluate correctness, architecture fit, and scope.
3. Check security, consistency, and coding conventions.
4. Document required changes or approval rationale.
5. Handoff results through the repository protocol.

## Validation

Before a review conclusion is accepted:

- the diff has been reviewed in full
- scope is validated against approved phase boundaries
- reasons for approval or rejection are explicit and reproducible

## Handoff

Review outcomes are transferred through the Phase 1 handoff protocol. The flow remains user-mediated and explicit.

## Forbidden Actions

- modifying production code as part of review
- approving without reviewing the actual diff
- unilaterally merging or releasing
- bypassing the handoff protocol

## Deferred Questions

This skill preserves unresolved review flow questions, including parallel reviews and conflict handling, without inventing a new architecture.
