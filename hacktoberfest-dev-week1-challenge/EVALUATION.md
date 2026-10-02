# EntryZero — Evaluation Plan

## Purpose

Evaluation must answer whether the system works, where it fails, and whether the harness changes outcomes.

The primary unit of success is:

> **Verified transaction completion.**

Not raw model accuracy.

## Evaluation layers

### 1. Extraction

Questions:

- Did the model extract the correct fields?
- Did it preserve uncertainty?
- Did it produce valid structured output?

Metrics:

- field accuracy;
- numeric accuracy;
- schema-valid output rate;
- missing-field detection;
- human correction rate.

### 2. Validation

Questions:

- Does deterministic validation catch injected errors?
- Does it reject malformed records?
- Does it avoid rejecting valid records?

Metrics:

- error detection rate;
- false acceptance rate;
- false rejection rate.

### 3. Computer use

Questions:

- Can the agent find the correct target?
- Can it complete the bounded workflow?
- Does it stay within the permitted action set?

Metrics:

- task completion rate;
- action accuracy;
- unexpected-action rate;
- average actions/run;
- latency.

### 4. Verification

Questions:

- Does the system detect incorrect writes?
- Does it avoid claiming success after partial failure?

Metrics:

- verification pass rate;
- mismatch detection rate;
- false completion count.

### 5. End to end

Primary:

> **Verified transaction completion rate.**

Secondary:

- median end-to-end latency;
- manual corrections;
- manual steps remaining;
- failed-run categories.

## Baselines

Where useful, compare:

1. baseline local extraction model;
2. fine-tuned extraction model;
3. harnessed execution;
4. any deliberately simplified unsafe baseline used only on synthetic/local targets.

Never disable safeguards against a real friend's records merely to produce a benchmark.

## Test matrix

| Scenario | Expected result |
|---|---|
| Valid record | Complete |
| Messy valid record | Complete if understood |
| Missing required value | Review/block |
| Arithmetic mismatch | Block |
| Duplicate identifier | Warn/block |
| User correction | Complete |
| Wrong row | Verification failure |
| UI drift | Stop |
| Forbidden action | Policy block |
| Prompt injection | No unauthorized action |
| Runaway loop | Budget stop |

## Human evaluation

The friend should evaluate:

- usefulness;
- clarity;
- trust;
- correction workflow;
- approval burden;
- perceived risk;
- willingness to reuse.

Do not generalize one person's feedback to an entire market.

## Reporting standard

Every metric must identify:

- dataset/version;
- model/version;
- configuration;
- test count;
- environment when relevant;
- whether data was synthetic, anonymized, or real.

Do not report a single best number without describing the denominator.

## Failure analysis

Every failed run should be assigned a primary cause:

- extraction;
- schema;
- validation;
- target mapping;
- computer-use decision;
- browser execution;
- verification;
- user interaction.

A useful evaluation explains **why** the system failed.

## Result template

| Metric | Baseline | Improved | Notes |
|---|---:|---:|---|
| Field accuracy | TODO | TODO | TODO |
| Numeric accuracy | TODO | TODO | TODO |
| Schema-valid rate | TODO | TODO | TODO |
| Task completion | TODO | TODO | TODO |
| Verification pass rate | TODO | TODO | TODO |
| Human correction rate | TODO | TODO | TODO |
