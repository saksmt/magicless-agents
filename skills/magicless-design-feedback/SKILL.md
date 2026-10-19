---
name: magicless-design-feedback
description: Format of design-feedback files (status and origin frontmatter) under feedback/ and decomposition/feedback/. Do not load unless explicitly told by the user or system prompt.
---

# Design feedback

A design-feedback file records a change the spec or decomposition itself must make.

```yaml
---
status: new | addressed
origin: user | implementation
---

<body>
```

- `status` — `new` until resolved, then `addressed`.
- `origin` — `user` (raised during review) or `implementation` (raised during implementation).
- body — the issue itself.

## Filenames

Relative to the spec directory:

- `feedback/<iteration>_<origin>_<subject>.md`
- `decomposition/feedback/<iteration>_<origin>_<subject>.md`

`<subject>` — the stem the feedback addresses: `spec`, `architecture`, `common`, `index`,
or a `<step-id>`.
