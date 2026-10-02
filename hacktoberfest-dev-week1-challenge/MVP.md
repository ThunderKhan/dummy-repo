# EntryZero \u2014 MVP Specification

> **Project:** EntryZero  
> **Document:** MVP specification  
> **Version:** 0.1  
> **Date:** 2026-10-02  
> **Status:** Implementation baseline  
> **Parent document:** PRD.md  
> **Primary use case:** Safe, human-approved small-business data entry  
> **Challenge:** Hacktoberfest DEV Weekend Challenge \u2014 Build for a Friend

---

## 1. Purpose

This document defines the **Minimum Viable Product** for EntryZero.

The MVP is not a reduced version of the entire product vision. It is the **smallest end-to-end system capable of testing the core product hypothesis with a real person and a real workflow**.

For EntryZero, that hypothesis is:

> **A local open-source AI system can remove repetitive business data entry while preserving human control over consequential records through deterministic validation, explicit approval, constrained computer use, and post-action verification.**

A useful MVP should maximize **learning per unit of implementation effort**, not the number of features shipped. Established product guidance similarly emphasizes starting with the smallest version capable of validating the core idea, focusing on the customer pain point, making assumptions explicit, limiting scope, testing with users, and using evidence to guide subsequent development.

Sources:
- https://www.atlassian.com/agile/product-management/minimum-viable-product/
- https://www.atlassian.com/agile/product-management/product-specification/
- https://www.atlassian.com/agile/product-management/requirements/
- https://www.aha.io/roadmapping/guide/plans/what-is-a-minimum-viable-product

---

## 2. MVP in One Sentence

> **A friend can paste one messy business message into EntryZero, review the locally extracted record, approve it, watch a constrained computer-use agent enter it into one browser-based spreadsheet, and receive a verified result or a clear safe failure.**

That is the MVP.

Everything else is secondary.

---

## 3. Core Learning Goal

The MVP exists to answer four questions:

### Q1 \u2014 Does the problem actually matter?

Will the real friend use automation for this specific repetitive task?

### Q2 \u2014 Can a small local model understand the input?

Can an open/local model reliably transform the friend's real-world input into the fields needed by the existing workflow?

### Q3 \u2014 Can a constrained agent safely perform the UI work?

Can the computer-use layer enter the already-approved record without requiring unrestricted control?

### Q4 \u2014 Does the harness make the workflow safer?

Can deterministic validation, approval, policy enforcement, and verification prevent unsafe or incorrect writes?

The MVP is successful only if it produces evidence about these questions.

---

## 4. The Smallest Useful Vertical Slice

The MVP must complete one real transaction from input to verified result:

~~~text
friend's business message
        \u2193
local AI extraction
        \u2193
strict structured record
        \u2193
deterministic validation
        \u2193
human review
        \u2193
human approval
        \u2193
computer-use agent
        \u2193
one browser-based target
        \u2193
read-back verification
        \u2193
complete / stop
~~~

This is deliberately a **vertical slice**, not a collection of disconnected features.

---

## 5. Product Boundary

### In scope

The MVP supports exactly one narrow workflow:

- one real friend;
- one real repetitive business-data-entry task;
- one primary input format;
- one structured record schema;
- one browser-based target;
- one local/open extraction model;
- one constrained computer-use agent;
- deterministic validation;
- explicit human approval;
- post-action verification;
- basic execution tracing.

### Out of scope

The MVP does not attempt to provide:

- a general-purpose Agents API replacement;
- arbitrary computer control;
- desktop automation;
- autonomous payments;
- autonomous purchasing;
- accounting or tax advice;
- multi-agent orchestration;
- many application integrations;
- unrestricted browsing;
- unattended financial writes;
- general-purpose memory;
- production SaaS deployment.

### Scope rule

> **If a feature does not help prove the core hypothesis in the one selected friend workflow, it does not belong in the MVP.**

---

## 6. The Real User

The MVP must be built for **one actual friend**, not a generic persona.

These details are placeholders until validated directly:

| Field | MVP requirement |
|---|---|
| Friend | Real person |
| Business | Real business/activity |
| Current tool | Existing tool actually used |
| Input | Actual input format |
| Repetitive task | Actual task performed |
| Required fields | Derived from the real workflow |
| Frequency | Observed/reported, not invented |
| Pain point | Confirmed with the friend |
| Test data | Permissioned, anonymized, or synthetic |
| Feedback | Captured after testing |

