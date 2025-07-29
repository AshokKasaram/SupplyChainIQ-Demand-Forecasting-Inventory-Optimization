# 📦 Supply Chain Demand Forecasting & Inventory Optimization

A complete end-to-end project that simulates supply chain inventory and demand data, applies inventory health logic, forecasts future demand using time series models, and presents actionable insights via interactive **Power BI dashboards**.

---

## 📊 Dashboard Preview

### 📌 Inventory Health Overview
![Inventory Overview](<insert path or use GitHub image URL>)

### 📌 Demand Trends & Forecast Overview
![Demand Forecast Overview](<insert path or use GitHub image URL>)

---

## 🛠 Project Overview

This project simulates and analyzes real-world inventory behavior using Python and visualizes inventory performance with Power BI. We focus on:

- Simulating parts and daily demand
- Applying inventory health logic (e.g., reorder point, safety stock)
- Detecting understock/overstock patterns
- Time-series forecasting using Simple Exponential Smoothing
- Building dynamic dashboards for executive-level insights

---

## 🧮 Inventory Logic – Math & Formulas

For each part, we compute:

- **Safety Stock**  
  \[
  SS = Z \times \sigma_d \times \sqrt{L}
  \]  
  Where:  
  - \( Z = 1.65 \) (for 95% service level)  
  - \( \sigma_d \): Std Dev of demand  
  - \( L \): Lead Time in days

- **Reorder Point (ROP)**  
  \[
  ROP = D \times L + SS
  \]  
  Where:  
  - \( D \): Daily average demand  
  - \( L \): Lead time  
  - \( SS \): Safety stock

- **Runout Days**  
  \[
  Runout = \frac{Current\_Stock}{Daily\_Demand}
  \]

- **Stock Status**
  - `Understocked` if `Current_Stock < Reorder_Point`
  - `Overstocked` if `Current_Stock > 1.5 * Reorder_Point`
  - `OK` otherwise

---

## 🧪 Demand Forecasting (Python)

We use **Simple Exponential Smoothing (SES)** to forecast future demand:

```python
from statsmodels.tsa.holtwinters import SimpleExpSmoothing

model = SimpleExpSmoothing(demand_series).fit(smoothing_level=0.2, optimized=False)
forecast_values = model.forecast(forecast_days)
```

This allows us to generate 15-day forecasts per part and compare them with actuals.

---

## 🐍 Python Implementation (Key Steps)

### 1. Dataset Creation
```python
# Simulate 30 real-world parts with categories, lead times, cost, and demand
parts = pd.DataFrame([...])
demand_history = pd.DataFrame([...])
```

### 2. Inventory Logic
```python
df_parts["Safety_Stock"] = Z * stddev * sqrt(lead_time)
df_parts["Reorder_Point"] = daily_demand * lead_time + safety_stock
df_parts["Runout_Days"] = current_stock / daily_demand
df_parts["Stock_Status"] = ... # Based on logic
```

### 3. Demand Forecasting
```python
for part in df_demand["PartID"].unique():
    model = SimpleExpSmoothing(series).fit(...)
    forecast = model.forecast(15)
```

### 4. Validation & Discrepancy Check
```python
# Compare expected vs actual reorder point & stock status
discrepancies = df_parts[df_parts["Expected_Status"] != df_parts["Stock_Status"]]
```

---

## 📈 Power BI Dashboard (Screenshots)

### ✅ Page 1: Inventory Health Overview
- 💰 Total Inventory Value
- ⏳ Average Runout Days
- 📉 Understocked % by Location
- 📦 Current Stock by Part
- 📌 Stock Status Donut Chart

### 📉 Page 2: Demand Trends & Forecasting
- 📅 Daily Actual vs Forecast Demand Line Chart
- ⚙️ Demand by Part (Top Contributors)
- 📉 Forecast Deviation by Part
- 📉 Demand Trend & Run Rate by Location

---

## 📍 Key Insights

- **% Understocked**:
  - California: 0.63  
  - New York: 0.15  
  - Texas: 0.22  
  - Overall: 0.30

- **Top Forecast Deviations**:
  - Seal Ring, Alternator, Throttle Body (over 6K)

- **Most Overstocked Parts**:
  - Axle Shaft, Ball Bearing, Circuit Breaker

- **Dynamic Slicers**:
  - Location, Category, PartName, Date Range

---

## 📁 Folder Structure

```
├── data/
│   ├── Updated_Inventory_Parts_Info.xlsx
│   ├── Updated_Inventory_Analyzed_With_Logic.xlsx
│   └── Updated_Inventory_Daily_Demand_History.xlsx
├── notebooks/
│   ├── inventory_logic.py
│   └── demand_forecasting.py
├── dashboard/
│   └── Inventory_Analysis.pbix
├── README.md
```

---

## 📌 Tools Used

- **Python**: Pandas, NumPy, statsmodels
- **Power BI**: DAX, custom visuals, filters
- **Excel**: For data handoff
- **Statistical Logic**: Inventory theory (ROP, Safety Stock)

---

## 🚀 Future Enhancements

- Integrate Prophet/ARIMA models
- Add inventory cost optimization logic
- Embed Power BI reports to web
- Enable real-time data connection (SQL/SharePoint)
---
