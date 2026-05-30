---
description: Generate a margin-safe customer quote. Reads price-book.json and margin-rules.md. Usage: /profit-engine:cost-quote [customer name] [SKUs or service description]
---

Generate a customer-facing quote using the Profit Engine pricing data.

## Steps

1. Read `Profit-Engine/01-cost-sheet/price-book.json` to get available SKUs, list prices, floor prices, and COGS.
2. Read `Profit-Engine/01-cost-sheet/margin-rules.md` for discount policy and tier rules.
3. Match the requested services to SKUs. If a requested service isn't an exact SKU match, suggest the closest one and ask for confirmation.
4. Calculate the proposed price:
   - Start at list price.
   - If the user specified a discount, check it against the approval thresholds in margin-rules.md.
   - Ensure the final price is at or above the floor price for every line item.
5. Output a clean quote in this format:

---
**Quote for [Customer Name]**  
Date: [today]  
Valid through: [today + 30 days]

| SKU | Description | Unit | Qty | Unit Price | Line Total |
|-----|-------------|------|-----|-----------|------------|
| ... | ... | ... | ... | $... | $... |

**Subtotal**: $...  
**Discount applied**: X% ([approval level required])  
**Total**: $...

*Margin check*: All lines above floor price. ✓ / ⚠ [flag any violations]

---

6. If any line is below floor price, flag it with ⚠ and state what the floor price is.
7. Note any discounts that require manager or executive approval per margin-rules.md.
