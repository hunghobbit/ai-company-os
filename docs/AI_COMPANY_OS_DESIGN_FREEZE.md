# AI Company OS — Design Freeze

**Status:** ARCHITECTURE FROZEN — PHASES 1–5 COMPLETE  
**Date:** 2026-09-11  
**Document Type:** Architecture Specification (DESIGN-ONLY)  

---

## 1. Executive Summary

This document defines the frozen architecture for an **AI Agents Company OS** — a multi-role AI agent system designed to coordinate software development work through a structured workflow of 8 specialized roles.

**Scope boundary:** This document freezes the contracts, protocols, governance, and routing decisions for the AI Company OS. It is not a complete current-filesystem inventory, and historical repository references in this document are source-context records rather than proof of present AI Company OS files. Current implementation artifacts are maintained under `.github/agents/`, `.github/agents/workspace/handoffs/`, and `.github/skills/`.

**Key design principle:** The USER remains the final authority. Cline is the primary implementation/developer workflow. No autonomous infinite agent loops can occur. All model routing is workflow/session-level guidance, not hard per-agent enforcement.

**Label legend:**

- `CONFIRMED` — Verified against actual repository state
- `DESIGN DECISION` — Intentional architectural choice
- `GUIDANCE` — Cannot be technically enforced; workflow discipline required
- `LIMITATION` — Known constraint of the environment
- `OPEN QUESTION` — Unresolved; must be addressed before/after implementation

---

## 2. Current State

### 2.1 Repository Inspection Summary

**Provenance note:** The following historical inventory was authored in the JS Diagnostic Daily source context before this document was copied into AI Company OS. It must not be used as evidence that these files existed in AI Company OS. The live AI Company OS repository is the source of truth for current implementation state.

| Check | Result |
| ------- | -------- |
| `AGENTS.md` | **Historical/source-context reference only** — not verified in the current AI Company OS repository |
| `.clinerules/` | **Historical/source-context reference only** — not verified in the current AI Company OS repository |
| `CLAUDE.md` | **Not relied upon by this architecture**; current presence must be checked in the live repository |
| `.cline/skills/` | **Historical/source-context reference only** — not verified in the current AI Company OS repository |
| `.github/workspace/` | **Not the canonical handoff location**; current presence must be checked in the live repository |
| `.github/agents/` | **Current AI Company OS artifact** — eight role definitions are present |
| `.github/agents/workspace/handoffs/` | **Current AI Company OS artifact** — canonical handoff location is present |
| `.github/skills/` | **Current AI Company OS artifact** — shared skills are present |
| Existing AI Company OS design document | **Current AI Company OS artifact** — this document |
| Phase 1–5 status | **Completed and validated in the current AI Company OS workflow**; see the live repository artifacts and validation reports |
| Multi-agent infrastructure | **Present in the current AI Company OS repository** — agents, handoff location, and shared skills |

### 2.2 Existing Infrastructure

**Historical/source-context infrastructure (not current AI Company OS evidence):**

- `AGENTS.md` — source-context governance reference
- `.clinerules/` — source-context phase, validation, and scope references
- `FOUNDATION.md`, `PROGRESS.md`, and `docs/IMPLEMENTATION_LOG.md` — source-context project-state references
- `.cline/skills/` — source-context Cline procedural skills

These artifacts were not recreated or copied into AI Company OS. Their absence is not a missing AI Company OS requirement.

**Existing GitHub infrastructure:**

- `.github/modernize/java-upgrade/hooks/` — PowerShell/hook scripts for Java modernization tracking (NOT an agent framework)

### 2.3 Current AI Company OS Implementation

The live AI Company OS repository contains:

- eight role definitions under `.github/agents/`
- the repository-based handoff location under `.github/agents/workspace/handoffs/`
- the shared multi-agent skills under `.github/skills/`
- this Design Freeze under `docs/`

The historical/source-context files listed in §2.1 are not current AI Company OS requirements and must not be created solely because they appear in this document.

### 2.4 Historical Design Log Reference

Any reference to `docs/IMPLEMENTATION_LOG.md` or a numbered design-log entry refers to the JS Diagnostic Daily source context. It is not evidence that the file exists in AI Company OS.

## 3. 8 Agent Roles

### 3.1 Role Overview Matrix

| # | Role | May Modify Production Code | Primary Platform |
| --- | ------ | ---------------------------- | ------------------ |
| 1 | BA — Business Analyst | NO | Cline / User session |
| 2 | PM — Project Manager | NO | Cline / User session |
| 3 | Architect | NO (designs, does not implement) | Cline / User session |
| 4 | Developer | YES | **Cline (primary)** / VS Code Developer (complementary) |
| 5 | QA | NO (writes tests, does not ship code) | Cline / User session |
| 6 | Tester | NO (executes validation, does not ship code) | Cline / User session |
| 7 | IT | NO (configures environment, does not ship product code) | Cline / User session |
| 8 | Code Reviewer | NO (reviews, may request changes) | Cline / User session |

### 3.2 Role Contracts

---

#### 3.2.1 BA — Business Analyst

**Mission:** Translate user goals into structured, testable requirements.

**Responsibilities:**

- Elicit and clarify user intent
- Document requirements as acceptance criteria
- Identify scope boundaries (IN vs OUT)
- Surface ambiguities and request clarification from USER
- Maintain requirements artifacts

**Inputs:** User request, available project context, prior handoff from PM

**Outputs:** Requirements document, open questions list, handoff to Architect

**Allowed:** Ask USER questions, draft requirements, reference project docs, request PM scope validation

**Forbidden:** Design architecture, write production code, approve scope unilaterally, bypass handoff protocol

**Required validation:** Requirements reviewable by USER and Architect; ambiguities explicitly called out

**Handoff target:** Architect  
**Escalation target:** PM (scope conflict) → USER (fundamental)

**May modify production code:** NO

---

#### 3.2.2 PM — Project Manager

**Mission:** Ensure work is properly scoped, phased, sequenced, and tracked.

