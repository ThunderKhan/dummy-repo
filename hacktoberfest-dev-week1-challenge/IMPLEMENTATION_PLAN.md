# Second Desk — Implementation Plan

> **Document:** Implementation plan
> **Version:** 0.1
> **Status:** Active build plan
> **Updated:** 2026-10-03
> **Project:** Second Desk
> **Former project name:** EntryZero
> **Purpose:** Guide an implementation agent through the MVP in small, verifiable increments.

---

## 1. Purpose

This is the execution plan for implementing the Second Desk MVP.

Use the project documents as follows:

- PRD.md defines product requirements and the intended outcome.
- MVP.md defines the minimum product boundary and MVP acceptance criteria.
- architecture.md defines the system design and architectural decisions.
- IMPLEMENTATION_PLAN.md defines the order, gates, and method of implementation.

The implementation agent may progress autonomously, but only through bounded phases with explicit completion gates.

The goal is not to maximize code produced. The goal is to reach a working, testable vertical slice with the fewest unnecessary architectural decisions.

---

## 2. Planning Principles

This plan follows common implementation-planning practices:

1. Break work into manageable tasks.
2. Sequence work using dependencies.
3. Give each phase a measurable endpoint.
4. Make assumptions, constraints, and risks explicit.
5. Define tests and success criteria before declaring work complete.
6. Provide fallback and rollback behavior for failed implementation paths.
7. Keep deferred work explicitly outside the active plan.

Planning references:

- https://www.atlassian.com/work-management/strategic-planning/implementation-plan
- https://docs.github.com/en/enterprise-cloud/latest/copilot/tutorials/customization-library/custom-agents/implementation-planner
- https://docs.aws.amazon.com/wellarchitected/2023-10-03/framework/ops_ready_to_support_informed_deploy_decisions.html

---

## 3. Authority and Conflict Resolution

When specifications disagree, use this order:

1. explicit security constraints and safety invariants;
2. PRD.md and MVP.md requirements;
3. architecture.md decisions;
4. this implementation plan;
5. implementation convenience.

Do not silently resolve a material contradiction.

For a material contradiction:

1. document it;
2. identify the affected phase;
3. stop that phase;
4. resolve the specification before making a broad architectural change.

Small implementation details that do not change behavior or architecture may be chosen by the agent.

---

## 4. Autonomous Execution Contract

The implementation agent may move through the phases without requiring a human prompt after every small task.

It must follow these rules.

### 4.1 One active phase

Only one phase may be IN_PROGRESS at a time.

A later phase cannot begin until the current phase gate passes.

### 4.2 Small work units

Within a phase, work in coherent units such as:

- one domain object;
- one interface;
- one validator;
- one policy rule;
- one adapter capability;
- one test group.

Avoid giant cross-cutting edits.

### 4.3 Test close to the change

After each logical implementation unit, run the smallest relevant tests.

Do not postpone all verification until the end.

### 4.4 Keep the repository usable

Every phase should finish with a repository that can be installed, tested, and inspected.

Do not knowingly leave broken integration behind unless the phase explicitly defines a temporary scaffold.

### 4.5 No silent scope expansion

Do not add a feature because it appears useful, fashionable, easy, or interesting.

A feature may be added only when it is:

- required by the current phase;
- required by an existing MVP requirement;
- required to preserve a safety invariant; or
- necessary to unblock a required MVP behavior.

### 4.6 No silent architecture changes

When implementation reveals that the documented architecture is insufficient:

1. isolate the problem;
2. determine the smallest required architectural change;
3. document the change;
4. then implement it.

Do not silently redesign unrelated components.

### 4.7 No unsafe shortcuts

Never weaken:

- validation;
- authorization;
- approval;
- target scope;
- action limits;
- verification;
- tracing

just to make the demo work.

### 4.8 No unverified completion

Code compiling, a UI rendering, a model returning output, or one successful manual run is not sufficient evidence of phase completion.

---

## 5. Global Definition of Ready

A phase is READY only when:

- its prerequisites are complete;
- its inputs and assumptions are known;
- its output is clearly defined;
- the required tests can be identified;
- no unresolved blocker is being hidden.

If these conditions are not met, use BLOCKED rather than guessing.

---

## 6. Global Definition of Done

A phase is COMPLETE only when:

