# WDO form completeness

Check their WDO or termite form pack: form fields, graph present, photos named if they require them. Do not stamp the inspection. Do not diagnose the structure. Do not invent findings or a moisture reading. Missing graph or missing signature stays a hole. Real-estate deadlines they wrote stay visible. They inspect and they sign. You write the completeness list and a write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: wdo-form-completeness
steps:
  - id: tickets
    needs: []
    produces: tickets
    produce_path: work/wdo-tickets.csv
    tool: docs/tools/ticket-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/wdo-tickets.csv ticket account
    on_fail: retry
    next: [photos]
  - id: photos
    needs: [tickets]
    produces: photos
    produce_path: work/wdo-photo-index.csv
    tool: docs/tools/photo-folder.md
    check: python docs/tools/checks/file-exists.py work/wdo-photo-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [tickets, photos]
    produces: wdo-pack
    produce_path: out/wdo-completeness.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/wdo-completeness.md
    on_fail: retry
    next: []
```
