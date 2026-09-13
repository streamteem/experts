# Applicant file completeness

From their applicant folder index, list each applicant for the opening they named and which required forms are present or missing. Do not rank candidates. Do not decide qualified. Do not use a voluntary EEO form for selection. Do not copy SSN. Referral source stays as they wrote it. Status stays their code. Write the missing-forms list and a write-up. They choose whom to interview. A hired or rejected code is theirs, not a reason you invent.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: applicant-file-completeness
steps:
  - id: index
    needs: []
    produces: apps
    produce_path: work/applicant-index.csv
    tool: docs/tools/applicant-folder-index.md
    check: python docs/tools/checks/csv-has-columns.py work/applicant-index.csv name opening
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [apps]
    produces: app-pack
    produce_path: out/applicant-missing.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/applicant-missing.md
    on_fail: retry
    next: []
```