- implementation exists;
- relevant tests pass;
- acceptance criteria pass;
- no required behavior regressed;
- safety invariants remain enforced;
- no unrelated scope was introduced;
- important limitations are documented;
- the next phase has a usable starting point.

---

## 7. Phase Status

Allowed status values:

- TODO
- IN_PROGRESS
- BLOCKED
- COMPLETE
- DEFERRED

| Phase | Name | Depends on | Status |
|---|---|---|---|
| 0 | Repository reconnaissance | None | TODO |
| 1 | Foundation | 0 | TODO |
| 2 | Domain core | 1 | TODO |
| 3 | Deterministic validation | 2 | TODO |
| 4 | Approval and versioning | 3 | TODO |
| 5 | Policy and capabilities | 4 | TODO |
| 6 | Harness runtime | 5 | TODO |
| 7 | Local extraction adapter | 6 | TODO |
| 8 | Review interface | 4, 7 | TODO |
| 9 | Target adapter | 6 | TODO |
| 10 | Browser execution | 5, 6, 9 | TODO |
| 11 | Verification | 9, 10 | TODO |
| 12 | End-to-end vertical slice | 7, 8, 10, 11 | TODO |
| 13 | Safety regression suite | 12 | TODO |
| 14 | Evaluation | 12, 13 | TODO |
| 15 | Optional improvements | 14 | DEFERRED |

---

## 8. Phase 0 — Repository Reconnaissance

**Goal:** Understand the existing repository before changing implementation.

**Dependency:** None
**Complexity:** S

### Tasks

- inspect repository structure;
- inspect current source;
- inspect dependencies and configuration;
- inspect tests and CI;
- identify reusable implementation;
- identify documentation/code contradictions;
- establish the real build and test commands.

### Deliverable

Create or update IMPLEMENTATION_NOTES.md with:

- existing implementation;
- reusable code;
- missing pieces;
- contradictions;
- build/test commands;
- blockers.

### Do not

- refactor;
- add speculative dependencies;
- redesign architecture;
- begin feature implementation.

### Gate

- [ ] repository structure understood;
- [ ] existing implementation understood;
- [ ] test command known;
- [ ] implementation path identified;
- [ ] blockers are documented.

---

## 9. Phase 1 — Foundation

**Goal:** Establish a reproducible development and test foundation.

**Dependency:** Phase 0
**Complexity:** S/M

### Tasks

- establish application/package structure;
- establish configuration handling;
- establish test runner;
- establish minimal application entry point;
- add only necessary dependencies;
- document local setup.

### Gate

- [ ] clean setup succeeds;
- [ ] application starts;
- [ ] test suite runs;
- [ ] at least one meaningful test exists;
- [ ] dependencies are justified.

---

## 10. Phase 2 — Domain Core

**Goal:** Implement the canonical transaction and explicit lifecycle before connecting AI or browser systems.

**Dependency:** Phase 1
**Complexity:** M

### Implement

- canonical transaction;
- transaction version;
- run identifier;
- validation status;
- approval status;
- execution status;
- verification status;
- explicit run state machine;
- legal state transitions;
- terminal states.

### Required invariant

These paths must be impossible:

~~~text
RECEIVED → EXECUTING
VALIDATING → EXECUTING
REVIEW_REQUIRED → EXECUTING
~~~

### Tests

- valid transitions;
- invalid transitions;
- terminal states;
- transaction version changes;
- serialization/deserialization.

### Gate

- [ ] state transitions are explicit;
- [ ] illegal transitions are rejected;
- [ ] transaction versioning exists;
- [ ] critical transition boundaries are tested.

---

## 11. Phase 3 — Deterministic Validation

**Goal:** Prevent malformed or internally inconsistent records from reaching execution.

**Dependency:** Phase 2
**Complexity:** M

### Implement

- schema validation;
- required/optional fields;
- explicit unknown values;
- numeric validation;
- date validation;
- currency validation;
- arithmetic validation;
- tax consistency;
- duplicate detection where supported;
- field-level validation messages.

### Critical rule

Never use an LLM to validate arithmetic that ordinary deterministic code can compute.

### Required fixtures

- valid record;
- missing required field;
- invalid type;
- invalid quantity;
- invalid monetary value;
- arithmetic mismatch;
- tax mismatch;
- malformed date;
- duplicate identifier;
- unknown value;
- corrected valid record.