Do not invent:

- user quotes;
- time-saved claims;
- transaction counts;
- error rates;
- revenue impact;
- business scale.

Real observations are preferable to impressive assumptions.

---

## 7. User Problem

The MVP addresses a very specific form of operational friction:

> **The friend already has the data, but spends time manually moving it from one representation into another.**

Typical workflow:

~~~text
Message / photo
       \u2193
Human reads values
       \u2193
Human switches application
       \u2193
Human finds destination row/form
       \u2193
Human retypes values
       \u2193
Human checks values
~~~

EntryZero aims to replace the repetitive transformation with:

~~~text
messy input
    \u2193
structured record
    \u2193
approved computer action
    \u2193
verified destination state
~~~

The friend retains control over the consequential action.

---

## 8. Product Promise

EntryZero promises only four things in the MVP:

### 1. Understand

Turn supported input into structured data.

### 2. Check

Detect relevant inconsistencies before a write.

### 3. Ask

Show the friend what will be entered and require explicit approval.

### 4. Execute and verify

Perform the approved computer interaction and confirm the resulting state.

It does **not** promise perfect autonomous business administration.

---

## 9. MVP Principles

### Principle 1 \u2014 Vertical slice over breadth

One workflow must work end to end before new capabilities are added.

### Principle 2 \u2014 Problem before platform

The friend's real workflow determines the schema, target, and interaction model.

### Principle 3 \u2014 Deterministic logic wherever possible

Arithmetic, schemas, permissions, and verification must not depend on probabilistic output when ordinary program logic is sufficient.

### Principle 4 \u2014 Consequential authority stays outside the model

The model can propose an action. The harness decides whether the action is allowed.

### Principle 5 \u2014 Human approval is a product boundary

Approval is deliberate. It is not a temporary workaround.

### Principle 6 \u2014 Verification is mandatory

A successful tool call is not equivalent to a successful business operation.

### Principle 7 \u2014 Measure learning, not activity

Lines of code, number of tools, model size, and UI polish are not MVP success metrics.

### Principle 8 \u2014 Fail closed

When the system cannot establish that an action is safe, it stops.

---

## 10. MVP User Story

> **As a small-business owner, when I receive a business record in a messy message, I want EntryZero to prepare the corresponding spreadsheet entry for my review and, after I approve it, enter and verify it for me so I do not have to manually retype it.**

Supporting stories:

- As the friend, I can provide the business message to EntryZero.
- As the friend, I can see what EntryZero understood before anything is written.
- As the friend, I can edit extracted fields before approval.
- As the friend, I can explicitly authorize one bounded transaction.
- As the friend, I can see the agent perform the approved entry.
- As the friend, I can see whether the resulting target state matches the approved record.
- As the friend, I am told clearly when EntryZero cannot safely continue instead of having it guess.

---

## 11. P0 MVP Requirements

### MVP-01 \u2014 Text input

The user can paste or type one business message.

Example:

~~~text
Rahul Traders 4 A4 packs 280 each GST 18
~~~

The input is associated with one run.

### MVP-02 \u2014 Local extraction

An open-weight/local model converts the message into a strict structured record.

Preferred direction:

- Gemma or another suitable open model.

The primary demo should use the local path.

### MVP-03 \u2014 Strict schema

The extracted output must conform to a predefined schema.

Example:

~~~json
{
  "customer": "Rahul Traders",
  "invoice_id": "INV-1042",
  "date": "2026-10-02",
  "items": [
    {
      "description": "A4",
      "quantity": 4,
      "unit_price": 280
    }
  ],
  "subtotal": null,
  "tax_rate": 0.18,
  "tax": null,
  "total": null,
  "currency": "INR"
}
~~~

The exact fields must be finalized from the friend's actual workflow.

Unknown values remain unknown.

The model must not silently invent missing values.

### MVP-04 \u2014 Deterministic validation

Validation runs after extraction and before approval.

Minimum checks:

- required fields;
- numeric types;
- valid quantities;
- non-negative monetary values;
- date format;
- currency;
- arithmetic consistency;
- tax consistency where relevant;
- schema validity.

Examples:

~~~text
quantity \u00d7 unit_price = expected amount
subtotal + tax = total
~~~

A validation failure blocks execution.

### MVP-05 \u2014 Review and edit

The user sees:

- extracted values;
- source input;
- validation status;
- warnings/errors;
- target application;
- intended high-level operation.

