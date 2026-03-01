# SDSS-Datathon

### Data Analysis Key Findings
*   The notebook's primary purpose is data analysis for airline models, using data initially loaded from `https://github.com/Speeb04/SDSS-Datathon/raw/refs/heads/main/Resources/Cases/Airline%20Tickets/airline_ticket_dataset.csv`.
*   Data preprocessing involved cleaning city names by removing the suffix ' (Metropolitan Area)' from `city1` and `city2` columns for standardization, and identifying unique cities and carrier types.
*   Feature engineering included the creation of boolean indicators: `city1_is_hub`, `city2_is_hub` (for hub cities), `carrier_lg_is_full_service`, and `carrier_low_is_low_cost` (for carrier types).
*   Population data (2020-2024 estimates) was successfully integrated into the dataset for `city1` and `city2` using a lookup table (`pop_lut`) and the `addPOP` function.
*   An attempt to integrate GDP data (2001-2018) encountered significant challenges, resulting in a large number of 'N/A' values after `GeoName` standardization, indicating difficulties in matching city names from the GDP dataset with those in the main DataFrame.

### Insights or Next Steps
*   The significant 'N/A' values encountered during GDP data integration highlight a need for more robust city name matching or alternative geographic data sources to effectively incorporate economic indicators.
*   The comprehensive data preparation, including cleaning, feature engineering, and partial external data integration, provides a solid foundation for building and training machine learning models to predict various airline-related outcomes, such as ticket prices or passenger demand.


# Airfare Prediction Notebook

This notebook aims to predict airfare prices based on various route and city attributes using machine learning models.

## Table of Contents
1.  [Problem Statement](#problem-statement)
2.  [Data Loading and Initial Exploration](#data-loading-and-initial-exploration)
3.  [Data Cleaning and Preprocessing](#data-cleaning-and-preprocessing)
4.  [Feature Engineering](#feature-engineering)
5.  [Model Training and Evaluation](#model-training-and-evaluation)
6.  [Conclusion and Next Steps](#conclusion-and-next-steps)

## 1. Problem Statement
Given information about a desired route, the objective is to predict the airfare for that route.

## 2. Data Loading and Initial Exploration
-   The dataset `final_output_data.csv` is downloaded from a GitHub repository.
-   Essential libraries like `pandas`, `matplotlib`, `numpy`, and `sklearn` are imported.
-   The CSV file is loaded into a pandas DataFrame named `data`.
-   Initial descriptive statistics (`data.describe()`) and the head of the DataFrame (`data.head()`) are displayed to understand the data structure.

## 3. Data Cleaning and Preprocessing
-   A copy of the original DataFrame (`data`) is made for preprocessing (`df`).
-   Columns with 100% missing values are dropped.
-   Numerical columns are identified, and their values are cleaned by removing currency symbols ('$'), commas (','), and converting '#DIV/0!' to NaN. Data types are then coerced to numeric.
-   Rows with NaN values in `city1_pop_2024` and `city2_pop_2024` are dropped.
-   Remaining NaN values in numerical columns are imputed using the median of their respective columns.
-   The `passengers` column is converted to integer type.

## 4. Feature Engineering
-   A `route` column is created by sorting and concatenating `city1` and `city2` to represent unique routes.
-   Categorical features such as `Year`, `quarter`, `city1`, `city2`, `carrier_lg`, `carrier_low`, and `route` are one-hot encoded using `pd.get_dummies()`.
-   The target variable `y` is set to `fare`.
-   Features `X` are selected, excluding `fare`, `fare_lg`, `fare_low`, `citymarketid_1`, and `citymarketid_2`.

## 5. Model Training and Evaluation
-   The data is split into training and testing sets (`X_train`, `X_test`, `y_train`, `y_test`) with a 80/20 split.
-   **Model 1: Random Forest Regressor**
    -   A `RandomForestRegressor` model is initialized and trained.
    -   Predictions are made on the test set.
    -   The model is evaluated using Mean Absolute Error (MAE), Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and R-squared (R2).
    -   A scatter plot visualizes actual vs. predicted fares.
-   **Model 2: Linear Regression**
    -   A `LinearRegression` model is initialized and trained.
    -   Predictions are made on the test set.
    -   The model is evaluated using MAE, MSE, RMSE, and R2.
    -   A scatter plot visualizes actual vs. predicted fares.
    -   The intercept and coefficients of the Linear Regression model are displayed to understand feature importance.

## 6. Conclusion and Next Steps
The notebook demonstrates the process of building and evaluating models for airfare prediction. Future steps include further feature selection to remove confounding features.
