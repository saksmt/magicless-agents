---
name: magicless-conventions
description: Spec-root resolution, spec/decomposition directory layout, and path tokens for spec-driven work. Do not load unless explicitly told by the user or system prompt.
---

# Magicless conventions

## Spec-root resolution

`<spec-root>` is the directory that CONTAINS the specs. Resolve in this order:

1. project `AGENTS.md` `spec_root` if declared
2. user-global convention
3. fallback `.ignoreme/specs/`

With NO declared override the root MUST be git-ignored — verify with `git check-ignore`
(create the dir first if missing). NOT ignored -> STOP and ask the user where specs
should live (they may want a tracked `spec_root`).

## Directory layout

```
<spec-root>/
└── <spec-id>_<slug>/              # one feature spec
    ├── spec.md
    ├── assets/                    # diagrams, images, other assets
    ├── feedback/                  # design feedback
    └── decomposition/
        ├── index.md               # step registry (orchestrate's only scheduling input)
        ├── architecture.md        # numbered decisions (AD-1, AD-2, …)
        ├── common.md              # operational context every step needs
        ├── assets/                # decomposition diagrams
        ├── feedback/              # design feedback
        └── implementation-steps/
            ├── <step-id>_<slug>.md
            └── feedback/          # per-step rework feedback
```

Feedback lives in a `feedback/` dir whose immediate parent names the entity the feedback is
about: `feedback/` -> the spec; `decomposition/feedback/` -> the decomposition;
`decomposition/implementation-steps/feedback/` -> one step.

## Tokens

- `<spec-id>` — lowest unused integer in `<spec-root>`.
- `<step-id>` — integer id within a decomposition, zero-padded two digits.
- `<slug>` — short kebab-case name (hyphens inside).
- `<round>` — an implement↔review round within a step.
- `<iteration>` — a feedback iteration.

Join tokens with `_` (e.g. `<spec-id>_<slug>`); a `<slug>` keeps its internal hyphens.