The user can:

~~~text
EDIT
APPROVE
REJECT
~~~

### MVP-06 \u2014 Approval gate

No consequential browser write may occur until the user explicitly approves the transaction.

Approval is scoped to the current transaction.

### MVP-07 \u2014 Agent harness

The harness controls:

- run state;
- available tools;
- current task;
- approved record;
- permissions;
- action count;
- retry count;
- verification state;
- event trace.

The model cannot bypass the harness.

### MVP-08 \u2014 Typed computer-use actions

The agent operates through a constrained tool set.

Initial candidates:

~~~text
OBSERVE_PAGE
CLICK
TYPE
SELECT
SCROLL
READ
DONE
~~~

The exact interface may evolve, but arbitrary unrestricted browser commands are out of scope.

### MVP-09 \u2014 One target application

The MVP supports exactly one browser-based target.

Preferred target:

- Google Sheets, if authentication and demonstration are reliable.

Fallback:

- a local spreadsheet-like web application that reproduces the relevant interaction and allows deterministic verification.

### MVP-10 \u2014 Target adapter

Target-specific behavior is isolated behind an adapter.

Conceptual interface:

~~~python
class TargetAdapter:
    def observe(self): ...
    def expose_tools(self): ...
    def execute(self, action): ...
    def verify(self, expected_record): ...
~~~

The adapter boundary exists to keep target logic separate from the core harness.

### MVP-11 \u2014 Execution

After approval, the computer-use agent shall:

1. observe the target;
2. locate the approved destination;
3. enter the approved values;
4. stop when the transaction is complete.

### MVP-12 \u2014 Verification

After execution, EntryZero reads back the relevant target values and compares them with the approved record.

~~~text
approved record
      \u2193
execute
      \u2193
read target
      \u2193
compare
      \u2193
MATCH \u2192 COMPLETE
MISMATCH \u2192 FAIL
~~~

A run cannot be marked complete without successful verification.

### MVP-13 \u2014 Safe stopping

EntryZero stops when:

- validation fails;
- approval is absent;
- a forbidden action is requested;
- the target is not recognized;
- action limits are exceeded;
- retry limits are exceeded;
- verification fails;
- required data is missing;
- an unexpected UI state is encountered.

### MVP-14 \u2014 Trace

Each run produces a basic structured trace:

~~~text
input_received
extraction_complete
validation_passed
approval_requested
approved
page_observed
action_selected
action_executed
verification_started
verification_passed
run_complete
~~~

Failure runs must explain where and why execution stopped.

---

## 12. Optional Features

These are allowed only after the P0 path works:

### P1 \u2014 Image input

Accept a photo of an invoice, receipt, or note.

### P1 \u2014 Fine-tuned extraction

Fine-tune a local open model for the friend's actual input distribution.

### P1 \u2014 Evaluation dashboard

Display baseline/fine-tuned extraction results and execution results.

### P1 \u2014 Developer API

Expose the harness through a small HTTP interface.

### P2 \u2014 Second adapter

Support another spreadsheet or billing-style target.

### P2 \u2014 Replayable traces

Replay a failed run for debugging.

Do not start P1/P2 work while the P0 path is unreliable.

---

## 13. Explicitly Excluded From the MVP

| Feature | Decision | Reason |
|---|---|---|
| Multi-agent architecture | Exclude | Adds complexity without proving the core hypothesis |
| General-purpose browser agent | Exclude | Conflicts with focused scope |
| Desktop computer use | Exclude | Browser target is sufficient |
| Autonomous payment | Exclude | Unnecessary and high-risk |
| Autonomous purchasing | Exclude | Unnecessary and high-risk |
| Automatic submission without review | Exclude | Violates the safety thesis |
| Unlimited retries | Exclude | Can create uncontrolled behavior |
| Arbitrary shell commands | Exclude | Unnecessary attack surface |
| Many integrations | Exclude | Dilutes the real workflow |
| General memory system | Exclude | Not required for first workflow |
| Production multi-user auth | Exclude | Not required to validate the idea |
| Enterprise deployment | Exclude | Not required for the challenge |
| Full accounting functionality | Exclude | Outside the problem |
| Tax advice | Exclude | The system validates data; it is not a tax advisor |

---

## 14. MVP Architecture

