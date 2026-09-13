# Assignment draft

Who is on which unit from the roster for the date. Draft options only if they asked and you label the draft. Do not invent qualifications, split a team, or put an off-roster driver on a unit as if dispatched. Copy only fields already in the export; no license images in docs/. Live board stays theirs. Starter / guess until they teach this shop.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: assignment-pack
steps:
  - id: pull
    needs: []
    produces: assign-raw
    produce_path: work/assignments.csv
    tool: docs/tools/roster.md
    check: python docs/tools/checks/csv-has-columns.py work/assignments.csv driver unit
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [assign-raw]
    produces: assign-pack
    produce_path: out/assignments.md
    tool: docs/tools/roster.md
    check: python docs/tools/checks/file-exists.py out/assignments.md
    on_fail: retry
    next: []
```
