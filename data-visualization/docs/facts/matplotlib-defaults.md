# Matplotlib defaults are a starting point

**Starter / guess until they teach.**

Matplotlib defaults (font size, grid, color cycle) are a starting point, not a house style you invent as a brand system. Typical US SMB charts need larger tick labels and a tight layout so titles do not clip. The Expert may run Python, import matplotlib.pyplot, set a readable figsize, call tight_layout or constrained_layout, and savefig to out/. Do not spend the pack on ornament. Do not hide the default grid if they want to read values. If matplotlib is missing, ask and install; do not deliver a fake PNG. Style sheets they stored may be used; do not download a random style pack from the web as a scrape. Pin the matplotlib version only if their requirements file says so. Done is a readable file, not a default window that vanished. Starter until they teach *this* shop’s size and font needs.
