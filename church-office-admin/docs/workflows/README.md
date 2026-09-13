# Workflows

Named jobs the person defined. Stubs from **define-role**. After a job works twice, **playbook-keeper** fills in the **work map** (the YAML block below).

A work map is the source of truth for multi-step work. **run-map** walks it. Do not skip a step with a chat summary. Data moves only as named files (**needs** / **produces**).

## Work map (required shape)

Put this YAML block at the top of `docs/workflows/<name>.md`. Human notes go under it.

```yaml
id: job-name
steps:
  - id: first-step
    needs: []
    produces: artifact-id
    produce_path: work/artifact-id.csv
    tool: docs/tools/some-tool.md
    check: python docs/tools/checks/file-exists.py work/artifact-id.csv
    on_fail: retry
    next: [second-step]
  - id: second-step
    needs: [artifact-id]
    produces: done-file
    produce_path: work/done-file.csv
    tool: docs/tools/some-tool.md
    check: python docs/tools/checks/file-exists.py work/done-file.csv
    on_fail: retry
    next: []
```

| Field | Meaning |
| --- | --- |
| `id` | Step name. Same idea as a first-principles **part**. |
| `needs` | Artifact ids that must already exist in `state.artifacts` (and on disk). |
| `produces` | Artifact id this step writes. |
| `produce_path` | Path under `work/` (or `out/` for a finished pack). |
| `tool` | File under `docs/tools/` to follow. |
| `check` | Command that exits **0** if the step passed, **non-zero** if not. Required. |
| `on_fail` | `retry` (at most 3) then **ask**. |
| `next` | Step ids that may run after this one passes. A next step still waits until its `needs` exist. |

See `_example-friday-invoices.md` for a filled-in example. Copy the shape. Do not treat that file as this shop’s real job unless they said it is.

## Rules

- Do not start a step if any `needs` file is missing.
- Do not start a step that has no `check` — **write-check** (they must approve) or **ask**.
- Do not mark the job done until every step has a passing check.
