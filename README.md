# Global Procurement & Supplier Performance Analytics

An end-to-end procurement analytics project that transforms purchasing, supplier delivery, and contract data into decision-ready insights using **Power BI and Python**. The solution covers spend and savings analysis, supplier performance, contract compliance, supplier risk and anomaly detection, spend forecasting, and supplier segmentation.

The project uses a synthetic enterprise procurement dataset inspired by **AdventureWorks Purchasing** and **SAP MM** concepts, providing a realistic environment for demonstrating an end-to-end procurement analytics workflow.

---

## Executive Summary

Procurement teams need a reliable, integrated view of spend, savings, supplier performance, contract compliance, and supplier risk to identify sourcing opportunities and prioritize supplier-management actions. This project addresses that need through a **Power BI analytics solution** supported by **Python-based advanced analytics**, bringing historical performance, supplier risk, forecasting, and segmentation into a connected reporting environment.

The report consists of **seven analytical dashboard pages plus a dedicated validation page**, covering Executive Overview, Spend & Savings, Supplier Performance, Contract Compliance, Supplier Risk, Spend Forecasting, and Supplier Segmentation. Python extends the reporting layer through composite supplier risk scoring, anomaly detection, six-month spend forecasting, and supplier segmentation.

Together, these capabilities provide visibility into procurement spend and savings, OTIF and quality performance, contract and maverick spend, supplier risk, forward-looking spend scenarios, and supplier portfolio composition — supporting both operational performance monitoring and **forward-looking procurement decision-making**.

---

### Dashboard Preview

![Executive Overview](images/executive-overview.png)

*Executive overview of procurement spend, savings, supplier delivery performance, contract compliance, and category-level contribution.*

---

## Business Problem

Procurement decisions depend on information spread across purchasing, delivery, supplier, contract, and spend data. Without an integrated analytical view, it can be difficult to consistently understand where money is being spent, which suppliers are underperforming, where contract leakage is occurring, and which areas require management attention.

This project addresses six core procurement challenges:

- **Fragmented spend visibility** — purchasing and supplier data must be brought together to provide a consistent view of spend, savings, categories, regions, and suppliers.

- **Supplier performance monitoring** — delivery reliability, including OTIF, on-time, and in-full performance, needs to be evaluated alongside quality measures such as defect rate to identify strong and underperforming suppliers.

- **Contract compliance and maverick spend** — procurement teams need visibility into contracted and off-contract purchasing across categories, regions, buyers, and suppliers to identify areas of potential spend leakage.

- **Multidimensional supplier risk** — supplier risk cannot be assessed effectively through a single KPI. Delivery, quality, compliance, concentration, performance trends, and supplier status need to be considered together, while anomaly detection can provide an additional signal for unusual supplier behavior.

- **Forward spend planning** — historical reporting explains what has already happened, but procurement planning also requires a forward-looking view of expected spend supported by forecast evaluation and alternative planning scenarios.

- **Supplier portfolio prioritization** — managing suppliers individually does not provide a strategic portfolio view. Supplier segmentation helps group suppliers with similar characteristics so that procurement teams can apply more targeted management strategies.

---
## Project Objectives

- Build and validate an integrated procurement analytics dataset across purchasing, supplier, delivery, contract, spend, and supporting dimension data.
- Independently validate core procurement KPIs to ensure consistency between source calculations and Power BI reporting.
- Develop supplier performance analysis using delivery reliability, quality, savings, and other procurement performance indicators.
- Construct a composite supplier risk framework incorporating delivery, quality, compliance, concentration, performance trend, and supplier-status signals.
- Apply anomaly detection to identify suppliers exhibiting unusual combinations of operational and commercial characteristics.
- Forecast monthly procurement spend, evaluate forecast performance through backtesting, and generate forward-looking planning scenarios.
- Apply K-Means clustering to segment suppliers into business-oriented groups based on spend and performance characteristics.
- Integrate descriptive procurement KPIs and Python-generated analytical outputs into Power BI for interactive analysis and decision support.

---

## Solution Architecture

The project follows an end-to-end analytical workflow that combines data preparation, independent KPI validation, advanced analytics, and interactive business intelligence reporting.

