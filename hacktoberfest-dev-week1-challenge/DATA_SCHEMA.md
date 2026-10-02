# EntryZero — Data Schema

## Purpose

The schema is the contract between probabilistic extraction and deterministic business logic.

The model proposes structured data. The application validates, versions, approves, executes, and verifies that data.

## Canonical transaction

~~~json
{
  "run_id": "run_123",
  "version": 1,
  "goal": "enter_business_record",
  "source": {
    "type": "text",
    "content_ref": "local://input/123"
  },
  "record": {
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
    "subtotal": 1120,
    "tax_rate": 0.18,
    "tax": 201.60,
    "total": 1321.60,
    "currency": "INR"
  }
}
~~~

The exact business fields are provisional until the friend's workflow is observed.

## Schema rules

### Required vs optional

Required fields come from the real target workflow.

Do not copy a generic invoice schema into production logic without validating it against the friend.

### Unknown values

Unknown values must remain unknown.

Do not replace uncertainty with:

- guessed customer identities;
- guessed invoice numbers;
- guessed dates;
- guessed prices;
- guessed taxes.

### Money

Use decimal-safe numeric representation.

Binary floating-point arithmetic must not be the source of truth for financial checks.

### Currency

Store currency explicitly.

Do not silently convert currencies in the MVP.

### Dates

Use a stable internal representation such as:

~~~text
YYYY-MM-DD
~~~

Display formatting can be adapted to the target.

## Versioning

Example:

~~~text
v1 = model extraction
v2 = human correction
v3 = further correction
~~~

Approval binds to one version.

Any edit after approval invalidates the previous approval.

## Extraction result

The extraction adapter should ideally return:

~~~json
{
  "record": {},
  "uncertain_fields": [],
  "missing_required_fields": [],
  "extraction_notes": []
}
~~~

The application should create a canonical transaction only after schema validation.

## Source separation

Raw source content is not part of the executable instruction set.

Keep it separate from the canonical record and treat it as untrusted data.

## Schema evolution

Every schema change should state:

- why it changed;
- which validators change;
- which adapters change;
- which fixtures change;
- whether previous data remains compatible.

Schema changes must not silently reinterpret existing transaction meaning.
