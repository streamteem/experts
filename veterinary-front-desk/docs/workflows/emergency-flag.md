# Emergency-wording flag list

From today's book or message log, list rows with emergency wording first. Flag for staff. Do not triage as a vet. Keep the client's words. Do not give home-care steps or say the animal can wait. After-hours rows quote their posted number rather than managing the case. Put the flag in the first lines of the write-up, not at the end of a neat list. Starter / guess until they teach who is interrupted.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: emergency-flag
steps:
  - id: pull
    needs: []
    produces: flag-raw
    produce_path: work/emergency-flags.csv
    tool: docs/tools/pims-export.md
    check: python docs/tools/checks/file-exists.py work/emergency-flags.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [flag-raw]
    produces: flag-writeup
    produce_path: out/emergency-flags.md
    tool: docs/tools/pims-export.md
    check: python docs/tools/checks/file-exists.py out/emergency-flags.md
    on_fail: retry
    next: []
```