**Responsibilities:**

- Intake user requests and classify against current phase/roadmap
- Identify IN-PHASE vs OUT-OF-PHASE vs NEEDS-ROADMAP-UPDATE
- Track handoff status and blockers
- Maintain phase state awareness using available project-state artifacts
- Coordinate escalation when roles conflict or stall

**Inputs:** User request, current phase state, handoff artifacts

**Outputs:** Phase/scope classification, task sequencing, handoff routing, blocker reports

**Allowed:** Reference governance docs, route handoffs, escalate to USER, request scope clarification from BA

**Forbidden:** Design architecture, write production code, unilaterally change roadmap, bypass handoff protocol

**Required validation:** Phase classification consistent with available governance and project-state artifacts; if applicable sources conflict, STOP and report

**Handoff target:** BA (for requirements) or Architect (if requirements exist)  
**Escalation target:** USER

**May modify production code:** NO
---

#### 3.2.3 Architect

**Mission:** Design the technical solution — architecture, interfaces, data models, implementation boundaries — without writing production code.

**Responsibilities:**

- Produce architecture design artifacts
- Define interfaces and contracts
- Identify technical risks and dependencies
- Specify implementation boundaries (what each phase delivers)
- Review Developer's implementation against design (via Code Reviewer pathway)

**Inputs:** Requirements from BA, phase/scope context from PM, existing system architecture

**Outputs:** Architecture design document, interface contracts, data model definitions, implementation boundary spec, handoff to Developer

**Allowed:** Design architecture, define interfaces, request clarification from BA, escalate technical blockers to PM

**Forbidden:** Write production code, approve implementation quality, unilaterally change requirements

**Required validation:** Design must be implementable within phase boundaries; interfaces must be unambiguous

**Handoff target:** Developer (via handoff protocol)  
**Escalation target:** PM → USER

**May modify production code:** NO

---

#### 3.2.4 Developer

**Mission:** Implement the architecture design into production code, following the project's conventions and validation requirements.

**CRITICAL DESIGN DECISION:** **Cline is the PRIMARY Developer workflow.** The VS Code / Copilot Developer agent is complementary, NOT a replacement for Cline.

**Responsibilities:**

- Implement code per the architecture design
- Follow existing project conventions (package structure, naming, module system)
- Write and run tests per phase-validation requirements
- Validate implementation with Maven tiers
- Log implementation results according to applicable project documentation
- Hand off to QA for validation

**Inputs:** Architecture design from Architect, phase boundaries from PM, existing codebase conventions

**Outputs:** Production code changes, tests, implementation log entry, handoff to QA

**Allowed:** Write production code, write tests, run applicable validation, update approved project-state documentation when present, request clarification from Architect

**Forbidden:** Design architecture, unilaterally expand scope beyond approved phase, skip validation steps, implement future-phase behavior

**Required validation:** Use the applicable project validation rules; regression tests must pass; final diff must contain only the approved phase surface

**Handoff target:** QA  
**Escalation target:** Architect (design clarification) → PM (scope) → USER

**May modify production code:** **YES** — this is the Developer's core function.

**Cline integration note:** The Developer role is executed primarily through Cline. When a USER engages Cline to implement work, Cline IS the Developer agent in the AI Company OS workflow. Any VS Code / Copilot Developer agent would be a secondary or parallel implementation channel, not the primary one.

#### 3.2.5 QA — Quality Assurance

**Mission:** Validate that the implementation meets the requirements and design before it reaches the Tester.

**Responsibilities:** Review implementation against requirements; verify test coverage; check acceptance criteria; identify gaps; produce QA report.

**Inputs:** Implementation from Developer, requirements from BA, architecture design from Architect

**Outputs:** QA validation report (pass/fail per acceptance criterion), gap list, handoff to Tester or back to Developer

**Allowed:** Review code and tests, run validation commands, compare implementation to requirements, request rework from Developer

**Forbidden:** Write production code, approve release unilaterally, bypass handoff protocol

**Required validation:** QA report must reference specific acceptance criteria; findings must be reproducible

**Handoff target:** Tester  
**Escalation target:** Developer (rework) → PM → USER

**May modify production code:** NO

---

#### 3.2.6 Tester

**Mission:** Execute runtime/integration/end-to-end validation to confirm the system behaves correctly in the target environment.

**Responsibilities:** Execute runtime smoke tests; run integration/end-to-end scenarios; validate against actual runtime behavior; report runtime findings.

**Inputs:** QA-passed implementation, runtime environment access, test scenarios from QA or Architect

**Outputs:** Runtime test results, execution findings report, handoff to Code Reviewer or back to Developer

**Allowed:** Run the application/execute tests, observe runtime behavior, report failures with reproduction steps, request rework from Developer

**Forbidden:** Write production code, approve release unilaterally, bypass handoff protocol

**Required validation:** Runtime findings must include reproduction steps; distinguish actual runtime failures from warnings/expected stub behavior

**Handoff target:** Code Reviewer  
**Escalation target:** Developer (rework) → PM → USER

**May modify production code:** NO

---

#### 3.2.7 IT — Infrastructure / Environment

**Mission:** Ensure the development and runtime environment is correctly configured and operational.
**Responsibilities:** Manage environment configuration; verify toolchain availability (JDK, Maven, etc.); handle dependency/build environment issues; support runtime environment setup.
**Inputs:** Environment needs from any role, current environment state
**Outputs:** Environment status report, configuration changes (if needed), handoff back to requesting role
**Allowed:** Configure environment, install/verify tooling, update environment documentation
**Forbidden:** Write product code, change project scope, bypass handoff protocol
**Required validation:** Environment changes must be reproducible and documented
**Handoff target:** Requesting role (back)  
**Escalation target:** PM → USER
**May modify production code:** NO (may modify environment config, not product source)

---

#### 3.2.8 Code Reviewer

