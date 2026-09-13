# Option-period pack

Calendar the option or termination-option window from the executed exhibit and the effective-date rule in their file. Show day count, day type, end date, option-fee receipt present or missing, and any executed extension. Do not invent a typical ten days. Do not advise terminate or proceed. A text is not a termination. Earnest money stays a log; you do not hold it. If the method for counting days is missing, stop and ask before you write an end date.

Starter work map. Replace tools and checks when they **teach**.

```yaml
id: option-period-pack
steps:
  - id: contract
    needs: []
    produces: option-dates
    produce_path: work/option-dates.csv
    tool: docs/tools/contract-pdf.md
    check: python docs/tools/checks/csv-has-columns.py work/option-dates.csv file option_end
    on_fail: retry
    next: [calendar]
  - id: calendar
    needs: [option-dates]
    produces: option-calendar
    produce_path: work/option-calendar.csv
    tool: docs/tools/dates-calendar.md
    check: python docs/tools/checks/file-exists.py work/option-calendar.csv
    on_fail: retry
    next: [pack]
  - id: pack
    needs: [option-dates, option-calendar]
    produces: option-pack
    produce_path: out/option-period.md
    tool: docs/tools/spreadsheet.md
    check: python docs/tools/checks/file-exists.py out/option-period.md
    on_fail: retry
    next: []
```
