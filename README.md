# Logistics Data Analysis Project


## 1. What is this project about?

Logistics means moving products from a warehouse to a customer. Three problems happen again and again:

- **Late delivery**: the order reaches the customer after the promised date.
- **Stockout or overstock**: a product runs out, or too much of it is stored.
- **High transport cost**: delivering each order costs too much money.

In this project I will use data and Python to measure these problems with simple numbers (KPIs) and then test a few data science methods to see how they can be improved.

**Why does it matter?** Estimates attributed to the Capgemini Research Institute say the last mile (the final step to the customer) can be around 41% to 53% of total delivery cost. McKinsey reports that early adopters of AI in supply chains improved logistics costs by 15%, inventory levels by 35% and service levels by 65%.

## 2. Objectives

1. Measure current delivery and inventory performance using standard KPIs.
2. Find where and why delivery delays happen.
3. Try demand forecasting, clustering, delay prediction and route optimization.
4. Suggest actions to improve on-time delivery and reduce cost per order.

## 3. KPIs (how performance is measured)

| KPI | Meaning | Formula |
| --- | --- | --- |
| On-Time Delivery (OTD) | Share of orders delivered on time | (Orders on time ÷ Total orders) × 100 |
| Order Cycle Time | Average days from order to delivery | Average of (Delivery date − Order date) |
| Inventory Turnover | How often stock is sold and replaced | Cost of goods sold ÷ Average inventory value |
| Stockout Rate | How often products are unavailable | (SKU-days out of stock ÷ Total SKU-days) × 100 |
| Perfect Order Rate | Orders that are on time, complete, undamaged and correctly documented | OTD% × In-full% × Damage-free% × Documentation-accurate% |
| Transport Cost per Order | Average transport spend per order | Total transport cost ÷ Orders shipped |
| Forecast Error (MAPE) | Average % gap between forecast and real demand | (1/n) Σ \|Actual − Forecast\| ÷ \|Actual\| × 100 |

These KPIs follow common logistics practice and the SCOR model (a standard supply chain framework from ASCM).

## 4. Datasets

All three datasets are public. They are **not uploaded here** because they are large. Download them from the links.

| Dataset | Approx. size | Used for | Link |
| --- | --- | --- | --- |
| DataCo Smart Supply Chain | about 180,500 rows, 53 columns | On-time delivery, cycle time, delay prediction | https://data.mendeley.com/datasets/8gx2fvg2k6 |
| M5 Forecasting (Walmart) | about 30,490 item series, 1,941 days | Demand forecasting | https://www.kaggle.com/c/m5-forecasting-accuracy |
| Olist Brazilian E-commerce | about 99,400 orders, 9 tables | Delivery delay, freight cost, regional zones | https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce |

Important columns to use: order date, shipping mode, scheduled and actual delivery days, delivery status, region, sales/quantity, freight value.

## 5. Methods (data science techniques)

| Technique | Problem it helps with | How |
| --- | --- | --- |
| Demand forecasting | Stockout, overstock | Seasonal-naive baseline, exponential smoothing, ARIMA |
| Route optimization | High transport cost, late delivery | Vehicle Routing Problem using Google OR-Tools |
| Clustering | Uneven service across regions | k-means to create delivery zones |
| Delay prediction | Late delivery | Logistic regression, random forest |

## 6. Tools used

| Library | Used for |
| --- | --- |
| pandas | Cleaning and handling data |
| matplotlib, seaborn | Charts |
| scikit-learn | Machine learning and clustering |
| statsmodels | Time series forecasting |
| OR-Tools | Route optimization |

## 7. How to set up and run

1. Install Python 3.9 or newer.
2. Download this repository (green **Code** button, then **Download ZIP**) or clone it:
   ```
   git clone https://github.com/<ranishruti432-oss>/logistics-data-analysis.git
   ```
3. Install the libraries:
   ```
   pip install -r requirements.txt
   ```
4. Download the datasets from Section 4 and keep them in a `data/` folder on your computer.
5. Example: calculate On-Time Delivery from the DataCo file:
   ```python
   import pandas as pd

   df = pd.read_csv("data/DataCoSupplyChainDataset.csv", encoding="latin-1")
   df = df[df["Delivery Status"] != "Shipping canceled"]
   on_time = df["Delivery Status"].isin(["Shipping on time", "Advance shipping"])
   print(f"OTD: {on_time.mean() * 100:.1f}%")
   ```
   (The DataCo file needs `encoding="latin-1"`, otherwise it gives an error.)

## 8. Project workflow

1. Define the problem
2. Collect data
3. Clean and prepare data
4. Explore the data (EDA)
5. Calculate baseline KPIs
6. Build models
7. Evaluate the results
8. Write recommendations and the final report

## 9. Repository structure

```
logistics-data-analysis/
├── README.md
├── requirements.txt
└── Logistics_Project_Research_Report.docx
```

Folders `notebooks/` (Python code) and `data/` (small sample files) will be added in the coming weeks.
## 10. Project plan

| Week | What will be done | Status |
| --- | --- | --- |
| 1 | Research, KPIs, dataset and tool selection, research report | Done |
| 2 | Data cleaning, EDA, baseline KPIs | Planned |
| 3 | Forecasting, clustering, delay prediction, routing | Planned |
| 4 | Evaluation, charts, final report | Planned |

## 11. Important note

The KPI baselines, sample order table and charts in the Week 1 report are marked **"illustrative"**. They are planning assumptions, not real results. They will be replaced with real values after the data analysis in Week 2 and 3.

## 12. References

- Dantzig, G. B. and Ramser, J. H. (1959). The Truck Dispatching Problem. *Management Science*, 6(1), 80-91.
- Hyndman, R. J. and Athanasopoulos, G. (2021). *Forecasting: Principles and Practice* (3rd ed.). https://otexts.com/fpp3
- Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research*, 12, 2825-2830.
- Google Developers. Vehicle Routing (OR-Tools). https://developers.google.com/optimization/routing
- McKinsey & Company (2021). Succeeding in the AI supply-chain revolution.
- Capgemini Research Institute (2019). The Last-Mile Delivery Challenge.

The full source list is in the report inside the `report/` folder.