```text
Raw Procurement Data
(Dimension & Fact CSV Tables)
        ↓
Python / Pandas
(Data Loading, Cleaning, Validation & Feature Engineering)
        ↓
SQL / SQLite
(Independent KPI Validation & Analytical Queries)
        ↓
Advanced Analytics
├── Composite Supplier Risk Scoring
├── Isolation Forest Anomaly Detection
├── Spend Forecasting & Scenario Planning
└── K-Means Supplier Segmentation
        ↓
Analytical CSV Outputs
├── Supplier Risk
├── Spend Forecast
└── Supplier Segmentation
        ↓
Power BI Data Model
(Core Procurement Tables + Analytical Outputs)
        ↓
DAX Measures & Business KPIs
        ↓
7 Analytical Dashboards + Validation Page
        ↓
Procurement Decision Support
```

The Python notebook loads the procurement dimension and fact tables from CSV files, performs data-quality checks and feature engineering, and uses an in-memory **SQLite** database to independently validate KPI and analytical logic with SQL.

The analytical workflow then extends the descriptive procurement analysis with **composite supplier risk scoring, Isolation Forest anomaly detection, spend forecasting and scenario planning, and K-Means supplier segmentation**. The resulting supplier-risk, spend-forecast, and supplier-segmentation datasets are exported as CSV files and integrated into the Power BI model alongside the core procurement tables.

Within **Power BI**, relationships connect the procurement data and analytical outputs, while **DAX measures** provide the reporting layer for spend, savings, supplier performance, contract compliance, and other business KPIs. The final report combines historical performance analysis with supplier-level risk, forecasting, and segmentation insights in a single interactive reporting environment.

The workflow is designed to run locally or in a notebook environment without requiring an external production database, cloud data platform, or orchestration service.

---

## Data Model

The solution uses a dimensional procurement model built around shared business dimensions, transactional fact tables, and Python-generated analytical outputs.

### Core Dimensions

- **`DimDate`** — calendar and fiscal attributes supporting time-based analysis
- **`DimSupplier`** — supplier master data, including supplier attributes, tier, status, and location
- **`DimCategory`** — procurement category and category-group structure
- **`DimRegion`** — geographic attributes supporting regional analysis
- **`DimBuyer`** — procurement buyer information
- **`DimPlant`** — plant and operational-location information

### Core Fact Tables

- **`FactProcurementSpend`** — procurement spend, baseline spend, savings, contract status, and related spend measures
- **`FactPurchaseOrders`** — purchase-order activity supporting purchasing and supplier analysis
- **`FactSupplierDeliveries`** — delivery and quality data supporting OTIF, on-time, in-full, and defect analysis
- **`FactContracts`** — supplier contract information supporting contract and compliance analysis

The fact tables connect to shared dimensions through key-based relationships, creating a **star-schema-style model** that supports consistent filtering and analysis across suppliers, categories, regions, buyers, plants, and time.

### Power BI Data Model

![Power BI Data Model](images/data-model.png)

*Star-schema-oriented Power BI model connecting procurement fact tables, shared dimensions, and Python-generated analytical outputs.*

### Analytical Output Tables

Three Python-generated analytical datasets extend the core procurement model:

- **`SupplierRisk`** — supplier-level risk components, composite risk score, risk tier, anomaly flag, and anomaly score
- **`SpendForecast`** — monthly actual and forecast spend, lower and higher planning scenarios, and forecast evaluation metrics
- **`SupplierSegments`** — supplier-level clustering results and business-oriented segment labels

These analytical tables are integrated with the relevant dimensions so that advanced analytical results can be explored alongside the core procurement data.

### DAX Measures Layer

A dedicated **DAX measures layer** contains the business KPIs used throughout the report, including spend, savings, supplier delivery performance, contract compliance, maverick spend, forecasting, and supplier-level metrics.

This architecture separates **interactive descriptive analytics** from more computationally intensive analytical workflows. Core procurement KPIs are calculated dynamically in Power BI, while supplier risk scoring, anomaly detection, forecasting, and clustering are prepared in Python and integrated into the model for reporting.

The result is a unified analytical model that supports both traditional procurement performance reporting and advanced supplier and forecasting analysis.

---

## Key KPIs

The report uses a consistent set of procurement, supplier-performance, compliance, forecasting, and segmentation KPIs across the analytical dashboards.