~~~text
                    USER INPUT
                        │
                 text / optional image
                        │
                        ↓
             ┌──────────────────────┐
             │ Local Open Model     │
             │ Extraction           │
             └──────────┬───────────┘
                        ↓
                STRUCTURED RECORD
                        │
                        ↓
             ┌──────────────────────┐
             │ Deterministic        │
             │ Validator            │
             └──────────┬───────────┘
                        │
                 PASS / REVIEW
                        │
                        ↓
             ┌──────────────────────┐
             │ Human Review         │
             │ EDIT / APPROVE       │
             └──────────┬───────────┘
                        │
                    APPROVED
                        │
                        ↓
             ┌──────────────────────┐
             │ Agent Harness        │
             │ State                │
             │ Policy               │
             │ Typed Tools          │
             │ Retry Limits         │
             │ Trace                │
             └──────────┬───────────┘
                        │
                        ↓
             ┌──────────────────────┐
             │ Computer-use Model   │
             │ Laya-style           │
             └──────────┬───────────┘
                        │
                        ↓
                    Playwright
                        │
                        ↓
                 Target Web App
                        │
                        ↓
                 READ BACK STATE
                        │
                        ↓
                    VERIFY
                    /     \
                   /       \
                PASS       FAIL
                 ↓           ↓
             COMPLETE       STOP
~~~

The extraction and computer-use models are intentionally separate.

---

## 15. MVP Safety Model

The key design rule is:

> **No single probabilistic component controls the complete transaction.**

| Component | Interpret | Validate | Approve | Write | Verify |
|---|---:|---:|---:|---:|---:|
| Extraction model | Yes | No | No | No | No |
| Validator | No | Yes | No | No | No |
| Human | Yes | Yes | Yes | Indirectly | Yes |
| Computer-use model | Yes | Limited | No | Propose | No |
| Harness | Controls | Enforces | Gates | Authorizes | Yes |
| Target adapter | No | Target rules | No | Executes | Reads |

---

## 16. Approval Policy

### Before approval

The agent may:

- inspect information necessary to prepare the task;
- propose an action sequence.

The agent may not perform a consequential write.

### After approval

The agent may execute only the bounded approved transaction.

### Outside the approved transaction

The harness rejects:

- unrelated edits;
- deletes;
- payments;
- external messages;
- unrelated navigation;
- unregistered actions.

---

## 17. Validation Rules

The exact rules depend on the friend's workflow, but the baseline should include:

### Schema

- required fields;
- correct types;
- allowed values;
- explicit unknown values.

### Numeric

- parse quantities;
- parse monetary values;
- reject invalid negatives where not allowed;
- control decimal precision.

### Arithmetic

~~~text
sum(line_items) = subtotal
subtotal + tax = total
quantity × unit_price = line_total
~~~

Apply only checks that correspond to the actual record format.

### Duplicate detection

Where the target has a stable unique identifier such as an invoice number, detect an existing matching record before writing.

### Ambiguity

When the system cannot safely determine a value:

~~~text
DO NOT GUESS
     ↓
ASK USER
~~~

---

## 18. Computer-Use Policy

### Allowed

- observe approved target;
- locate relevant cells/forms;
- click;
- type;
- select;
- scroll;
- read;
- finish.

### Disallowed by default

- delete;
- payment;
- file-system access;
- arbitrary shell commands;
- credential extraction;
- unrelated external navigation;
- unrelated data modification.

The action space should be as small as possible while completing the real workflow.

---

## 19. MVP Evaluation

A good MVP is an experiment, not merely a demo. The evaluation therefore measures whether the core assumptions hold.

### 19.1 User validation

At least one real friend should:

- confirm that the workflow is real;
- perform or observe the task;
- use or review the prototype;
- provide feedback on usefulness and trust.

### 19.2 Functional validation

A valid test transaction must complete:

~~~text
input
→ extraction
→ validation
→ approval
→ execution
→ verification
~~~

### 19.3 Safety validation

Deliberately test:

- incorrect totals;
- missing fields;
- duplicate records;
- ambiguous values;
- forbidden actions;
- unexpected target state;
- incorrect write results.

Expected behavior is **block, ask, stop, or fail verification**, not silent execution.

### 19.4 Extraction evaluation

Measure at least:

- field accuracy;
- numeric accuracy;
- schema validity;
- human correction rate.

### 19.5 Execution evaluation

Measure at least:

- successful task completion rate;
- verification pass rate;
- unexpected-action rate;
- action count;
- latency.

