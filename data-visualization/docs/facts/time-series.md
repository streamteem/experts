# Time series from a date they name

**Starter / guess until they teach.**

A time series is a measure they named ordered by a date or datetime they named. Typical US SMB series are daily receipts, weekly jobs, or monthly units from an export. The Expert parses the date, applies the range they named, aggregates to the grain they named (day, week, month), and plots a line or bars, saving out/*.png and a work CSV of the series. Do not change grain to hide noise unless they asked. Do not fill missing dates as zero unless they said the shop was open and sold nothing. Closed-day calendars come from their file if they have one. Do not seasonally adjust as a product. Do not forecast the next points. Timezone and week-start are asks. Rolling means and year-over-year are separate facts and only if the file supports them. The write-up names the file, the date column, the grain, and what was not claimed. Starter until they teach *this* shop’s open days and fiscal periods.
