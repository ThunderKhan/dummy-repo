# EntryZero — Agent Policy

## Purpose

This document defines what the computer-use agent may and may not do.

The policy engine is deterministic enforcement. The model is never trusted to enforce its own permissions.

## Tool registry

| Tool | Meaning | Default authorization |
|---|---|---|
| OBSERVE | Read current target state | Allowed |
| READ | Read target content | Allowed |
| CLICK | Click an approved UI element | Policy + scope |
| TYPE | Enter an approved value | Approval required |
| SELECT | Choose an approved option | Approval if state changes |
| SCROLL | Move viewport | Allowed |
| WAIT | Wait for expected state | Allowed |
| DONE | End action sequence | Allowed |

The MVP provides no shell command tool, arbitrary JavaScript tool, or unrestricted URL-fetch tool.

## Action classes

### Observation

Low-side-effect actions such as observe and read.

### Navigation

Actions such as scroll or navigating within the approved target scope.

### Data modification

Actions such as typing or changing a selected value.

These require transaction approval.

### Destructive or irreversible

Delete, payment, external message, or unrelated account changes.

These are blocked by default.

## Authorization pipeline

~~~text
Model proposal
     |
     v
Schema check
     |
     v
Capability check
     |
     v
Target-scope check
     |
     v
Approval check
     |
     v
Precondition check
     |
     v
ALLOW / BLOCK
~~~

## Target scope

Each action must identify:

- the active run;
- the configured application;
- an allowed resource;
- an allowed operation;
- an approved transaction version when the action changes data.

## Approval invalidation

If the user edits an approved transaction:

~~~text
old approval -> INVALID
new transaction version -> NEW APPROVAL REQUIRED
~~~

## Fail-closed rules

Block when:

- a tool is not registered;
- the target is out of scope;
- approval is missing;
- capability has expired;
- preconditions fail;
- action budget is exhausted;
- target state is ambiguous.

## Policy invariants

1. Model output cannot override policy.
2. A forbidden operation cannot execute even if the model requests it repeatedly.
3. Approval does not grant permissions outside the approved transaction.
4. Completion cannot bypass verification.

## Required policy tests

The automated suite must prove:

- unapproved TYPE is blocked;
- DELETE is blocked;
- another target is blocked;
- stale approval is blocked;
- over-budget execution is blocked;
- malformed actions are blocked.

## Security basis

OWASP identifies excessive functionality, permissions, and autonomy as key causes of excessive agency and recommends granular tools, minimum permissions, downstream authorization, and human approval.

Source:
https://genai.owasp.org/llmrisk/llm062025-excessive-agency/
