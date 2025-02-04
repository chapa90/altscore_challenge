# altscore_challenge
csv file containing test data and cost of living predictions (y) per hex_id (x) using a predictive model (RandomForestRegressor), train data and mobility data (parquet file). Random Forest Regressor predictive model was chosen due to having a lower MSE (please see attached python script)

Galactic Empire Cost of Living Prediction

Overview

The Galactic Empire Cost of Living Prediction project is designed to analyze geospatial mobility data to predict the cost of living in various sectors of the galaxy. Using data provided by the Galactic Council's H3 geospatial grid and machine learning techniques, the project generates insights that can aid in the Rebellion's efforts to expose the Empire's secrets.

Objective

As a Rebel intelligence officer, your mission is to:

Decode encrypted mobility data.

Engineer meaningful features.

Predict the true cost of living for regions across the galaxy.

Save predictions in a format suitable for submission.

Data Description

The project uses three key datasets:

1. train.csv

Purpose: Training dataset containing known cost-of-living values.

Columns:

hex_id: Geospatial H3 hexagon ID.

cost_of_living: A numeric value between 0 and 1 representing the cost of living.

2. test.csv

Purpose: Dataset for generating predictions.

Columns:

hex_id: Geospatial H3 hexagon ID.

cost_of_living: (Empty) Column to be filled with predictions.

3. mobility.parquet

Purpose: Dataset containing movement patterns.

Columns:

device_id: Unique anonymized identifier for mobile devices.

lat: Latitude of the observation.

lon: Longitude of the observation.

timestamp: UNIX timestamp indicating when the observation occurred.

Workflow

The project follows these steps:

1. Data Loading

Load the train.csv and test.csv files to understand the existing data.

Load mobility.parquet in chunks to handle its large size efficiently.

2. Data Processing

Convert latitude and longitude into H3 hexagon IDs.

Aggregate mobility features (e.g., device count, visit count, average timestamp) for each hexagon ID.

Merge these features with the train.csv and test.csv datasets.

3. Model Training and Evaluation

Two machine learning models were trained and evaluated:

Random Forest Regressor

XGBoost Regressor

Both models were trained on the processed data, and their performance was compared using the Mean Squared Error (MSE) metric.
The model with the lower MSE was selected for predictions, which was the Random Forest Regressor.

4. Prediction

Apply the selected model to the test.csv dataset.

Generate predictions for the cost of living in regions under Imperial control.

5. Submission

Save the predictions in a CSV format matching the structure of test.csv.

How to Run

Install the required libraries:

pip install pandas pyarrow h3 xgboost scikit-learn

Ensure the following files are in the specified paths:

train.csv

test.csv

mobility.parquet

Run the Python script provided.

Check the output submission.csv for predictions.

Key Highlights

H3 Geospatial Grid: The project leverages the H3 system for geospatial indexing, enabling precise regional analysis.

Machine Learning Models: Both Random Forest and XGBoost models were evaluated, with the Random Forest Regressor yielding better performance.

Efficient Data Processing: Processes large datasets in chunks to handle memory constraints.

Outputs

submission.csv: Contains the predicted cost_of_living for all hexagon IDs in the test dataset.

Example Format

hex_id,cost_of_living
8a2a1072b59ffff,0.45
8a2a1072a7bffff,0.60
8a2a1072959ffff,0.33

Evaluation Metric

Mean Squared Error (MSE): Measures the accuracy of predictions on the validation set.