### Gate

- [ ] validator is deterministic;
- [ ] invalid records fail;
- [ ] valid records pass;
- [ ] financial arithmetic is decimal-safe;
- [ ] unknown values are not silently invented;
- [ ] critical validation rules are tested.

---

## 12. Phase 4 — Approval and Transaction Versioning

**Goal:** Make human authorization an enforceable system boundary.

**Dependency:** Phase 3
**Complexity:** M

### Implement

- approval object;
- approval timestamp;
- integrity marker/hash;
- transaction-version binding;
- approve;
- reject;
- approval invalidation.

### Required behavior

~~~text
Transaction v1
    ↓
Approved
    ↓
User edits
    ↓
Transaction v2
    ↓
Approval INVALID
~~~

### Tests

- write denied without approval;
- matching approval accepted;
- stale approval rejected;
- edited transaction invalidates approval;
- rejected transaction cannot execute;
- approval cannot authorize a different target.

### Gate

- [ ] approval exists independently of UI;
- [ ] approval is transaction-scoped;
- [ ] approval binds to an exact version;
- [ ] stale approval is rejected;
- [ ] write-boundary tests pass.

---

## 13. Phase 5 — Policy and Capabilities

**Goal:** Deterministically authorize every agent action.

**Dependency:** Phase 4
**Complexity:** M

### Initial action vocabulary

~~~text
OBSERVE
READ
CLICK
TYPE
SELECT
SCROLL
WAIT
DONE
~~~

Add an action only when a real MVP path requires it.

### Implement

- tool registry;
- action schema;
- capability model;
- target-scope checks;
- approval checks;
- precondition interface;
- policy decision result.

### Block by default

~~~text
DELETE
PAYMENT
PURCHASE
CREDENTIAL EXTRACTION
ARBITRARY SHELL
UNRELATED EXTERNAL ACTION
~~~

### Required tests

- malformed action;
- unregistered action;
- unapproved write;
- wrong target;
- wrong transaction version;
- expired capability;
- forbidden action;
- out-of-scope action;
- failed precondition.

### Gate

- [ ] every action is typed;
- [ ] every action is policy-checked;
- [ ] capabilities are bounded;
- [ ] model output cannot grant permission;
- [ ] blocked actions cannot reach the driver.

---

## 14. Phase 6 — Harness Runtime

**Goal:** Implement the control loop around state, policy, approval, budgets, recovery, and traces.

**Dependency:** Phase 5
**Complexity:** M/L

### Implement

- run orchestration;
- state progression;
- action budget;
- replan/retry budget;
- runtime timeout;
- target scope;
- precondition checks;
- postcondition hooks;
- bounded recovery;
- structured trace.

### Starting configuration

~~~yaml
max_actions: 30
max_replans: 2
max_run_seconds: 180
max_navigation_steps: 10
~~~

These are configurable defaults, not production guarantees.

### Safe recovery

Allowed:

- re-observe;
- retry an explicitly idempotent action;
- ask the user;
- stop.

Disallowed:

- guess;
- broaden permissions;
- switch to an unrelated target;
- bypass approval;
- execute arbitrary commands.

### Gate

- [ ] harness owns run state;
- [ ] budgets are enforced;
- [ ] traces are structured;
- [ ] recovery is bounded;
- [ ] terminal states are respected.

---

## 15. Phase 7 — Local Extraction Adapter

**Goal:** Put local/open AI on the critical path without making the model a trusted authority.

**Dependency:** Phase 6
**Complexity:** M

### Primary MVP input

Use plain text for the first reliable path.

Image input is optional.

### Implement

~~~text
source
→ extraction adapter
→ structured candidate
→ schema validation
→ canonical transaction
~~~

Keep model access behind an interface such as:

~~~python
class Extractor:
    def extract(self, source):
        ...
~~~

### Required behavior

Never silently invent:

- identifiers;
- dates;
- quantities;
- prices;
- tax;
- totals.

### Tests

- normal input;
- messy input;
- abbreviations;
- missing field;
- ambiguous field;
- malformed model output;
- extra prose around structured output;
- schema-invalid output.

### Gate

