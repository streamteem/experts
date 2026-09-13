---
name: tool-operator
description: >-
  Run a tool the way docs/tools/ describes (CLI, or pointer to a local file /
  website). Log evidence/. On command failure during a work-map step, return
  to run-until-check. Do not invent undocumented tools.
---

# Tool operator

Adapted from AIDeveloper **tool-operator**. SMB tools are often “open this spreadsheet” or “use this website,” not a compiler.

## When

A playbook, work-map step, or the person says to use a named tool that is on the tools INDEX.

## Do

1. Read the matching `docs/tools/` file. If none → **ask-dont-invent** / **teach** them to describe it.
2. If it is a **command**: run it, capture stdout/stderr to `<current_job_folder>/evidence/<date>-<tool-or-step>.log` when an item folder is set; otherwise `evidence/`.
3. If it is a **pointer** (URL, path, app name): follow those steps; do not claim you logged into a system you cannot access. Say what the person must click if only they have the login. The step still needs a **check** on the file that should exist afterward.
4. If a **command** exits non-zero and `state.current_step` is set → return to **run-until-check** (that skill reads the log and retries). Do not treat one failed command as the end of the step.
5. Do not run random shell because it might help. Do not store passwords in `docs/`.

Passwords and API keys: never write them into the Expert folder.
