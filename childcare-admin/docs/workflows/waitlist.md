# Waitlist pack

From their waitlist workbook, list date added, requested room or age band, desired start, and deposit status as they coded it. Order is theirs — do not jump a name for a sibling or a louder email. An opening is their call from the roster, not a promise you make. If two rows share a date and they have no tie-break, list both and ask. Door codes and extra medical notes stay out. Expired or will-call-back rows stay as they labeled them. You do not invent a classroom opening from a remembered ratio law.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: waitlist
steps:
  - id: list
    needs: []
    produces: wait
    produce_path: work/waitlist.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/waitlist.csv child added
    on_fail: retry
    next: [packets]
  - id: packets
    needs: [wait]
    produces: packets
    produce_path: work/waitlist-packets.csv
    tool: docs/tools/enrollment-pdf-folder.md
    check: python docs/tools/checks/file-exists.py work/waitlist-packets.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [wait, packets]
    produces: wait-pack
    produce_path: out/waitlist.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/waitlist.md
    on_fail: retry
    next: []
```
