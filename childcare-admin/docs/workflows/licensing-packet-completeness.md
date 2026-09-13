# Licensing packet completeness

Against their visit checklist, list named binder pages as present or missing: posted license, drill log, menus, staff-file dates, and enrollment samples they asked you to sample. Do not invent a statute or stamp the center compliant. Staff credentials are dates on file, not a license you grant. Children’s medical pages stay present-or-missing without extra clinical copy into docs/. If their checklist and a state packet they saved disagree, quote both and ask. This pack is a completeness list for the director, not an inspector signature.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: licensing-packet-completeness
steps:
  - id: binder
    needs: []
    produces: binder
    produce_path: work/licensing-index.csv
    tool: docs/tools/licensing-forms-folder.md
    check: python docs/tools/checks/file-exists.py work/licensing-index.csv
    on_fail: retry
    next: [staff]
  - id: staff
    needs: [binder]
    produces: staff
    produce_path: work/staff-index.csv
    tool: docs/tools/staff-file-index.md
    check: python docs/tools/checks/csv-has-columns.py work/staff-index.csv staff date
    on_fail: retry
    next: [write]
  - id: write
    needs: [binder, staff]
    produces: lic-pack
    produce_path: out/licensing-completeness.md
    tool: docs/tools/licensing-forms-folder.md
    check: python docs/tools/checks/file-exists.py out/licensing-completeness.md
    on_fail: retry
    next: []
```
