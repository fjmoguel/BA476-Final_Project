# Predicting Flight Delays: A Consumer-Centric Model

## Overview

Flight delays are a pervasive issue affecting millions of passengers annually, resulting in significant financial costs and travel disruptions. This project aims to develop a predictive model that forecasts flight delays, leveraging machine learning techniques to assist airlines, airports, and passengers in managing schedules and reducing operational inefficiencies.

The work was completed as part of the **BA476: Predictive Analytics** course at Boston University, by Team 6.

---

## Dataset Information

The dataset for this project was sourced from Kaggle and provides comprehensive data on U.S. domestic flights from 2019 to 2023. It includes detailed information about flights, delays, and associated features, making it suitable for both regression and classification tasks.

### Dataset Details
- **Source:** Kaggle: [Flight Delay and Cancellation Dataset (2019-2023)](https://www.kaggle.com/datasets/patrickzel/flight-delay-and-cancellation-dataset-2019-2023/data?select=flights_sample_3m.csv)
- **URL:** `https://www.kaggle.com/datasets/patrickzel/flight-delay-and-cancellation-dataset-2019-2023/data?select=flights_sample_3m.csv`
- **Size:** Over 29 million records
- **Variables:** 32 features, including both categorical and numerical data

### Key Variables
- **Categorical Features:** Origin, Destination, Airline, etc.
- **Numerical Features:** Distance, Air Time, Elapsed Time, various Delay Reasons
- **Target Variable:** Arrival Delay (ARR_DELAY) – numerical for regression and binary (0/1) for classification (delays > 15 minutes).

---

## Problem Statement

### Objectives
1. **Predict Delay Occurrence:** Classify whether a flight will be delayed based on a 15-minute threshold.
2. **Forecast Delay Duration:** For delayed flights, predict the expected delay duration in minutes.

### Stakeholders
- **Passengers:** Gain actionable insights to make informed travel decisions.
- **Airlines:** Optimize resource allocation and improve customer satisfaction.
- **Airports:** Enhance operational efficiency and streamline passenger flow.

---

## Data Cleaning and Preprocessing

The raw dataset underwent extensive cleaning and preprocessing to prepare it for analysis and modeling. Below are the steps taken:

### Data Cleaning
1. **Filtering Major Airports:**
   - Restricted the dataset to the 30 largest U.S. airports to focus on high-traffic hubs.
   - **Rationale:** These airports exhibit more consistent patterns, reducing variability and simplifying modeling.

2. **Excluding Canceled Flights:**
   - Removed rows with cancellations (CANCELLED = True).
   - **Rationale:** Cancellation causes differ significantly from delay causes and would introduce noise.

3. **Removing Extreme Delays:**
   - Excluded flights with delays exceeding 8 hours (480 minutes).
   - **Rationale:** Extreme outliers skew the results and do not represent typical delay conditions.

4. **Excluding COVID-19 Data:**
   - Removed all data from 2020.
   - **Rationale:** Flight patterns during the pandemic were atypical, making the data less generalizable.

5. **Leakage Prevention:**
   - Dropped columns that directly revealed the target variable (e.g., DEP_DELAY, ARR_TIME).

6. **Handling Missing Data:**
   - Imputed or removed records with missing critical variables, depending on their significance.

### Feature Engineering
Several features were engineered to enhance predictive power:

1. **Date-Based Features:**
   - **MONTH:** Extracted numerical values (1-12) from flight dates.
   - **DAY_OF_WEEK:** Encoded days as integers (0=Monday, 6=Sunday).
   - **DEP_HOUR:** Extracted scheduled departure hour from CRS_DEP_TIME.
   - **Rationale:** Captures seasonal, weekly, and hourly travel trends.

2. **Route Characteristics:**
   - **DISTANCE:** Flight distance between origin and destination airports.
   - **AIR_TIME:** Actual time spent in flight.
   - **ELAPSED_TIME:** Scheduled flight duration.
   - **Rationale:** These features account for flight logistics and operational complexity.

3. **Weather-Related Features:**
   - **AVG_WEATHER_DELAY:** Monthly averages of weather-related delays.
   - **Rationale:** Captures historical weather impacts without causing data leakage.

---

## Modeling Approach

### Models Explored
1. **Baseline Model:**
   - Mean-based predictions for benchmarking.
   - **Purpose:** Establish a minimum performance benchmark.

2. **Linear Models:**
   - **Lasso Regression:** Feature selection and regularization.
   - **Ridge Regression:** Penalization for overfitting.

3. **Tree-Based Models:**
   - **Decision Trees:** For interpretable results.
   - **Random Forests:** For capturing complex patterns.

4. **Boosting:**
   - **LightGBM:** For enhanced accuracy and categorical feature handling.

5. **Neural Networks:**
   - Tested various architectures to capture nonlinear relationships.

### Evaluation Metrics
- **Mean Squared Error (MSE):** For regression.
- **Accuracy:** For binary classification.
- **Baseline Comparison:** To gauge model improvement over naive predictions.

### Results
- **Best Model:** LightGBM achieved the lowest MSE and excelled at capturing non-linear relationships.
- **Key Insights:** Boosting models outperformed others in both regression and classification tasks.

---

## Key Challenges

1. **Handling Large Datasets:** Computational demands necessitated feature selection and dimensionality reduction.
2. **Categorical Variables:** Encoding methods, such as one-hot encoding, introduced challenges in memory usage.
3. **Outliers:** Predicting extreme delays proved difficult due to their rarity.
4. **Leakage Mitigation:** Ensuring the model did not inadvertently use target-related information.

---

## Future Directions

1. **Incorporate Contextual Data:**
   - Regional holidays, weather patterns, and airport-specific factors.

2. **Develop Specialized Models:**
   - Separate models for predicting extreme delays (>2 hours).

3. **Expand Data Sources:**
   - Include inbound flight delays and airport maintenance data.

---

## How to Use

### Repository Setup
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/fjmoguel/flight-delay-prediction.git
   ```

2. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run Analysis:**
   - Navigate to the `notebooks/` directory and execute the provided Jupyter notebooks for data exploration, preprocessing, and model training.

### Directory Structure
- `data/`: Contains cleaned datasets.
- `notebooks/`: Jupyter notebooks for analysis and modeling.
- `src/`: Core scripts for data processing and feature engineering.
- `reports/`: Final presentation slides and results.

---

## Contributors

Team 6:
- Francisco Moguel
- Uriel Choi
- Zachary Held
- Vivian Shen
- Albert Zhang

---

## Acknowledgments

- [Kaggle Dataset: Flight Delay and Cancellation (2019-2023)](https://www.kaggle.com/datasets/patrickzel/flight-delay-and-cancellation-dataset-2019-2023/data?select=flights_sample_3m.csv)
- Boston University’s BA476: Predictive Analytics course and Dr. Georgios Zervas for guidance.

---