### 19.6 Comparative evaluation

Where practical, compare:

~~~text
manual workflow
vs
EntryZero workflow
~~~

using actual:

- steps;
- corrections;
- latency;
- successful completion.

Do not claim a percentage improvement until it has been measured.

---

## 20. Minimum Test Dataset

Create a small evaluation set containing realistic examples.

Recommended categories:

1. Normal valid records.
2. Messy wording.
3. Missing optional fields.
4. Missing required fields.
5. Arithmetic mismatch.
6. Duplicate record.
7. Ambiguous quantity or price.
8. Unexpected target state.
9. Adversarial instruction embedded inside source content.
10. Corrected record after user editing.

Use anonymized or synthetic data unless the friend explicitly permits real records.

---

## 21. Mandatory Failure Demonstration

The final MVP demo should intentionally include a bad input.

Example:

~~~text
Customer: Rahul Traders
Quantity: 4
Unit price: ₹500
Total: ₹1,800
~~~

The validator computes:

~~~text
4 × ₹500 = ₹2,000
~~~

Expected behavior:

> **Entry blocked: the extracted arithmetic is inconsistent. No spreadsheet write will occur.**

This demonstrates why EntryZero needs:

- deterministic validation;
- an approval gate;
- a harness.

A second failure should demonstrate UI protection if possible:

> **Target state not recognized. Agent stopped rather than guessing.**

---

## 22. MVP Demo Flow

The demo should be understandable without technical context.

### Part 1 — The friend's problem

Show the real manual workflow.

### Part 2 — Input

Paste the real or anonymized business message.

### Part 3 — Local AI

Show the extracted structured record.

### Part 4 — Validation

Show the rule checks.

### Part 5 — Human control

Show:

~~~text
review
→ edit if necessary
→ APPROVE
~~~

### Part 6 — Computer use

Show the agent operating the spreadsheet.

### Part 7 — Verification

Show:

~~~text
approved record
vs
actual target state

MATCH ✓
~~~

### Part 8 — Failure

Show the intentionally incorrect transaction getting blocked.

The demo should make the harness visible rather than presenting the model as an unexplained black box.

---

## 23. Implementation Order

The order should reduce project risk.

1. Validate the friend's workflow.
2. Define the record schema.
3. Build deterministic validation.
4. Build extraction baseline.
5. Build review and approval.
6. Build the harness.
7. Integrate one target.
8. Add computer-use execution.
9. Add verification.
10. Add failure tests.
11. Fine-tune if justified.
12. Test with the friend.
13. Polish the demo and documentation.

The important rule is **working vertical slice first, optimization second**.

---

## 24. Fine-Tuning Decision Gate

Fine-tuning is **optional in the MVP**.

It becomes MVP-worthy only when:

1. the baseline local extraction works;
2. a meaningful training dataset exists;
3. training is feasible on available compute/time;
4. evaluation can be performed fairly;
5. improvement is measurable;
6. the improvement matters to the real workflow.

Preferred target:

> **messy business-language or document input → strict structured record**

The computer-use model should not be the first fine-tuning target unless the extraction path and evaluation are already stable.

---

## 25. Weekend Time-Box

The DEV challenge ends on **October 5, 2026 at 6:59 AM UTC / 12:29 PM IST**.

Source:
https://dev.to/challenges/hackertoberfest-weekend-2026-10-01

### First priority

Get this working:

~~~text
TEXT
→ LOCAL EXTRACTION
→ VALIDATION
→ APPROVAL
→ ONE TARGET WRITE
→ VERIFICATION
~~~

### Second priority

Add:

~~~text
IMAGE INPUT
→ FINE-TUNING
→ BETTER TRACING
~~~

### Last priority

Consider:

~~~text
API
→ SECOND ADAPTER
→ REPLAY
→ ADDITIONAL UX
~~~

If time becomes constrained, cut breadth rather than weakening the core safety loop.

---

## 26. Fallback Strategy

### Fallback A — Image extraction is unreliable

Use text input for the primary demo.

### Fallback B — Google Sheets authentication is fragile

Use a local spreadsheet-like target that reproduces the relevant workflow.

### Fallback C — Computer-use model is unreliable

Constrain the target UI further and reduce the action space.

### Fallback D — Fine-tuning is unstable

Ship the local baseline and document fine-tuning as an experiment/future step.

### Fallback E — Local multimodal inference is too slow

