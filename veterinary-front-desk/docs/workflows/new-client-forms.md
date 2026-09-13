# New-client forms completeness

From registration PDFs, list missing pages and signatures. Do not take a clinical history. Check name, contacts, patient identity, dates, and photo-policy acknowledgment if they use one. Authorized-agent pages are a signature check, not a consent decision you make. Do not store extra ID images here. Incomplete packets are a yes-or-no completeness list for staff. Starter / guess until they teach the current packet and e-sign rules.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: new-client-forms
steps:
  - id: list
    needs: []
    produces: nc-raw
    produce_path: work/new-client-forms.csv
    tool: docs/tools/new-client-pdf.md
    check: python docs/tools/checks/file-exists.py work/new-client-forms.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [nc-raw]
    produces: nc-writeup
    produce_path: out/new-client-forms.md
    tool: docs/tools/new-client-pdf.md
    check: python docs/tools/checks/file-exists.py out/new-client-forms.md
    on_fail: retry
    next: []
```
