---
name: handoff-protocol
description: "Create, validate, review, and transfer repository-based user-mediated handoff artifacts using the canonical handoff.json contract."
---

# Handoff Protocol

## Purpose

This skill defines the repository-based, user-mediated handoff contract for AI Company OS. It is a procedural guidance artifact only. It does not replace the authoritative project governance files, the frozen design freeze, or the final authority of the USER.

## Governing Authority

This skill must defer to the following in order:

1. USER directive
2. `AGENTS.md` (if present in the workspace)
3. `.clinerules/`
4. `FOUNDATION.md`
5. `PROGRESS.md`
6. `docs/IMPLEMENTATION_LOG.md`
7. `docs/AI_COMPANY_OS_DESIGN_FREEZE.md`

If a governance file is absent from the current workspace, the skill must not invent a replacement authority. It must operate within the available project rules and preserve the frozen baseline.

## Scope Boundary

This skill is limited to the Phase 1 handoff protocol only.

It must not:

- create `.github/agents/*.agent.md` files
- create Phase 2 agent definitions
- create non-handoff Phase 3 skill implementations
- redesign the frozen architecture
- change the 8-role workflow
- change governance precedence
- replace Cline as the primary Developer workflow
- introduce autonomous agent chaining
- introduce automatic model routing
- create background automation
- create hidden continuation logic

## Handoff Contract

The handoff artifact is a repository artifact transferred between roles and reviewed by the receiving role and/or the USER.

Canonical artifact name:

- `handoff.json`

Required structure:

```json
{
  "handoffId": "",
  "sourceRole": "",
  "targetRole": "",
  "status": "PENDING",
  "createdAt": "",
  "context": "",
  "artifacts": [],
  "openQuestions": [],
  "blockers": [],
  "governanceChecks": {
    "phaseAlignment": "",
    "scopeBoundary": ""
  },
  "retryCount": 0,
  "completionCriteria": []
}
```

This schema is the minimum canonical contract required by the frozen design. Additional metadata may only be added when it is clearly required for repository auditability and does not alter the frozen architecture or deferred decisions.

## Canonical `handoff.json` Schema

The canonical repository handoff contract is defined as follows:

```json
{
  "handoffId": "string",
  "sourceRole": "string",
  "targetRole": "string",
  "status": "PENDING | IN_PROGRESS | COMPLETED | BLOCKED | REJECTED | RETRY",
  "createdAt": "ISO-8601 timestamp string",
  "context": "string",
  "artifacts": ["string"],
  "openQuestions": ["string"],
  "blockers": ["string"],
  "governanceChecks": {
    "phaseAlignment": "CONFIRMED | GUIDANCE | OPEN QUESTION",
    "scopeBoundary": "CONFIRMED | GUIDANCE | OPEN QUESTION"
  },
  "retryCount": 0,
  "completionCriteria": ["string"]
}
```

### Required fields and validation

Each handoff artifact MUST contain all required keys listed above. Validation rules:

- `handoffId`: required string; must be unique within the repository scope for the current handoff lifecycle
- `sourceRole`: required string; must identify the emitting role
- `targetRole`: required string; must identify the receiving role
- `status`: required string; must be one of the allowed status values
- `createdAt`: required ISO-8601 timestamp string
- `context`: required string; human-readable operational context for the receiving role
- `artifacts`: required array of strings; may be empty but must exist
- `openQuestions`: required array of strings; may be empty but must exist
- `blockers`: required array of strings; may be empty but must exist
- `governanceChecks`: required object; must contain `phaseAlignment` and `scopeBoundary`
- `retryCount`: required integer; must be >= 0 and <= 3 for normal operation
- `completionCriteria`: required array of strings; may be empty but must exist

### Allowed status values

The allowed status values are exactly:

- `PENDING`
- `IN_PROGRESS`
- `COMPLETED`
- `BLOCKED`
- `REJECTED`
- `RETRY`

Any other value is invalid for the canonical contract.

### Allowed status transitions

The canonical status transitions are:

```text
PENDING → IN_PROGRESS
PENDING → REJECTED
PENDING → COMPLETED

IN_PROGRESS → COMPLETED
IN_PROGRESS → BLOCKED
IN_PROGRESS → REJECTED

BLOCKED → RETRY
BLOCKED → IN_PROGRESS
BLOCKED → REJECTED

REJECTED → RETRY
REJECTED → IN_PROGRESS

RETRY → IN_PROGRESS
RETRY → REJECTED
RETRY → BLOCKED

COMPLETED → (terminal; no further status change required)
```

The following are invalid for the canonical contract:

- autonomous state jumps without a recorded handoff action
- undocumented statuses
- direct `COMPLETED → RETRY` without a new review cycle
- repeated `RETRY` after the retry limit is exceeded without PM escalation

### Retry rule

The frozen Design Freeze defines a maximum retry count of `3`.

Validation rule:

- `retryCount` is an integer value from `0` to `3` during the normal retry lifecycle
- if `retryCount > 3`, the handoff MUST be escalated to PM for governance review
- the retry counter is not an automatic daemon; it is recorded as part of the repository handoff artifact and updated via the user-mediated workflow

This preserves the frozen requirement that the retry counter is a contract field, not an autonomous runtime mechanism.

### Completion rule

A handoff is `COMPLETED` only when all of the following are true:

1. the target role reviewed and accepted the handoff
2. the expected output artifacts were produced
3. the next handoff was created, or the workflow ended

A handoff is not considered complete merely because a source artifact exists.