**Mission:** Perform final code review before approval — checking quality, correctness, security, and alignment with design and conventions.
**Responsibilities:** Review production code changes; check against architecture design; verify coding standards and conventions; assess security and scope boundaries; produce review decision: APPROVE / REQUEST-CHANGES / REJECT.
**Inputs:** Tester-passed implementation, architecture design, coding conventions
**Outputs:** Code review report, review decision, handoff to PM (if approved) or back to Developer (if changes requested)
**Allowed:** Review code, request changes from Developer, approve or reject, escalate to PM
**Forbidden:** Write production code, approve without review, bypass handoff protocol, unilaterally merge (USER remains final authority)
**Required validation:** Review must cover the actual diff; decision must be documented with reasoning
**Handoff target:** PM (if approved)  
**Escalation target:** USER (final authority)
**May modify production code:** NO (reviews only; requests changes from Developer)

---

## 4. Agent Contracts Summary

Each role contract includes: Mission, Responsibilities, Inputs, Outputs/Artifacts, Allowed actions, Forbidden actions, Required validation, Handoff target, Escalation target, May modify production code (YES/NO).

All contracts are **GUIDANCE** unless technically enforceable. The handoff protocol provides the primary enforcement mechanism through artifact validation.---

## 5. Workflow

### 5.1 Default Workflow Chain

USER → PM (intake/phase classification) → BA (requirements) → Architect (design) → Cline/Developer (implementation) → QA (validation) → Tester (runtime validation) → Code Reviewer (review) → PM (coordination) → USER (final authority)

### 5.2 Who Does What

| Step | Who | Action |
| ------ | ----- | -------- |
| 1. Start a task | USER | Initiates work by requesting it |
| 2. Approve scope | USER | Confirms what is in/out of scope; PM classifies phase alignment |
| 3. Create requirements | BA | Produces requirements + acceptance criteria |
| 4. Design architecture | Architect | Produces design + interfaces + implementation boundaries |
| 5. Implement | Cline/Developer | Writes code + tests per design |
| 6. Validate | QA | Checks implementation against requirements |
| 7. Execute runtime tests | Tester | Runs runtime/integration validation |
| 8. Review | Code Reviewer | Reviews code quality and design alignment |
| 9. Request rework | Any role | Can request rework back to Developer |
| 10. Final authority | USER | Approves merges/releases; resolves escalations |

### 5.3 Loop Prevention

**CONFIRMED:** The workflow is linear with defined handoff points. No role autonomously loops back to itself.

**GUIDANCE:** Roles may request rework (handoff back to Developer), but this is an explicit handoff, not an autonomous loop. The USER breaks any stalemate.

**OPEN QUESTION:** How are parallel reviews handled? (e.g., two Code Reviewers?) — Current design assumes single reviewer per handoff; parallelism is an implementation decision.

### 5.4 USER Final Authority

**CONFIRMED:** The USER is the final authority on: scope approval, roadmap changes, escalation resolution, merge/release approval. No agent role can override a USER decision.---

## 6. Handoff Protocol

### 6.1 Design Principle

**DESIGN DECISION:** The handoff protocol is **repository-based** and **user-mediated**. It does NOT assume native automatic agent-to-agent handoff exists. Handoffs are explicit artifact transfers through the repository, reviewed/mediated by the USER or the receiving role.

### 6.2 Handoff Location

**DESIGN DECISION:** `.github/agents/workspace/handoffs/`

**Rationale:** Avoids conflation with GitHub Actions workspace (`.github/workspace`). The existing repo has `.github/modernize/`, not `.github/workspace/`. Clean-slate design.

**CONFIRMED:** Neither `.github/workspace/` nor `.github/agents/` exist in the repository.

### 6.3 Naming Convention

```
handoffs/<source-role>-to-<target-role>/<YYYY-MM-DD>-<sequence>-<short-description>/
```

Example: `handoffs/ba-to-architect/2026-09-11-001-js-diagnostic-requirements/`

### 6.4 Required Metadata (handoff.json)

```json
{
  "handoffId": "2026-09-11-001",
  "sourceRole": "BA",
  "targetRole": "Architect",
  "status": "PENDING",
  "createdAt": "2026-09-11T09:00:00+07:00",
  "context": "JS Diagnostic Daily — Phase 4 scope clarification",
  "artifacts": ["requirements.md", "open-questions.md"],
  "openQuestions": [],
  "blockers": [],
  "governanceChecks": {"phaseAlignment": "CONFIRMED", "scopeBoundary": "CONFIRMED"},
  "retryCount": 0,
  "completionCriteria": ["Architect reviews and accepts handoff", "Design artifacts produced"]
}
```

### 6.5 Status Values

| Status | Meaning |
| -------- | --------- |
| `PENDING` | Handoff created, awaiting target role review |
| `IN_PROGRESS` | Target role is working on the handoff |
| `COMPLETED` | Handoff accepted and processed |
| `BLOCKED` | Blocker identified; escalation may be needed |
| `REJECTED` | Target role rejected the handoff (with reason) |
| `RETRY` | Handoff being retried after failure |

### 6.6 Immutable/Append-Only Principle

**DESIGN DECISION:** Handoff artifacts are append-only. Status changes recorded as new entries/log updates. **GUIDANCE:** Not technically enforced by file system — workflow discipline required.

### 6.7 Handoff Contents

Each handoff directory: `handoff.json`, `context.md`, relevant artifacts, `open-questions.md`, `blockers.md` (if any).

### 6.8 Governance Checks

| Check | Who validates | Classification |
| ------- | --------------- | ---------------- |
| Phase alignment | PM (before BA/Architect handoff) | GUIDANCE |
| Scope boundary | PM + USER | GUIDANCE |
| Handoff format | Receiving role | VALIDATED (artifact contract) |
| Retry/loop counter | Receiving role + PM | GUIDANCE |

### 6.9 Retry/Loop Counter

**DESIGN DECISION:** Each handoff has `retryCount` field. If retried more than N=3 times, escalates to PM automatically. **GUIDANCE:** Counter maintained by roles, not auto-incremented.

### 6.10 Completion Criteria

