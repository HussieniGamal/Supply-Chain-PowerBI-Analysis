# Project Insights & Stakeholder Recommendations

## Executive Summary

This Power BI project analyzes supply-chain performance across 100 SKUs and connects commercial performance with inventory, supplier, manufacturing, and logistics decisions.

The dataset represents approximately **$577.6K in revenue** and **46,099 units sold**.

## 1. Commercial Performance

### Skincare is the strongest product category

- Revenue: approximately **$241.6K**
- Units sold: approximately **20.7K**
- It leads both revenue and sales volume.

### Business implication

Skincare should receive close attention in inventory planning and production capacity because shortages in the strongest category can have a disproportionate impact on commercial performance.

---

## 2. Inventory Risk

The dashboard flags:

- **21 Potential Stockout SKUs**
- **25 Potential Overstock SKUs**

The classification compares each SKU's stock and sales against dynamic portfolio benchmarks.

### Potential Stockout

High sales + low stock.

**Recommended action:** prioritize replenishment and review supplier lead times for affected SKUs.

### Potential Overstock

Low sales + high stock.

**Recommended action:** review purchasing quantities, reduce future replenishment, and consider promotional or redistribution strategies.

### Business implication

The coexistence of stockout and overstock signals suggests that inventory may be sufficient in aggregate but distributed inefficiently across products.

---

## 3. Supplier Performance

### Supplier 3

- Longest average supplier lead time: approximately **20.13 days**

**Recommended action:** investigate lead-time drivers and consider alternative sourcing for time-sensitive SKUs.

### Supplier 5

- Highest average defect rate: approximately **2.67**

**Recommended action:** strengthen quality requirements, root-cause analysis, and incoming inspection monitoring.

### Supplier 1

- Lowest average defect rate: approximately **1.80**
- Strong lead-time performance
- However, it is linked to the highest number of stock-risk SKUs in the current analysis: **7**

**Recommended action:** investigate ordering frequency and replenishment policies before interpreting stock risk as a supplier performance problem.

---

## 4. Manufacturing Performance

- Total production volume: approximately **57K**
- Average manufacturing cost: approximately **47**
- Average manufacturing lead time: approximately **15 days**
- Failed inspections: **36**
- Average defect rate: **2.28**

### Category observations

- Skincare has the highest production volume at approximately **24K**.
- Haircare has the longest average manufacturing lead time at approximately **17.06 days**.
- Skincare has the highest average manufacturing cost at approximately **49**.

### Business implication

Manufacturing performance should be evaluated using a combined view of cost, lead time, production volume, and quality rather than optimizing a single KPI independently.

---

## 5. Shipping & Logistics

### Shipping speed

- Carrier B: fastest average shipping time at approximately **5.30 days**
- Road: fastest transportation mode at approximately **4.72 days**
- Sea: slowest transportation mode at approximately **7.12 days**

### Transportation cost

- Air: highest average transportation cost at approximately **562**
- Route B: highest average route cost at approximately **596**

### Business implication

The cheapest option is not always the fastest and the fastest option is not always the most economical. Transportation decisions should therefore consider service level and cost together.

---

# Stakeholder Action Priorities

## Priority 1 — Inventory Availability

1. Review the 21 potential stockout SKUs.
2. Prioritize high-demand products with long replenishment lead times.
3. Validate safety-stock and reorder-point policies once historical demand data becomes available.

## Priority 2 — Working Capital

1. Review the 25 potential overstock SKUs.
2. Investigate purchasing quantities and replenishment frequency.
3. Reduce excess inventory where demand does not justify current stock.

## Priority 3 — Supplier Risk

1. Review Supplier 3 for lead-time performance.
2. Review Supplier 5 for quality performance.
3. Investigate why Supplier 1 is associated with multiple stock-risk SKUs despite strong quality and lead-time metrics.

## Priority 4 — Manufacturing Efficiency

1. Investigate Haircare's longer manufacturing lead time.
2. Review high-cost Skincare production.
3. Track manufacturing cost, lead time, and defect rate together.

## Priority 5 — Logistics Optimization

1. Validate why Route B carries the highest average transportation cost.
2. Compare Road and Air based on required service level.
3. Use carrier performance to support shipping allocation decisions.

---

# Recommended Future Enhancements

The current dataset has no date dimension. A future version of the project would benefit from:

- Historical demand by SKU
- Order dates and delivery dates
- Purchase-order history
- Supplier OTIF performance
- Inventory snapshots
- Stockout dates
- Safety stock
- Reorder point
- Inventory turnover
- Days of inventory
- Forecast accuracy
- Service level / fill rate

These additions would allow the dashboard to move from descriptive and diagnostic analytics toward more advanced forecasting and inventory planning.
