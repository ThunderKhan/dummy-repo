# Contributing to EntryZero

EntryZero is intentionally small. Contributions should improve the real workflow or strengthen the safety and reproducibility of the system.

## Start here

Read:

1. PRD.md
2. MVP.md
3. architecture.md
4. AGENT_POLICY.md
5. SECURITY.md

## Useful contribution areas

Good contributions include:

- deterministic validators;
- regression tests;
- model adapters;
- target adapters;
- evaluation tooling;
- trace improvements;
- reproducibility fixes;
- documentation improvements.

## High-scrutiny changes

Changes affecting:

- permissions;
- approval;
- tool definitions;
- verification;
- credentials;
- target scope;
- logging of sensitive values;

should include tests that demonstrate the relevant invariant.

## Contribution principles

- Keep changes focused.
- Prefer deterministic controls over prompt-only fixes.
- Add regression tests for bugs.
- Do not commit private business data.
- Do not expose credentials.
- Do not add dependencies without a concrete reason.
- Do not expand the MVP without evidence.

## Pull requests

A useful PR should explain:

- what changed;
- why;
- which requirement it addresses;
- how it was tested;
- what risk it introduces.

For behavior changes, include examples or measured results where useful.

## Security-sensitive reports

Do not publish credentials or private customer information in public issues.

For an exploitable security issue, contact the maintainer privately when possible and include reproduction information without exposing real secrets.

## Third-party components

Preserve required model/library notices and licenses.

## Scope

The goal is not to turn EntryZero into a huge autonomous platform during the challenge.

The strongest contribution is the one that makes the constrained workflow more correct, more observable, safer, or easier to reproduce.
