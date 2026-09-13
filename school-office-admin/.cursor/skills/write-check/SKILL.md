---
name: write-check
description: >-
  After they say what “done” looks like, propose a command that exits 0 on
  pass, save it under docs/tools/checks/ only after they approve. Use when a
  work-map step has no check, or during define-role.
---

# Write check

A step is done when a **command** says so, not when the chat sounds done.

## When

A work-map step has no `check`. They described “done.” **define-role** asked what a command would see. **verifier** found a step with no check.

## Do

1. Restate in one line what must be true (file exists, CSV has columns they named, a rule they taught).
2. Propose a **check**: a command line, often `python docs/tools/checks/file-exists.py <path>` or `python docs/tools/checks/csv-has-columns.py <path> <cols…>`, or a new small script in `docs/tools/checks/`.
3. Show them the command and what exit 0 vs 1 means. **Wait for approval.**
4. After they approve: write the script if needed; set the step’s `check` field on the work map; INDEX the tool file if new.
5. Do not save a check that encodes how *this* business works until they said that rule. Do not invent tax, legal, or “best practice” assertions.

If they cannot name a machine-visible done: **ask** what file or column would exist. Do not mark the step passed without a check.