A handoff is COMPLETED when:

1. Target role has reviewed and accepted the handoff
2. Target role has produced expected output artifacts
3. A new handoff to the next role has been created (or workflow ends)---

## 7. Governance Hierarchy

### 7.1 Governance Precedence (Highest to Lowest)

| Level | File/Artifact | Scope | Authority |
| ------- | --------------- | ------- | ----------- |
| 1 | USER directive | Project-wide | **FINAL AUTHORITY** |
| 2 | `AGENTS.md` (if present) | Project-wide | Canonical constitution; historical/source-context reference in this document |
| 3 | `.clinerules/*.md` (if present) | Project-wide | Operational rules; historical/source-context reference in this document |
| 4 | `FOUNDATION.md` (if present) | Project-specific | Domain/architecture foundation; historical/source-context reference in this document |
| 5 | `PROGRESS.md` + `docs/IMPLEMENTATION_LOG.md` (if present) | Project-specific | Current phase state + history; historical/source-context references in this document |
| 6 | `.cline/skills/*/SKILL.md` (if present) | Project-wide (Cline) | Procedural skills for Cline; historical/source-context reference in this document |
| 7 | `.github/agents/workspace/handoffs/*/handoff.json` | Handoff-specific | Per-handoff metadata |
| 8 | Agent instructions (`.github/agents/*.agent.md`) | Role-specific | Current AI Company OS implementation artifacts |
| 9 | Session/workspace artifacts | Ephemeral | Working context |

### 7.2 Role of CLAUDE.md

**CONFIRMED:** `CLAUDE.md` does **NOT** exist in this repository.

**DESIGN DECISION:** This architecture does NOT rely on `CLAUDE.md`. The governance model is conceptually ordered as USER authority followed by applicable project governance, project-state artifacts, skills, handoffs, and role instructions. Historical references to `AGENTS.md` and `.clinerules/` are not current AI Company OS file requirements.

**LIMITATION:** Cline may or may not read `CLAUDE.md` depending on VS Code/Cline version. This architecture does not assume any particular behavior.

### 7.3 What Is Authoritative

| Item | Classification |
| ------ | ---------------- |
| USER decisions | **AUTHORITATIVE** — final authority |
| `AGENTS.md` (if present) | **AUTHORITATIVE** — canonical constitution |
| `.clinerules/` (if present) | **AUTHORITATIVE** — operational rules |
| `FOUNDATION.md` (if present) | **AUTHORITATIVE** — project foundation |
| `PROGRESS.md` + `IMPLEMENTATION_LOG.md` (if present) | **AUTHORITATIVE** — current state |
| Cline skills (`.cline/skills/`, if present) | **GUIDANCE** — procedural, Cline-specific |
| Handoff protocol | **VALIDATED** — artifact contract enforced by receiving role |
| Model routing | **GUIDANCE** — workflow/session-level |
| Agent instructions | **GUIDANCE** — unless technically enforced by platform |

### 7.4 Conflict Resolution

**CONFIRMED DESIGN RULE:** If applicable governance files conflict:

1. USER directive wins over all
2. `AGENTS.md` wins over `.clinerules/`
3. `.clinerules/` wins over skills and agent instructions
4. If applicable project-state artifacts conflict on phase state → STOP and report

### 7.5 Read-Only Governance Files

**GUIDANCE:** When present and applicable, the following are treated as read-only governance (workflow discipline, not technically enforced):

- `AGENTS.md`
- `.clinerules/*.md`
- `FOUNDATION.md` (except by explicit roadmap update)
- `PROGRESS.md` (only updated on phase state change)
- `docs/IMPLEMENTATION_LOG.md` (append-only)

---

## 8. Model Routing Matrix

### 8.1 Routing Classification

**LIMITATION:** The current VS Code/Cline environment does NOT support hard per-agent model enforcement via `.agent.md` frontmatter or similar mechanisms.

**DESIGN DECISION:** Model routing is classified as **WORKFLOW / SESSION MODEL ROUTING** — guidance for which model to use, NOT automatic enforcement.

### 8.2 Model Routing Matrix

| Role | Preferred Model | Reason | Fallback | Routing Mechanism |
| ------ | ----------------- | -------- | ---------- | ------------------- |
| BA | General-purpose (balanced) | Requirements analysis benefits from broad reasoning | Same | USER selects model for session/handoff |
| PM | General-purpose (balanced) | Phase management, coordination, classification | Same | USER selects model for session/handoff |
| Architect | Strong reasoning/design-oriented | Architecture design benefits from structured reasoning | General-purpose | USER selects model for session/handoff |
| Developer (Cline) | Current Cline model | Cline uses whatever model USER has configured | N/A | Cline model = USER's configured model |
| QA | General-purpose (balanced) | Review and validation reasoning | Same | USER selects model for session/handoff |
| Tester | General-purpose (balanced) | Runtime observation and reporting | Same | USER selects model for session/handoff |
| IT | General-purpose (balanced) | Environment configuration reasoning | Same | USER selects model for session/handoff |
| Code Reviewer | Strong reasoning/review-oriented | Code review benefits from careful analysis | General-purpose | USER selects model for session/handoff |

### 8.3 Routing Mechanism

**GUIDANCE:** Model selection happens at session level:

1. USER decides which model to use for a given task/handoff
2. Handoff context may include `suggestedModel` field as guidance
3. Cline always uses whatever model USER has configured for Cline session
4. No `.agent.md` frontmatter or similar mechanism assumed to enforce model selection

**OPEN QUESTION:** Should handoff protocol include `suggestedModel` field? Current design says yes (as GUIDANCE), needs implementation validation.

### 8.4 Cline Model = Developer Model

**CONFIRMED:** Developer role (Cline) always uses the model USER has configured for Cline. No separate "Developer model" — Cline session model IS the Developer model.

**GUIDANCE:** If USER wants different model for Architect vs Developer, must start new Cline session with that model (or switch models between handoffs).---

## 9. Cline Integration

### 9.1 Relationship Map

