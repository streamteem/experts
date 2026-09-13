---
name: run-until-check
description: >-
  Run a work-map step’s tool, then its check command. On fail, read the log,
  fix only what this step owns, and retry (at most 3). Use instead of a
  single tool run when the step must pass a check.
---

# Run until check

Run the step, read the output, correct mistakes, repeat until the **check** exits 0.

## When

**run-map** has a current step with a `tool` and a `check`. **tool-operator** just got a non-zero tool exit and this step is still active.

## Do

1. If `check` is missing or empty → **write-check** or **ask**. Stop. Do not pass the step.
2. Run the step’s **tool** via **tool-operator**. Save the log under `<current_job_folder>/evidence/` (or `evidence/` only if no item folder is set).
3. Run the `check` command **against files in the current item folder**. If the map says `work/foo.csv`, the check must use `items/.../work/foo.csv`. Capture stdout/stderr to `<current_job_folder>/evidence/<date>-<step-id>-check.log`. Set `state.last_check` to `{ step, command, exit_code, log }`.
4. If exit code is **0**: the step passed. Stop (caller records artifacts).
5. If exit is not 0: read the tool log and the check log. Change **only** this step’s output file, command args, or a script under `docs/tools/` that this step owns. Increment `state.retry_count`.
6. If `retry_count` < 3 and `on_fail` is `retry`: go to step 2.
7. If cap hit: **ask**. Put the failure in `blocking_questions`. Do not mark passed. Do not invent a pass.

## Do not

- Run random shell because it might help.
- Retry more than 3 times.
- Edit other steps’ files to make this check green.
- Store passwords or API keys.
