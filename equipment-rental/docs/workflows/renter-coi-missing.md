# Renter COI missing list

Compare commercial or flagged contracts to the renter COI folder. List missing, expired, or name-mismatch certificates using only their checklist fields. Do not give a coverage opinion and do not invent a limit. Waiver or RPP does not replace COI unless their policy file says so. They hold the reservation or they waive in writing. Produce the missing list and write-up. No insurer-portal password and no card PAN.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: renter-coi-missing
steps:
  - id: coi
    needs: []
    produces: cois
    produce_path: work/renter-cois.csv
    tool: docs/tools/renter-coi-folder.md
    check: python docs/tools/checks/file-exists.py work/renter-cois.csv
    on_fail: retry
    next: [contracts]
  - id: contracts
    needs: [cois]
    produces: contracts
    produce_path: work/contracts.csv
    tool: docs/tools/contract-pdf-folder.md
    check: python docs/tools/checks/file-exists.py work/contracts.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [cois, contracts]
    produces: coi-pack
    produce_path: out/renter-coi-missing.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/renter-coi-missing.md
    on_fail: retry
    next: []
```