| KPI | Business Purpose |
|---|---|
| **Total Spend** | Total procurement expenditure within the selected reporting period |
| **Baseline Spend** | Reference spend used to evaluate actual procurement expenditure and realized savings |
| **Realized Savings** | Difference between baseline and actual spend, representing savings achieved against the reference spend |
| **Savings %** | Realized savings expressed as a percentage of baseline spend |
| **OTIF %** | Percentage of deliveries received both on time and in full; a key measure of supplier delivery reliability |
| **On-Time %** | Percentage of deliveries received on or before the promised delivery date |
| **In-Full %** | Percentage of deliveries received in the required quantity |
| **Defect Rate %** | Percentage of received units identified as defective; used to assess supplier quality performance |
| **Contract Compliance %** | Percentage of procurement spend transacted under contract |
| **Contract Spend** | Procurement spend associated with contracted purchasing |
| **Maverick Spend** | Procurement spend occurring outside contracted purchasing |
| **Maverick Spend %** | Maverick spend expressed as a percentage of total procurement spend |
| **Supplier Count** | Number of distinct suppliers represented in the analysis |
| **Forecasted Spend** | Projected procurement spend across the forward forecast horizon |
| **Forecast MAPE %** | Mean Absolute Percentage Error used to evaluate forecast performance during backtesting |
| **Forecast Accuracy %** | Forecast performance expressed as `1 − MAPE` for business-friendly interpretation |
| **Segmented Suppliers** | Number of suppliers assigned to a supplier segment |
| **Segment Spend** | Total procurement spend represented by suppliers within a segment |
| **Avg Segment Risk Score** | Average composite supplier risk score for suppliers within a segment |
---

## Dashboard Pages

The Power BI report contains a dedicated validation page followed by seven analytical dashboards covering procurement performance from executive, operational, risk, forecasting, and supplier-portfolio perspectives.

### 01. Executive Overview

Provides procurement leadership with a high-level view of overall performance through headline KPIs for Total Spend, Realized Savings, Savings %, OTIF %, Contract Compliance %, and Supplier Count.

Supporting visuals show the **Monthly Procurement Spend Trend**, **Global Spend Distribution**, and **Savings Contribution by Category**, providing a concise view of procurement scale, cost performance, supplier delivery reliability, and where savings are concentrated.

### 02. Spend & Savings

Focuses on procurement cost performance through KPIs for Baseline Spend, Realized Savings, Savings %, and Maverick Spend.

The page compares **Actual vs. Baseline Procurement Spend**, analyzes **Spend by Category Group**, highlights **Savings Contribution by Category**, and compares **Contract vs. Maverick Spend by Category**. These views help identify major spend areas, savings contributors, and categories with higher levels of off-contract purchasing.

### 03. Supplier Performance

Evaluates supplier delivery reliability and quality using OTIF %, On-Time %, In-Full %, and Defect Rate %.

Visuals compare **Delivery Performance by Supplier Tier**, identify suppliers with the **Highest Supplier Defect Rates**, rank the **Top 10 Suppliers by OTIF**, and position suppliers within a **Supplier Performance Matrix** based on delivery reliability and quality performance.

Together, these views provide a more balanced assessment of supplier performance than relying on a single service or quality metric.

### 04. Contract Compliance

Examines procurement governance through Contract Compliance %, Contract Spend, Maverick Spend, and Maverick Spend %.

The dashboard tracks **Contract Compliance over time**, compares compliance across procurement categories, examines contract and maverick spend across regions, and identifies **Buyers with High Maverick Spend**.

These views help identify where off-contract purchasing is concentrated and where stronger contract adoption may be required.

### 05. Supplier Risk

Extends supplier monitoring beyond individual performance KPIs by combining a composite supplier risk framework with anomaly detection.

The dashboard presents **Supplier Risk Tier Distribution**, **Highest-Risk Suppliers**, a **Supplier Risk Landscape**, and a **Supplier Risk & Anomaly Watchlist** containing supplier-level risk and anomaly indicators.

Risk scoring and anomaly detection are treated as separate analytical concepts. The composite risk score combines predefined business-risk dimensions, while the Isolation Forest model identifies suppliers exhibiting unusual combinations of observed characteristics. This provides an additional signal for supplier investigation rather than treating every unusual supplier as inherently high risk.

### 06. Spend Forecasting

Adds a forward-looking perspective through KPIs for **6-Month Forecast Spend, Forecast Accuracy %, and Forecast MAPE %**.

