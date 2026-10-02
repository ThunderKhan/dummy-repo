# EntryZero — Computer Use

## Purpose

The computer-use subsystem turns an approved transaction into constrained browser actions.

It is not a general desktop-control system.

## Context given to the model

The computer-use model receives:

- current browser state;
- approved goal;
- approved record;
- available action types;
- target-specific context.

It returns one proposed action.

~~~text
browser state
+
approved transaction
+
allowed actions
       |
       v
computer-use model
       |
       v
typed action proposal
~~~

## Browser state

Prefer structured accessibility/page state over raw screenshots when the target exposes it.

Playwright provides accessibility snapshots with element references. Those references are useful for targeted interactions, but they can become invalid when page state changes.

Sources:
- https://playwright.dev/agent-cli/snapshots
- https://playwright.dev/mcp/snapshots

## Action format

~~~json
{
  "op": "TYPE",
  "target_ref": "e42",
  "value": "INV-1042"
}
~~~

The harness validates the object before execution.

## Interaction loop

~~~text
OBSERVE
   |
DECIDE
   |
POLICY CHECK
   |
PRECONDITION CHECK
   |
EXECUTE
   |
POSTCONDITION CHECK
   |
TRACE
   |
DONE? ---- no ----> OBSERVE
   |
  yes
   |
VERIFY TRANSACTION
~~~

## Targeting hierarchy

1. fresh accessibility/page state references;
2. semantic locators;
3. deterministic adapter locators;
4. visual/screenshot reasoning only where necessary.

Avoid coordinate-based clicking in the core MVP when structured state is available.

## State freshness

Rule:

> **After navigation or a meaningful page mutation, reacquire browser state before using element references from the previous state.**

## Credentials

The agent operates within an authenticated browser session.

Credentials, cookies, access tokens, and passwords must not be placed into model-visible context.

## Action limits

The harness enforces:

- maximum actions;
- maximum replans;
- maximum runtime;
- optional navigation depth.

A loop is a failure condition.

## Failure behavior

### Wrong target

Stop.

### Stale reference

Re-observe; do not blindly retry the stale reference.

### Unrecognized field

Stop or request user intervention.

### Unexpected dialog

Handle only if it is part of the known workflow; otherwise stop.

## Completion

The computer-use agent cannot declare the business transaction successful.

Only the verification engine can transition a run to COMPLETED.
