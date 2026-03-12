# Air Quality Prediction MVP
This is our baseline model for predicting air quality.

## Data Setup
1. Download the historical air quality dataset from Kaggle.
2. Extract the file and place the .csv inside a folder named data/ in the root directory.

## Data Ingestion & Preprocessing

For this project, we utilize the historical air quality dataset from Seoul (Kaggle). To optimize processing time and focus our MVP, we extracted a strict 1-year sample for the year **2021**.

**Data Validation & Sanity Check:**
* The dataset was filtered strictly by the first 4 digits of the `dt` column (format: `YYYYMMDDHH`) using the `.startswith()` method to prevent false positives.
* **Resulting shape:** 213,414 rows.
* **Validation:** The year 2021 has approximately 8,760 hours. With exactly 25 measuring stations in Seoul (Station IDs 101 to 125), the theoretical maximum is 219,000 measurements (8,760 hours * 25 stations). 
* Our extracted 213,414 rows represent a highly realistic dataset. The missing ~5,500 rows (approx. 2.5%) are expected due to normal real-world sensor downtime and maintenance.
* The reduced sample is saved locally as `seoul_2021_sample.csv` and excluded from version control via `.gitignore` to maintain repository performance.