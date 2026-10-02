# EntryZero — Dataset Specification

## Purpose

The dataset supports model extraction and evaluation of the real friend workflow without exposing unnecessary private data.

## Dataset layers

### Private source examples

Real examples observed with permission.

Stored locally and not committed by default.

### Anonymized examples

Business structure retained while identifying information is replaced.

Example:

~~~text
Rahul Traders -> CUSTOMER_A
INV-1042 -> INV-XXXX
~~~

### Synthetic examples

Publicly safe examples generated from observed workflow patterns and edge cases.

## Example schema

~~~json
{
  "id": "ex_001",
  "input_type": "text",
  "input": "...",
  "target": {
    "customer": "...",
    "invoice_id": "...",
    "items": []
  },
  "tags": [
    "normal",
    "messy"
  ]
}
~~~

## Categories

Include examples for:

1. normal valid input;
2. abbreviations;
3. spelling variation;
4. missing required field;
5. missing optional field;
6. arithmetic inconsistency;
7. ambiguous price/quantity;
8. duplicate candidate;
9. mixed formatting;
10. source-content prompt injection.

## Splits

Maintain:

- train;
- validation;
- test.

The test set must remain untouched during tuning.

Avoid near-duplicate examples across splits.

## Annotation rules

Annotators should:

- preserve ambiguity;
- never invent missing values;
- use the canonical schema;
- record uncertainty;
- separate data from instructions.

## Privacy review

Before any example becomes public:

- remove identifying information;
- remove account numbers;
- remove addresses;
- remove phone numbers;
- remove credentials;
- verify permission/consent;
- review metadata and filenames.

## Versioning

Every dataset change receives a version.

Example:

~~~text
dataset-v0.1
dataset-v0.2
~~~

Evaluation reports must state the dataset version.

## Dataset size

The MVP does not require a huge corpus.

A small, carefully curated set representing the friend's actual input style is more useful than an arbitrarily large dataset that does not reflect the workflow.

The final report should publish the actual dataset size and composition.
