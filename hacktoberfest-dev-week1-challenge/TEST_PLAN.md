# EntryZero — Test Plan

## Objective

The test plan protects the most important invariant:

> **AI failure must not silently become an incorrect business write.**

## Test pyramid

### Unit

Test pure logic:

- schemas;
- arithmetic;
- date rules;
- duplicate checks;
- capabilities;
- policy;
- approval invalidation;
- state transitions;
- budgets.

### Integration

Test:

- extraction to canonical record;
- record to validator;
- approval to harness;
- harness to adapter;
- adapter to verification.

### Browser

Use a controlled local target or isolated test account.

Test:

- destination discovery;
- correct row selection;
- field entry;
- stale references;
- unexpected dialogs;
- UI changes;
- save behavior;
- read-back verification.

### End to end

Run:

~~~text
input
→ extraction
→ validation
→ review
→ approval
→ computer use
→ verification
~~~

## Safety regression suite

Required cases:

1. unapproved write;
2. delete request;
3. wrong target;
4. wrong row;
5. arithmetic mismatch;
6. missing required field;
7. duplicate record;
8. stale approval;
9. prompt injection;
10. action budget exceeded;
11. verification mismatch.

Expected result:

> No unauthorized business write.

## Property-style invariants

Where practical, test that:

- identical canonical input produces deterministic validation;
- editing an approved transaction invalidates the approval;
- blocked actions cannot reach the driver;
- completion requires verification;
- budgets are monotonic and cannot be reset by model output.

## Browser-state tests

Playwright provides accessibility snapshots that can be asserted at the structural level, while ordinary assertions are better for exact cell values.

Source:
https://playwright.dev/docs/aria-snapshots

## Test data

Use synthetic or anonymized fixtures.

Real customer/business data is not required for automated tests.

## Pass criteria

### Happy path

A valid run passes only if:

- extraction is schema-valid;
- validation passes;
- approval is explicit;
- actions are authorized;
- target state changes correctly;
- verification passes.

### Safety path

A failure test passes only if:

- the unsafe action is blocked or stopped;
- no unauthorized write occurs;
- the trace identifies the failure;
- the final state is non-completed.

## CI minimum

Before submission, aim for:

- unit tests;
- validator tests;
- policy tests;
- browser smoke test;
- end-to-end success path;
- end-to-end failure path.
