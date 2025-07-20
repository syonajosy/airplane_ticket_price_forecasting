✈️ Airfare Prediction and Optimization with PySpark

📘 Project Overview

The airline industry is characterized by complex, fluctuating pricing mechanisms influenced by demand, seasonality, and market competition. This project leverages PySpark to develop a scalable solution for predicting airfares and exploring pricing optimization strategies.

Using a large dataset of historical flight information, the project focuses on:

Accurately predicting airfare prices.

Extracting insights on influential variables.

Exploring revenue optimization strategies for airlines based on predicted demand.

🎯 Objectives

🔮 Prediction Goals

Build a regression model with:

RMSE within 10–15% of average fare.

R² > 0.9 for strong model fit.

📊 Inference Goals

Analyze feature importance (e.g., day of week, distance, layovers).

Identify non-linear relationships (e.g., days until departure vs. fare).

Detect seasonality effects (e.g., holidays, weekends).

💰 Optimization Goals

Simulate demand-based pricing using predictions.

Propose strategies for dynamic fare adjustments to maximize revenue.

📦 Dataset

Sourced from Kaggle, the dataset includes millions of flight itineraries and features such as:

Temporal: searchDate, flightDate, elapsedDays

Flight Info: originAirportCode, destinationAirportCode, segmentsAirlineCode

Pricing: baseFare, totalFare

Additional: seatsRemaining, cabinCode, isRefundable, isBasicEconomy

🧪 Key Findings

Non-Linearity of Pricing: Fare vs. days until departure did not follow a linear pattern. Sometimes prices decreased as the date approached, but often spiked just before departure.

Layovers and Pricing: While more layovers generally meant lower fares, certain single-layover routes were more expensive than direct flights, likely due to route popularity.

Seasonal Effects: Significant fare increases were observed around summer and holiday seasons.

Airport and Airline Influence: Different airports and airlines showed varied pricing strategies even for similar routes.

Weekday Trends: Flight demand peaks midweek, while weekend traffic drops. However, day-of-week had minimal impact on average fare.

Strong Correlations:

totalFare ↔ travelDuration (0.95)

totalFare ↔ totalTravelDistance (0.76)

days_until_departure ↔ fare_difference (−0.48)

🧰 Exploratory Data Analysis (EDA)

Skewed Distributions: totalFare and travelDuration showed strong right skew.

Missing Values: Handled using KNN imputation.

Outliers: Removed using IQR method.

Segment Handling: Exploded multi-segment fields to extract meaningful features.

🔧 Data Preprocessing

Categorical Encoding: Used StringIndexer and OneHotEncoder

Feature Engineering:

days_until_departure, search_day_of_week, price_per_mile

Interaction terms: fare * days_until_departure

Feature Selection:

Removed highly correlated variables

Selected top features based on tree-based importance

💡 Modeling Approach

Models were trained using PySpark MLlib:

Model

RMSE

R²

GBTRegressor

12.60

0.99

RandomForestRegressor

16.86

0.98

DecisionTreeRegressor

15.25

0.98

LinearRegression

18.47

0.98

GBTRegressor was the most accurate due to its ability to capture non-linear patterns.

⚠️ Challenges

KNN Imputation was resource-intensive on large data.

High-cardinality categorical variables required careful encoding.

Multicollinearity required removal of redundant features.

Segment explosion increased feature space and complexity.

🤔 Insights and Future Work

Use price elasticity estimation to dynamically optimize fares.

Integrate real-time booking trends for live fare adjustments.

Extend the model to include seat availability and customer behavior patterns.

💪 Tech Stack

Apache Spark / PySpark

Python (Pandas, NumPy, Matplotlib, Seaborn)

MLlib (PySpark’s ML Library)

Jupyter Notebooks

📚 Citations

Kaggle Flight Prices Dataset

Hastie, Tibshirani, Friedman — The Elements of Statistical Learning

Apache Spark Documentation

Matplotlib

Pandas

Scikit-learn

Seaborn
