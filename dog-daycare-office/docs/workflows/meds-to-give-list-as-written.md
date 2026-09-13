# Meds-to-give list as written

From boarding cards and the feeding or meds sheet, list meds-to-give exactly as written and whether today’s medication log page is present. Never prescribe, convert a dose, or fill staff initials. Flag unreadable lines and blank log boxes. This is not a veterinary refill list. Late-med codes copy as theirs and route. Starter / guess until they teach who gives meds and which clipboard is official.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: meds-to-give-list-as-written
steps:
  - id: cards
    needs: []
    produces: cards
    produce_path: work/boarding.csv
    tool: docs/tools/boarding-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/boarding.csv patient stay
    on_fail: retry
    next: [sheet]
  - id: sheet
    needs: [cards]
    produces: meds
    produce_path: work/feeding.csv
    tool: docs/tools/feeding-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/feeding.csv patient food
    on_fail: retry
    next: [write]
  - id: write
    needs: [cards, meds]
    produces: meds-pack
    produce_path: out/meds-to-give.md
    tool: docs/tools/feeding-sheet.md
    check: python docs/tools/checks/file-exists.py out/meds-to-give.md
    on_fail: retry
    next: []
```
