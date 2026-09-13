# Architectural form completeness

List missing pages, sketches, neighbor notes, and unsigned fields on the architectural application they use, against their form or guidelines. Not an approval or denial and not a committee stamp. A lot that does not match the roster is a question. One application per row unless they asked for a batch completeness list. Produce the CSV the checks can see, then the write-up.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: acc-completeness
steps:
  - id: list
    needs: []
    produces: acc-raw
    produce_path: work/acc-forms.csv
    tool: docs/tools/acc-form.md
    check: python docs/tools/checks/file-exists.py work/acc-forms.csv
    on_fail: retry
    next: [write]
  - id: write
    needs: [acc-raw]
    produces: acc-writeup
    produce_path: out/acc-check.md
    tool: docs/tools/acc-form.md
    check: python docs/tools/checks/file-exists.py out/acc-check.md
    on_fail: retry
    next: []
```
