# Waitlist pack

Read their waitlist CSV in the existing order and write the pack. Do not jump a row. Do not mix a market list with an affordable program list. A seat is not a hold and not an approval. Expire a row only if their policy file already says to. They decide whom to call when a unit comes up. Ask if the date-joined column is missing.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: waitlist
steps:
  - id: list
    needs: []
    produces: list
    produce_path: work/waitlist.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/waitlist.csv name date
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [list]
    produces: waitlist-pack
    produce_path: out/waitlist.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/waitlist.md
    on_fail: retry
    next: []
```
