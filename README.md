# nyc-traffic-accident-analysis
# NYC Traffic Accident Analysis

## Project Overview

This project analyzes the relationship between traffic volume and motor vehicle collisions in New York City. The goal is to move from raw traffic and crash data toward useful insights about when accidents are more likely to occur and whether traffic volume can help predict accident frequency.

The project uses two NYC datasets:

* **NYC Automated Traffic Volume Counts**
* **NYC Collisions**

The main urban problem explored is:

> How does traffic volume relate to accident frequency in NYC, and can traffic patterns help predict collision counts?

## Datasets Used

### NYC Automated Traffic Volume Counts

This dataset contains traffic count records collected at different street segments in NYC.

Important columns used:

| Column | Description                                |
| ------ | ------------------------------------------ |
| `Yr`   | Year of traffic count                      |
| `M`    | Month of traffic count                     |
| `D`    | Day of traffic count                       |
| `HH`   | Hour of traffic count                      |
| `MM`   | Minute of traffic count                    |
| `Vol`  | Vehicle volume counted during the interval |

### NYC Collisions

This dataset contains motor vehicle collision records in NYC.

Important columns used:

| Column                | Description                  |
| --------------------- | ---------------------------- |
| `Date`                | Collision date               |
| `Time`                | Collision time               |
| `Borough`             | NYC borough                  |
| `Latitude`            | Collision latitude           |
| `Longitude`           | Collision longitude          |
| `Persons Injured`     | Number of injured persons    |
| `Persons Killed`      | Number of killed persons     |
| `Contributing Factor` | Reported contributing factor |
| `Vehicle Type`        | Type of vehicle involved     |

---

## Data Processing

The traffic dataset was large, so chunk-based sampling was used to avoid loading the full file into memory. Only the columns needed for analysis were selected.

Both datasets were converted into datetime format, then time-based features were extracted:

* `month`
* `day_of_week`
* `hour`

Because the datasets did not share a clean common street-level identifier, they were merged using temporal features:

```text
month + day_of_week + hour
```

This allowed the project to compare general traffic patterns with collision frequency.

The final merged dataset contained:

| Column           | Description             |
| ---------------- | ----------------------- |
| `month`          | Month of the record     |
| `day_of_week`    | Day of week as a number |
| `hour`           | Hour of day             |
| `traffic_volume` | Average vehicle volume  |
| `accident_count` | Number of collisions    |

---

## Exploratory Data Analysis

The EDA section focuses on understanding the data before modeling.

Planned analysis includes:

* Distribution of traffic volume
* Distribution of accident counts
* Correlation between numeric variables
* Relationship between traffic volume and accident count
* Accident patterns by hour and day of week

The goal of this step is to answer questions like:

* Are accident counts skewed?
* Are there certain hours with higher collision counts?
* Does traffic volume appear related to accident frequency?
* Are any features strongly correlated with each other?

---

## Hypothesis Testing

A formal statistical test is used to validate whether traffic conditions are associated with accident frequency.

Example hypothesis:

**Null Hypothesis (H0):**
There is no significant difference in accident counts between low-traffic and high-traffic conditions.

**Alternative Hypothesis (H1):**
There is a significant difference in accident counts between low-traffic and high-traffic conditions.

A t-test can be used by splitting traffic volume into low-volume and high-volume groups, then comparing their accident counts.

The p-value is used to determine statistical significance:

* If `p < 0.05`, reject the null hypothesis.
* If `p >= 0.05`, fail to reject the null hypothesis.

---

## Model Building

This project uses **supervised learning** because the goal is to predict a known numerical target.

The target variable is:

```text
accident_count
```

The model predicts accident count using features such as:

```text
traffic_volume, hour, day_of_week, month
```

Since the target is numeric, this is a **regression problem**.

The model used is:

```text
Random Forest Regressor
```

This model was chosen because it can capture non-linear relationships between traffic volume, time-based features, and accident counts.

---

## Model Evaluation

The regression model is evaluated using:

| Metric   | Meaning                                                                 |
| -------- | ----------------------------------------------------------------------- |
| R² Score | Measures how much variation in accident count is explained by the model |
| RMSE     | Measures the average prediction error in accident count                 |

A higher R² score means the model explains more of the variation in the target variable.

A lower RMSE means the predictions are closer to the actual accident counts.

---

## Knowledge Discovery

The most important insight from the model is that traffic volume appears to be a major predictor of accident count.

Feature importance from the Random Forest model showed that traffic volume had the strongest influence on predictions, followed by time-based features such as hour of day.

This suggests that collision frequency is not random. It is connected to traffic patterns and specific time periods.

---

## Actionable Insight

Based on the analysis, NYC traffic safety efforts should prioritize time periods with both high traffic volume and high accident counts.

Possible recommendations include:

* Increasing traffic monitoring during high-risk hours
* Improving signal timing in busy traffic periods
* Prioritizing enforcement or safety campaigns around peak accident times
* Studying high-volume periods more closely for infrastructure improvements

---

## Project Structure

```text
nyc-traffic-accident-analysis/
│
├── README.md
├── notebook/
│   └── NYC_Traffic_Accident_Analysis.ipynb
│
├── data/
│   └── merged_dataset.csv
│
├── report/
│   └── final_report.pdf
│
└── visuals/
    └── plots/
```

---

## Technologies Used

* Python
* Google Colab
* Pandas
* NumPy
* Matplotlib
* Scikit-learn
* SciPy

---

## How to Run

1. Open the Google Colab notebook.
2. Mount Google Drive.
3. Make sure the datasets are stored in:

```text
/content/drive/MyDrive/TrafficData/
```

4. Run the notebook cells in order.
5. The notebook will:

   * sample the large traffic dataset
   * load the collision dataset
   * aggregate both datasets
   * merge them by temporal features
   * perform analysis
   * train and evaluate the model

---

## Limitations

This project uses a temporal merge rather than a perfect street-level merge. This was necessary because the two datasets did not share a clean common location identifier.

Because of this, the model should be interpreted as analyzing general traffic-time patterns rather than exact street-by-street accident risk.

A future improvement would be to use geospatial joins with latitude, longitude, street segment IDs, or GIS tools to match collisions more directly to traffic count locations.

---

## Final Takeaway

This project shows that traffic volume and time-based patterns can help explain accident frequency in NYC. While the model is not perfect, it provides useful evidence that traffic safety planning should consider both vehicle volume and temporal accident patterns when identifying high-risk periods.