The dashboard compares **Actual vs. Forecast Procurement Spend**, presents a **6-Month Forecast Scenario Range** with lower, base, and higher scenarios, and provides a monthly forward spend planning table.

Using multiple planning scenarios alongside the base forecast gives procurement teams additional context for budgeting, anticipated expenditure, and sourcing planning rather than relying solely on a single-point forecast.

### 07. Supplier Segmentation

Provides a portfolio-level view of the supplier base using clustering results generated in Python.

KPIs summarize **Portfolio Spend, Average Risk Score, and Suppliers Segmented**, while the dashboard presents **Supplier Segment Distribution**, a **Segment Performance Summary**, and a **Supplier Segmentation Matrix**.

The final analysis contains three populated business segments:

- **High-Spend At-Risk** — suppliers with greater spend exposure combined with elevated performance or risk concerns
- **Reliable Long-Tail** — lower-spend suppliers demonstrating comparatively reliable operating characteristics
- **Development Required** — suppliers whose performance characteristics indicate greater opportunity for improvement

The segmentation supports differentiated supplier-management strategies by allowing procurement teams to prioritize attention according to supplier characteristics rather than applying the same management approach across the entire supplier base.

### Selected Dashboard Views

#### Spend & Savings

![Spend & Savings Dashboard](images/spend-savings.png)

*Analysis of procurement spend, baseline spend, realized savings, category contribution, and contract versus maverick spend.*

#### Supplier Performance

![Supplier Performance Dashboard](images/supplier-performance.png)

*Supplier delivery and quality analysis combining OTIF, on-time, in-full, defect-rate, ranking, and performance-matrix views.*

---

## Advanced Analytics

The Python workflow extends the descriptive Power BI analysis with four advanced analytical components: **supplier risk scoring, anomaly detection, spend forecasting, and supplier segmentation**. These outputs are generated at the supplier or monthly level and integrated into Power BI for interactive analysis.

### Supplier Risk Scoring

A composite **Supplier Risk Score** on a 0–100 scale combines six normalized operational and commercial risk components:

| Risk Component | Weight | Calculation / Interpretation |
|---|---:|---|
| **Delivery Risk** | 28% | Increases as supplier OTIF performance declines |
| **Quality Risk** | 22% | Increases as supplier defect rate rises |
| **Compliance Risk** | 16% | Based on the supplier's maverick-spend percentage |
| **Concentration Risk** | 12% | Based on the supplier's maximum share of spend within a procurement category |
| **Trend Risk** | 12% | Captures deterioration in recent OTIF performance relative to prior performance |
| **Supplier Status Risk** | 10% | Incorporates supplier status such as Active, Under Review, or Suspended |

The delivery component is derived from `1 − OTIFRate`, while the trend component compares supplier OTIF performance during the most recent 90 days with the preceding historical period. Individual components are normalized before being combined using the predefined weights.

The resulting score is classified into four potential risk tiers:

- **Low:** 0–25
- **Moderate:** >25–45
- **Elevated:** >45–65
- **High:** >65

This framework provides a consistent method for prioritizing supplier risk using multiple business indicators rather than relying on a single performance metric.

#### Supplier Risk Dashboard

![Supplier Risk Dashboard](images/supplier-risk.png)

*Supplier risk dashboard combining composite risk scoring, risk-tier classification, supplier positioning, and anomaly indicators.*

### Anomaly Detection

Supplier anomaly detection is implemented separately from the composite risk framework using an **Isolation Forest** model from scikit-learn.

The model evaluates five supplier-level features:

- OTIF Rate
- Defect Rate
- Maverick Spend %
- Maximum Category Share
- OTIF Trend Delta

The features are min-max scaled before model fitting. The Isolation Forest is configured with **200 estimators** and a **10% contamination parameter**, producing an `AnomalyFlag` that classifies each supplier as **Normal** or **Anomalous**.

An additional `AnomalyScore` provides a continuous measure of relative anomaly severity, with higher values representing more unusual combinations of supplier characteristics.

The anomaly model complements rather than replaces the composite risk score. The **risk score measures predefined business-risk dimensions**, while **Isolation Forest identifies unusual multivariate patterns relative to the supplier population**. An anomaly is therefore treated as a signal for further investigation, not as evidence of fraud or supplier failure.

### Spend Forecasting