- [ ] local/open model is used by the primary path;
- [ ] model access is replaceable;
- [ ] output is schema-validated;
- [ ] malformed output fails safely;
- [ ] model output cannot bypass validation.

---

## 16. Phase 8 — Review Interface

**Goal:** Let the human inspect and approve the exact proposed transaction.

**Dependency:** Phases 4 and 7
**Complexity:** M

### Must show

- source input;
- extracted fields;
- validation status;
- warnings/errors;
- transaction version;
- target;
- high-level planned operation.

### Required controls

~~~text
EDIT
APPROVE
REJECT
~~~

### Edit behavior

An edit must:

1. create/update the current transaction version;
2. invalidate prior approval;
3. rerun validation.

### Gate

- [ ] exact proposed record is visible;
- [ ] user can edit;
- [ ] edits invalidate approval;
- [ ] approval is explicit;
- [ ] UI cannot bypass the harness.

---

## 17. Phase 9 — Target Adapter

**Goal:** Isolate one browser application's semantics from the core harness.

**Dependency:** Phase 6
**Complexity:** M

### Target selection

Prefer Google Sheets only when authentication and repeated demonstration are reliable.

Otherwise use a local spreadsheet-like application that reproduces the relevant workflow.

Do not weaken the authorization model to accommodate the target.

### Implement

~~~python
class TargetAdapter:
    def observe(self): ...
    def expose_tools(self): ...
    def execute(self, action): ...
    def verify(self, expected_record): ...
~~~

### Adapter responsibilities

- target state observation;
- target scope;
- permitted operations;
- semantic-to-UI mapping;
- destination identification;
- read-back;
- target-specific verification.

### Gate

- [ ] harness contains no target-specific selectors;
- [ ] current target state can be observed;
- [ ] adapter exposes only required capabilities;
- [ ] destination mapping is testable;
- [ ] credentials remain outside model-visible context.

---

## 18. Phase 10 — Browser Execution

**Goal:** Execute one already-approved transaction through constrained browser actions.

**Dependency:** Phases 5, 6, and 9
**Complexity:** L

### Loop

~~~text
OBSERVE
→ DECIDE
→ POLICY CHECK
→ PRECONDITION CHECK
→ EXECUTE
→ POSTCONDITION CHECK
→ TRACE
→ OBSERVE
~~~

### State priority

Use:

1. structured accessibility/page state;
2. semantic references;
3. deterministic adapter locators;
4. screenshots only where necessary.

Do not make coordinate-based clicking the primary path.

### Freshness rule

After meaningful navigation or page mutation:

~~~text
re-observe before reusing state references
~~~

### Gate

- [ ] computer-use model emits only typed actions;
- [ ] model cannot call Playwright directly;
- [ ] policy runs before consequential actions;
- [ ] preconditions are enforced;
- [ ] postconditions are enforced;
- [ ] budgets are enforced;
- [ ] stale state does not trigger blind retries.

---

## 19. Phase 11 — Verification

**Goal:** Prove that the actual target state matches the approved transaction.

**Dependency:** Phases 9 and 10
**Complexity:** M

### Level 1 — Action verification

Confirm a consequential interaction produced the expected local state.

### Level 2 — Record verification

Compare relevant target fields with the approved transaction.

### Level 3 — Workflow verification

Confirm:

- correct target;
- correct destination;
- expected record;
- expected values;
- save/commit state;
- no unexpected error state.

Only Level 3 may produce:

~~~text
COMPLETED
~~~

### Fault tests

- wrong row;
- wrong value;
- missing value;
- altered value;
- save failure;
- duplicate;
- UI drift.

### Gate

- [ ] read-back exists;
- [ ] approved vs actual state is compared;
- [ ] verification mismatch produces failure;
- [ ] COMPLETED requires verification;
- [ ] false completion is covered by tests.

---

## 20. Phase 12 — End-to-End Vertical Slice

**Goal:** Integrate the minimum path and prove the system with one realistic transaction.

**Dependency:** Phases 7, 8, 10, and 11
**Complexity:** L

### Required path

~~~text
INPUT
↓
LOCAL EXTRACTION
↓
CANONICAL TRANSACTION
↓
VALIDATION
↓
REVIEW
↓
APPROVAL
↓
HARNESS
↓
COMPUTER USE
↓
TARGET
↓
READ BACK
↓
VERIFICATION
↓
COMPLETED
~~~

