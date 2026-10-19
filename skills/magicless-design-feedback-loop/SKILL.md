---
name: magicless-design-feedback-loop
description: The review loop for spec and decomposition files: submit via submit_plan, record user feedback, apply targeted edits, resubmit. Do not load unless explicitly told by the user or system prompt.
---

# Design feedback loop

Drive each file to approval:

1. Write the file, then submit it via `submit_plan`.
2. On feedback: write the feedback verbatim to a design-feedback file with `status: new`
   (see `magicless-design-feedback`); apply targeted edits that address ONLY the raised
   issues; mark the feedback file `status: addressed`. Never rewrite the whole file unless
   the user explicitly asks.
3. Post a short summary of what changed and resubmit via `submit_plan`.
4. Repeat until the user approves and no `status: new` feedback file remains for the file.