Monthly procurement spend is forecast using a **linear trend model** combined with **multiplicative monthly seasonal indices** derived from historical spend patterns.

The forecasting workflow separates the underlying trend from recurring monthly seasonality and evaluates predictive performance through a **six-month holdout backtest**. Forecast values for the holdout period are compared with actual spend using **Mean Absolute Percentage Error (MAPE)**.

The final model achieved:

- **MAPE:** 7.49%
- **Forecast Accuracy (`1 − MAPE`):** 92.51%

After validation, the methodology is applied to the full historical series to generate a **six-month forward procurement-spend forecast**.

To support planning under uncertainty, two additional scenarios are generated around the base forecast:

- **Lower Scenario:** 95% of the base forecast
- **Base Scenario:** model forecast
- **Higher Scenario:** 108% of the base forecast

These scenarios provide a practical planning range for budgeting and sourcing decisions rather than presenting the forecast as a single guaranteed outcome.

#### Forecast Model Output

![Spend Forecast Model](images/forecast-model.png)

*Six-month procurement spend forecast generated in Python, showing historical actual spend, the forward forecast, and the planning scenario range. The model achieved 92.5% backtested forecast accuracy.*

#### Power BI Forecast Dashboard

![Spend Forecasting Dashboard](images/spend-forecasting.png)

*Six-month procurement forecast presented with forecast accuracy, MAPE, and lower, base, and higher planning scenarios.*

### Supplier Segmentation

Supplier segmentation is performed using **K-Means clustering** from scikit-learn on standardized supplier-level features:

- Total Spend
- OTIF Rate
- Defect Rate
- Maverick Spend %
- Savings Rate

The model uses **four statistical clusters (`n_clusters=4`)**. Cluster-level characteristics are then interpreted and translated into business-oriented segment labels so that the statistical output can be used more easily in procurement decision-making.

In the final analytical output, the business-labeling logic results in three populated supplier segments:

| Segment | Suppliers | Approx. Spend | Avg. OTIF | Interpretation |
|---|---:|---:|---:|---|
| **High-Spend At-Risk** | 33 | ~$1.31B | 78% | Higher-spend suppliers with elevated performance or risk concerns |
| **Reliable Long-Tail** | 18 | ~$662M | 86% | Lower-spend suppliers with comparatively stronger delivery reliability |
| **Development Required** | 9 | ~$346M | 78% | Suppliers presenting greater opportunities for performance improvement |

The segmentation creates a portfolio-level view of the supplier base and supports differentiated management strategies based on supplier characteristics rather than applying a uniform approach to every supplier.

#### Supplier Segmentation Dashboard

![Supplier Segmentation Dashboard](images/supplier-segmentation.png)

*Supplier portfolio segmentation showing business-oriented supplier groups, segment performance, spend exposure, and supplier positioning.*

---

## Key Insights

- **Supplier delivery performance shows meaningful variation.** Overall OTIF performance is **80.7%**, while the strongest individual suppliers reach the upper-90% range, indicating a noticeable gap between top-performing suppliers and the broader supplier base.

- **Contract leakage represents a significant share of procurement spend.** Overall Contract Compliance is **50.4%**, while Maverick Spend accounts for **49.6%** of total spend — approximately **$1.15B** — highlighting substantial off-contract purchasing exposure.

- **Procurement generated approximately $75M in realized savings** against roughly **$2.39B in baseline spend**, resulting in an overall savings rate of approximately **3.1%** across the analyzed period.

- **Composite supplier risk is concentrated in the lower risk tiers.** Of the 60 suppliers analyzed, **52 were classified as Low risk and 8 as Moderate risk**, with no suppliers classified as Elevated or High risk in the final run. This indicates that the model is primarily differentiating suppliers within the lower end of the predefined risk scale rather than identifying extreme-risk cases.

- **Risk scoring and anomaly detection provide complementary signals.** Isolation Forest identifies suppliers with unusual combinations of operational and compliance characteristics, including suppliers that do not necessarily have the highest composite risk scores. This demonstrates the value of reviewing anomaly indicators alongside the predefined business-risk framework.

- **The spend forecast achieved a six-month backtest MAPE of 7.49%, corresponding to a reported forecast accuracy of 92.51%.** The result provides a quantified benchmark for interpreting the six-month forward forecast and its lower/base/higher planning scenarios.

