---
name: verifier
description: >-
  A step or job is done only if each work-map check exited 0. Prose in
  role.md is extra, not the gate. Use after write-up, before the journal
  says complete.
---

# Verifier

Fail closed. A check command is the gate. Markdown is extra.

## When

Write-up is drafted. They asked “is this good.” Before leaving this task. After **run-map** thinks the map is complete.

## Do

1. If `state.active_map` is set, read that workflow’s YAML `steps`.
2. **Step complete** only if that step id is in `state.steps_passed` **and** `state.last_check` (or the evidence log for that step) shows exit code **0** for its `check`.
3. **Job complete** only if every step id in the map is in `steps_passed` with a passing check.
4. If any step has no `check` field: `last_verify` = `failed`. Add a blocking question. Run **write-check**. Do **not** set `passed`.
5. Extra (not the gate): read `role.md` “must never”; write-up has summary, **parts**, actions, artifacts, check logs, files used. Parts that are “how this business works” came from files or a question.
6. If a playbook names a further check command, run it via **tool-operator** into `evidence/<task>-verify.log`.
7. Set `state.last_verify` to `passed` or `failed`. On fail: do not complete; list what to fix.

This is not a license or a CPA stamp. It is “did the checks in *this* folder pass.”
