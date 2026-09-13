# Lease-packet checklist

Index the lease-packet folder, tick addenda against their checklist, and write the pack. Completeness only — no legal review and no invented riders. Lead pamphlet present or missing if their checklist calls for it on pre-1978 homes. Concession addenda must match the specials file if that file is in the folder; do not invent a special. They send the packet.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: lease-packet
steps:
  - id: folder
    needs: []
    produces: folder
    produce_path: work/packet-index.csv
    tool: docs/tools/lease-packet-folder.md
    check: python docs/tools/checks/file-exists.py work/packet-index.csv
    on_fail: retry
    next: [checklist]
  - id: checklist
    needs: [folder]
    produces: checklist
    produce_path: work/addendum-checklist.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/addendum-checklist.csv addendum required
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [folder, checklist]
    produces: packet-pack
    produce_path: out/lease-packet.md
    tool: docs/tools/lease-packet-folder.md
    check: python docs/tools/checks/file-exists.py out/lease-packet.md
    on_fail: retry
    next: []
```