- **The largest supplier segment is also the largest area of spend exposure.** The **High-Spend At-Risk** segment contains 33 suppliers representing approximately **$1.31B in spend**, with average OTIF of about **78%**, making this group particularly relevant for supplier-performance and risk-management attention.

- **Reliable Long-Tail suppliers demonstrate stronger delivery performance despite representing less spend.** The segment contains 18 suppliers representing approximately **$662M in spend** and achieves average OTIF of about **86%**, the strongest delivery performance among the three populated supplier segments.
---

## Business Recommendations

Based on the procurement performance, compliance, risk, forecasting, and segmentation analysis, the following actions should be considered:

- **Strengthen contract adoption in high-maverick-spend areas.** With approximately half of procurement spend occurring outside contracted purchasing, prioritize categories, regions, and buyers with the greatest maverick-spend exposure for contract-coverage and purchasing-compliance reviews.

- **Prioritize High-Spend At-Risk suppliers for performance improvement.** Suppliers in this segment combine significant spend exposure with weaker delivery characteristics, making them strong candidates for supplier development plans, performance reviews, and corrective-action tracking.

- **Use anomaly flags as an additional supplier-review signal.** Suppliers identified as anomalous by the Isolation Forest model should be investigated alongside their composite risk scores and underlying performance metrics. Particular attention can be given to suppliers where anomaly indicators coincide with higher business-risk scores.

- **Investigate buyers with high maverick spend.** Buyer-level off-contract purchasing can be used to identify potential gaps in contract awareness, purchasing-policy adherence, supplier availability, or existing contract coverage.

- **Incorporate forecast scenarios into procurement planning.** Use the six-month base forecast together with the lower and higher scenarios to support budget planning, anticipated cash requirements, and the timing of major sourcing or contract-renewal activities.

- **Identify candidates for preferred-supplier strategies.** Suppliers demonstrating consistently strong OTIF, low defect rates, and strong contract compliance can be evaluated for preferred-supplier status, longer-term agreements, or increased strategic allocation where commercially appropriate.

- **Apply differentiated supplier-management strategies.** Use supplier segments to tailor the level of procurement attention: apply closer monitoring and development initiatives to **High-Spend At-Risk** suppliers, targeted improvement actions to **Development Required** suppliers, and a more efficient monitoring approach for the **Reliable Long-Tail** segment.

---

## Technical Implementation

### Python & SQL

- Loaded and validated a multi-table procurement warehouse consisting of **six dimension tables and four fact tables**, with explicit checks for required source files and data availability.
- Loaded the source tables into an **in-memory SQLite database** to independently validate procurement KPIs and analytical logic using SQL.
- Applied SQL analytical techniques, including window functions such as **`RANK()`** and **`NTILE()`**, for supplier-level analysis and validation.
- Engineered supplier-level features covering **delivery performance, quality, contract compliance, spend concentration, performance trends, supplier status, total spend, and savings**.
- Performed exploratory procurement analysis across time, regions, categories, suppliers, spend, savings, delivery performance, and quality.
- Developed a weighted **composite supplier risk score** and corresponding risk-tier classification.
- Applied **Isolation Forest** for multivariate supplier anomaly detection.
- Applied **K-Means clustering** to segment suppliers using spend and performance characteristics.
- Developed a monthly procurement-spend forecasting workflow using **linear trend estimation and multiplicative seasonal factors**, evaluated through a six-month holdout backtest using MAPE.
- Generated lower, base, and higher forecast scenarios to support forward procurement planning.
- Exported Power BI-ready analytical datasets for **supplier risk, spend forecasting, and supplier segmentation**.

### Power BI

- Built a **star-schema-oriented semantic model** combining procurement fact tables, shared dimensions, and Python-generated analytical outputs.
- Modeled business dimensions including **Date, Region, Plant, Supplier, Category, and Buyer** to support consistent filtering across the report.
- Developed a dedicated **DAX measures layer** for spend, savings, supplier delivery performance, contract compliance, maverick spend, forecasting, risk, and segmentation metrics.
- Implemented interactive slicers and dimension-based filtering across analytical pages, including year, region, category, supplier tier, supplier, and buyer selections where relevant.
- Designed **seven analytical dashboards plus a dedicated validation page** using KPI cards, line and combo charts, bar/column charts, scatter plots, treemaps, donut charts, and tabular/matrix visuals.
- Built a dedicated **Validation** page to reconcile key DAX measures with independently validated calculations from the Python/SQL workflow.
- Integrated Python-generated **Supplier Risk, Spend Forecast, and Supplier Segmentation** outputs into the Power BI reporting model for interactive analysis.
---

