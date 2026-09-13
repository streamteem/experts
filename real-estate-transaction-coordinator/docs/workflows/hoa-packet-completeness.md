# HOA packet completeness

Index the HOA or condo packet against their checklist: resale or estoppel, bylaws, rules, budget, questionnaire, and fee letters. Fees come only from those pages. Do not invent a transfer amount. Do not interpret CC&Rs as legal advice. A listing flyer is not the packet. Lender-named extras stay on a missing row. If property type is unclear, quote the files and ask before you apply a condo checklist. They order the set. You list holes.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: hoa-packet-completeness
steps:
  - id: folder
    needs: []
    produces: hoa-index
    produce_path: work/hoa-index.csv
    tool: docs/tools/hoa-packet-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/hoa-index.csv document status
    on_fail: retry
    next: [checklist]
  - id: checklist
    needs: [hoa-index]
    produces: hoa-checklist
    produce_path: work/hoa-checklist.csv
    tool: docs/tools/checklist-sheet.md
    check: python docs/tools/checks/file-exists.py work/hoa-checklist.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [hoa-index, hoa-checklist]
    produces: hoa-pack
    produce_path: out/hoa-packet.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/hoa-packet.md
    on_fail: retry
    next: []
```
