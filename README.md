# NYC Traffic Accident Analysis

## Project Overview

This project analyzes the relationship between NYC traffic volume and motor vehicle collision frequency. The goal is to determine whether traffic volume and time-based patterns can help explain or predict accident counts.

The project uses supervised learning because the target variable, `accident_count`, is a numerical value. A Random Forest Regressor was used to predict accident frequency based on traffic volume and time-related features.

---

## Datasets Used

Two datasets were used:

### NYC Automated Traffic Volume Counts

This dataset contains vehicle volume counts across NYC traffic segments.

Key columns used:

| Column | Description |
|---|---|
| `Yr` | Year |
| `M` | Month |
| `D` | Day |
| `HH` | Hour |
| `MM` | Minute |
| `Vol` | Traffic volume |

### NYC Collisions

This dataset contains NYC motor vehicle collision records.

Key columns used:

| Column | Description |
|---|---|
| `Date` | Collision date |
| `Time` | Collision time |
| `Borough` | Borough of collision |
| `Street Name` | Street where collision occurred |
| `Persons Injured` | Number of people injured |
| `Persons Killed` | Number of people killed |
| `Contributing Factor` | Reported cause of the collision |
| `Vehicle Type` | Type of vehicle involved |

---

## Data Processing

The traffic volume dataset was very large, so chunk-based sampling was used to process it efficiently. A sample of 500,000 traffic records was taken from the larger dataset.

Both datasets were converted into datetime format. From the datetime values, the following features were created:

- `month`
- `day_of_week`
- `hour`

The two datasets did not share a clean street-level identifier, so they were merged using these shared time-based features:

`month + day_of_week + hour`

After aggregation and merging, the final dataset contained 2,016 rows and 5 columns:

| Column | Description |
|---|---|
| `month` | Month of the record |
| `day_of_week` | Day of the week |
| `hour` | Hour of the day |
| `traffic_volume` | Average traffic volume |
| `accident_count` | Number of collisions |

---

## Exploratory Data Analysis

The EDA focused on feature distributions, correlations, and bivariate relationships.

The distributions of `traffic_volume` and `accident_count` were approximately normal, with skew values close to 0. This meant the target variable did not require a log transformation before regression.

The correlation analysis showed that `traffic_volume` had the strongest relationship with `accident_count`. Hour of day also showed a meaningful relationship with accident frequency.

The bivariate analysis showed that accident counts were higher during busier traffic periods, especially during evening rush hours. Weekday traffic showed clearer peak patterns, while weekend traffic was flatter and peaked later in the day.

---

## Hypothesis Testing

Two statistical tests were used to validate assumptions before model building.

| # | Hypothesis | Test |
|---|---|---|
| 1 | Weekdays have different accident counts than weekends | Welch's T-Test |
| 2 | Time-of-day category affects accident frequency | One-Way ANOVA |

The Welch's T-Test compared weekday and weekend accident counts. The One-Way ANOVA tested whether accident frequency differed across time-of-day groups, including Off-Peak, Morning Rush, Midday, and Evening Rush.

Both tests rejected the null hypothesis at the 0.05 significance level. This supports the idea that accident frequency changes based on day type and time of day.

---

## Model Building

A Random Forest Regressor was used to predict `accident_count`.

The model used `hour` and `traffic_volume` as input features.

The target variable was `accident_count`.

The dataset was split into training and testing sets, with 25% of the data used for testing.

Model performance:

| Metric | Value |
|---|---|
| R² Score | 0.6299 |
| RMSE | 31.6174 |

The R² score means the model explained about 63% of the variation in accident counts. The RMSE means the model's predictions were off by about 32 accidents on average.

---

## Knowledge Discovery

The analysis showed that traffic volume was the strongest predictor of accident count. This confirms that collision frequency is closely related to how many vehicles are on the road.

The results also showed that time matters. Evening rush hours had much higher accident counts than off-peak hours, and weekdays showed stronger traffic peaks than weekends.

This suggests that accident risk is not random. It follows patterns connected to traffic volume, commuting behavior, and time of day.

---

## Actionable Insight

NYC should prioritize traffic safety resources during high-volume time periods, especially weekday evening rush hours.

Possible actions include:

- Increased traffic enforcement during 4 PM to 7 PM
- Better signal timing during rush hour
- More monitoring in high-volume traffic periods
- Targeted safety campaigns for commuters

Instead of only responding after accidents happen, the city could use traffic and time patterns to predict when collision risk is likely to increase.

---

## Final Takeaway

Traffic volume and time-based features can help explain accident frequency in NYC. The model was able to predict accident counts with moderate accuracy, showing that traffic behavior is useful for understanding urban collision patterns.

Although this project uses a temporal merge rather than a perfect street-level merge, the results still provide useful insight into how traffic volume and time of day relate to accident risk.
