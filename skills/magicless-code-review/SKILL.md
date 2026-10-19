---
name: magicless-code-review
description: Finding format, severity taxonomy (BLOCKER/MAJOR/MINOR/NIT), and quality checklist for judging code. Do not load unless explicitly told by the user or system prompt.
---

# Code review — quality gate

## Finding format (machine-parseable, one per line)

```
[SEVERITY] <file>:<line> — <issue> — <suggested fix>
```

## Severities

| Severity | Meaning | Effect |
|----------|---------|--------|
| BLOCKER | Broken: doesn't build, security hole, data-loss risk, or otherwise fundamentally wrong | Must fix |
| MAJOR | Works but wrong shape: real design flaw, missing error handling, broken edge case | Must fix |
| MINOR | Should fix soon, doesn't endanger the change: weak naming, missing test for an edge case | Non-blocking |
| NIT | Taste, style beyond declared codestyle | Non-blocking, never demanded |

When unsure between two severities, pick the lower one and say why in the finding.

## Quality checklist (in priority order)

- [ ] Correctness: edge cases, error paths, concurrency, resource cleanup
- [ ] Security: injection, secrets, input trust, authz
- [ ] Efficiency: memory/CPU/disk asymptotics, obvious waste
- [ ] Structure: naming, boundaries, duplication, dead code, simpler equivalent design
- [ ] Comments: grammar, no self-evident or diff-narrating comments
- [ ] Long prose (docs, doc blocks): apply the `stop-slop` skill

Judgement rule: SOLID/DRY/KISS/YAGNI, "Code Complete", Fowler's smells — all applied with
judgement, not worshipped. When KISS/YAGNI conflict with other practices, prefer the more
elegant design. Project codestyle beats generic advice.
