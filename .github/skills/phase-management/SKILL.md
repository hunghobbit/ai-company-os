---
name: phase-management
description: "Classify work against project phases, scope boundaries, governance, blockers, and user-mediated handoff routing without creating autonomous execution."
---

# Phase Management

## Purpose

This skill defines the shared, multi-agent process for phase classification, sequencing, and escalation within the project workflow.

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

- change the frozen design workflow
- create autonomous task execution
- invent new governance precedence
- bypass the handoff protocol
- create non-phase multi-agent behavior

## Role Use

Primary users:

- PM
- BA
- Architect
- Developer

## Inputs

- current phase state
- governance documentation
- backlog and request context
- active handoff artifacts

## Outputs

- phase/scope classification
- handoff routing decisions
- blocker reports
- escalation record

## Required Process

1. Classify the request as IN-PHASE, OUT-OF-PHASE, or NEEDS-ROADMAP-UPDATE.
2. Confirm alignment with AGENTS.md and the frozen design baseline.
3. Identify blockers and unresolved items.
4. Route the work to the correct role using the user-mediated handoff protocol.
5. Escalate only when governance or phase conflict requires USER intervention.

## Validation

Before the phase decision is accepted:

- classification is grounded in current governance
- phase conflicts are reported rather than silently overridden
- the next action is explicit and user-mediated

## Handoff

Phase decisions are tracked through the repository handoff protocol. They do not create autonomous execution or model routing.

## Forbidden Actions

- unilaterally changing the roadmap
- bypassing PM governance checks
- moving work into future phases without approval
- creating hidden continuation or autonomous task loops

## Deferred Questions

This skill preserves unresolved items such as parallel handoffs, simultaneous conflict handling, and detailed escalation procedure without inventing new architecture.
