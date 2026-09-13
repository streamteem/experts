# Insurance binder present

List HOI binders, dec pages, master policies, and flood policies in their insurance-binder folder. Copy effective dates and mortgagee line as printed. Do not bind. Do not invent a limit. Do not say they are covered. Flood and HOI stay separate. Quote versus binder stay labeled. Expired dates stay flagged. Write-up is present-missing plus date flags, not a coverage opinion.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: insurance-binder-present
steps:
  - id: ins
    needs: []
    produces: insurance
    produce_path: work/insurance-index.csv
    tool: docs/tools/insurance-binder-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/insurance-index.csv loan document
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [insurance]
    produces: insurance-pack
    produce_path: out/insurance-binder-present.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/insurance-binder-present.md
    on_fail: retry
    next: []
```
