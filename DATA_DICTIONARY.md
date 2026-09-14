# Data Dictionary

The project is based on a supply-chain dataset containing **100 SKUs** and **24 fields** covering product, sales, inventory, suppliers, manufacturing, quality, and logistics.

| Field | Business Meaning |
|---|---|
| `product_type` | Product category such as Skincare, Haircare, or Cosmetics |
| `sku` | Unique stock keeping unit identifier |
| `price` | Product price |
| `availability` | Product availability measure supplied in the source data |
| `number_of_products_sold` | Units sold for the SKU |
| `revenue_generated` | Revenue recorded for the SKU |
| `customer_demographics` | Customer demographic segment |
| `stock_levels` | Current inventory level |
| `order_lead_time_days` | Lead time associated with orders |
| `order_quantities` | Quantity ordered |
| `shipping_times` | Shipping duration |
| `shipping_carriers` | Shipping carrier used |
| `shipping_costs` | Shipping cost |
| `supplier_name` | Supplier associated with the SKU |
| `location` | Source location in the dataset |
| `supplier_lead_time_days` | Supplier lead time in days |
| `production_volumes` | Manufacturing production volume |
| `manufacturing_lead_time` | Manufacturing lead time |
| `manufacturing_costs` | Manufacturing cost |
| `inspection_results` | Quality inspection outcome: Pass, Fail, or Pending |
| `defect_rates` | Defect-rate measure |
| `transportation_modes` | Transportation mode such as Road, Air, Rail, or Sea |
| `routes` | Transportation route |
| `costs` | Transportation cost measure |

## Important Modeling Notes

### Dataset grain

The current dataset contains one record per SKU. Measures were nevertheless written with explicit aggregation and filter-context logic so the model remains understandable and easier to extend.

### Revenue

`revenue_generated` is treated as the source-of-truth revenue field. It is not recalculated as `price × number_of_products_sold` because the supplied dataset does not consistently satisfy that relationship.

### Inventory risk

Inventory risk is a relative classification based on current sales and stock compared with dynamic portfolio benchmarks. It should not be interpreted as a forecasted stockout probability.

### Time analysis limitation

The source dataset does **not** contain a date field. Therefore, the dashboard intentionally avoids invented monthly trends, seasonality, forecasting, or year-over-year comparisons.

## Product Mix

- Skincare: **40 SKUs**
- Haircare: **34 SKUs**
- Cosmetics: **26 SKUs**

## Quality Inspection Mix

- Pending: **41 SKUs**
- Fail: **36 SKUs**
- Pass: **23 SKUs**
