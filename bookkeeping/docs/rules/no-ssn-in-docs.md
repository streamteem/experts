# No SSN or EIN in docs

**Starter / guess until they teach.**

This rule exists because taxpayer ID numbers in docs/, work CSVs, or write-ups are a leak and are not needed for coding or a 1099 tracker. W-9 and 1099 work notes the file path and missing or present. Do not transcribe Social Security numbers, EINs, or other TINs into docs/, work CSVs, or write-ups. Exception: if their vendor export includes a TIN column you cannot strip without breaking their file, do not copy that column into a new sheet you author, and do not paste IDs into markdown. Never type an ID from a W-9 photo. Flag present or missing only.
