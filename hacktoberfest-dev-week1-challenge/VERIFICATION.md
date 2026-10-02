# EntryZero — Verification

## Purpose

Verification closes the loop between intended action and actual application state.

A successful browser command is not a successful business operation.

The system must answer:

> **Did the target application end in the state corresponding to the exact transaction the user approved?**

## Verification levels

### Level 1 — Action verification

After a consequential action, read back the affected control.

Example:

~~~text
TYPE INV-1042
       |
READ FIELD
       |
value == INV-1042
~~~

### Level 2 — Record verification

Compare all approved business fields against the target record.

### Level 3 — Workflow verification

Confirm the expected workflow state:

- correct row/form;
- expected record exists;
- expected values are present;
- save/commit succeeded where applicable;
- no unexpected error state remains.

Only Level 3 may produce COMPLETED.

## Preconditions

Before execution verify:

- correct target application;
- correct resource;
- correct destination;
- current transaction version;
- valid approval;
- required target controls are present.

## Postconditions

After a data-changing action, verify the expected local state where practical.

If a postcondition fails:

~~~text
STOP
TRACE FAILURE
DO NOT GUESS
~~~

## Final comparison

Compare:

- customer/entity;
- identifier;
- date;
- line items;
- quantities;
- amounts;
- tax;
- currency;
- target-specific status.

## Mismatch result

~~~json
{
  "status": "failed",
  "checks": [
    {
      "field": "total",
      "expected": "5664.00",
      "actual": "5604.00",
      "status": "failed"
    }
  ]
}
~~~

The UI should explain the mismatch in user-readable language.

## Fault injection

Test verification by deliberately producing:

- wrong row;
- wrong amount;
- missing field;
- changed value;
- save failure;
- duplicate;
- UI change.

## False completion

Track:

> **false completion count**

A false completion occurs when EntryZero reports success although the approved transaction was not actually achieved.

For the tested evaluation suite, the goal is zero known false completions.

This is a test target, not a production guarantee.

## Why verification is first-class

The agent can make a mistake.

The system must make that mistake visible before claiming success.

That distinction is central to EntryZero's architecture.
