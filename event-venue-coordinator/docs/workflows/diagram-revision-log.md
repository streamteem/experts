# Diagram revision log

List diagram PDFs by event, date, and revision label. Mark the latest dated file and any undated overwrite. Note chair-count changes that no longer match the BEO if that pack was also pulled. Do not stamp fire approval. Do not silently replace a signed layout. They send the new PDF to the floor. You deliver the revision log plus write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: diagram-revision-log
steps:
  - id: diags
    needs: []
    produces: diagrams
    produce_path: work/diagrams.csv
    tool: docs/tools/diagram-pdf.md
    check: python docs/tools/checks/file-exists.py work/diagrams.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [diagrams]
    produces: rev-pack
    produce_path: out/diagram-revision-log.md
    tool: docs/tools/diagram-pdf.md
    check: python docs/tools/checks/file-exists.py out/diagram-revision-log.md
    on_fail: retry
    next: []
```