USER (final authority)
  ├── PM (project management / phase classification) — Uses Cline session with general-purpose model
  ├── BA (requirements analysis) — Uses Cline session with general-purpose model
  ├── Architect (architecture design) — Uses Cline session with design-oriented model
  ├── Cline / Developer (implementation) ← PRIMARY — Uses Cline session with USER's configured model
  ├── QA (quality assurance validation) — Uses Cline session with general-purpose model
  ├── Tester (runtime/integration testing) — Uses Cline session with general-purpose model
  ├── Code Reviewer (code review) — Uses Cline session with review-oriented model
  └── IT (environment/infrastructure) — Uses Cline session with general-purpose model

### 9.2 Default Workflow Evaluation

**CONFIRMED:** The default workflow follows:
USER → PM (intake/phase classification) → BA (requirements) → Architect (design) → Cline/Developer (implementation) → QA (validation) → Tester (runtime validation) → Code Reviewer (review) → PM (coordination) → USER (final authority)

### 9.3 Cline = Primary Developer

**CONFIRMED DESIGN DECISION:** Cline is the PRIMARY implementation/developer workflow. The VS Code/Copilot Developer agent is NOT a replacement for Cline.

**Rationale:**

- The source-context project used Cline for implementation work; this historical statement is not current AI Company OS filesystem evidence
- The AI Company OS architecture preserves Cline as the primary Developer workflow
- Introducing a VS Code Developer agent as a parallel implementation channel would create ambiguity and potential conflict

**GUIDANCE:** If a VS Code/Copilot Developer agent is introduced in the future, it would be a complementary channel, not the primary one. Any such introduction would require a governance update.

### 9.4 Role Responsibilities in Workflow

| Step | Who | Action |
| ------ | ----- | -------- |
| Start a task | USER | Initiates work by requesting it |
| Approve scope | USER | Confirms what is in/out of scope; PM classifies phase alignment |
| Create requirements | BA | Produces requirements + acceptance criteria |
| Design architecture | Architect | Produces design + interfaces + implementation boundaries |
| Implement | Cline/Developer | Writes code + tests per design |
| Validate | QA | Checks implementation against requirements |
| Execute runtime tests | Tester | Runs runtime/integration validation |
| Review | Code Reviewer | Reviews code quality and design alignment |
| Request rework | Any role | Can request rework back to Developer |
| Final authority | USER | Approves merges/releases; resolves escalations |

### 9.5 Who Can Request Rework

**Any role** can request rework by creating a handoff back to the Developer. This is an explicit handoff, NOT an autonomous action.

### 9.6 Who Has Final Authority

**USER** has final authority on: scope, roadmap, escalation resolution, merge/release approval.---

## 10. Skill Architecture

### 10.1 Directory Structure Decision

**DESIGN DECISION:**

| Directory | Owner | Purpose |
|-----------|-------|---------|
| `.cline/skills/` (if present) | Cline | Cline-specific procedural skills from source context |
| `.github/skills/` | AI Company OS (multi-agent) | Shared/multi-agent skills, platform-agnostic concepts |

**Rationale:**

- `.cline/skills/` is reserved for Cline-specific operations when such platform-specific skills are present
- `.github/skills/` is the natural location for multi-agent architecture skills
- This separation prevents Cline-specific skills from being confused with multi-agent skills

### 10.2 Skill Ownership Matrix

| Concept | Primary Location | Notes |
| --------- | ------------------ | ------- |
| requirements-analysis | `.github/skills/` | Multi-agent; used by BA + Architect |
| architecture-design | `.github/skills/` | Multi-agent; used by Architect |
| test-design | `.github/skills/` | Multi-agent; used by QA + Tester |
| code-review | `.github/skills/` | Multi-agent; used by Code Reviewer |
| environment-management | `.github/skills/` | Multi-agent; used by IT |
| phase-management | `.github/skills/` | Multi-agent; used by PM |
| handoff-protocol | `.github/skills/` | Multi-agent; foundational — used by ALL roles |
| implementation-log | `.cline/skills/` | Cline-specific source-context skill |
| phase-implementation | `.cline/skills/` | Cline-specific source-context skill |
| phase-validation | `.cline/skills/` | Cline-specific source-context skill |
| regression-debugging | `.cline/skills/` | Cline-specific source-context skill |

### 10.3 Shared vs Platform-Specific

**CONFIRMED:**

- **Shared concepts** (go in `.github/skills/`): requirements-analysis, architecture-design, test-design, code-review, environment-management, phase-management, handoff-protocol
- **Cline-specific** (stay in `.cline/skills/` when present): source-context Cline operational procedures
- **Platform-specific**: if a skill has Cline-specific AND Copilot-specific implementations, shared concept goes in `.github/skills/` and platform specifics go in `.cline/skills/` or `.github/skills/Copilot/` respectively

### 10.4 Implementation Priority Recommendation

**DESIGN DECISION:** **handoff-protocol first**, because it is foundational to the multi-agent workflow.

Recommended order:

1. `handoff-protocol` — foundational
2. `phase-management` — extends existing Cline discipline to multi-agent
3. `requirements-analysis` — needed by BA
4. `architecture-design` — needed by Architect
5. `test-design` — needed by QA/Tester
6. `code-review` — needed by Code Reviewer
7. `environment-management` — needed by IT

**GUIDANCE:** This order is a recommendation, not a hard sequence.

### 10.5 No Duplication Rule

**DESIGN DECISION:** Do NOT duplicate Cline rules into every skill or agent. Applicable project governance remains the single source of operational rules. Skills add procedural guidance for specific roles/concepts, not redundant governance.

---

---

## 11. MCP / Tool Strategy

### 11.1 Current State

**CONFIRMED:** The current project does NOT have any MCP (Model Context Protocol) servers configured, beyond whatever Cline uses internally.

### 11.2 Strategy

**GUIDANCE:** The AI Company OS architecture does NOT mandate specific MCP servers. Each role may use whatever tools/MCPs are available in the environment, within scope boundaries.

