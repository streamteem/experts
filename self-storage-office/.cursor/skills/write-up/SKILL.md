---
name: write-up
description: >-
  Save finished work as a file under out/: summary, parts, artifacts,
  check logs, actions, questions, docs files used. Use after the work map
  passed, not instead of checks.
---

# Write-up

Finished work is a **file they can keep**, not only a chat reply.

## When

They asked for work done, not a casual question. After **read-saved-files**. If a work map was used: after **run-map** has passed every step (or they asked for a status write-up). Then **verifier**.

## Write

Create or update `<current_job_folder>/out/write-up.md` (or `out/<date>-<short-name>.md` **inside that item folder**). If `state.current_job_folder` is empty, run **start-job** first. Do not write a new pack into the top-level `out/` folder.

1. **Summary** — what you concluded, in their words.
2. **Parts** — the pieces of the solution (step ids / artifacts), where each came from (saved file, guess, or question), and how they fit. Skip only if the ask was a yes/no from a saved rule.
3. **Artifacts** — id → path produced (`state.artifacts`).
4. **Checks** — for each step: command, exit code, log path under `evidence/`.
5. **Actions** — numbered, who does them (them vs this Expert).
6. **Open questions** — only what blocks finishing.
7. **Files used** — paths under `docs/` you actually read.
8. **Guesses** — anything not from those files, labeled as a guess.

Then **verifier**. Then **after-task**. Then **journal-keeper** (`last_writeup` = that path).

Do not call the job done in the write-up if checks have not passed. **verifier** is the gate.
