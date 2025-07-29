# SupplyChainIQ-Demand Forecasting & Inventory Optimization

A comprehensive end-to-end supply chain inventory optimization and forecasting project built with Python and Power BI. This solution simulates real-world parts inventory, forecasts demand using time series models, and visualizes critical inventory KPIs for informed decision-making.

---

## Project Overview

This project focuses on simulating inventory behavior and forecasting demand across multiple part categories and warehouse locations. The primary goal is to track inventory health, predict upcoming demand, detect under/overstock risks, and deliver actionable insights through dynamic Power BI dashboards.

---

## Dashboard Preview

### Inventory Health Overview
![Inventory Overview](<https://github.com/AshokKasaram/SupplyChainIQ-Demand-Forecasting-Inventory-Optimization/blob/main/SupplyChainIQ/Images/Page1.JPG>)

### Demand Trends & Forecast Overview
![Demand Forecast Overview](<https://github.com/AshokKasaram/SupplyChainIQ-Demand-Forecasting-Inventory-Optimization/blob/main/SupplyChainIQ/Images/Page2.JPG>)

---

## Key Objectives

- Simulate realistic part demand and inventory behavior
- Implement statistical inventory control logic
- Forecast future demand using time series models
- Track and visualize trends using Power BI
- Identify parts at risk of understocking or overstocking
- Build FAANG-level dashboards with smart filters and drill-downs

---

## Technologies Used

- **Python** (Pandas, NumPy, Statsmodels)
- **Power BI** (DAX, Power Query)
- **Excel** (for simulation data output)
- **Statsmodels** (Simple Exponential Smoothing)

---

## Project Structure

```
bash
├── data/
│   ├── Updated_Inventory_Parts_Info.xlsx
│   ├── Updated_Inventory_Daily_Demand_History.xlsx
│   └── Simple_Forecasted_Demand_Per_Part.xlsx
├── notebooks/
│   └── inventory_forecasting_analysis.ipynb
├── dashboards/
│   └── SupplyChain_Inventory_Forecasting.pbix
├── README.md
```

---

## Data Generation & Simulation (Python)

### Dataset Creation

- Simulated 30 unique part names with attributes like category, location, daily demand, unit cost, lead time, and demand variability.
- Generated 90-day historical demand data per part using Gaussian distribution centered around daily demand.

### Sample Part Features

- PartID, PartName
- Category (Electrical, Mechanical, Hydraulic, Pneumatic)
- Location (New York, California, Texas, Illinois)
- Daily\_Demand, StdDev\_Demand, UnitCost
- Current\_Stock, LeadTime\_Days

---

## Inventory Logic – Math & Formulas

For each part:

### Safety Stock

```
SS = Z * σ_d * sqrt(L)
```

Where:

- `Z = 1.65` (for 95% service level)
- `σ_d`: Std deviation of daily demand
- `L`: Lead Time (in days)

### Reorder Point (ROP)

```
ROP = D * L + SS
```

Where:

- `D`: Daily average demand
- `L`: Lead time
- `SS`: Safety stock

### Runout Days

```
Runout = Current_Stock / Daily_Demand
```

### Stock Status Logic

```
Understocked   if Current_Stock < Reorder_Point
Overstocked   if Current_Stock > 1.5 * Reorder_Point
OK            otherwise
```

---

## Demand Forecasting (Python)

Used **Simple Exponential Smoothing (SES)** for each part's 90-day historical demand:

- Smoothing level = 0.2
- Forecast horizon = 15 days
- Model used: `statsmodels.tsa.holtwinters.SimpleExpSmoothing`

Generated part-level future demand estimates saved to Excel.

---

## Power BI Dashboard

Built a two-page interactive dashboard to visualize insights.

### Page 1: Inventory Health Overview

**Visuals:**

- Total Inventory Value
- Average Runout Days
- Percent Understocked
- Current Stock by PartName (Bar Chart)
- Stock Status Breakdown (Donut Chart)
- Part Inventory Summary (Table with KPIs)

**DAX Highlights:**

- `% Understocked = CALCULATE(COUNTROWS(...), ...)/ COUNTROWS(...)`
- `Average Runout Days = AVERAGE(df[Runout_Days])`

---

### Page 2: Demand Trends & Forecast Overview

**Visuals:**

- Total Actual Demand vs Forecasted Demand
- Actual vs Forecasted Trend Line by Date
- Top Parts by Demand (Bar Chart)
- Forecast Deviation by PartName
- Forecast Accuracy, 30/Prev 30 Day Trend

**Key Metrics:**

- `Forecast Deviation = ABS(Total Forecast - Actual)`
- `Demand_Trend = (Last30 - Prev30) / Prev30`
- `Trend Type = IF(Trend < 0, "Falling", "Rising")`

**Note:** MAPE was removed due to divide-by-zero issues from low-volume parts.

---

## Key Learnings

- Implemented statistical inventory logic with business thresholds
- Built reusable Python pipelines for simulation and forecasting
- Designed executive-level dashboards using filters, cards, slicers, and calculated KPIs
- Applied storytelling techniques for data transparency and interpretability

---

## Future Enhancements

- Integrate real-time stock data via APIs
- Replace SES with ARIMA or Prophet for better forecast accuracy
- Add anomaly detection for demand spikes
- Enable alert system for understocked/overstocked parts

---

## Tags

`#SupplyChain` `#Forecasting` `#InventoryManagement` `#Python` `#PowerBI` `#FAANGReady` `#DataStorytelling`

---


