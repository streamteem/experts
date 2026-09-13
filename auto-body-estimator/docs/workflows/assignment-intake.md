# Assignment intake

Build an intake pack from the assignment sheet and the VIN file: claim, VIN, DOL, insurer, mileage if present. Do not invent an assignment or a VIN. Quote VIN mismatches and stop. Customer-pay with no assignment stays labeled customer-pay. Write-up is missing-field asks, not a coverage opinion and not a mechanical RO open. Distinct from opening a mechanical RO. You do not invent DOL or carrier. Write-up names which VIN source won only if they already picked; otherwise both stay listed. Missing assignment on insurer-pay is an ask.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: assignment-intake
steps:
  - id: assign
    needs: []
    produces: assign
    produce_path: work/assignment.csv
    tool: docs/tools/assignment-sheet.md
    check: python docs/tools/checks/csv-has-columns.py work/assignment.csv claim vin
    on_fail: retry
    next: [vin]
  - id: vin
    needs: [assign]
    produces: vin
    produce_path: work/vin-file.csv
    tool: docs/tools/vin-file.md
    check: python docs/tools/checks/file-exists.py work/vin-file.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [assign, vin]
    produces: intake-pack
    produce_path: out/assignment-intake.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/assignment-intake.md
    on_fail: retry
    next: []
```