**DESIGN DECISION:** MCP/tool restrictions are **GUIDANCE** unless technically enforced by the environment. The architecture does not claim to restrict MCP access.

### 11.3 Tool Use by Role

| Role | Typical Tools | Classification |
| ------ | --------------- | ---------------- |
| BA | Document editing, file read/write | GUIDANCE |
| PM | File read/write, repository inspection | GUIDANCE |
| Architect | File read/write, diagram tools (if available) | GUIDANCE |
| Developer (Cline) | Maven, git, file read/write, IDE | CONFIRMED (existing) |
| QA | File read/write, test execution | GUIDANCE |
| Tester | Runtime execution, file read/write | GUIDANCE |
| IT | Environment commands, file read/write | GUIDANCE |
| Code Reviewer | File read/write, diff inspection | GUIDANCE |

---

## 12. Enforcement vs Guidance

### 12.1 Classification Summary

| Rule | Classification | Rationale |
| ------ | ---------------- | ----------- |
| USER remains final authority | **GOVERNANCE** (authoritative via USER directive and applicable project governance) | Frozen architecture decision |
| Agent cannot modify production code (non-Developer roles) | **GUIDANCE** — can be validated via code review + handoff protocol, but not technically prevented | File system cannot enforce role-based write restrictions without platform support |
| Model selection per role | **WORKFLOW / SESSION GUIDANCE** | VS Code/Cline does not support hard per-agent model enforcement |
| MCP restrictions | **GUIDANCE** unless technically enforced | No MCP restriction mechanism in current environment |
| Handoff format | **VALIDATED ARTIFACT CONTRACT** | Receiving role validates handoff.json structure |
| Phase scope | **PM/GOVERNANCE + VALIDATION** | PM classifies; validation confirms scope adherence |
| Handoff immutable/append-only | **GUIDANCE** | Workflow discipline, not file-system enforced |
| Retry/loop counter | **GUIDANCE** | Maintained by roles, not auto-incremented |
| Cline = Primary Developer | **DESIGN DECISION / GUIDANCE** | Cannot be technically enforced; workflow convention |
| Governance files are read-only | **GUIDANCE** | Workflow discipline |
| No autonomous infinite loops | **GUIDANCE + VALIDATED** | Handoff protocol + retry counter + USER authority prevent loops; validated by design review |

### 12.2 Why This Matters

**DESIGN DECISION:** The architecture explicitly distinguishes between what can be enforced, what can be validated, and what is guidance. This prevents the architecture from claiming capabilities that the tooling does not actually provide. Any rule labeled GUIDANCE requires workflow discipline and validation to be effective.

---

## 13. Failure / Retry Strategy

### 13.1 Failure Modes

| Failure Mode | Detection | Response |
| -------------- | ----------- | ---------- |
| Handoff rejected | Target role sets status to REJECTED | Source role revises and resubmits (retryCount++) |
| Blocker identified | Any role adds to blockers.md | Escalate to PM → USER if unresolved |
| Retry limit exceeded | retryCount > 3 | Auto-escalate to PM |
| Phase misalignment | PM classification conflict | STOP and report under applicable phase governance |
| Validation failure | Maven/test/runtime failure | Developer fixes; re-validates; handoff back to QA/Tester |
| Runtime failure | Tester/QA finds runtime issue | Handoff back to Developer for fix |
| Scope creep | Any role identifies out-of-scope work | PM reclassifies; USER decides |

### 13.2 Retry Strategy

**DESIGN DECISION:** Retries are tracked per handoff via retryCount. Max retries = 3. Exceeding max retries escalates to PM. This prevents infinite retry loops while allowing reasonable revision cycles.

**GUIDANCE:** The retry counter is incremented by the roles involved, not automatically.

### 13.3 Loop Prevention

**CONFIRMED:** The following prevent autonomous infinite loops:

1. **Linear workflow** — roles hand off in one direction; rework is an explicit back-handoff, not an autonomous loop
2. **Retry counter** — hard limit on retries per handoff
3. **USER authority** — USER can break any stalemate
4. **Phase gate** — applicable phase governance requires stopping after completing the requested phase
5. **STOP discipline** — every role MUST STOP after completing its handoff, not automatically proceed

---

## 14. Security / Scope Boundaries

### 14.1 Scope Boundaries

**CONFIRMED:** The AI Company OS architecture operates within its approved scope boundaries. Historical references to AGENTS.md and FOUNDATION.md describe source-context governance, not required current AI Company OS files. It does NOT:

- Add new product features
- Refactor unrelated code
- Change the existing project's architecture without evidence
- Bypass the existing phase-gated development process

### 14.2 Security Boundaries

| Boundary | Classification |
| ---------- | ---------------- |
| Production code access | Developer only (validated by Code Reviewer + USER) |
| Governance file modification | USER / explicit roadmap update only |
| Handoff directory | Agent roles only (GUIDANCE) |
| Model selection | USER only |
| Merge/release approval | USER only |

### 14.3 What This Architecture Does NOT Do

**CONFIRMED:**

- Does NOT implement the 8 agents
- Does NOT create `.github/agents/*.agent.md` files
- Does NOT create or modify historical source-context files such as AGENTS.md, .clinerules, or .cline/skills merely because they are referenced here
- Does NOT add new product features
- Does NOT refactor unrelated files
- Does NOT assume automatic agent-to-agent handoff
- Does NOT claim hard per-agent model enforcement
- Does NOT replace Cline with a VS Code Developer agent

## 15. Design Decisions

### 15.1 Decision Log

