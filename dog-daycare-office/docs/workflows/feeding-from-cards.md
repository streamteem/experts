# Feeding sheet from boarding cards

Transcribe feeding as the client wrote it onto the feeding sheet for the stay date. Do not substitute a bag or invent cups. Unreadable lines are questions. Allergy words stay theirs, not a diagnosis. Confirm the occupancy list so you do not feed a dog who is not here. House food is only a named backup on their sheet. Starter / guess until they teach who initials the clipboard.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: feeding-from-cards
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
    produces: feed
    produce_path: work/feeding.csv
    tool: docs/tools/feeding-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/feeding.csv patient food
    on_fail: retry
    next: [write]
  - id: write
    needs: [cards, feed]
    produces: feed-pack
    produce_path: out/feeding-from-cards.md
    tool: docs/tools/feeding-sheet.md
    check: python docs/tools/checks/file-exists.py out/feeding-from-cards.md
    on_fail: retry
    next: []
```
