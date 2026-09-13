---
name: define-role
description: >-
  First session: ask what this Expert is for, write role.md and stub
  workflows with work-map shape. Use when role.md is still a stub or they
  name a new job.
---

# Define role

Generic Experts start empty. Ask; then write files.

## When

`role.md` is a stub. They name a job. New Expert folder.

## Ask (do not skip)

1. What should we **call** this Expert (their words)?
2. What **workflows** do you repeat (names + rough steps)?
3. What **tools** do you already use (apps, websites, files on disk)? Notes only — no passwords.
4. What does **done** look like — what would a **command** see (a file that exists, columns in a CSV, a folder that is not empty)? If they only have words, still write them, then **write-check** before the first real run.
5. What must we **never** do?
6. What is **not our job** (another person / another Expert)?

## Write

- Fill `role.md`.
- Create `docs/workflows/<name>.md` stubs: title + steps they said + a work-map YAML skeleton (`needs`, `produces`, `tool` if named, `check` empty until **write-check**). See `docs/workflows/README.md` and `_example-friday-invoices.md`.
- For each tool they named, a stub in `docs/tools/` until **teach** fills it.
- `state.role_defined: true`, then wait for work or start the first workflow.
- **journal-keeper**.

Do not pretend the files are complete. Thin is correct. Learning starts on the first real task. Do not copy `_example-friday-invoices.md` as their live job unless they said that is the job.
