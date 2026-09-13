# Change and PCO register

Open potential changes and signed change orders from their register. No pricing by this Expert. Keep their names such as PCO, COR, or CO. Do not create a number or say a ticket is billable. Verbal extras stay flagged as missing written follow-up when that is their rule. Directed-change papers are listed if they are on the register, not upgraded to a signed CO. The pack quotes status and amounts as printed and asks where notice dates are blank.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: change-register
steps:
  - id: list
    needs: []
    produces: pco-raw
    produce_path: work/pco-register.csv
    tool: docs/tools/procore-pattern.md
    check: python docs/tools/checks/csv-has-columns.py work/pco-register.csv number status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [pco-raw]
    produces: pco-pack
    produce_path: out/change-register.md
    tool: docs/tools/procore-pattern.md
    check: python docs/tools/checks/file-exists.py out/change-register.md
    on_fail: retry
    next: []
```