### User-mediated protocol contract

The repository handoff remains user-mediated and must not create autonomous chaining:

```text
Create handoff artifact
  ↓
STOP
  ↓
USER / receiving role reviews
  ↓
Accept / Reject / Retry
  ↓
Next user-mediated session
```

This preserves the frozen distinction:

- handoff architecture / design contract = FROZEN
- handoff runtime implementation = NOT IMPLEMENTED

### Deferred questions preserved

The following remain explicitly deferred and must not be converted into protocol decisions in this Phase 1 contract:

- parallel handoffs
- simultaneous or conflicting outputs
- detailed rejection sequence rules
- detailed escalation procedure beyond PM → USER
- suggestedModel handling

The protocol definition validates the contract without inventing runtime behavior.

## Handoff Location

The canonical repository location is:

```text
.github/agents/workspace/handoffs/
└── <source-role>-to-<target-role>/
    └── <YYYY-MM-DD>-<sequence>-<short-description>/
```

Example:

```text
.github/agents/workspace/handoffs/
└── ba-to-architect/
    └── 2026-09-11-001-js-diagnostic-requirements/
        ├── handoff.json
        ├── context.md
        ├── open-questions.md
        └── blockers.md
```

Do not create a second handoff location or an alternate execution system.

## Required Files

### `handoff.json`

Required metadata:

- handoff identity
- source role
- target role
- status
- creation time
- context
- artifact references
- open questions
- blockers
- governance checks
- retry count
- completion criteria

### `context.md`

Human-readable context for the receiving role. It should include:

- objective
- current state
- completed work
- remaining work
- relevant decisions
- constraints
- dependencies
- risks

### `open-questions.md`

Contains unresolved questions relevant to the receiving role.

If no open questions exist, the file should still document the empty-state convention rather than inventing a new workflow.

### `blockers.md`

Contains blockers preventing normal progress.

If no blockers exist, the file should document the empty-state convention.

## Status Model

The valid status values are:

- `PENDING`
- `IN_PROGRESS`
- `COMPLETED`
- `BLOCKED`
- `REJECTED`
- `RETRY`

Required explicit transitions:

```text
PENDING
  → IN_PROGRESS
  → COMPLETED

PENDING
  → REJECTED
  → RETRY
  → IN_PROGRESS

IN_PROGRESS
  → BLOCKED

BLOCKED
  → RETRY
  → IN_PROGRESS

Any active state
  → REJECTED
  → RETRY
```

Do not invent undocumented states.

## Retry Rule

The Design Freeze defines:

- `retryCount` exists on the handoff
- maximum retry count = 3
- retry limit exceeded escalates to PM

This must be reflected in the artifact and recorded by the roles involved. The protocol must not implement background retry logic or automatic agent behavior.

## Governance Checks

The protocol must preserve the frozen classification:

- phase alignment = GUIDANCE
- scope boundary = GUIDANCE
- handoff format = VALIDATED ARTIFACT CONTRACT
- retry / loop counter = GUIDANCE

The protocol must not falsely claim technical enforcement where only workflow validation exists.

## Completion Criteria

A handoff is `COMPLETED` only when:

1. the target role has reviewed and accepted the handoff
2. the expected output artifacts were produced
3. a new handoff was created for the next step, or the workflow ended

A handoff is not complete merely because the source role created the artifact.

## Rejection and Retry

The protocol must allow the following to be explicitly represented in repository artifacts:

- rejection
- rejection reason
- retry
- retry count
- escalation after retry limit

The handoff must remain user-mediated. Nothing in this skill authorizes autonomous continuation.

## Escalation

Escalation remains within the frozen authority chain:

```text
Role
  ↓
PM
  ↓
USER
```

The protocol must not create autonomous escalation to another model, another agent, or an unapproved workflow.

## User-Mediated Protocol

The expected flow is:

```text
Agent/session
  ↓
Create repository handoff artifact
  ↓
STOP
  ↓
USER / receiving role reviews
  ↓
Accept / Reject / Retry
  ↓
Next user-mediated session
```

This model preserves the frozen requirement that handoff is repository-based and user-mediated, not automatic.

## Immutable / Append-Only Principle

The Design Freeze states that handoff artifacts are conceptually append-only. The protocol must preserve this intent without falsely claiming filesystem-level enforcement.

Status history and retry changes must be recorded in repository artifacts and reviewed by the receiving role and/or USER.

## `suggestedModel` Guidance

The Design Freeze leaves `suggestedModel` as an open/deferred design item.

Therefore:

- do not make it mandatory
- do not enforce it
- do not use it for automatic routing
- do not create automatic model-selection logic

If it appears in a handoff artifact, it must be clearly marked as optional guidance only.

## Parallel / Conflict Handling

The Design Freeze does not define a final architecture for parallel handoffs or simultaneous conflicting outputs. This skill must not invent such an architecture.

Where these issues arise, the protocol must document the deferred operational question and preserve the current governance and workflow baseline.

## Operational Rules

When using this skill:

1. create the handoff artifact only when a valid handoff is needed
2. keep the artifact readable and auditable
3. preserve the frozen design contract and deferred questions
4. keep the workflow user-mediated
5. stop after the handoff is created or the decision is made
6. defer unresolved implementation details instead of inventing a new architecture

## Final Boundary

This skill is a Phase 1 protocol artifact, not the implementation of the full AI Company OS runtime. It is intentionally limited to the handoff design contract and its repository-based operational guidance.
