# EntryZero — Threat Model

## Scope

~~~text
untrusted input
→ local extraction
→ validation
→ human approval
→ computer-use model
→ browser target
→ verification
~~~

## Protected assets

- business records;
- transaction integrity;
- approval authority;
- target application state;
- browser session;
- credentials;
- execution traces.

## Threat categories

### T-001 — Prompt injection in source content

**Attack:** a message, document, or image contains text intended to redirect the agent.

**Impact:** unauthorized action proposal.

**Controls:**
- source/data separation;
- strict extraction schema;
- typed actions;
- policy engine;
- human approval;
- blocked destructive operations.

### T-002 — Excessive tool permissions

**Attack:** the agent receives capabilities that are not necessary.

**Impact:** larger blast radius.

**Controls:**
- minimal tool registry;
- no shell;
- no arbitrary external request tool;
- transaction-scoped capabilities.

### T-003 — Extraction error

**Attack/failure:** model misreads amount, quantity, date, or identifier.

**Impact:** incorrect business record.

**Controls:**
- schema validation;
- deterministic rules;
- human review;
- target verification.

### T-004 — Wrong destination

**Attack/failure:** agent writes approved data into the wrong row or form.

**Impact:** record corruption.

**Controls:**
- explicit destination state;
- preconditions;
- action trace;
- final verification.

### T-005 — Duplicate transaction

**Attack/failure:** retry repeats a completed transaction.

**Impact:** duplicate record.

**Controls:**
- stable identifier check;
- idempotency key where possible;
- bounded retries.

### T-006 — Stale approval

**Attack:** approved data changes and old approval remains valid.

**Impact:** unauthorized data write.

**Controls:**
- transaction versioning;
- approval integrity marker;
- approval invalidation after edits.

### T-007 — UI drift

**Attack/failure:** target UI changes.

**Impact:** action applied to the wrong element.

**Controls:**
- fresh browser state;
- target adapter;
- preconditions;
- fail closed.

### T-008 — Agent loop

**Attack/failure:** model repeatedly acts without progress.

**Impact:** repeated or excessive operations.

**Controls:**
- action budget;
- replan budget;
- runtime timeout;
- terminal states.

### T-009 — Sensitive trace leakage

**Attack:** logs expose private records.

**Impact:** confidentiality loss.

**Controls:**
- redaction;
- local storage;
- minimal payloads;
- synthetic public fixtures.

## Priority

| Threat | Impact | MVP control priority |
|---|---|---|
| Incorrect financial value | High | P0 |
| Wrong destination | High | P0 |
| Excessive permission | Critical | P0 |
| Prompt injection | High | P0 |
| Duplicate write | High | P0 |
| UI drift | High | P0 |
| Runaway loop | Medium/High | P0 |
| Sensitive logging | Critical | P0 |

These are engineering priorities, not empirical likelihood estimates.

## Security test rule

Each P0 threat must have at least one repeatable regression test.
