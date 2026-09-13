# Deposit file pack

Pull the ledger lines for the units they name, then index move-in and move-out photo paths. The output is questions and a proposed-charge worksheet labeled proposed, not a legal disposition and not a refund. Do not invent a mail-by date, do not rule wear versus damage, and do not send money. Last-month versus deposit labels stay as they booked them. Bank logins never enter the pack.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: deposit-file
steps:
  - id: ledger
    needs: []
    produces: deposit-raw
    produce_path: work/deposit-ledger.csv
    tool: docs/tools/deposit-ledger.md
    check: python docs/tools/checks/csv-has-columns.py work/deposit-ledger.csv unit amount
    on_fail: retry
    next: [photos]
  - id: photos
    needs: [deposit-raw]
    produces: condition-index
    produce_path: work/condition-photos.csv
    tool: docs/tools/inspection-photos.md
    check: python docs/tools/checks/file-exists.py work/condition-photos.csv
    on_fail: retry
    next: [dep-questions]
  - id: dep-questions
    needs: [condition-index]
    produces: deposit-questions
    produce_path: out/deposit-questions.md
    tool: docs/tools/deposit-ledger.md
    check: python docs/tools/checks/file-exists.py out/deposit-questions.md
    on_fail: retry
    next: []
```
