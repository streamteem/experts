# HOS / ELD questions

List gaps from their ELD export as questions: certify, unassigned, edits, malfunctions, date-range misses. No compliance stamp. No remaining-hours legal math. Do not assign unassigned driving or suggest a duty-status change. Say public limit names are orientation only. A human decides status. Starter / guess until they teach this shop. Date range must cover the route date; if it does not, that is the first question. No fake ELD math.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: hos-questions
steps:
  - id: pull
    needs: []
    produces: eld-raw
    produce_path: work/eld.csv
    tool: docs/tools/eld-export.md
    check: python docs/tools/checks/csv-has-columns.py work/eld.csv driver status
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [eld-raw]
    produces: eld-pack
    produce_path: out/hos-questions.md
    tool: docs/tools/eld-export.md
    check: python docs/tools/checks/file-exists.py out/hos-questions.md
    on_fail: retry
    next: []
```
