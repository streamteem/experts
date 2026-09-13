# Facility requests missing COI

Index facility requests they stored, then mark which still-scheduled outside uses lack a COI on their checklist. Do not approve the request. Do not decide coverage or invent a limit. Expired certificates on live dates stay flagged. Member-only exemptions come only from their policy sentence. Write-up is a missing-COI list plus form-versus-calendar holes. They chase the group. You do not waive a certificate.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: facility-coi-missing
steps:
  - id: requests
    needs: []
    produces: requests
    produce_path: work/facility-requests.csv
    tool: docs/tools/facility-request-folder.md
    check: python docs/tools/checks/file-exists.py work/facility-requests.csv
    on_fail: retry
    next: [coi]
  - id: coi
    needs: [requests]
    produces: coi
    produce_path: work/coi-index.csv
    tool: docs/tools/coi-folder.md
    check: python docs/tools/checks/file-exists.py work/coi-index.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [requests, coi]
    produces: coi-pack
    produce_path: out/facility-coi-missing.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/facility-coi-missing.md
    on_fail: retry
    next: []
```
