# Checkout list from their invoices

List invoice lines and tenders from their export. You do not take payment or add clinical charges. Discounts stay their codes. Open versus closed invoices stay as exported. If the invoice and a signed estimate disagree, list both and ask. Do not store card numbers. Multi-patient visits follow their household billing rule as shown. Starter / guess until they teach grouping and the close report they drop.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: checkout-list
steps:
  - id: pull
    needs: []
    produces: inv-raw
    produce_path: work/invoices.csv
    tool: docs/tools/invoice-export.md
    check: python docs/tools/checks/file-exists.py work/invoices.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [inv-raw]
    produces: inv-cols
    produce_path: work/invoices.csv
    tool: docs/tools/invoice-export.md
    check: python docs/tools/checks/csv-has-columns.py work/invoices.csv invoice amount
    on_fail: retry
    next: [write]
  - id: write
    needs: [inv-cols]
    produces: inv-writeup
    produce_path: out/checkout.md
    tool: docs/tools/invoice-export.md
    check: python docs/tools/checks/file-exists.py out/checkout.md
    on_fail: retry
    next: []
```
