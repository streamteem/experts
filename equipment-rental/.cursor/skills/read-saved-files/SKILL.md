---
name: read-saved-files
description: >-
  Before doing work, read role.md and the indexes of facts, rules, tools, and
  playbooks, then only the files that match this task. Do not start as if
  nothing was already saved in this folder.
---

# Read saved files

## When

Before every real task. After **define-role**. When **continue** starts a work step.

## Do

1. Read `role.md`. If it is still a stub → **define-role** instead.
2. Read `docs/facts/INDEX.md`, `docs/rules/INDEX.md`, `docs/tools/INDEX.md`, `docs/playbooks/INDEX.md`, `docs/workflows/README.md`, `docs/facts/how-we-file.md` if it exists, and `items/INDEX.md`. Then the matching `docs/workflows/<name>.md` if the request names a job.
3. From words in the request, pick **at most 8** files. Read those (search first if a file is long).
4. Set `journal/state.json` `allowed_reads` to those paths (+ `role.md`).
5. In one short paragraph: what we already have on file for this task, and what is **missing** (then **ask-dont-invent**). If a work map matches, say so and run **run-map** next.

Do not load every file under `docs/`. Do not skip this and guess.
