# Orientation missing

Compare the orientation-ack folder to people on the employee list who should have a packet — new starts they named or everyone they said must ack. List missing sign-ins, safety-video acks, handbook acks if they keep them here, and drug-policy acks. Do not invent an agenda. Do not treat a missing tick as a safety-law citation. Agency versus client-site packets stay separate if they split them. Write the missing list and a write-up. They collect acks. No LMS password.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: orientation-missing
steps:
  - id: acks
    needs: []
    produces: acks
    produce_path: work/orientation-acks.csv
    tool: docs/tools/orientation-ack-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/orientation-acks.csv name
    on_fail: retry
    next: [people]
  - id: people
    needs: [acks]
    produces: people
    produce_path: work/employee-list.csv
    tool: docs/tools/employee-list.md
    check: python docs/tools/checks/file-exists.py work/employee-list.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [acks, people]
    produces: ori-pack
    produce_path: out/orientation-missing.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/orientation-missing.md
    on_fail: retry
    next: []
```
