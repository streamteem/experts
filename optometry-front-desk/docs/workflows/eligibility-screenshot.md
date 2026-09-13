# Eligibility from screenshot

Quote only the dated screenshot or clearinghouse print they saved: plan name, active wording, exam or materials copay and allowance sentences as printed, image date. No screenshot: ask. Do not invent remaining vision benefits and do not promise the plan will pay. Do not adjudicate VSP or EyeMed. If the image is cropped, stale, or for the wrong member, ask for a dated full page. Quote vision and medical prints separately when both exist. Least PHI on the quote sheet. They verify; you do not log into the payer portal. Card images are not eligibility.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: eligibility-screenshot
steps:
  - id: shots
    needs: []
    produces: elig
    produce_path: work/eligibility.csv
    tool: docs/tools/eligibility-folder.md
    check: python docs/tools/checks/file-exists.py work/eligibility.csv
    on_fail: retry
    next: [columns]
  - id: columns
    needs: [elig]
    produces: elig-cols
    produce_path: work/eligibility.csv
    tool: docs/tools/eligibility-folder.md
    check: python docs/tools/checks/csv-has-columns.py work/eligibility.csv chart date
    on_fail: retry
    next: [write]
  - id: write
    needs: [elig-cols]
    produces: elig-writeup
    produce_path: out/eligibility.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/eligibility.md
    on_fail: retry
    next: []
```
