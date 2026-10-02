# EntryZero — Agent Harness

## Purpose

The harness is the reusable control layer around the AI components.

Its job is not to make the model smarter. Its job is to make agent behavior bounded, inspectable, interruptible, and verifiable.

## Responsibilities

The harness owns:

1. run lifecycle;
2. canonical transaction;
3. authorization state;
4. policy;
5. tool registry;
6. action budget;
7. retry budget;
8. target scope;
9. preconditions;
10. postconditions;
11. trace;
12. recovery;
13. completion status.

## State machine

~~~text
RECEIVED
   |
EXTRACTING
   |
VALIDATING
   |
REVIEW_REQUIRED
   |
APPROVED
   |
PREPARING
   |
EXECUTING
   |
VERIFYING
   |
COMPLETED
~~~

Interruption/terminal states:

~~~text
REJECTED
BLOCKED
STOPPED
FAILED
VERIFICATION_FAILED
WAITING_FOR_INPUT
WAITING_FOR_APPROVAL
~~~

## Control loop

~~~text
observe state
    |
determine safe phase
    |
obtain model proposal
    |
policy check
    |
precondition check
    |
execute typed action
    |
postcondition check
    |
trace
    |
continue / verify / stop
~~~

## Transaction-scoped authorization

Approval should bind to:

- run identifier;
- transaction version;
- target;
- allowed operation class;
- approved-record integrity marker;
- approval timestamp.

Any edit to approved business data invalidates the existing authorization.

## Capability model

Prefer:

~~~text
write:
  target = spreadsheet
  transaction = run_123
  fields = customer, invoice_id, amount
  duration = current run
~~~

over a global permission such as "agent can edit spreadsheet".

## Budgets

Example starting values:

~~~yaml
max_actions: 30
max_replans: 2
max_run_seconds: 180
max_navigation_steps: 10
~~~

These are configurable starting values, not production guarantees.

## Recovery

Safe recovery may include:

- re-observe browser state;
- retry one idempotent action;
- ask the user;
- stop.

Unsafe recovery includes:

- guessing;
- broadening permissions;
- selecting unrelated records;
- bypassing approval;
- arbitrary shell commands.

## Completion invariant

A run can become COMPLETED only if:

1. the transaction was approved;
2. all actions stayed within policy;
3. the intended state was reached;
4. final verification passed;
5. the trace was persisted.

## Security basis

OWASP's Excessive Agency guidance recommends minimizing tool functionality, permissions, and autonomy and using human approval for high-impact actions.

Source:
https://genai.owasp.org/llmrisk/llm062025-excessive-agency/
