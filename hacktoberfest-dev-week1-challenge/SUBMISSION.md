# EntryZero — Hackathon Submission Plan

## Purpose

This is the final submission checklist for the Hacktoberfest DEV Weekend Challenge.

Challenge:
https://dev.to/challenges/hacktoberfest-weekend-2026-10-01

Rules:
https://dev.to/page/hacktoberfest-weekend-challenge-26-10-01-contest-rules

## Story structure

The submission should follow:

~~~text
REAL FRIEND
    ↓
REAL REPETITIVE TASK
    ↓
WHY THE CURRENT WORKFLOW HURTS
    ↓
ENTRYZERO
    ↓
LOCAL OPEN AI
    ↓
VALIDATION
    ↓
HUMAN APPROVAL
    ↓
COMPUTER USE
    ↓
VERIFICATION
    ↓
FRIEND FEEDBACK
~~~

## Opening

Start with the person, not the framework.

Template:

> "My friend runs [real business/activity]. I noticed they repeatedly [actual task]. The data already existed; the tedious part was moving it into [actual application]."

Then introduce the constraint:

> "Because these are business records, I did not want a general AI to have unrestricted permission to change them."

Then introduce EntryZero.

## Technical framing

Use the "Agents API killer" angle as a question or thesis rather than a feature-parity claim:

> **"What if the right agent runtime for one consequential workflow did not need to be general-purpose?"**

Then explain:

~~~text
open local model
+
deterministic validation
+
transaction-scoped approval
+
typed computer use
+
verification
~~~

## Evidence package

Prepare:

- public repository;
- concise README;
- architecture diagram;
- working demo;
- friend story;
- evaluation results;
- deliberate failure demonstration;
- friend feedback;
- model/license attribution.

## Friend evidence

Before publishing:

- [ ] real friend confirmed;
- [ ] real workflow observed;
- [ ] permission obtained for story;
- [ ] public examples anonymized;
- [ ] friend tested/reviewed prototype;
- [ ] feedback recorded.

## Open-source evidence

Document specifically:

- what model is open/local;
- what runs locally;
- which components are replaceable;
- what can be fine-tuned;
- what policies are inspectable;
- what verification is open.

## Partner categories

Only claim a partner category when the technology is genuinely integrated and used.

Possible candidates:

- Gemma for local/open extraction;
- Tinker for fine-tuning if used;
- Sentry Agent Tracing if materially used;
- Temporal only if durable execution is actually part of the shipped workflow.

Do not add integrations solely to increase the technology list.

## Claims discipline

Before publishing every quantitative or comparative statement, classify it:

- observed;
- measured;
- design property;
- future intention.

Do not present a single friend's experience as market research.

Do not present a safety intention as a safety guarantee.

Do not claim benchmark improvements without a test set.

## Final checklist

- [ ] Project created during challenge window.
- [ ] Open-source AI is core.
- [ ] One real friend is central.
- [ ] P0 end-to-end path works.
- [ ] Human approval works.
- [ ] Failure path works.
- [ ] Verification works.
- [ ] Evaluation is documented.
- [ ] Source code is public.
- [ ] README and docs link together.
- [ ] No private data is exposed.
- [ ] Submission describes the implementation that actually exists.
