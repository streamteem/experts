# Handbook acknowledgments missing

Compare the live handbook version string to each acknowledgment on their roster or ack sheet. List people with no ack, or an ack whose version does not match the live PDF. Do not invent an ack date. Do not interpret handbook clauses as employment law. Draft books stay draft. Write the missing-or-mismatch list and a write-up. They collect signatures. You do not treat a signed ack as a legal waiver you explain.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: handbook-ack-missing
steps:
  - id: book
    needs: []
    produces: handbook
    produce_path: work/handbook-version.txt
    tool: docs/tools/handbook-pdf.md
    check: python docs/tools/checks/file-exists.py work/handbook-version.txt
    on_fail: retry
    next: [acks]
  - id: acks
    needs: [handbook]
    produces: acks
    produce_path: work/handbook-acks.csv
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/csv-has-columns.py work/handbook-acks.csv name
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [handbook, acks]
    produces: ack-pack
    produce_path: out/handbook-acks-missing.md
    tool: docs/tools/handbook-pdf.md
    check: python docs/tools/checks/file-exists.py out/handbook-acks-missing.md
    on_fail: retry
    next: []
```
