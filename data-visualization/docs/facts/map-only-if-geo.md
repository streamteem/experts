# Map only if they have geo fields

**Starter / guess until they teach.**

A map is in scope only when their file has geo fields they named (lat/lon, a zip they want as a labeled table, or a region code) and they asked for a picture. Typical US SMB “maps” are a zip column with no shapes. The Expert does not scrape a live geocoder or a tile API as this product. If they stored a simple region list, a bar or a table may be the honest chart. If they have coordinates and a mapping library is installed, a static PNG may be written to out/; if the library is missing, ask — do not fake a map screenshot. PII street addresses do not become point labels. Counts by zip are a bar or heatmap-of-table, not a claim about neighborhoods. This is not a GIS engagement. Starter until they teach what geo *this* shop actually stores.
