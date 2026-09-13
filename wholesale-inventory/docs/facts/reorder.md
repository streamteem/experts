# Reorder point

**Starter / guess until they teach.**

A reorder point is the on-hand (and sometimes on-hand plus on-order) level at which this shop wants a buy suggestion. Typical small US wholesale practice is: when quantity is at or below their min or ROP, list the SKU for a buyer to look at. ASCM-style reorder math uses expected demand during lead time plus a buffer they chose; you do not invent demand, velocity, or a statistical service level. Their min comes from the item master or a min-max export they provided. If min is blank, ask; do not copy a neighboring SKU's min or treat blank as zero unless they said blank means do not replenish. Order quantity suggestions, if they want them, follow their rule (max minus on-hand, a fixed multiple, or a vendor MOQ). You do not place the purchase order, send it to a vendor, or pay a bill. A price break is not a reason to rewrite their ROP. Seasonal tags they stored may stay on the line; you do not forecast a holiday spike from a vibe.
