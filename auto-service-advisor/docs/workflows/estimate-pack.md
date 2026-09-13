# Estimate from their prices

Build estimate lines from their labor guide or menu plus the parts file they confirmed. Label any missing hour or price as a question. Do not invent book time or mix two guides. Diagnostic fees stay if they sell them. Shop fees copy from their RO settings, not from another store. Quality labels stay as quoted; do not rule OEM safer than aftermarket. Independent menus and dealer factory operations both apply. The pack is not sold work. Auth still required. Ask which matrix is source of truth.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: estimate-pack
steps:
  - id: guide
    needs: []
    produces: guide-raw
    produce_path: work/labor-lines.csv
    tool: docs/tools/labor-guide.md
    check: python docs/tools/checks/csv-has-columns.py work/labor-lines.csv op hours
    on_fail: retry
    next: [parts]
  - id: parts
    needs: [guide-raw]
    produces: est-parts
    produce_path: work/est-parts.csv
    tool: docs/tools/parts-counter.md
    check: python docs/tools/checks/csv-has-columns.py work/est-parts.csv part price
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [est-parts]
    produces: estimate-pack
    produce_path: out/estimate.md
    tool: docs/tools/labor-guide.md
    check: python docs/tools/checks/file-exists.py out/estimate.md
    on_fail: retry
    next: []
```
