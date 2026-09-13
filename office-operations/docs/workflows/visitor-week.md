# Visitor week log

If they use a visitor sheet, list the week they named. No ID numbers, license photos, or badge data in the pack. Ask whether a visitor log is even in scope. Host and times come from their columns. Lobby printouts omit personal cells and home addresses. You do not decide who may enter. Unsigned-out rows are flags. One week unless they asked. Starter notes for most SMB reception desks; they still teach this shop's form.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: visitor-week
steps:
  - id: list
    needs: []
    produces: visitors
    produce_path: work/visitors.csv
    tool: docs/tools/visitor-log.md
    check: python docs/tools/checks/csv-has-columns.py work/visitors.csv date host
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [visitors]
    produces: vis-pack
    produce_path: out/visitors.md
    tool: docs/tools/visitor-log.md
    check: python docs/tools/checks/file-exists.py out/visitors.md
    on_fail: retry
    next: []
```
