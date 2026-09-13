---
name: playbook-keeper
description: >-
  After a workflow has succeeded more than once, write docs/playbooks/<name>.md
  and a work map (YAML steps) in docs/workflows/ so the next run follows those
  steps with needs, produces, and checks.
---

# Playbook keeper

Save a repeatable way of working where the person can see it.

## When

The same kind of write-up succeeded twice, or they say “this is how we always do X.”

## Do

1. Read what actually worked (write-up, journal, `docs/` files used, `state.artifacts`, check logs).
2. Write `docs/playbooks/<name>.md`: when to use, steps, tools, pitfalls, which facts/rules it depends on.
3. Add or update `docs/workflows/<name>.md` with a **work map** YAML (`id`, `needs`, `produces`, `produce_path`, `tool`, `check`, `on_fail`, `next`). Every step must have a `check` they already approved (or run **write-check** first). See `docs/workflows/README.md`.
4. Add a row to `docs/playbooks/INDEX.md`.
5. Point the workflow file at this playbook in the human notes under the YAML.

Do not save a one-off as a playbook. Do not overwrite a playbook they have not seen. Do not write a map with empty `check` fields.
