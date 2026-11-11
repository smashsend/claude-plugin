---
name: workflows
description: Read, analyse and edit SmashSend workflows (automations such as welcome series, onboarding drips, win-back and abandoned-checkout flows) - inspect steps and runs, find weak steps, and save changes as a draft for a person to publish. Use when the user asks about their automations or workflows, wants to add, change or remove steps, or wants to build a new automated sequence.
---

# SmashSend workflows

**Reading.** `list_workflows` → `get_workflow` for the steps → `get_workflow_performance` for per-email stats → `list_workflow_runs` / `get_workflow_run` to see where contacts stop or fail.

**Editing (EDITOR key).** You only ever change a draft; a person publishes it from the SmashSend builder.

1. `list_workflow_catalog` lists the triggers and actions that exist. For each app you use, `get_workflow_app` returns the exact fields each step takes. Use dropdown values from `get_workflow_field_options`, and `{{variables}}` from `get_workflow_step_variables` for that step.
2. Existing workflow: `start_workflow_draft`. New workflow: `create_workflow`. Keep the `updatedAt` you get back.
3. `save_workflow_draft` with the full step graph and `expectedUpdatedAt`. A 422 lists every structural problem by step: fix all of them in one go. A 409 means someone edited it in the builder meanwhile; re-read it, re-apply your change and save again. Don't overwrite their edit.
4. `validate_workflow` until it's valid. Every branch path needs a destination (a step id, or `null` to end), and loops are rejected.
5. Give the user the builder link from the response and tell them to review and publish it there. There is no publish tool.

Write workflow emails with react-email or email-safe HTML, the same way the email-campaigns skill describes.
