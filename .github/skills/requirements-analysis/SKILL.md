---
name: requirements-analysis
description: "Translate stakeholder intent into testable requirements, scope boundaries, open questions, acceptance criteria, and a handoff package."
---

# Requirements Analysis

## Purpose

This skill defines the shared, multi-agent process for translating stakeholder intent into testable requirements and scope boundaries.

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

It must not override governance. It adds procedural guidance for the BA and related roles.

## Scope

This skill applies to Phase 3 multi-agent skill creation only.

It must not:

- design architecture beyond the requirement boundary
- write production code
- create product features
- redefine governance hierarchy
- replace the Phase 1 handoff protocol
- create autonomous execution logic

## Role Use

Primary users:

- BA
- Architect
- PM

## Inputs

- USER request
- project context from FOUNDATION.md
- PM scope classification
- prior handoff artifacts
- existing docs and constraints

## Outputs

- structured requirements
- scope boundaries
- open questions
- acceptance criteria
- handoff package for Architect

## Required Process

1. Clarify the user goal.
2. Document the problem statement.
3. Identify what is in scope and out of scope.
4. Write testable acceptance criteria.
5. Record ambiguities and unresolved decisions.
6. Prepare a handoff to the receiving role.

## Validation

Before the output is considered ready:

- requirements are specific and testable
- ambiguities are explicit
- scope is clearly classified
- acceptance criteria are reviewable by USER and Architect

## Handoff

Requirements output is transferred to the next role by the Phase 1 handoff protocol. The handoff must include the requirement summary, scope boundaries, open questions, and acceptance criteria.

## Forbidden Actions

- designing implementation architecture
- writing product code
- approving scope unilaterally
- inventing new governance rules
- bypassing the handoff protocol

## Deferred Questions

This skill must preserve any design-freeze open questions, including parallel handoff handling, conflict resolution, and suggestedModel guidance, without converting them into new architecture.
