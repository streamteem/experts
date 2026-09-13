# Vendor insurance-certificate dates

List expiration dates, named insured, and additional-insured wording as printed from certificates they filed. Not a coverage opinion. Flag expired dates, wrong community names, and missing lines their checklist requires for staff. Do not store producer logins. One vendor per row unless they asked for a certificate-aging index. Produce the CSV the checks can see, then the write-up. Confirm the association name on each certificate before you flag a date.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: vendor-certs
steps:
  - id: index
    needs: []
    produces: coi-raw
    produce_path: work/vendor-certs.csv
    tool: docs/tools/vendor-coi.md
    check: python docs/tools/checks/file-exists.py work/vendor-certs.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [coi-raw]
    produces: coi-writeup
    produce_path: out/vendor-certs.md
    tool: docs/tools/vendor-coi.md
    check: python docs/tools/checks/file-exists.py out/vendor-certs.md
    on_fail: retry
    next: []
```