### Do not start yet

Do not begin:

- fine-tuning;
- image support;
- a second target;
- replay;
- a developer API;
- advanced dashboards

until this vertical slice works.

### Gate

- [ ] one realistic transaction succeeds end to end;
- [ ] no consequential write occurs before approval;
- [ ] policy is enforced;
- [ ] verification passes;
- [ ] trace covers the full run;
- [ ] intended automated browser execution requires no hidden manual intervention.

---

## 21. Phase 13 — Safety Regression Suite

**Goal:** Prove failure containment rather than only happy-path success.

**Dependency:** Phase 12
**Complexity:** M

### Required scenarios

1. missing required field;
2. arithmetic mismatch;
3. duplicate record;
4. stale approval;
5. forbidden action;
6. wrong target;
7. wrong row;
8. UI drift;
9. prompt injection in source content;
10. malformed action;
11. action budget exhausted;
12. retry budget exhausted;
13. verification mismatch;
14. authentication unavailable.

### Expected outcomes

Every unsafe case must result in:

~~~text
BLOCK
ASK USER
STOP
FAIL VERIFICATION
~~~

Never silently succeed.

### Core invariant

> **AI failure must not silently become an incorrect business write.**

### Gate

- [ ] P0 safety scenarios have automated regression tests where practical;
- [ ] forbidden actions cannot reach the driver;
- [ ] unsafe runs remain non-completed;
- [ ] traces identify the stopping point.

---

## 22. Phase 14 — Evaluation

**Goal:** Measure the implementation instead of relying on demo impression.

**Dependency:** Phases 12 and 13
**Complexity:** M

### Extraction

Measure:

- field accuracy;
- numeric accuracy;
- schema-valid rate;
- missing-field detection;
- human correction rate;
- latency.

### Execution

Measure:

- task completion rate;
- verification pass rate;
- unexpected-action rate;
- actions per run;
- latency.

### Harness

Measure:

- blocked actions;
- retries;
- approval interruptions;
- budget utilization;
- failures by category.

### Primary end-to-end metric

~~~text
verified transaction completion rate
~~~

### Reporting rule

Every metric must include:

- dataset version;
- model/version;
- test count;
- configuration;
- environment where relevant;
- synthetic/anonymized/real data status.

Do not publish unsupported percentages.

### Gate

- [ ] evaluation is reproducible;
- [ ] every metric has a denominator;
- [ ] baseline exists;
- [ ] failures have categories;
- [ ] no unsupported performance claim is published.

---

## 23. Phase 15 — Optional Improvements

**Dependency:** Phase 14
**Status:** DEFERRED until P0 is stable.

Potential work:

### P1

- image input;
- fine-tuned extraction;
- evaluation dashboard;
- developer API;
- improved trace viewer.

### P2

- second target adapter;
- replay;
- additional workflow types.

### Fine-tuning gate

Fine-tuning may start only when:

- baseline extraction works;
- meaningful training data exists;
- a held-out test set exists;
- baseline measurements exist;
- training is feasible;
- improvement can be measured;
- the improvement matters to the actual workflow.

The validation, approval, harness, and verification boundaries must not be weakened by the fine-tuning experiment.

---

## 24. Cross-Phase Testing Strategy

Use the lowest-cost test layer that can prove the behavior.

### Unit

Use for:

- schemas;
- arithmetic;
- state transitions;
- policy;
- capabilities;
- approval;
- budgets;
- verification comparisons.

### Integration

Use for:

- extraction → transaction;
- transaction → validation;
- approval → harness;
- harness → adapter;
- adapter → verification.

### Browser

Use for:

- target discovery;
- field selection;
- field entry;
- stale references;
- save/read-back;
- UI changes.

### End to end

Use for:

~~~text
input
→ extraction
→ validation
→ approval
→ execution
→ verification
~~~

Lower-level deterministic behavior must not be left exclusively to end-to-end tests.

---

## 25. Change Control

Implementation may reveal that a planned approach is wrong.

Do not respond by continuously expanding scope.

For any material change, record:

~~~text
CHANGE:
WHY:
EVIDENCE:
AFFECTED PHASE:
DEPENDENCIES:
SAFETY IMPACT:
SCOPE IMPACT:
ALTERNATIVES:
DECISION:
~~~

