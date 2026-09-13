# Credential expirations

From their credential log and employee list, list types with expiration or issued dates on or before the pack date they asked for, plus blank dates on types they said they track. Do not invent a date or a required cert. Do not decide the license is the right class. Do not copy license numbers when dates will do. Do not write a background verdict. Write the due-and-missing list and a write-up. They decide who may still be sent.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: credential-expirations
steps:
  - id: creds
    needs: []
    produces: creds
    produce_path: work/credentials.csv
    tool: docs/tools/credential-log.md
    check: python docs/tools/checks/csv-has-columns.py work/credentials.csv name date
    on_fail: retry
    next: [people]
  - id: people
    needs: [creds]
    produces: people
    produce_path: work/employee-list.csv
    tool: docs/tools/employee-list.md
    check: python docs/tools/checks/file-exists.py work/employee-list.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [creds, people]
    produces: cred-pack
    produce_path: out/credential-expirations.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/credential-expirations.md
    on_fail: retry
    next: []
```
