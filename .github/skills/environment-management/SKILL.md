---
name: environment-management
description: "Configure and validate development or runtime environments, resolve toolchain issues, document reproducible changes, and report environment blockers."
---

# Environment Management

## Purpose

This skill defines the shared, multi-agent process for configuring and validating the development or runtime environment required by the project.

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

- write product code
- change project scope
- duplicate governance responsibilities
- create autonomous environment repair loops
- replace the handoff protocol

## Role Use

Primary users:

- IT
- Developer
- PM

## Inputs

- environment request
- current system state
- current project phase and constraints
- relevant tooling and dependency requirements

## Outputs

- environment status report
- environment configuration changes
- documented setup state
- return handoff to the requesting role

## Required Process

1. Confirm the environment requirements.
2. Validate the current toolchain and runtime state.
3. Apply only the necessary environment changes.
4. Document the state and constraints.
5. Return a handoff to the requesting role or escalate through PM when required.

## Validation

Before closure, the environment must be confirmed to be:

- reproducible
- documented
- aligned with the current phase and task requirements

## Handoff

Environment outcomes are transferred using the Phase 1 handoff protocol. Any unresolved blocker must be escalated through PM and then USER.

## Forbidden Actions

- writing product code
- changing scope without authority
- bypassing the review and escalation flow
- claiming technical enforcement for rules that are only guidance

## Deferred Questions

This skill preserves unresolved environment and escalation questions without inventing extra implementation architecture.
