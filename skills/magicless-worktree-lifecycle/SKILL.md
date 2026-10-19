---
name: magicless-worktree-lifecycle
description: Per-step git worktree lifecycle for spec-driven implementation. Do not load unless explicitly told by the user or system prompt.
---

# Worktree lifecycle for spec steps

Conditional procedure: applies ONLY when the project's AGENTS.md explicitly enables
worktrees (default is OFF — sequential main tree).

## Rules

- Create the worktree on a temp branch forked from the CURRENT working-branch HEAD — it
  must contain all previously committed steps, or dependent steps build on a tree missing
  their dependency.
- Implementation, gate, and review all happen inside the worktree; the reviewer gets the
  worktree path too.
- On user "proceed": commit IN the worktree, then fast-forward/merge the working branch to
  that commit, remove the worktree, and delete the temp branch.
- Parallel steps each fork from the same base and are merged back in the order the user
  approves them — disjoint `touches` makes conflicts unlikely.
- Parallel execution REQUIRES worktrees. Main-tree execution is strictly sequential:
  concurrent implementers in one tree contaminate each other's diffs and break the
  reviewer's scope check.
