# Salary-Prediction
This is a repository of the project Salary Predictions

Salary Prediction Analysis is done with data over million rows using Python.
We have three CSV data files:
• train_features.csv: Each row represents metadata for an individual job posting.
The “jobId” column represents a unique identifier for the job posting. The remaining columns describe features of the job posting.
• train_salaries.csv: Each row associates a “jobId” with a “salary”.
• test_features.csv: Similar to train_features.csv, each row represents metadata for an individual job posting.
The first row of each file contains headers for the columns. The metadata and salary data may contain errors(but fixed during regressional analysis)

By using the data an Exploratory Data Analysis is done determining the factors that are helpful to predict salary using various graphs following the 
concept of IQR and outliers. 
A heat map is generated to get the clear view of the co-relations within the factors.
