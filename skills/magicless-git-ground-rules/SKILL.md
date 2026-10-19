---
name: magicless-git-ground-rules
description: Git conventions for spec-driven implementation: session-start guards, commit messages, branch naming, ignored-artifact hygiene. Do not load unless explicitly told by the user or system prompt.
---

# Git conventions for spec-driven implementation

Obligations, not reference material.

## Session start (before ANY other action)

1. Run `git status` and check the current branch.
2. Uncommitted changes present -> STOP. Ask the user what to do with them (commit, stash,
   discard, or they belong to the work) before doing anything else. Never silently build on
   a dirty tree. If they belong to the work: record the baseline
   (`git status --porcelain`) and relay it to every reviewer spawn — the reviewer subtracts
   it from its changed-file set.
3. On the project's default branch (main/master/develop — check AGENTS.md and git remote
   for the convention) -> STOP. Ask the user whether to proceed directly on it or create a
   feature branch per project rules. Record the answer; all steps and commits use it.
4. Resolve the spec root per `magicless-conventions`.

## Branch naming

Follow the project's convention (AGENTS.md, git history). The name describes the FEATURE
and nothing else — no spec-root paths, no session ids, no round numbers.

## Commit messages

- The message covers the ENTIRE step as one logical change, written against the final
  state — never the process. No iteration history: anything introduced and flagged within
  the same step (review findings, rework) never happened as far as history is concerned.
- Refine the implementer's SUGGESTED-COMMIT-MESSAGE to the repo's convention (check git
  history and AGENTS.md for style — conventional commits or otherwise).
- Never include ignored-artifact references (see below).

## Ignored-artifact hygiene (strict)

Git-ignored artifacts (a fallback spec root, feedback files, anything the repo excludes)
must NEVER appear in anything tracked by git:

- Not in commit messages, branch names, or tags.
- Not in code, comments, doc blocks, or tracked docs.
- Not in tracked AGENTS.md either — the default spec location needs no documentation; a
  project override points to a TRACKED path instead.

This rule is shared: the `orchestrate` agent owns messages/branch names, the implementer owns
code/comments (its hard rule 6), the reviewer verifies (a MAJOR finding). Fix any
violation before committing.

Under a tracked `spec_root`, git-ignore `feedback/`, `decomposition/feedback/`, and
`decomposition/implementation-steps/feedback/` (or exclude them from step
commits): feedback files are orchestration artifacts in EVERY configuration, never part
of the step's changeset. Other tracked spec artifacts (index updates, Amendments entries)
ride in their OWN commits, separate from step code commits.
