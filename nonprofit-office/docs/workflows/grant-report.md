# Grant report from their PDFs

Map the funder template questions to program files and the grant financial export they coded to that award. Flag missing attachments, missing census months, and template-versus-agreement mismatches. Fill narrative only from cited files. Do not invent outcomes or headcount. They submit. You do not click the portal. Budget-versus-actual variances stay questions, not silent rebudgets. Period and fund code come from the award PDF. Output is the template in work/, the program extract, and a report map that shows what is present and what still needs staff.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: grant-report
steps:
  - id: tmpl
    needs: []
    produces: template
    produce_path: work/funder-template.pdf
    tool: docs/tools/grant-pdf.md
    check: python docs/tools/checks/file-exists.py work/funder-template.pdf
    on_fail: retry
    next: [program]
  - id: program
    needs: [template]
    produces: program
    produce_path: work/program.csv
    tool: docs/tools/program-report-folder.md
    check: python docs/tools/checks/file-exists.py work/program.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [template, program]
    produces: report-out
    produce_path: out/grant-report.md
    tool: docs/tools/grant-pdf.md
    check: python docs/tools/checks/file-exists.py out/grant-report.md
    on_fail: retry
    next: []
```
