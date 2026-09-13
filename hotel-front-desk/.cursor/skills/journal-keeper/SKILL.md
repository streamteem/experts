---
name: journal-keeper
description: >-
  Update journal/progress.md and journal/state.json after work, decisions,
  or session end. Use whenever next_action or the week’s story changes.
---

# Journal keeper

Keep a readable progress file and a small state file so **continue** works.

## When

After define-role, after a write-up, after a decision, at session end, when `next_action` changes.

## Do

1. Update `journal/progress.md`: what happened, decisions, open questions, work done.
2. Update `journal/state.json` to match:
   - `role_defined`, `next_action`, `active_workflow`, `active_task`
   - `active_map`, `current_step`, `artifacts` (id → path), `retry_count`
   - `current_job_folder` (path under `items/`), `current_job_label`
   - `last_check` (`step`, `command`, `exit_code`, `log`), `steps_passed`
   - `allowed_reads` (at most about 8 paths for the next step)
   - `blocking_questions` (empty if none)
   - `last_session_summary`, `last_verify`, `last_writeup`
3. Long Q&A: one line in progress.md; details in `journal/decisions.md` if it is getting long.
4. Do not mark work complete if `blocking_questions` is non-empty, or if `active_map` still has steps not in `steps_passed`.
5. Extra workers must not edit the journal. Only this chat, using this skill.

`next_action` examples: `define-role`, `read-saved-files`, `run-map`, `wait for person`, `continue`.
