# Air Quality Prediction MVP
This is our baseline model for predicting air quality.

## Data Setup
1. Download the historical air quality dataset from Kaggle.
2. Extract the file and place the .csv inside a folder named data/ in the root directory.

## Data Ingestion & Preprocessing
For this project, we utilize the historical air quality dataset from Seoul (Kaggle). To optimize processing time and focus our MVP, we extracted a strict 1-year sample for the year **2021**.

### Data Validation & Setup
* **Filtering:** We grabbed only the data for 2021. To be safe, we checked that the `dt` column (format `YYYYMMDDHH`) actually starts with "2021" using `.startswith()`. This way, we avoid picking up wrong dates that just happen to have "2021" somewhere in the middle.
* **Sanity Check:** 2021 has 8,760 hours and we have 25 stations in Seoul (IDs 101 to 125). That means we could have a maximum of 219,000 measurements (8,760 * 25). 
* **Realistic Data:** We ended up with 213,414 rows, which is really close! The missing ~5,500 rows (around 2.5%) make perfect sense because real-world sensors sometimes go offline or need maintenance.
* **Local Save:** We saved this smaller 1-year dataset locally as `seoul_2021_sample.csv`. We also made sure to put it in our `.gitignore` so we don't accidentally push large data files to GitHub.

### Quick Data Check (2021 Subset)
* **Size:** Our filtered dataset for 2021 has 213,414 rows and 10 columns.
* **Data Types:** Everything looks good here. Pandas correctly loaded all the sensor data (`so2`, `pm10`, etc.) as numbers (`float64`). The date and location columns are integers (`int64`). 
* **Missing Data:** We used `df.info()` and noticed that there are some missing values (NaNs). For example, the `pm10` column only has 210,804 valid entries instead of the full 213,414. Handling these missing values will be our first task in the upcoming Data Cleaning phase.

## 📊 Baseline Model Results
Our initial prediction pipeline utilizes a **Random Forest Regressor** trained on historical 2021 air quality data from Seoul.

### Data Preparation
* **Target:** PM2.5 concentration
* **Features:** SO2, NO2, CO, O3, PM10
* **Preprocessing:** Missing values dropped, datetime formatting fixed, and features scaled using `StandardScaler`.
* **Split:** 80% Training (167k rows) / 20% Testing (41k rows)

### Initial Performance Metrics
| Metric | Score | Description |
| :--- | :--- | :--- |
| **$R^2$ Score** | `0.8671` | The model explains 86.7% of the variance in PM2.5 levels. |
| **MSE** | `40.48` | Mean Squared Error (Standard benchmark). |
| **MAPE** | `34.09%` | Mean Absolute Percentage Error. |

*Further hyperparameter tuning and cross-validation are ongoing to optimize these baseline metrics.*