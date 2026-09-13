---
name: run-map
description: >-
  Load a work map from docs/workflows/, pick the next ready step (needs met,
  not yet passed), run it until its check passes, then stop or continue.
  Use for any named multi-step job. Do not only talk through the steps.
---

# Run map

Walk the work map one ready step at a time. Data is files, not chat recap.

## When

After **read-saved-files**, a `docs/workflows/<name>.md` has a YAML `steps` list. They named a job that matches. **continue** when `active_map` is set.

Skip `_example-friday-invoices.md` unless they said this shop’s job is that example.

## Do

0. If `state.current_job_folder` is empty, run **start-job** first. Map paths `work/` and `out/` mean **inside that folder**. Rewrite each step’s `produce_path` and any `work/` or `out/` path in `check` to sit under `current_job_folder` unless the path already starts with `items/`.
1. Read the YAML `steps` from the matching workflow file. Set `state.active_map` to that path.
2. **Ready step:** `needs` every artifact id is in `state.artifacts` **and** the file at that path exists on disk; `id` is not in `state.steps_passed`; if several are ready, pick the first in the file order (or one listed in a prior step’s `next`).
3. If no ready step and `steps_passed` contains every step id → **write-up** then **verifier**. If some steps remain but none are ready → **ask** (missing file or missing check). Stop.
4. If the ready step has no `check` → **write-check** or **ask-dont-invent**. Do not run the step.
5. Set `state.current_step` to that `id`. **journal-keeper**.
6. Run **run-until-check** for this step.
7. On pass: record `produces` → `produce_path` in `state.artifacts`; append `id` to `steps_passed`; reset `retry_count` to 0. Stop after this one step unless they asked to run the whole named job.
8. On ask / cap: set `blocking_questions`. Do not mark the step passed.

Do not start a step whose `needs` files are missing. Do not skip ahead because the write-up would be faster.
