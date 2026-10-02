# EntryZero — Fine-Tuning Plan

## Objective

Fine-tune a local open model only where customization materially improves the friend's actual workflow.

Preferred target:

> **messy business input -> strict structured transaction**

## Why extraction first?

Extraction is:

- narrower;
- easier to score;
- closer to the friend;
- independent of browser UI changes;
- safer to iterate.

The validator and harness remain unchanged.

## Training data

Before training, define:

- input format;
- canonical output schema;
- annotation rules;
- train/validation/test splits;
- ambiguity policy;
- anonymization.

See DATASET.md.

## Training approach

Prefer parameter-efficient methods such as LoRA/QLoRA when supported by the chosen model and available hardware.

Record:

- base model;
- training method;
- dataset version;
- hyperparameters;
- hardware;
- random seed where relevant;
- resulting adapter/checkpoint identifier.

## Example

Input:

~~~text
rahul traders 4 a4 packs 280 each gst 18
~~~

Target:

~~~json
{
  "customer": "Rahul Traders",
  "item": "A4",
  "quantity": 4,
  "unit_price": 280,
  "tax_rate": 0.18
}
~~~

The example is illustrative until the friend's actual schema is known.

## Evaluation

Compare:

~~~text
BASE MODEL
vs
FINE-TUNED MODEL
~~~

on a held-out set that was not used for training decisions.

Metrics:

- field accuracy;
- numeric accuracy;
- schema validity;
- missing-field detection;
- human correction rate;
- latency/resource use.

## Ship gate

Fine-tuning is included in the MVP only if:

1. the baseline path is already working;
2. the dataset is adequate;
3. training completes reliably;
4. held-out results improve;
5. the improvement matters to the workflow.

Otherwise the baseline model remains the shipped model.

## Leakage prevention

Never:

- train on the test split;
- publish private business records;
- use production credentials as training data;
- create near-duplicate test examples that make evaluation trivial.

## References

- Gemma tuning: https://ai.google.dev/gemma/docs/tune
- Gemma cookbook: https://github.com/google-gemma/cookbook