## Repository Structure

```text
Global-Procurement-Supplier-Performance-Analytics/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebook/
│   └── Global_Procurement_Analytics.ipynb
│
├── powerbi/
│   └── Global_Procurement_Supplier_Performance_Analytics.pbix
│
├── data/
│   ├── raw/
│   │   ├── dim_buyer.csv
│   │   ├── dim_category.csv
│   │   ├── dim_date.csv
│   │   ├── dim_plant.csv
│   │   ├── dim_region.csv
│   │   ├── dim_supplier.csv
│   │   ├── fact_contracts.csv
│   │   ├── fact_procurement_spend.csv
│   │   ├── fact_purchase_orders.csv
│   │   └── fact_supplier_deliveries.csv
│   │
│   └── processed/
│       ├── spend_forecast_powerbi.csv
│       ├── supplier_risk_powerbi.csv
│       └── supplier_segments_powerbi.csv
│
└── images/
    ├── data-model.png
    ├── executive-overview.png
    ├── forecast-model.png
    ├── spend-forecasting.png
    ├── spend-savings.png
    ├── supplier-performance.png
    ├── supplier-risk.png
    └── supplier-segmentation.png
```

- **`notebook/`** contains the Python analytics workflow, including data validation, KPI verification, supplier risk analysis, anomaly detection, forecasting, and segmentation.
- **`powerbi/`** contains the final Power BI report.
- **`data/raw/`** contains the synthetic source dimension and fact tables used by the analytical workflow.
- **`data/processed/`** contains the Python-generated analytical outputs prepared for Power BI.
- **`images/`** contains Power BI dashboard screenshots, the data-model diagram, and analytical visualizations used throughout this README.
- **`requirements.txt`** lists the Python dependencies required to run the notebook.
- **`.gitignore`** excludes local development files, virtual environments, notebook checkpoints, and temporary files from version control.
---

## How to Use This Project

### 1. Install Python Dependencies

Clone or download the repository and install the required Python libraries:

```bash
pip install -r requirements.txt
```

The analytical workflow primarily uses **Pandas** and **NumPy** for data preparation, **SQLite/SQL** for KPI validation, **scikit-learn** for machine learning and forecasting, and **Matplotlib/Seaborn** for exploratory visualization.

### 2. Prepare the Source Data

Place the ten synthetic procurement warehouse CSV files in the `data/raw/` directory:

```text
data/raw/
├── dim_buyer.csv
├── dim_category.csv
├── dim_date.csv
├── dim_plant.csv
├── dim_region.csv
├── dim_supplier.csv
├── fact_contracts.csv
├── fact_procurement_spend.csv
├── fact_purchase_orders.csv
└── fact_supplier_deliveries.csv
```

The Python workflow generates the following analytical outputs in `data/processed/`:

```text
data/processed/
├── spend_forecast_powerbi.csv
├── supplier_risk_powerbi.csv
└── supplier_segments_powerbi.csv
```

### 3. Run the Analytics Notebook

Open:

```text
notebook/Global_Procurement_Analytics.ipynb
```

Run the notebook cells in sequence. The workflow performs:

- source-data loading and validation
- SQL-based KPI validation using SQLite
- supplier feature engineering and composite risk scoring
- Isolation Forest anomaly detection
- spend forecasting and backtesting
- K-Means supplier segmentation
- export of analytical datasets for Power BI

The notebook can be executed in a local Jupyter environment or adapted for use in **Google Colab**.

### 4. Open the Power BI Report

Open the following file in **Power BI Desktop**:

```text
powerbi/Global_Procurement_Supplier_Performance_Analytics.pbix
```

### 5. Configure Data Sources and Refresh

If the local file locations differ from those used when the report was developed, update the CSV source paths through **Power Query** before refreshing the model.

After the paths are configured, refresh the Power BI model to load the core procurement tables and the latest Python-generated analytical outputs.

---

## Technologies Used