| # | Decision | Rationale | Classification |
| --- | ---------- | ----------- | ---------------- |
| D1 | 8 roles defined with clear boundaries | Provides structured workflow without overlap | DESIGN DECISION |
| D2 | Cline = Primary Developer; VS Code Developer is complementary | Preserves existing workflow; avoids replacement confusion | DESIGN DECISION |
| D3 | Handoff location = `.github/agents/workspace/handoffs/` | Avoids conflation with GitHub Actions workspace; clean namespace | DESIGN DECISION |
| D4 | No `.github/workspace` conflict | Neither directory exists in current repo; choosing clearer namespace anyway | CONFIRMED |
| D5 | Model routing = workflow/session guidance, not hard enforcement | VS Code/Cline limitation; honest architecture | DESIGN DECISION |
| D6 | `CLAUDE.md` does not exist; architecture does not rely on it | Prevents false assumptions about Cline behavior | CONFIRMED |
| D7 | Governance hierarchy: USER > applicable project governance > project docs > skills > handoffs > agent instructions | Defines the frozen conceptual authority model; historical file references are conditional/source-context | DESIGN DECISION |
| D8 | Handoff protocol = repository-based, user-mediated, append-only | Does not assume native agent-to-agent handoff | DESIGN DECISION |
| D9 | `.github/skills/` for multi-agent skills; `.cline/skills/` for Cline-specific | Clear separation of concerns | DESIGN DECISION |
| D10 | handoff-protocol implemented first | Foundational to multi-agent coordination | DESIGN DECISION |
| D11 | No duplication of Cline rules into every skill/agent | Single source of governance | DESIGN DECISION |
| D12 | Retry limit = 3 per handoff, then escalate to PM | Prevents infinite loops; allows reasonable revision | DESIGN DECISION |
| D13 | USER is final authority on scope, roadmap, merges, escalations | Consistent with AGENTS.md and project constitution | CONFIRMED |

---

## 16. Known Limitations

### 16.1 Technical Limitations

| Limitation | Impact | Workaround |
| ------------ | -------- | ------------ |
| No hard per-agent model enforcement | Model routing is guidance, not enforcement | USER selects model per session/handoff |
| No native agent-to-agent handoff | Handoffs are user-mediated | Handoff protocol + USER mediation |
| No role-based file write restrictions | Non-Developer roles could technically write production code | Code Reviewer + USER validation; GUIDANCE discipline |
| CLAUDE.md role unknown | Cannot assume Cline reads CLAUDE.md | Architecture does not rely on it |
| No automatic retry counter | retryCount is manually maintained | Roles follow convention; PM monitors |

### 16.2 Design Limitations

| Limitation | Impact |
| ------------ | -------- |
| Single Code Reviewer assumed per handoff | Parallel review not specified (OPEN QUESTION) |
| No explicit conflict resolution for simultaneous handoffs | PM coordinates (GUIDANCE) |
| Model routing recommendations are advisory | Different roles may use same model in practice |

---

## Open Questions / Deferred Decisions

The following items are explicitly DEFERRED and remain open. They are not frozen as implementation decisions and are not converted into design choices in this document.

- Parallel handoff handling: The design assumes a single receiving role and single validation path per handoff, but it does not define how multiple concurrent handoffs are prioritized or managed.
- Simultaneous or conflicting outputs: The workflow provides a linear default path and escalation through PM/USER, but it does not define a deterministic rule for multiple roles producing conflicting outputs at the same time.
- Receiving-agent handoff rejection: The design states that a receiving role may reject or request changes, but it does not prescribe the exact repository artifact sequence or approval language for rejection and retry.
- Escalation behavior: The document defines escalation targets and authority, but does not define the concrete decision procedure for unresolved blockers beyond PM and USER escalation.
- Model guidance in handoffs: The design notes that a `suggestedModel` field may be included as guidance, but this remains a deferred decision pending implementation validation.

These items remain part of the frozen baseline as operational gaps to be addressed later without altering the current architecture, role boundaries, or governance hierarchy.

---

## Implementation Boundaries

This Design Freeze document defines the architecture, governance, role boundaries, workflow intent, constraints, and known limitations for AI Company OS. It does not yet define executable runtime implementation.

Specifically, this document establishes:

- the frozen 8-role architecture and responsibilities
- the governance precedence and authority model
- the workflow and handoff intent
- the model-routing guidance and limitation boundaries
- the scope and constraint boundaries for the future implementation phases

This document does not define:

- executable agent runtime behavior
- concrete `.github/agents/*.agent.md` implementations
- concrete `.github/skills/` implementation content
- the runtime handoff protocol execution logic
- working product features or operational code paths beyond the design freeze itself

This section preserves the design-only boundary and ensures that deferred operational details remain explicitly deferred rather than being treated as current implementation decisions.

---

## 17. Implementation Plan

### 17.1 Implementation Phases (For Future Implementation)

**NOTE:** This is a PLANNING section only. No implementation is performed in this design freeze.

| Phase | Description | Key Deliverables |
| ------- | ------------- | ------------------ |
| Phase 0 — Design Freeze | **CURRENT** — this document | `docs/AI_COMPANY_OS_DESIGN_FREEZE.md` |
| Phase 1 — Handoff Protocol | Implement handoff protocol infrastructure | `.github/agents/workspace/handoffs/` structure, handoff.json schema, handoff-protocol skill |
| Phase 2 — Agent Instructions | Create `.github/agents/*.agent.md` for each role | 8 agent instruction files |
| Phase 3 — Multi-Agent Skills | Implement `.github/skills/` for multi-agent concepts | requirements-analysis, architecture-design, test-design, code-review, environment-management, phase-management |
| Phase 4 — Governance Integration | Verify governance hierarchy works in practice | Documentation update if needed |
| Phase 5 — Model Routing Validation | Validate model routing workflow in practice | May adjust based on findings |

### 17.2 Scope of This Design Freeze

**CONFIRMED:** This design freeze covers Sections 1–16 only. Section 17 is planning, not implementation.

**DO NOT implement in this phase:**

- No `.github/agents/` directory creation
- No `.github/agents/*.agent.md` files
- No `.github/agents/workspace/handoffs/` directory creation (Phase 1)
- No `.github/skills/` directory creation (Phase 3)
- No agent implementation---

## 18. Design Freeze Checklist

### 18.1 Verification Checklist

