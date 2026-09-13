# Parts status board

On order, in stock, backorder, and returned from vendor files and POs they saved. No guessed ETA. Match part number and quantity to the RO. Flag cores, special-order notes, and shorts. You do not log into a portal or place an order. Quality words stay as quoted; this is not an OEM-versus-aftermarket safety ruling. Independent jobbers and dealer depots both apply. Missing confirmation is a question. Hold reasons on the board should match this file, not a story.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: parts-status
steps:
  - id: pull
    needs: []
    produces: parts-raw
    produce_path: work/parts-status.csv
    tool: docs/tools/parts-po.md
    check: python docs/tools/checks/csv-has-columns.py work/parts-status.csv ro part status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [parts-raw]
    produces: parts-pack
    produce_path: out/parts-status.md
    tool: docs/tools/parts-counter.md
    check: python docs/tools/checks/file-exists.py out/parts-status.md
    on_fail: retry
    next: []
```
