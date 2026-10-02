# EntryZero — Deterministic Validation

## Purpose

Validation is the deterministic barrier between AI interpretation and business-data authorization.

It answers:

> **Is this structured record internally consistent and acceptable for the selected workflow?**

It does not attempt to decide whether a record merely "looks plausible".

## Pipeline

~~~text
Model output
   |
Schema validation
   |
Normalization
   |
Business rules
   |
Arithmetic checks
   |
Duplicate checks
   |
ValidationResult
~~~

## Validation result

~~~json
{
  "status": "passed",
  "errors": [],
  "warnings": [],
  "checks": [
    {
      "name": "total_matches_subtotal_plus_tax",
      "status": "passed"
    }
  ]
}
~~~

Possible statuses:

- passed;
- warning;
- failed.

A failed result blocks execution.

## Rule categories

### Schema

- required fields;
- types;
- formats;
- allowed values.

### Numeric

- valid quantity;
- valid monetary value;
- allowed sign;
- precision.

### Arithmetic

Where the source contains sufficient information:

~~~text
quantity * unit_price = line_total
sum(line_totals) = subtotal
subtotal + tax = total
~~~

Use decimal arithmetic.

### Date

Check calendar validity and any workflow-specific date constraints.

Do not invent missing dates.

### Duplicate

When a stable identifier exists:

~~~text
candidate identifier
      |
search target
      |
existing?
 /     \
yes     no
 |       |
block  continue
~~~

### Cross-field

Examples:

- tax rate and tax amount are compatible;
- line totals reconcile with subtotal;
- currency matches target;
- required fields occur together.

## Severity

### ERROR

Blocks execution.

### WARNING

Requires visible user review and an explicit decision if the workflow permits continuation.

### INFO

Context only.

## User correction

Return field-level messages when possible.

Bad:

> Validation failed.

Better:

> Total is INR 1,800 but the supplied quantity and unit price imply INR 2,000.

## Deterministic boundary

Never replace ordinary arithmetic or schema checks with a second LLM call.

The model interprets. The validator enforces invariants.

## Required test fixtures

Include:

- valid record;
- missing field;
- invalid type;
- arithmetic mismatch;
- tax mismatch;
- invalid negative;
- malformed date;
- duplicate identifier;
- ambiguous value;
- corrected valid record.
