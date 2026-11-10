# Supply Chain Inventory Risk Analysis with KNIME

An inventory analytics project built with **KNIME Analytics Platform**, focused on stock coverage, replenishment lead times, and warehouse-level inventory risk.

> **Data disclaimer:** This project uses synthetic data for educational and portfolio purposes. It does not represent a real company's operations.

## Project Overview

The goal is to identify product–warehouse combinations at risk of running out of stock before replenishment arrives. The workflow calculates stock coverage, compares it against supplier lead time, classifies inventory risk, and summarizes records by warehouse.

## Dataset

The `supply_chain_inventory_sample.csv` dataset contains **60 records**, covering **20 products** and **3 warehouses** (Istanbul, Ankara, and Izmir).

| Column | Description |
| --- | --- |
| `Product_ID` | Product identifier |
| `Product_Name` | Product name |
| `Category` | Product category |
| `Warehouse` | Warehouse location |
| `Stock_Quantity` | Current stock in units |
| `Daily_Sales` | Daily sales in units |
| `Lead_Time_Days` | Replenishment lead time in days |
| `Unit_Price` | Unit price |

## KNIME Workflow

`CSV Reader → Math Formula → Math Formula → Rule Engine → GroupBy → Bar Chart`

1. **CSV Reader:** Import the inventory CSV dataset.
2. **Math Formula:** Calculate the estimated number of days the current stock will last.
3. **Math Formula:** Calculate the difference between stock coverage and replenishment lead time.
4. **Rule Engine:** Classify inventory risk into High, Medium, or Low.
5. **GroupBy:** Count product records by warehouse and risk level.
6. **Bar Chart:** Visualize the grouped warehouse counts.

## Calculations

**Days of Stock**

```text
Days_of_Stock = Stock_Quantity / Daily_Sales
```

**Stock Coverage Gap**

```text
Stock_Coverage_Gap = Days_of_Stock - Lead_Time_Days
```

### Risk Classification

| Condition | Classification | Interpretation |
| --- | --- | --- |
| `Stock_Coverage_Gap < 0` | High Risk | Stock may run out before replenishment |
| `0 <= Stock_Coverage_Gap <= 3` | Medium Risk | Limited coverage buffer |
| `Stock_Coverage_Gap > 3` | Low Risk | More than three days of coverage buffer |

**Example:** A product with 44 units in stock and 27 daily sales has approximately **1.63 days** of stock coverage. If replenishment takes 13 days, its coverage gap is approximately **−11.37 days**, so it is classified as **High Risk**.

## How to Run

1. Install [KNIME Analytics Platform](https://www.knime.com/downloads).
2. Open the uploaded `Supply_Chain_Inventory_Analytics` workflow folder in KNIME, or import the `.knwf` file if provided.
3. Open the **CSV Reader** node and select the repository's `supply_chain_inventory_sample.csv` file. The saved workflow may reference a local path from the original computer.
4. Execute the workflow nodes from left to right.
5. Inspect the Rule Engine and GroupBy output tables and open the Bar Chart view.

## Limitations and Future Improvements

- Daily sales are assumed constant; this is a simple inventory coverage calculation, **not a demand forecasting model**.
- Zero sales and missing values require explicit handling before applying the workflow to operational data.
- The initial bar chart shows warehouse-grouped counts but does not clearly identify the risk category of each bar. A pivoted stacked bar chart would improve interpretation.
- Possible extensions include safety stock, reorder points, supplier reliability, and demand forecasting.

## Tools and Skills

**KNIME Analytics Platform**, CSV data processing, calculated features, rule-based classification, aggregation, and data visualization.

## Author

**Özgür Yılmaz** — Computer Engineering student

*Personal portfolio project using synthetic data.*