Use local text extraction as the reliable MVP and treat image extraction as optional.

The rule is:

> **A smaller working MVP beats a broader unfinished prototype.**

---

## 27. MVP vs Post-MVP

| Capability | MVP | Post-MVP |
|---|---:|---:|
| One real friend | ✓ | — |
| One workflow | ✓ | — |
| Text input | ✓ | — |
| Image input | Optional | ✓ |
| Local model | ✓ | ✓ |
| Fine-tuning | Optional | ✓ |
| Deterministic validation | ✓ | ✓ |
| Human approval | ✓ | ✓ |
| Typed agent actions | ✓ | ✓ |
| One browser target | ✓ | — |
| Multiple adapters | — | ✓ |
| Verification | ✓ | ✓ |
| Basic traces | ✓ | ✓ |
| Replay | — | ✓ |
| Developer API | Optional | ✓ |
| Multi-user auth | — | ✓ |
| General desktop automation | — | ✓ |
| Autonomous financial actions | — | Explicitly avoided |

---

## 28. MVP Acceptance Criteria

### AC-MVP-001 — Valid transaction

Given a valid supported input, EntryZero produces a structured record that passes validation.

### AC-MVP-002 — Review

The user can inspect the proposed record before execution.

### AC-MVP-003 — Edit

The user can modify extracted values before approval.

### AC-MVP-004 — Approval gate

No consequential target write occurs before explicit approval.

### AC-MVP-005 — Browser execution

After approval, the agent can enter the approved record into the selected target.

### AC-MVP-006 — Verification

After execution, EntryZero reads back the relevant target state and confirms the values match the approved record.

### AC-MVP-007 — Arithmetic protection

A deliberately inconsistent amount is rejected before writing.

### AC-MVP-008 — Missing-data protection

A required missing field prevents execution.

### AC-MVP-009 — Policy protection

A deliberately forbidden action is rejected by the harness.

### AC-MVP-010 — UI mismatch protection

A deliberately altered or unexpected target state causes a safe stop.

### AC-MVP-011 — Traceability

Every run produces a readable execution trace.

### AC-MVP-012 — Friend validation

The real friend tests or reviews the workflow and provides documented feedback.

---

## 29. Definition of Done

The EntryZero MVP is done when:

- [ ] One real friend and one real workflow are validated.
- [ ] One target application is selected.
- [ ] One P0 input path works.
- [ ] A local open model performs core extraction.
- [ ] Extracted output conforms to a strict schema.
- [ ] Deterministic validation works.
- [ ] User review works.
- [ ] Human approval is required before writes.
- [ ] Harness policies are enforced.
- [ ] Computer-use execution works.
- [ ] Target verification works.
- [ ] Incorrect data is blocked.
- [ ] Unexpected target state fails safely.
- [ ] Traces are recorded.
- [ ] At least one successful transaction is demonstrated.
- [ ] At least one deliberate failure is demonstrated.
- [ ] The MVP runs reproducibly from documented instructions.
- [ ] Friend feedback is captured.
- [ ] No private business data is exposed publicly without permission.
- [ ] Challenge requirements are satisfied.
- [ ] Scope remains limited to the defined MVP.

---

## 30. Evidence Required Before Calling It Viable

Do not declare the MVP successful merely because the happy path works once.

Collect evidence in three layers.

### Technical

- extraction outputs;
- validator results;
- agent traces;
- verification results;
- failure-case results.

### User

- friend confirms the problem is real;
- friend understands the approval model;
- friend can use/review the prototype;
- friend identifies whether the product removes actual work.

### Comparative

Where practical:

~~~text
manual workflow
vs
EntryZero workflow
~~~

Compare actual steps, corrections, latency, and successful completion.

This reflects the general MVP principle of using the product to test the core hypothesis and learn from real users rather than treating the first implementation as the final product.

---

## 31. Hypothesis and Evidence Table

| Hypothesis | Test | Evidence |
|---|---|---|
| Friend has a repetitive data-entry problem | Interview/observe | Actual workflow notes |
| Local model can extract needed fields | Held-out evaluation | Field/numeric accuracy |
| Validator catches important mistakes | Fault injection | Block/detection results |
| Friend is comfortable approving entries | User test | Feedback |
| Computer-use agent can perform the bounded UI task | Repeated browser tests | Completion rate |
| Harness can contain unsafe behavior | Policy/failure tests | Blocked actions |
| Verification catches incorrect writes | Fault injection | Detection rate |
| Open/local architecture is useful | Friend + technical evidence | Privacy/control/model-freedom evidence |

