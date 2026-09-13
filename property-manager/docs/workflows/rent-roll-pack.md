# Rent roll snapshot

Export the roll as-of the date they name and read the header before you review. List vacancies, notice units, odd credits, and subsidy splits as their columns show. Do not change charged rent, do not invent market rent, and do not hide vacancy by leaving a past tenant on a row. Late fees stay as they configured them. The write-up is a snapshot plus questions, not a legal lease and not a rent-control opinion.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: rent-roll-pack
steps:
  - id: export
    needs: []
    produces: roll-raw
    produce_path: work/rent-roll-raw.csv
    tool: docs/tools/rent-roll-export.md
    check: python docs/tools/checks/file-exists.py work/rent-roll-raw.csv
    on_fail: retry
    next: [review]
  - id: review
    needs: [roll-raw]
    produces: roll-review
    produce_path: work/rent-roll-review.csv
    tool: docs/tools/rent-roll-export.md
    check: python docs/tools/checks/csv-has-columns.py work/rent-roll-review.csv unit rent status
    on_fail: retry
    next: [roll-pack]
  - id: roll-pack
    needs: [roll-review]
    produces: roll-writeup
    produce_path: out/rent-roll.md
    tool: docs/tools/rent-roll-export.md
    check: python docs/tools/checks/file-exists.py out/rent-roll.md
    on_fail: retry
    next: []
```
