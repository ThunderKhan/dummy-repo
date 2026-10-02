# EntryZero

> A local open-source agent harness for safe computer-use automation.

EntryZero is a focused experiment in delegating one boring but consequential task: moving business data from messy human input into the software a small-business owner already uses.

## Core workflow

~~~text
Business message / document
        |
        v
Local open model
        |
        v
Structured transaction
        |
        v
Deterministic validation
        |
        v
Human review + approval
        |
        v
Agent harness
        |
        v
Laya-style computer-use model
        |
        v
Playwright
        |
        v
One browser-based target
        |
        v
Read-back verification
        |
        v
VERIFIED / STOPPED
~~~

## Why it exists

The project is being built for one real friend who performs repetitive data entry in a small business.

The friend should not need to give an AI unrestricted authority over their records. EntryZero therefore separates perception, validation, authorization, execution, and verification.

The core principle is:

> **The model proposes. The rules validate. The human approves. The agent executes. The harness verifies.**

## The "Agents API killer" thesis

EntryZero is not a feature-for-feature clone of a general-purpose hosted agent platform.

The provocative question is:

> **Can a much smaller open-source local harness solve one consequential workflow with more control, less infrastructure, and clearer boundaries?**

The project optimizes for constrained usefulness rather than maximum generality.

## Current scope

The MVP supports one real friend, one real workflow, one primary input format, one structured transaction schema, one browser target, one local/open extraction model, one constrained computer-use model, deterministic validation, transaction-scoped approval, bounded execution, post-action verification, and execution traces.

See [MVP.md](MVP.md) and [architecture.md](architecture.md).

## Documentation map

| Document | Purpose |
|---|---|
| [PRD.md](PRD.md) | Product requirements and thesis |
| [MVP.md](MVP.md) | Smallest testable product scope |
| [architecture.md](architecture.md) | System architecture and trust boundaries |
| [FRIEND_PROFILE.md](FRIEND_PROFILE.md) | Real friend and business context |
| [USER_RESEARCH.md](USER_RESEARCH.md) | Evidence about the real workflow |
| [TECH_STACK.md](TECH_STACK.md) | Technology choices and tradeoffs |
| [AGENT_HARNESS.md](AGENT_HARNESS.md) | Harness lifecycle and internals |
| [AGENT_POLICY.md](AGENT_POLICY.md) | Permissions and action policy |
| [DATA_SCHEMA.md](DATA_SCHEMA.md) | Canonical transaction schema |
| [VALIDATION.md](VALIDATION.md) | Deterministic validation |
| [COMPUTER_USE.md](COMPUTER_USE.md) | Browser-agent design |
| [VERIFICATION.md](VERIFICATION.md) | Post-action verification |
| [SECURITY.md](SECURITY.md) | Security controls |
| [THREAT_MODEL.md](THREAT_MODEL.md) | Threats and mitigations |
| [MODEL_SELECTION.md](MODEL_SELECTION.md) | Model evaluation criteria |
| [FINE_TUNING.md](FINE_TUNING.md) | Fine-tuning plan |
| [DATASET.md](DATASET.md) | Dataset design and governance |
| [EVALUATION.md](EVALUATION.md) | Evaluation methodology |
| [TEST_PLAN.md](TEST_PLAN.md) | Test strategy |
| [DEMO.md](DEMO.md) | Demo script |
| [OPEN_SOURCE_RATIONALE.md](OPEN_SOURCE_RATIONALE.md) | Why open source matters |
| [SUBMISSION.md](SUBMISSION.md) | Hackathon submission checklist |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Contribution rules |

## Status

This is a challenge prototype, not production accounting software.

The repository should publish measured results and limitations rather than implying production-grade accuracy or safety without evidence.

## Challenge

Hacktoberfest DEV Weekend Challenge: Build for a Friend

https://dev.to/challenges/hacktoberfest-weekend-2026-10-01
