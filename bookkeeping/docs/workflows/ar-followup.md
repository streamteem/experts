# AR aging questions

Export or paste AR for the period they name, age it with their buckets and their date basis (invoice versus due), and list credits, unapplied payments, and odd balances. Produce raw AR, an aged CSV with customer, amount, and bucket, and a questions pack. Do not write off. Do not apply a payment because the amount matches. Do not email customers unless they asked and the list is theirs. Do not call 90-plus uncollectible. Ask their cash-application rule. Starter buckets follow their export; do not invent a collections script or late fees they did not teach.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: ar-followup
steps:
  - id: export
    needs: []
    produces: ar-raw
    produce_path: work/ar-raw.csv
    tool: docs/tools/ar-aging.md
    check: python docs/tools/checks/file-exists.py work/ar-raw.csv
    on_fail: retry
    next: [age]
  - id: age
    needs: [ar-raw]
    produces: ar-aged
    produce_path: work/ar-aged.csv
    tool: docs/tools/ar-aging.md
    check: python docs/tools/checks/csv-has-columns.py work/ar-aged.csv customer amount bucket
    on_fail: retry
    next: [ar-pack]
  - id: ar-pack
    needs: [ar-aged]
    produces: ar-questions
    produce_path: out/ar-aging.md
    tool: docs/tools/ar-aging.md
    check: python docs/tools/checks/file-exists.py out/ar-aging.md
    on_fail: retry
    next: []
```
