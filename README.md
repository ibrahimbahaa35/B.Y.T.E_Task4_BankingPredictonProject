Banking Market Prediction: Decision Tree Classifier (B.Y.T.E Task 4)
This project analyzes the Bank Marketing dataset to predict whether a client will subscribe to a term deposit. Using a Decision Tree Classifier, the workflow covers end-to-end machine learning pipeline steps, from initial exploratory data analysis to feature importance extraction.

Dataset
Source: Bank Marketing - UCI Machine Learning Repository
The dataset contains records from direct marketing campaigns (phone calls) of a Portuguese banking institution. The classification goal is to predict if the client will subscribe to a term deposit (the y or target variable).

Project Workflow
1. Data Exploration
Initial Inspection: Loaded the bank-additional-full.csv dataset, examining the shape (41,188 rows, 21 columns), data types, and descriptive statistics.
Correlation Analysis: Generated a correlation heatmap for numerical variables. Discovered strong positive relationships between macroeconomic indicators, particularly between euribor_3m, number_employed, and employment_variation_rate.
2. Data Cleaning
Standardization: Renamed columns to standard snake_case for readability (e.g., emp.var.rate to employment_variation_rate).
Outlier Detection & Handling: Identified extreme outliers in the duration column and filtered the dataset to retain values between the 10th and 90th percentiles.
Deduplication: Identified and removed duplicate rows.
Target Transformation: Mapped the binary target variable from 'yes'/'no' to 1/0.
Handling Missing Values: Converted 'unknown' string values to standard NaN and dropped rows containing missing data to ensure clean inputs for the model.
3. Training the Decision Tree Model
Feature Engineering: Dropped the duration column from the feature matrix to prevent data leakage, as call duration is only known after a call has concluded.
Data Splitting: Split the data into training and validation sets (80/20 split) to ensure unbiased evaluation.
Baseline Establishment: Calculated a baseline accuracy of ~90.23% by predicting the majority class (0 - No) for all observations.
Hyperparameter Tuning: Built a modeling pipeline using OrdinalEncoder and DecisionTreeClassifier. Iterated through maximum tree depths (1 to 15) to find the optimal balance between bias and variance. Visualized train vs. test accuracies to identify max_depth = 4 as the optimal parameter to prevent overfitting.
4. Calculating Metrics & Evaluation
The final Decision Tree model (max_depth = 4) yielded the following performance metrics:

Training Accuracy: 97%
Testing Accuracy: 89%
Precision Score: 0.47 (Caught ~47% of the actual positive predictions correctly).
Recall Score: 0.40 (Identified ~40% of the actual true positive cases).
Confusion Matrix: Plotted to visualize the exact breakdown of True Positives, True Negatives, False Positives, and False Negatives, highlighting the model's performance against the imbalanced classes.
5. Feature Importance & Key Insights
Extracted and plotted the top 5 driving features determining a client's likelihood to subscribe:

number_employed
consumer_confidence_index
previous_outcome
month
euribor_3m
The primary insight is that macroeconomic conditions drive term deposit subscriptions far more than personal demographics. The number of employees (number_employed) and the consumer confidence index (consumer_confidence_index) are the strongest predictors of a client's decision. Additionally, past engagement success (previous_outcome) plays a crucial role. Overall, economic stability and prior positive interactions are the best indicators for successful conversions in this dataset.                                                                                                                                                     write this with markdown for organizing a readme file 