Update this table as evidence is collected.

---

## 32. What We Learn If the MVP Fails

A failed MVP is still useful if it identifies the bottleneck.

### Extraction fails

Likely learning:

> Local model quality is the limiting factor.

Potential next steps:

- improve dataset;
- narrow schema;
- fine-tune;
- change model.

### Computer use fails

Likely learning:

> The target interaction is too unconstrained.

Potential next steps:

- improve target adapter;
- reduce action space;
- improve target-state representation.

### Friend rejects the workflow

Likely learning:

> The product is solving the wrong problem or creating too much review friction.

Potential next steps:

- change workflow;
- simplify review;
- select a different task.

### Verification catches frequent failures

Likely learning:

> The computer-use path is not reliable enough for the target.

That is valid evidence and should be reported honestly.

---

## 33. Post-MVP Expansion Criteria

A capability should move from post-MVP into active development only when at least one is true:

1. The friend explicitly asks for it.
2. The current workflow repeatedly exposes the limitation.
3. Evaluation identifies it as a bottleneck.
4. It materially expands the number of similar workflows that can be supported without weakening safety.

This keeps EntryZero focused on evidence rather than speculative platform growth.

---

## 34. MVP Relationship to the "Agents API Killer" Positioning

The MVP is not attempting to recreate a general-purpose agent platform feature by feature.

It tests a narrower proposition:

~~~text
General-purpose agent
        ↓
maximum capability
~~~

versus:

~~~text
EntryZero
        ↓
minimum necessary capability
        +
maximum control
~~~

EntryZero tests whether:

~~~text
local model
+
typed tools
+
policy
+
human approval
+
deterministic validation
+
verification
~~~

is sufficient for a real, constrained business workflow.

The "Agents API killer" phrase is deliberately provocative. The actual engineering claim is narrower:

> **A focused open harness may be a better fit than a general-purpose cloud-first agent for a constrained workflow where safety, privacy, inspectability, and predictable behavior matter.**

That claim must be supported by the actual implementation and evaluation results.

---

## 35. Challenge Alignment

The official DEV challenge requires a **new project built during the challenge period**, with open-source AI at its core, solving a real problem for a friend or loved one, accompanied by a demo, source-code link, and an explanation of why open-source AI matters.

Source:
https://dev.to/page/hackertoberfest-weekend-challenge-26-10-01-contest-rules

For EntryZero, the MVP directly maps to those requirements:

| Challenge requirement | MVP evidence |
|---|---|
| New project | Repository/project created during challenge window |
| Open-source AI at core | Local open-weight model on critical path |
| Build for a Friend | One real friend and real workflow |
| Working demo | End-to-end verified transaction |
| Code | Public repository |
| Why open source matters | Local inference, privacy, model freedom, inspectability |
| Strong writing | PRD + MVP + final DEV write-up |
| Technical execution | Harness, validation, computer use, verification |

---

## 36. Final MVP Definition

> **EntryZero MVP is a local open-source, human-approved computer-use workflow for one real friend's repetitive business data-entry task. It accepts one supported input, extracts a strict record with a local model, validates it deterministically, waits for explicit approval, uses a constrained computer-use agent to enter the approved data into one target application, and verifies the resulting state.**

The MVP succeeds when it demonstrates:

~~~text
REAL FRIEND
    ↓
REAL PROBLEM
    ↓
LOCAL OPEN AI
    ↓
SAFE VALIDATION
    ↓
HUMAN APPROVAL
    ↓
COMPUTER USE
    ↓
VERIFICATION
    ↓
REAL FEEDBACK
~~~

The guiding rule:

> **Take away the typing. Keep the human in control.**

---

## 37. Change Log

### 2026-10-02

- Initial MVP specification created.
- Scope reduced to one friend, one real workflow, one primary input, and one browser target.
- Core hypothesis made explicit.
- Added vertical-slice definition.
- Added P0/P1/P2 scope boundaries.
- Added deterministic validation and mandatory approval.
- Added constrained computer-use execution.
- Added post-action verification.
- Added deliberate failure testing.
- Added measurable technical, user, safety, and comparative evidence.
- Added fallback strategy for hackathon time/resource constraints.
- Added fine-tuning decision gate.
- Added challenge-alignment section.
