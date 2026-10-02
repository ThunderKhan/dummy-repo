# EntryZero — Technology Stack

## Selection goal

Use the smallest stack that can support the core thesis:

- local open inference;
- deterministic validation;
- constrained computer use;
- browser execution;
- verification;
- reproducible development.

Technology is selected for the workflow, not for novelty.

## Proposed stack

| Layer | Choice | Rationale |
|---|---|---|
| Language | Python | ML ecosystem and fast orchestration |
| API | FastAPI | Thin developer boundary if needed |
| Validation | Pydantic + Python | Typed schemas and deterministic rules |
| Local model runtime | Ollama or Transformers-compatible runtime | Local experimentation |
| Extraction model | Gemma family or suitable open model | Open/local extraction |
| Computer-use model | Laya-style typed-action model | Small action vocabulary |
| Browser | Chromium | Reproducible target |
| Browser driver | Playwright | Structured state and deterministic interaction |
| Storage | SQLite | Lightweight local state |
| Tests | pytest + Playwright | Unit + browser coverage |
| Evaluation | Python scripts | Repeatable metrics |

## Architectural constraints

### Local-first

The primary AI inference path should work without a hosted inference dependency.

### Model abstraction

Business logic must not call a specific model implementation directly.

Conceptual interfaces:

~~~python
class Extractor:
    def extract(self, source):
        ...

class ComputerUseModel:
    def decide(self, browser_state, goal):
        ...
~~~

### Deterministic core

Arithmetic, permissions, transaction state, and verification remain ordinary application logic.

### Browser state

Prefer structured accessibility/page state whenever available.

Playwright documents accessibility snapshots with element references for browser interaction:

https://playwright.dev/agent-cli/snapshots

## Dependency policy

A dependency is justified when it:

1. materially reduces implementation risk;
2. is stable enough for the challenge;
3. does not hide the core work behind a closed service;
4. has compatible licensing.

Avoid dependencies added only to increase the apparent size of the stack.

## Resource fallback

If the preferred model is too slow or unreliable:

1. preserve the end-to-end transaction path;
2. use a smaller model;
3. narrow the schema;
4. reduce target complexity;
5. keep validation and verification intact.

The project should lose capability before it loses safety.

## Reproducibility

Record:

- Python version;
- package versions;
- model identifier;
- browser version;
- hardware assumptions;
- environment variables;
- evaluation commands;
- benchmark configuration.
