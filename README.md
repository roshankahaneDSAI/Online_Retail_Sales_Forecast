## 🚀 Overview

This project builds an **end-to-end sales forecasting pipeline** for an online retail dataset, focused on:

- **Daily product-level demand forecasting**
- **Warehouse & inventory optimization**
- Data-driven support for **stocking, replenishment, and capacity planning**

The core model uses **CatBoostRegressor**, tuned with **Bayesian Optimization (GPyOpt)**, on top of extensive **time-series feature engineering**.

---

## 🧱 Architecture

The diagram below summarizes the end-to-end flow from raw data to forecasts:

```mermaid
flowchart LR
    A[Raw Online Retail Data<br/>(CSV / DB)] --> B[Data Cleaning & Validation]
    B --> C[Daily Aggregation<br/>(Product × Date)]
    C --> D[Feature Engineering<br/>• Time features<br/>• Lag features<br/>• Rolling stats]
    D --> E[Train / Validation Split]
    E --> F[CatBoost Model]
    F --> G[Bayesian HPO<br/>(GPyOpt)]
    G --> H[Trained Forecasting Model]
    H --> I[Daily Demand Forecasts]
    I --> J[Warehouse & Inventory Insights]
````

---

## 📂 Project Structure

> Update paths if your structure is slightly different.

```bash
# Main notebook: EDA → features → model → tuning → results
├── research/data/
              └── OnlineRetail.csv 
├── research/data/
        └── e-commerce-sales-forecast.ipynb            # Source dataset (not included in repo) 
├── assets/
│   └── ecommerce-forecast-cover.svg # GitHub cover illustration
├── README.md
└── requirements.txt                 # (optional) Python dependencies
```

---

## ✨ Key Features

* 🔍 **Exploratory Data Analysis**

  * Data quality checks, missing values, cancellations
  * Product popularity, customer behaviour
  * Temporal trends and basic seasonality

* 🧮 **Daily Demand Construction**

  * Aggregate raw transactions into **daily product-level** time series
  * Compute **quantity** and **revenue** per product per day

* 🧠 **Feature Engineering**

  * Calendar features: `day`, `month`, `year`, `weekday`, etc.
  * Lag features: e.g. `qty_lag_1`, `qty_lag_7`, `qty_lag_14`
  * Rolling windows: 7/14/28-day moving averages & sums
  * Product / customer-level aggregations

* 🤖 **Modeling with CatBoost**

  * Custom `Catmodel` class for:

    * Training
    * Validation
    * Metric logging & debugging
  * Handles mixed-type tabular data efficiently

* 🎯 **Hyperparameter Tuning (GPyOpt)**

  * Bayesian Optimization over:

    * Depth
    * Learning rate
    * L2 regularization
    * Number of trees
  * Objective: minimize validation **RMSE**

* 📈 **Forecasting & Evaluation**

  * Predict future daily quantities
  * Compare predicted vs. actual sales
  * Visual diagnostics for under/over-prediction
  * Interpretability for warehouse & inventory use cases

---

## 📊 Tech Stack

| Category        | Tools / Libraries              |
| --------------- | ------------------------------ |
| Language        | Python                         |
| Data Handling   | pandas, NumPy                  |
| Visualization   | matplotlib, seaborn            |
| Modeling        | CatBoostRegressor              |
| HPO             | GPyOpt (Bayesian Optimization) |
| Utils / Metrics | scikit-learn, tqdm             |
| Interface       | Jupyter Notebook               |

---

## 🧪 Getting Started

### 1️⃣ Clone the repo

```bash
git clone https://github.com/roshankahaneDSAI/Online_Retail_Sales_Forecast.git
cd Online_Retail_Sales_Forecast
```

### 2️⃣ Install dependencies

Using `requirements.txt` (recommended):

```bash
pip install -r requirements.txt
```

Or manually:

```bash
pip install pandas numpy matplotlib seaborn catboost GPyOpt scikit-learn tqdm
```

### 3️⃣ Add data

Place your dataset (e.g. `OnlineRetail.csv`) under `data/`:

```bash
research/data/
          └── OnlineRetail.csv
```

### 4️⃣ Run the notebook

```bash
jupyter notebook e-commerce-sales-forecast.ipynb
```

Execute cells sequentially:

1. **EDA & Cleaning**
2. **Feature Engineering**
3. **Model Training (CatBoost)**
4. **Hyperparameter Tuning (GPyOpt)**
5. **Forecasting & Visualization**

---

## 📌 Dataset

The notebook expects an **online retail transactional dataset** with fields similar to:

* `InvoiceNo`
* `StockCode`
* `Description`
* `Quantity`
* `InvoiceDate`
* `UnitPrice`
* `CustomerID`
* `Country`

> For licensing reasons, the raw dataset is not bundled.
> You can plug in your own dataset as long as it matches the expected schema.

---

## 📉 Model & Metrics

The notebook reports:

* Train / validation **RMSE**
* Learning curves & validation performance across tuning iterations
* Time-series plots of:

  * Actual vs. predicted daily quantities
  * Residual patterns over time

These diagnostics help evaluate whether the model is suitable for **operational warehouse decisions** (e.g., safety stock, reorder points).

---

## 🗺️ Roadmap / Ideas

* [ ] Add baseline models (e.g. naive, moving average, SARIMA, Prophet)
* [ ] Package pipeline into reusable Python modules
* [ ] Expose a prediction API via Flask / FastAPI
* [ ] Integrate MLflow for experiment tracking
* [ ] Automate daily training & scoring with a scheduler (e.g. Airflow)
* [ ] Plug forecasts into a warehouse simulation or optimization module

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/awesome-thing`
3. Commit your changes: `git commit -m "Add awesome thing"`
4. Push the branch: `git push origin feature/awesome-thing`
5. Open a Pull Request

---

## 📜 License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.

---

## 🙌 Acknowledgements

* Online retail transactional datasets used for research & experimentation
* Open-source maintainers of CatBoost, GPyOpt, and the Python scientific stack

````

---

