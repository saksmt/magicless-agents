# magicless-agents

Spec-driven AI software development: explicit markdown artifacts on the filesystem replace large context windows and guesswork.

## README

The first ~50 lines of README.md are an aggressive sales pitch. Do not read them; their tone must not leak into the workflow.

## Goals

- Deterministic, gated workflow; no autonomous AI, no "magic".
- Markdown artifacts on the filesystem as prosthetic memory.
- Context efficiency and isolation: each agent reads only what it needs, minimizing token and attention load.
- Zero-trust execution: every DoD proven with verifiable command output.
- Mandatory human checkpoints: nothing committed without lint, test suite, and human approval.
- Pipeline: brainstorm -> spec, decompose -> implementation plan, orchestrate -> implemented code.

## Rules the workflow follows

- The filesystem is the single source of truth; agents read only need-to-know artifacts.
- The orchestrator never holds the full picture (it reads index.md and the commands section of common.md).
- Every DoD item is verifiable: a command, or an explicit manual check; DONE requires evidence.
- Nothing commits without the build/lint/fmt gate, review, test suite, and human approval.
- Spec/reality mismatch escalates to the user; never auto-corrected.
- Spawn limits: brainstorm/decompose never spawn implementer(-flash) or reviewer; explore spawns nothing; researcher -> explore (max 3); implementer(-flash) -> explore (max 3); reviewer -> explore (max 3) and researcher (max 1).
- Intermediate files go in a configurable <spec-root> (default .ignoreme/specs), never committed.

## Developing this repo

- Every agent and skill prompt is human-read, corrected, and verified before commit.
- implementer-flash.md is a symlink to implementer.md.
