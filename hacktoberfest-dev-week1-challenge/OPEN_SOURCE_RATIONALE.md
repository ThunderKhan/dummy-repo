# EntryZero — Why Open Source Matters

## Thesis

Open source is a product property in EntryZero, not a label placed on a closed application.

The project needs an architecture where the user can control the model, inference path, policy layer, and verification behavior.

## Local inference

The core extraction workflow should be able to run locally.

This can keep sensitive business inputs out of a hosted-model request.

The precise claim is:

> **Core AI inference can be local-first.**

It is not:

> "The whole system is offline."

A browser-based business target may still require network access.

## Model freedom

The harness should not be coupled to one model provider.

A compatible open model should be replaceable without rewriting:

- validation;
- policy;
- approval;
- verification;
- target adapters.

## Fine-tuning

Open models make it possible to adapt extraction to the friend's actual terminology and message style.

This can be evaluated rather than assumed.

## Inspectability

A developer can inspect:

- tool definitions;
- state machine;
- authorization logic;
- validation;
- target adapter;
- verification;
- traces.

This is important for a system that can modify business records.

## Cost

Local inference can remove an inherent per-request hosted-model dependency.

Do not claim that local inference is always cheaper. Hardware, power, setup, maintenance, and engineering time have costs.

## Forkability

Another developer can adapt EntryZero for:

- another open model;
- another business workflow;
- another spreadsheet;
- another policy.

## Security is still required

Open source does not make the system trustworthy by itself.

The system still needs:

- least privilege;
- deterministic validation;
- explicit approval;
- verification;
- safe defaults.

## Challenge-facing explanation

The useful answer to:

> "Why not just call a hosted AI API?"

is:

> "Because local, inspectable AI is part of the solution. The business owner can keep the core interpretation step close to their data, swap models, adapt the model to their workflow, and inspect the code that controls what the AI is allowed to do."

Any claim about actual cost, accuracy, or privacy must be backed by project measurements or clearly marked as a design property.
