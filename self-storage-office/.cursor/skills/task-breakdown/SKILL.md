---
name: task-breakdown
description: >-
  Split a large request into a work map (or a slice of an existing map) under
  docs/workflows/ or docs/tasks/. Use when they dump a week of work or say
  “handle this.”
---

# Task breakdown

## When

The request is more than one write-up, or they ask for a list. Prefer a work map over a disconnected task list.

## Do

1. **read-saved-files** so steps match known workflows.
2. If a `docs/workflows/<name>.md` map already fits: set `state.active_map` to it and list which step ids this request covers. Do not invent a second list that ignores `needs` / `produces`.
3. If none fits: write `docs/workflows/<short-name>.md` with a YAML work map (see `docs/workflows/README.md`). Each step: outcome, `needs`, `produces`, `tool` if known, `check` (or mark missing and **write-check** / **ask**). Optionally also write `docs/tasks/task-001.md` as a pointer to a step id.
4. Set `state.active_map`, `state.current_step` null, `steps_passed` []. **journal-keeper**.
5. Do **not** start all steps at once unless they asked. One ready step → **run-map**.

Do not create a task list that skips the work map when the job has more than one step.
