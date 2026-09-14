# DAX Measures Used in the Project

Below are the main DAX patterns used in the Supply Chain Power BI project.

## Core Measures

```DAX
Total Revenue =
SUM(supply_chain_data_cleaned[revenue_generated])
```

```DAX
Total Units Sold =
SUM(supply_chain_data_cleaned[number_of_products_sold])
```

```DAX
Total SKUs =
DISTINCTCOUNT(supply_chain_data_cleaned[sku])
```

```DAX
Avg Revenue per SKU =
DIVIDE(
    [Total Revenue],
    [Total SKUs]
)
```

```DAX
Revenue per Unit =
DIVIDE(
    [Total Revenue],
    [Total Units Sold]
)
```

## Revenue Share

```DAX
Revenue Share % =
DIVIDE(
    [Total Revenue],
    CALCULATE(
        [Total Revenue],
        ALLSELECTED(supply_chain_data_cleaned[sku])
    )
)
```

`ALLSELECTED` preserves the user's current report selections while removing the current SKU row context from the denominator.

## Revenue Ranking

```DAX
Revenue Rank =
RANKX(
    ALLSELECTED(supply_chain_data_cleaned[sku]),
    [Total Revenue],
    ,
    DESC,
    DENSE
)
```

## Inventory Benchmarks

```DAX
Benchmark Avg Stock =
CALCULATE(
    AVERAGE(supply_chain_data_cleaned[stock_levels]),
    REMOVEFILTERS(supply_chain_data_cleaned[sku])
)
```

```DAX
Benchmark Avg Sales =
CALCULATE(
    AVERAGE(supply_chain_data_cleaned[number_of_products_sold]),
    REMOVEFILTERS(supply_chain_data_cleaned[sku])
)
```

## Potential Stockout SKU Count

```DAX
Stock Risk SKUs =
SUMX(
    VALUES(supply_chain_data_cleaned[sku]),

    VAR CurrentStock =
        CALCULATE(
            SELECTEDVALUE(supply_chain_data_cleaned[stock_levels])
        )

    VAR CurrentSales =
        CALCULATE(
            SELECTEDVALUE(supply_chain_data_cleaned[number_of_products_sold])
        )

    VAR AvgStock =
        [Benchmark Avg Stock]

    VAR AvgSales =
        [Benchmark Avg Sales]

    RETURN
        IF(
            CurrentSales > AvgSales &&
            CurrentStock < AvgStock,
            1,
            0
        )
)
```

## Potential Overstock SKU Count

```DAX
Overstock SKUs =
SUMX(
    VALUES(supply_chain_data_cleaned[sku]),

    VAR CurrentStock =
        CALCULATE(
            SELECTEDVALUE(supply_chain_data_cleaned[stock_levels])
        )

    VAR CurrentSales =
        CALCULATE(
            SELECTEDVALUE(supply_chain_data_cleaned[number_of_products_sold])
        )

    VAR AvgStock =
        [Benchmark Avg Stock]

    VAR AvgSales =
        [Benchmark Avg Sales]

    RETURN
        IF(
            CurrentSales < AvgSales &&
            CurrentStock > AvgStock,
            1,
            0
        )
)
```

## Inventory Risk Classification

```DAX
Inventory Risk Status =
VAR CurrentStock =
    SELECTEDVALUE(supply_chain_data_cleaned[stock_levels])

VAR CurrentSales =
    SELECTEDVALUE(supply_chain_data_cleaned[number_of_products_sold])

VAR AvgStock =
    [Benchmark Avg Stock]

VAR AvgSales =
    [Benchmark Avg Sales]

RETURN
    SWITCH(
        TRUE(),

        CurrentSales > AvgSales &&
        CurrentStock < AvgStock,
        "Potential Stockout",

        CurrentSales < AvgSales &&
        CurrentStock > AvgStock,
        "Potential Overstock",

        CurrentSales >= AvgSales &&
        CurrentStock >= AvgStock,
        "Healthy High Demand",

        "Low Priority"
    )
```

## Quality & Supplier Measures

```DAX
Avg Defect Rate =
AVERAGE(supply_chain_data_cleaned[defect_rates])
```

```DAX
Failed Inspections =
CALCULATE(
    COUNTROWS(supply_chain_data_cleaned),
    supply_chain_data_cleaned[inspection_results] = "Fail"
)
```

```DAX
Supplier Count =
DISTINCTCOUNT(supply_chain_data_cleaned[supplier_name])
```

```DAX
Avg Supplier Lead Time =
AVERAGE(supply_chain_data_cleaned[supplier_lead_time_days])
```

## Manufacturing Measures

```DAX
Total Production Volume =
SUM(supply_chain_data_cleaned[production_volumes])
```

```DAX
Avg Manufacturing Cost =
AVERAGE(supply_chain_data_cleaned[manufacturing_costs])
```

```DAX
Avg Manufacturing Lead Time =
AVERAGE(supply_chain_data_cleaned[manufacturing_lead_time])
```

## Shipping & Logistics Measures

```DAX
Avg Shipping Time =
AVERAGE(supply_chain_data_cleaned[shipping_times])
```

```DAX
Avg Shipping Cost =
AVERAGE(supply_chain_data_cleaned[shipping_costs])
```

```DAX
Avg Transportation Cost =
AVERAGE(supply_chain_data_cleaned[costs])
```

```DAX
Carrier Count =
DISTINCTCOUNT(supply_chain_data_cleaned[shipping_carriers])
```

```DAX
Route Count =
DISTINCTCOUNT(supply_chain_data_cleaned[routes])
```
