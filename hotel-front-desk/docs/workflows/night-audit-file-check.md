# Night-audit file check

Check that the night-audit packet they dropped has the usual pages versus their PMS export: flash, occupancy, no-show, high-balance, exceptions. Name missing pages. Do not run audit or roll the date. Do not invent a flash total. Ask for a redacted file if PAN appears. They close the day. You deliver the completeness list and write-up. Trial versus final, if they drop both, stay labeled. High-balance folios already on the packet become exception pointers, not new amounts you invent.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: night-audit-file-check
steps:
  - id: audit
    needs: []
    produces: audit
    produce_path: work/night-audit.pdf
    tool: docs/tools/night-audit-pdf.md
    check: python docs/tools/checks/file-exists.py work/night-audit.pdf
    on_fail: retry
    next: [pms]
  - id: pms
    needs: [audit]
    produces: pms
    produce_path: work/pms-house.csv
    tool: docs/tools/pms-export.md
    check: python docs/tools/checks/file-exists.py work/pms-house.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [audit, pms]
    produces: audit-pack
    produce_path: out/night-audit-file-check.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/night-audit-file-check.md
    on_fail: retry
    next: []
```
