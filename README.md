# SDSS-Datathon
We will succeed

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