| Technology | Purpose |
|---|---|
| **Python** | Core analytical workflow, data preparation, feature engineering, and advanced analytics |
| **Pandas / NumPy** | Data loading, cleaning, joining, aggregation, transformation, and numerical feature engineering |
| **SQLite (`sqlite3`)** | In-memory SQL database used for independent KPI validation and analytical queries |
| **SQL** | KPI verification, supplier analysis, aggregation, and window-function calculations including `RANK()` and `NTILE()` |
| **scikit-learn** | Isolation Forest anomaly detection, K-Means supplier segmentation, Linear Regression forecasting, and feature scaling |
| **Matplotlib / Seaborn** | Exploratory data analysis and analytical visualization within the notebook |
| **Jupyter Notebook** | Interactive environment for developing, documenting, validating, and executing the analytical workflow |
| **Power BI Desktop** | Semantic modeling, interactive dashboard development, and business intelligence reporting |
| **Power Query** | Data ingestion, transformation, data-type management, and preparation within Power BI |
| **DAX** | Business KPI and analytical measure calculation within the Power BI semantic model |
---

## Skills Demonstrated

- **Procurement Analytics & KPI Design** — spend, savings, supplier performance, contract compliance, maverick spend, and supplier risk metrics
- **Data Preparation & Validation** — data cleaning, transformation, multi-table joins, data-quality checks, and reconciliation
- **SQL Analytics** — KPI validation, aggregations, and analytical window functions including `RANK()` and `NTILE()`
- **Data Modeling** — dimensional modeling and star-schema-oriented design for business intelligence reporting
- **Feature Engineering** — development of supplier-level risk, performance, compliance, concentration, trend, and segmentation features
- **DAX & Power Query** — business-measure development, data transformation, and analytical modeling within Power BI
- **Machine Learning** — unsupervised anomaly detection with Isolation Forest and supplier clustering with K-Means
- **Forecasting & Model Evaluation** — trend and seasonality modeling, holdout backtesting, MAPE evaluation, and scenario-based forecasting
- **Supplier Risk Analytics** — composite risk scoring, risk-tier classification, anomaly analysis, and supplier prioritization
- **Dashboard Design & Data Storytelling** — development of interactive Power BI dashboards for executive and operational analysis
- **Business Translation** — converting analytical and machine-learning outputs into interpretable supplier segments, insights, and procurement recommendations

---

## Limitations & Future Enhancements

This project is a portfolio-scale analytics solution built on a **synthetic procurement dataset** and executed through a notebook-driven workflow. It demonstrates an end-to-end analytical approach but is not intended to represent a production deployment.

Potential areas for further development include:

- **Automated data pipelines** — replace the manual notebook-driven ingestion and export process with scheduled ETL/ELT workflows for repeatable data processing.

- **ERP and procurement-system integration** — connect the analytical model directly to operational sources such as SAP or other procurement platforms rather than relying on static CSV extracts.

- **Incremental and scheduled refresh** — introduce incremental data loading and automated Power BI refresh to support larger datasets and more frequent reporting cycles.

- **Forecast monitoring and retraining** — track forecast error over time, compare alternative forecasting approaches, and retrain the model as new procurement data becomes available.

- **Supplier risk monitoring and alerting** — extend risk tiers and anomaly indicators into an automated workflow that flags suppliers requiring review when defined thresholds or conditions are met.

- **Interactive scenario analysis** — introduce Power BI what-if parameters to allow users to test alternative spend, savings, compliance, or forecasting assumptions directly within the report.

- **Row-level security (RLS)** — implement role-based access for buyers, regions, business units, or procurement leadership in a multi-user deployment.

- **Power BI Service deployment** — publish the report to a managed workspace with scheduled refresh, controlled access, and dashboard distribution for business stakeholders.

---

## Conclusion

This project demonstrates an end-to-end approach to **procurement and supplier performance analytics**, combining data validation, business intelligence, and advanced analytics within a single workflow.

The solution moves from validating core spend, savings, delivery, and contract-compliance KPIs through Python and SQL to applying **supplier risk scoring, anomaly detection, spend forecasting, and supplier segmentation**. These analytical outputs are then integrated into Power BI alongside the core procurement data to provide an interactive reporting environment for both historical performance monitoring and forward-looking analysis.

By connecting procurement KPIs with supplier risk, forecasting, and portfolio segmentation, the project demonstrates how analytical techniques can be translated into practical insights for **spend management, supplier performance improvement, contract compliance, risk prioritization, and procurement planning**.