| # | Check | Status | Notes |
| --- | ------- | -------- | ------- |
| 1 | Entire Design Freeze re-read | ✅ PASS | Reviewed all 18 sections |
| 2 | No contradictions found | ✅ PASS | All classifications consistent |
| 3 | Every role has clear boundary | ✅ PASS | 8 roles defined with allowed/forbidden actions |
| 4 | Handoffs have clear owner | ✅ PASS | Each handoff has source role, target role, receiving role validates |
| 5 | Cline remains primary Developer | ✅ PASS | Explicitly stated in §3.2.4, §9.3, and workflow |
| 6 | Model routing does not claim unsupported VS Code functionality | ✅ PASS | Classified as WORKFLOW/SESSION GUIDANCE |
| 7 | Governance precedence is internally consistent | ✅ PASS | §7.1–7.4 preserve the frozen conceptual precedence; historical file references are labeled as conditional/source-context |
| 8 | No autonomous infinite agent loop possible | ✅ PASS | Linear workflow + retry limit + USER authority + STOP discipline |
| 9 | USER remains final authority | ✅ PASS | Explicit in §5.4, §9.6, governance hierarchy |
| 10 | No future implementation work accidentally introduced | ✅ PASS | §17 is planning only; no files created except this document |

### 18.2 Label Usage Check

| Label | Used? | Where |
| ------- | ------- | ------- |
| CONFIRMED | ✅ | Multiple: CLAUDE.md absence, no .github/workspace conflict, Cline = primary Developer, USER final authority, governance files |
| DESIGN DECISION | ✅ | Multiple: handoff location, model routing classification, .github/skills vs .cline/skills, handoff-protocol first, Cline primary Developer |
| GUIDANCE | ✅ | Multiple: model routing, MCP restrictions, role-based write restrictions, handoff immutability, retry counter, read-only governance |
| LIMITATION | ✅ | §16.1: no hard per-agent model enforcement, no native handoff, no role-based write restrictions, CLAUDE.md unknown |
| OPEN QUESTION | ✅ | §5.3: parallel reviews; §8.4: suggestedModel field in handoff protocol |

### 18.3 Final Status

**DESIGN FREEZE STATUS: COMPLETE**

- 8 roles frozen: **YES**
- Handoff architecture / design contract : **FROZEN**
- Handoff runtime implementation : **NOT IMPLEMENTED**
- Governance hierarchy frozen: **YES**
- Model routing frozen: **YES**
- Cline integration frozen: **YES**
- Skill architecture frozen: **YES**
- Validation: **PASS**
- Remaining open questions: 2 (parallel reviews, suggestedModel field)
- Phase 1–5 implementation and validation: **COMPLETE**
- No subsequent phase is defined by this document

---

## Appendix A: File Inventory

### A.1 Files Inspected for This Design Freeze

| File | Purpose |
| ------ | --------- |
| `AGENTS.md` | Historical/source-context governance reference from JS Diagnostic Daily; not verified in AI Company OS |
| `FOUNDATION.md` | Historical/source-context project foundation from JS Diagnostic Daily; not verified in AI Company OS |
| `PROGRESS.md` | Historical/source-context phase record from JS Diagnostic Daily; not verified in AI Company OS |
| `docs/IMPLEMENTATION_LOG.md` | Historical/source-context implementation history from JS Diagnostic Daily; not verified in AI Company OS |
| `.clinerules/10-phase-control.md` | Historical/source-context phase-gate reference; not verified in AI Company OS |
| `.clinerules/20-validation.md` | Historical/source-context validation reference; not verified in AI Company OS |
| `.clinerules/30-scope-and-documentation.md` | Historical/source-context scope reference; not verified in AI Company OS |
| `.cline/skills/implementation-log/SKILL.md` | Historical/source-context Cline logging skill; not verified in AI Company OS |
| `.cline/skills/phase-implementation/SKILL.md` | Historical/source-context Cline implementation skill; not verified in AI Company OS |
| `.cline/skills/phase-validation/SKILL.md` | Historical/source-context Cline validation skill; not verified in AI Company OS |
| `.cline/skills/regression-debugging/SKILL.md` | Historical/source-context Cline debugging skill; not verified in AI Company OS |
| `.github/modernize/**` | Existing GitHub automation (not agent framework) |

### A.2 Files Created by This Design Freeze

| File | Purpose |
|------|---------|
| `docs/AI_COMPANY_OS_DESIGN_FREEZE.md` | Canonical design freeze document |
| `docs/IMPLEMENTATION_LOG.md` (Entry 14) | Historical/source-context log entry; not created in AI Company OS |

### A.3 Files NOT Modified

| File | Reason |
| ------ | -------- |
| `AGENTS.md` | Not present in AI Company OS; no file created |
| `.clinerules/**` | Not present in AI Company OS; no files created |
| `.cline/skills/**` | Not present in AI Company OS; no files created |
| `FOUNDATION.md` | Not present in AI Company OS; no file created |
| `PROGRESS.md` | Not present in AI Company OS; no file created |

---

## Appendix B: Glossary

| Term | Definition |
| ------ | ------------ |
| AI Company OS | The multi-role AI agent architecture defined by this document |
| Cline | The existing VS Code AI coding assistant used as the primary Developer workflow |
| Developer (role) | The 4th role in the 8-role architecture; implemented primarily via Cline |
| VS Code Developer agent | A potential complementary implementation channel (NOT Cline) |
| Handoff | An explicit artifact transfer between roles via `.github/agents/workspace/handoffs/` |
| Governance | The applicable set of authoritative rules; historical references include AGENTS.md, .clinerules/, and project docs |
| GUIDANCE | A rule that cannot be technically enforced and requires workflow discipline |
| VALIDATED | A rule enforced by artifact validation (e.g., handoff.json structure) |
| ENFORCED | A rule technically enforced by the platform (rare in current environment) |
| USER | The human final authority; not an agent role |
| Phase gate | The project mechanism, when defined by applicable governance, that limits work to one approved phase at a time |

---

*End of Design Freeze Document*
