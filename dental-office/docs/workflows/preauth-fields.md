# Predetermination paperwork check

Check that predetermination requests have the fields and attachments they require. No approval promise. No CDT choice. Copy a preauth number only from their payer letter or portal print; do not invent one. The dentist chooses what is proposed. Name attachment files or say missing; do not write the narrative or read films. A predetermination is not a scheduled visit and not a paid claim. Least PHI on the check sheet.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: preauth-fields
steps:
  - id: pull
    needs: []
    produces: preauth-raw
    produce_path: work/preauth.csv
    tool: docs/tools/claim-form-pdf.md
    check: python docs/tools/checks/file-exists.py work/preauth.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [preauth-raw]
    produces: preauth-writeup
    produce_path: out/preauth-check.md
    tool: docs/tools/claim-form-pdf.md
    check: python docs/tools/checks/file-exists.py out/preauth-check.md
    on_fail: retry
    next: []
```
