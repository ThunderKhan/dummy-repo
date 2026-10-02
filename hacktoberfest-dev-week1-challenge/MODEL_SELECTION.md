# EntryZero — Model Selection

## Objective

Select models based on the real workflow, available hardware, measurable task performance, and licensing.

Popularity is not a selection criterion.

## Two-model architecture

EntryZero separates:

### Extraction model

Input:

~~~text
text / image / document
~~~

Output:

~~~text
structured business record
~~~

### Computer-use model

Input:

~~~text
browser state
+
approved goal
+
allowed actions
~~~

Output:

~~~text
typed next action
~~~

A single model is not required.

## Extraction criteria

Evaluate:

- field accuracy;
- numeric accuracy;
- schema-valid output rate;
- ambiguity handling;
- image capability where required;
- local inference speed;
- memory/VRAM;
- fine-tuning support;
- license;
- reproducibility.

Gemma is a natural candidate because the project explicitly values open/local model execution, but the implementation must keep the model replaceable.

Source:
https://ai.google.dev/gemma/docs

## Computer-use criteria

Evaluate:

- action selection accuracy;
- element targeting;
- handling of fresh browser state;
- local resource requirements;
- latency;
- robustness across repeated runs.

A Laya-style model is a natural candidate because its task maps well to typed browser operations.

Source:
https://github.com/ChenneyZhuang/laya-browser-agent/

## Selection protocol

1. Define a fixed test set.
2. Run baseline candidates on identical examples.
3. Measure performance and resources.
4. Run stress tests.
5. Evaluate the full end-to-end path.
6. Record the decision.

## Model record

| Role | Candidate | Dataset | Result | Decision |
|---|---|---|---|---|
| Extraction | Gemma candidate | TODO | TODO | TODO |
| Extraction | Alternative | TODO | TODO | TODO |
| Computer use | Laya-style | TODO | TODO | TODO |
| Computer use | Alternative | TODO | TODO | TODO |

## Reporting

Avoid unsupported statements such as:

> "Model X is the best."

Prefer:

> "Model X met our MVP requirements on the tested evaluation set."

If results are inconclusive, say so.

## Fine-tuning

Fine-tuning is considered separately from selection.

See:
- FINE_TUNING.md
- DATASET.md
- EVALUATION.md
