## Project Overview
The airline industry operates in a dynamic market where airfares fluctuate based on real-time demand, seasonal trends, competitive pricing, fuel costs, and other factors. This project, "Airfare Prediction and Optimization with PySpark," aims to:
  - Develop a predictive model to anticipate airfare fluctuations, helping travelers make informed booking decisions.
  - Explore optimization strategies for airlines to maximize revenue by dynamically adjusting prices based on predicted demand.
    
Due to the large-scale nature of airfare data, we leverage Apache Spark and PySpark for data processing, feature engineering, and machine learning model training.

## Project Goals
### 1. Prediction Goals
- Develop a high-accuracy predictive model for airfare prices.
- Target RMSE within 10-15% of average fare and R² above 0.9.

### 2. Inference & Analysis Goals
- Feature Importance: Identify key factors driving airfare fluctuations (e.g., departure days, route, airline, cabin class).
- Variable Relationships: Determine whether pricing follows a linear pattern or has optimal booking windows.
- Seasonality & Temporal Effects: Quantify how holidays, weekdays, and peak travel times affect airfares.

### 3. Optimization Exploration
- Investigate demand-based pricing strategies where airlines can adjust fares dynamically.

## Dataset
Using a large-scale flight dataset containing millions of itineraries with various flight details.
#### Dataset Source: Kaggle - https://www.kaggle.com/datasets/dilwong/flightprices

- Key Features
  - Temporal Data: searchDate, flightDate, elapsedDays, travelDuration
  - Flight Details: originAirportCode, destinationAirportCode, airlineCode, totalTravelDistance, non-stop indicator
  - Pricing Information: baseFare, totalFare
  - Other Attributes: seatsRemaining, economy vs. refundable tickets, cabin class

## Data Processing & Feature Engineering
### 1. Data Cleaning
- Handled missing values (e.g., segment-related features) using KNN imputation.
- Removed outliers in travel duration and fare using IQR method.

### 2. Feature Engineering
- Time-based Features:
- Days until departure, day of the week, month of travel

### Route-based Features:
- Airport codes, route distance

### Pricing-based Features:
- Fare difference, price per mile

### Interaction Features:
- Captured non-linear relationships (e.g., fare × days_until_departure)

### 3. Feature Selection
- Correlation analysis to remove redundant features.
- Feature importance ranking using tree-based models.

## Models & Evaluation  
We trained multiple regression models using **PySpark MLlib**, comparing their performance using **RMSE (Root Mean Squared Error)** and **R² (R-squared)** metrics.  

| **Model**                 | **RMSE** | **R²**  |  
|---------------------------|---------|--------|  
| **GBTRegressor**          | **12.60**  | **0.99**  |  
| **RandomForestRegressor** | 16.86  | 0.98  |  
| **DecisionTreeRegressor** | 15.25  | 0.98  |  
| **Linear Regression**     | 18.47  | 0.98  |  

✅ **Gradient Boosting Trees (GBTRegressor)** performed best, capturing complex patterns in airfare pricing.  


## Final Findings & Insights
### 1. Key Correlations
- Fare increases with travel duration (correlation = 0.95).
- Fare increases with total distance (correlation = 0.76).
- Fare decreases as departure date nears (correlation = -0.48).

### 2. Surprising Findings
- Airfare patterns are non-linear:
- Prices often decrease before departure but can spike last-minute.

### 3. Layovers & Pricing:
- Flights with one layover were sometimes more expensive than direct flights.
- Airport-specific pricing:
- The same airline & route had different fares based on departure airport.

### 4. Seasonality & Trends
- Peak seasons (holidays, summer) drive higher fares.
- Midweek flights tend to be cheaper but weekday differences are minimal.
