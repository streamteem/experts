# Rolling mean only as a helper series

**Starter / guess until they teach.**

A rolling mean is a helper series they asked for, with a window they named (7-day, 4-week). Typical US SMB owners want a less jumpy line next to the raw daily series. The Expert may run Python, import pandas, and call rolling mean on the measure they named, then plot raw and rolled together or as they asked, saving a PNG and a work CSV with both columns. The window and whether the window is centered or trailing must be written on the chart. Do not replace the raw series without asking. Do not pick a window that makes a desired shape. Do not treat a smooth as a forecast or a seasonal adjustment. Edges of the series have a shorter window or are blank — say which. Missing days affect the roll; do not impute unless they said how. This is descriptive. It is not a trading signal. If pandas is missing, ask; do not hand-draw a smooth. Starter until they teach which window *this* shop uses for weekly packs.
