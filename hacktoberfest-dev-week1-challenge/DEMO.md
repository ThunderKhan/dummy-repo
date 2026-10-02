# EntryZero — Demo Script

## Demo goal

Explain the problem through the friend first, then use the technical demo to prove the architecture.

The audience should understand the product before they understand the model.

## Scene 1 — The friend

Show the real workflow or a consented anonymized reconstruction.

Narrative:

> "My friend already has this information. The repetitive part is typing it into the system they already use."

Show:

~~~text
message
→ read
→ switch application
→ find destination
→ type fields
→ check result
~~~

## Scene 2 — EntryZero input

Provide one realistic input.

Preferred primary demo:

- a messy business text message.

Stretch:

- photo/document input.

## Scene 3 — Local extraction

Show:

- local model indicator;
- structured output;
- uncertainty if present.

Do not claim perfect understanding.

## Scene 4 — Deterministic validation

Show the exact checks.

Then demonstrate a bad record:

~~~text
quantity = 4
unit price = 500
reported total = 1800
~~~

Expected:

~~~text
4 * 500 = 2000

BLOCKED
~~~

State clearly:

> "The model is allowed to misunderstand. The validator prevents that misunderstanding from becoming a write."

## Scene 5 — Human approval

Return to a valid record.

Show:

~~~text
REVIEW
[EDIT]
[APPROVE]
~~~

Say:

> "The agent has no permission to make the consequential edit until the friend approves this exact transaction."

## Scene 6 — Harness

Show:

- current state;
- allowed action class;
- transaction ID/version;
- remaining budget;
- trace.

The purpose is to make the control layer visible.

## Scene 7 — Computer use

Show the agent:

~~~text
OBSERVE
→ FIND DESTINATION
→ TYPE APPROVED VALUES
→ READ BACK
~~~

## Scene 8 — Verification

Show:

~~~text
APPROVED RECORD
        ==
TARGET STATE

VERIFIED
~~~

## Scene 9 — UI failure

If reliable, deliberately alter the target state or present an unrecognized control.

Expected:

> "The harness cannot establish that the target is safe, so it stops."

Do not fake a failure that bypasses the actual code.

## Scene 10 — Open-source thesis

Explain:

- local inference;
- model freedom;
- fine-tuning;
- inspectable policy;
- inspectable validation;
- inspectable traces;
- open target adapters.

## Final line

> **"We did not build an AI that replaces the business owner. We built an open agent that takes away the typing and leaves the decision with them."**

## Demo rules

Never:

- expose private credentials;
- show private customer data without permission;
- manually edit the target after the agent run;
- hide failed runs;
- quote unmeasured performance;
- rely on network-dependent services in a supposedly local-only step without disclosing them.
