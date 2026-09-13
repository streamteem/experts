# Export the CSV of what was plotted

**Starter / guess until they teach.**

Every chart pack includes a CSV of the values that actually went to the picture: the aggregated x, y, group, and n. Typical US SMB arguments are “the chart is wrong” with no table. The Expert writes work/*.csv via pandas to_csv after the groupby and before or after savefig. Column names stay readable. Filters and the source file name belong in the write-up and may be extra columns if they asked. Do not export extra PII that was not plotted. Do not export a different aggregation than the PNG. The check for many workflows is that this CSV exists and has the expected columns. Refresh writes a new dated CSV or a clear name so last week is not overwritten unless they said replace. Starter until they teach where *this* shop files the numbers behind the picture and whether last week’s CSV is kept.
