# Return damage pack

Compare return inspection to outgoing: new marks, missing kit, fuel and cleaning codes. Attach photos they stored. Do not invent damage, a repair dollar, or a fee. Fuel and cleaning amounts wait for their policy file. Do not diagnose a leak. Meter return below outgoing is a meter exception to list, not a quiet fix. They post charges. You produce the difference list and write-up. No collection lawsuit and no card PAN in the pack.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: return-damage
steps:
  - id: ret
    needs: []
    produces: return
    produce_path: work/return-inspections.csv
    tool: docs/tools/inspection-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/return-inspections.csv unit
    on_fail: retry
    next: [photos]
  - id: photos
    needs: [return]
    produces: photos
    produce_path: work/return-photos.csv
    tool: docs/tools/photo-folder.md
    check: python docs/tools/checks/file-exists.py work/return-photos.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [return, photos]
    produces: damage-pack
    produce_path: out/return-damage.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/return-damage.md
    on_fail: retry
    next: []
```
