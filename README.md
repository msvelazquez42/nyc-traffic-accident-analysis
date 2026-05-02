# NYC Traffic Accident Analysis

## Project Overview

This project analyzes the relationship between traffic volume and motor vehicle collisions in New York City. The main goal is to determine whether traffic patterns, especially traffic volume and time of day, can help explain or predict accident frequency.

The project uses supervised learning because the model predicts a numerical target: `accident_count`.

---

## Datasets Used

### NYC Automated Traffic Volume Counts

This dataset provides traffic count information across NYC street segments.

Key columns used:

| Column         | Description                                |
| -------------- | ------------------------------------------ |
| `Yr`, `M`, `D` | Date information                           |
| `HH`, `MM`     | Time information                           |
| `Vol`          | Vehicle volume counted during the interval |

### NYC Collisions

This dataset provides motor vehicle collision records in NYC.

Key columns used:

| Column            | Description                          |
| ----------------- | ------------------------------------ |
| `Date`            | Date of collision                    |
| `Time`            | Time of collision                    |
| `Borough`         | Borough where the collision occurred |
| `Persons Injured` | Number of people injured             |
| `Persons Killed`  | Number of people killed              |

The datasets were merged using time-based features: `month`, `day_of_week`, and `hour`.

---

## Knowledge Discovery

The model showed that traffic volume was the strongest predictor of accident count. Hour of day also influenced the results, showing that accident frequency is connected not only to how many vehicles are on the road, but also to when the traffic occurs.

This suggests that collision patterns are not random. They follow time-based and volume-based trends that can be useful for urban traffic safety analysis.

---

## Actionable Insight

NYC should prioritize safety planning during time periods where both traffic volume and accident counts are high. This could include increased monitoring, adjusted traffic signal timing, targeted enforcement, or further investigation into high-risk time periods.

Instead of only focusing on locations after accidents happen, the city could use traffic volume and time patterns to identify when risk is more likely to increase.

---

## Final Takeaway

Traffic volume and time-based patterns can help explain accident frequency in NYC. While this project uses a general temporal merge rather than a perfect street-level merge, the model still shows that traffic behavior is useful for understanding and predicting collision trends.
