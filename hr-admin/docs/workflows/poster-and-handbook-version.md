# Poster index and handbook version

Read their poster index and the live handbook PDF. List poster files or wall-check dates as they logged them, plus the handbook version string. Do not invent a legally required poster set. Do not rewrite the handbook. If two handbook PDFs look current, ask which wins. Missing poster on their index is an ask. Write the version-and-poster pack. They hang posters and they publish the book. DOL poster pages are orientation for names they may already use, not a citation list you create.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: poster-and-handbook-version
steps:
  - id: posters
    needs: []
    produces: posters
    produce_path: work/poster-index.csv
    tool: docs/tools/poster-index.md
    check: python docs/tools/checks/file-exists.py work/poster-index.csv
    on_fail: retry
    next: [book]
  - id: book
    needs: [posters]
    produces: handbook
    produce_path: work/handbook-version.txt
    tool: docs/tools/handbook-pdf.md
    check: python docs/tools/checks/file-exists.py work/handbook-version.txt
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [posters, handbook]
    produces: ver-pack
    produce_path: out/poster-handbook-version.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/poster-handbook-version.md
    on_fail: retry
    next: []
```
