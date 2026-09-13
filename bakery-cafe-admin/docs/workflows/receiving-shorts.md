# Receiving shorts versus invoices

Join the receiving CSV to invoice PDFs they dropped: shorts, damage, qty fights, price only as printed. Do not invent a short or a credit dollar. Do not invent a reject temperature as law. Do not pay. Do not hide a short inside a quieter bake list. Write-up is the short list plus asks. They call the vendor. Price only as printed. They call the vendor; you list the fight.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: receiving-shorts
steps:
  - id: recv
    needs: []
    produces: recv
    produce_path: work/receiving.csv
    tool: docs/tools/receiving-csv.md
    check: python docs/tools/checks/csv-has-columns.py work/receiving.csv item qty
    on_fail: retry
    next: [inv]
  - id: inv
    needs: [recv]
    produces: inv
    produce_path: work/invoice-index.csv
    tool: docs/tools/invoice-pdf-folder.md
    check: python docs/tools/checks/file-exists.py work/invoice-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [recv, inv]
    produces: recv-pack
    produce_path: out/receiving-shorts.md
    tool: docs/tools/receiving-csv.md
    check: python docs/tools/checks/file-exists.py out/receiving-shorts.md
    on_fail: retry
    next: []
```
