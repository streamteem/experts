# Progress meeting pack

Agenda plus open actions from last minutes they filed. They send anything to people. Extract only numbered actions with owners and dates they recorded. Do not add implied work or speak for the owner. Unsigned minutes, if they track approval, stay marked unsigned. This week's agenda topics come from their template or notes, not from a starter list you invent. The pack names the minutes file and keeps action rows the check can see so the next meeting starts from their record.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: weekly-minutes
steps:
  - id: agenda
    needs: []
    produces: agenda-raw
    produce_path: work/meeting-agenda.csv
    tool: docs/tools/meeting-minutes.md
    check: python docs/tools/checks/csv-has-columns.py work/meeting-agenda.csv topic owner
    on_fail: retry
    next: [actions]
  - id: actions
    needs: [agenda-raw]
    produces: actions-raw
    produce_path: work/meeting-actions.csv
    tool: docs/tools/meeting-minutes.md
    check: python docs/tools/checks/csv-has-columns.py work/meeting-actions.csv action owner
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [actions-raw]
    produces: meet-pack
    produce_path: out/meeting-pack.md
    tool: docs/tools/meeting-minutes.md
    check: python docs/tools/checks/file-exists.py out/meeting-pack.md
    on_fail: retry
    next: []
```
