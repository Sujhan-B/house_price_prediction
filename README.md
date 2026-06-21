requirements.txt
pandas
numpy
matplotlib
scikit-learn

Bengaluru House Price Prediction
Project Overview
This project aims to predict house prices in Bengaluru, India, using a dataset containing various property features. The notebook covers data loading, extensive data cleaning, feature engineering, outlier detection, and training multiple regression models to find the best fit for price prediction.

Dataset
The dataset used is Bengaluru_House_Data.csv, which includes information such as area_type, availability, location, size, society, total_sqft, bath, balcony, and price.

Key Steps
Data Loading and Initial Exploration:

Loaded the dataset into a pandas DataFrame.
Inspected the shape and initial rows of the data.
Data Cleaning:

Dropped irrelevant columns (area_type, availability, balcony, society).
Handled missing values by dropping rows with NaN (after verifying their count).
Cleaned the size column to extract the number of BHKs/Bedrooms.
Feature Engineering:

Converted total_sqft column to a consistent numerical format, handling range values by taking their average.
Created a new feature price_per_sqft for outlier detection.
Outlier Detection and Removal:

Addressed properties with bhk count greater than 20 (e.g., 27 BHK in 8000 sqft, 43 Bedroom in 2400 sqft) as potential data errors.
Removed properties where total_sqft per bhk was less than 300 (a common heuristic for reasonable room size).
Applied standard deviation-based outlier removal for price_per_sqft grouped by location.
Removed bhk outliers by comparing price_per_sqft of a BHK with the mean price_per_sqft of bhk-1 in the same location.
Filtered properties where the number of bathrooms was significantly higher than the number of BHKs (e.g., bath > bhk+2).
Dimensionality Reduction:

Categorized locations with very few data points (less than or equal to 10) into an 'others' category to manage the high cardinality of the location feature.
One-Hot Encoding:

Converted the location categorical feature into numerical format using one-hot encoding.
Dropped the original location column and one of the dummy variables to avoid multicollinearity.
Model Training:

Split the data into training and testing sets.
Trained a Linear Regression model, achieving a test score of approximately 84.3%.
Used K-Fold Cross Validation with ShuffleSplit to evaluate the Linear Regression model, showing consistent scores around 80-88%.
Performed GridSearchCV to compare Linear Regression, Lasso Regression, and Decision Tree Regressor models, confirming Linear Regression (with StandardScaler) as the best-performing model for this dataset.
Technologies Used
Python 3
pandas (for data manipulation and analysis)
numpy (for numerical operations)
matplotlib (for data visualization)
scikit-learn (for machine learning models and utilities)
How to Run
Download the Notebook: Save this .ipynb file to your local machine or Google Drive.
Upload Data: Ensure Bengaluru_House_Data.csv is available at the file.
Open in Google Colab: Open the notebook in Google Colab.
Run Cells: Execute all cells sequentially. The output, including model performance and predictions, will be displayed.
Prediction Function
The notebook includes a predict_price function that takes location, total_sqft, bath, and bhk as input to predict the house price using the trained Linear Regression model.