### Minor change

A change is minor when it:

- does not change public behavior;
- does not change trust boundaries;
- does not add a subsystem;
- does not alter MVP scope.

Minor implementation choices may be made directly.

### Material change

A change is material when it changes:

- trust boundaries;
- authorization;
- target scope;
- model responsibility;
- state machine;
- persistence semantics;
- external dependencies;
- MVP scope.

Material changes must be documented before broad implementation continues.

---

## 26. Blocker Protocol

When blocked:

1. stop the current implementation unit;
2. preserve the last passing boundary;
3. record the blocker;
4. identify the smallest affected surface;
5. do not build speculative work around it;
6. continue only after evidence or an explicit design decision resolves it.

Use:

~~~text
STATUS: BLOCKED

BLOCKER:
IMPACT:
EVIDENCE:
CURRENT ASSUMPTION:
MINIMUM RESOLUTION:
~~~

---

## 27. Recovery and Rollback

When a phase introduces a regression:

1. identify the first failing invariant or test;
2. determine whether the problem is local or architectural;
3. avoid stacking unrelated fixes;
4. return to the last known passing boundary when necessary;
5. fix the root cause;
6. rerun the phase gate.

Never disable a test just to preserve progress.

Never weaken a safety control because it makes the demo easier.

---

## 28. Agent Checkpoint

At the end of every phase, update a concise checkpoint:

~~~text
PHASE:
STATUS:

IMPLEMENTED:
- ...

TESTS:
- ...

COMMANDS:
- ...

FILES CHANGED:
- ...

EVIDENCE:
- ...

KNOWN LIMITATIONS:
- ...

NEXT PHASE:
- ...
~~~

A phase must not be marked COMPLETE without evidence.

The agent may automatically start the next phase only after this checkpoint and the phase gate are satisfied.

---

## 29. Commit Discipline

Use focused commits that describe one coherent implementation change.

Good examples:

~~~text
feat(core): add transaction state machine
test(validation): add arithmetic consistency cases
feat(harness): add transaction-scoped policy checks
feat(adapter): add spreadsheet target
test(e2e): add verified transaction path
~~~

Avoid vague commits such as:

~~~text
changes
update project
fix stuff
build everything
~~~

Do not mix unrelated refactors into feature commits.

---

## 30. Explicit No-Go Scope

Do not implement these during the MVP:

- general-purpose browser automation;
- general desktop control;
- multi-agent swarms;
- autonomous payments;
- autonomous purchasing;
- unrestricted browsing;
- credential extraction;
- arbitrary shell commands;
- generalized long-term memory;
- enterprise IAM;
- multi-tenant SaaS;
- many application adapters;
- production accounting features;
- tax advice;
- unattended background financial writes.

If one of these becomes necessary for the MVP, treat that as an architectural blocker rather than silently adding it.

---

## 31. Priority Under Time Pressure

Preserve functionality in this order:

~~~text
1. deterministic transaction core
2. validation
3. approval
4. policy/capabilities
5. harness
6. one target
7. browser execution
8. verification
9. safety tests
10. extraction quality
11. image input
12. fine-tuning
13. API/dashboard/replay
14. second target
~~~

Cut breadth before weakening the control loop.

---

## 32. MVP Exit Gate

The MVP implementation is ready for submission only when:

- [ ] one real friend workflow has been validated;
- [ ] one supported input path works;
- [ ] local/open AI is on the critical path;
- [ ] structured extraction works;
- [ ] deterministic validation works;
- [ ] human review works;
- [ ] approval is transaction-scoped;
- [ ] policy enforcement works;
- [ ] one target adapter works;
- [ ] computer-use execution works;
- [ ] verification works;
- [ ] an incorrect record is safely blocked;
- [ ] unexpected target state safely stops;
- [ ] traces exist;
- [ ] evaluation is reproducible;
- [ ] no unauthorized business write occurs in the tested path.

---

## 33. Final Implementation Principle

Optimize for:

~~~text
small
explicit
deterministic
testable
bounded
observable
~~~

not:

~~~text
general
autonomous
clever
feature-rich
~~~

The objective is to prove the system's core thesis with a real workflow.

> **Build one verified transaction before building a platform.**
