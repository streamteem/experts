# Incident routing pack

From the incident log and completed forms, list time, patient-dog, form present or missing, and who was notified as their process. Do not diagnose. Do not write a legal opinion on a bite. Do not bury interrupt rows. Minimum data: IDs and filenames. Escapes stay on the same pack if they logged them. Starter / guess until they teach who is interrupted and the current form version.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: incident-routing
steps:
  - id: log
    needs: []
    produces: inc
    produce_path: work/incidents.csv
    tool: docs/tools/incident-log.md
    check: python docs/tools/checks/csv-has-columns.py work/incidents.csv time patient
    on_fail: retry
    next: [form]
  - id: form
    needs: [inc]
    produces: forms
    produce_path: work/incident-forms.csv
    tool: docs/tools/incident-form.md
    check: python docs/tools/checks/csv-has-columns.py work/incident-forms.csv file patient
    on_fail: retry
    next: [write]
  - id: write
    needs: [inc, forms]
    produces: inc-pack
    produce_path: out/incident-routing.md
    tool: docs/tools/incident-log.md
    check: python docs/tools/checks/file-exists.py out/incident-routing.md
    on_fail: retry
    next: []
```
