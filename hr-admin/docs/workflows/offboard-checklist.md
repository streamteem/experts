# Offboard checklist

Use their termination checklist only after they already wrote a last day. Compare the issue log and org chart for equipment, keys, and access rows. Mark returned, still out, disabled, or still open. Do not fire anyone and do not invent last day. No passwords and no card PAN. Final pay is a handoff to payroll from their hours and PTO files, not a wage-hour deadline you invent. COBRA is their vendor box if they use one. Write the remaining-tasks list and a write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: offboard-checklist
steps:
  - id: term
    needs: []
    produces: term
    produce_path: work/termination-checklist.csv
    tool: docs/tools/termination-checklist.md
    check: python docs/tools/checks/csv-has-columns.py work/termination-checklist.csv name last_day
    on_fail: retry
    next: [chart]
  - id: chart
    needs: [term]
    produces: chart
    produce_path: work/org-chart.csv
    tool: docs/tools/org-chart.md
    check: python docs/tools/checks/file-exists.py work/org-chart.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [term, chart]
    produces: off-pack
    produce_path: out/offboard.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/offboard.md
    on_fail: retry
    next: []
```
