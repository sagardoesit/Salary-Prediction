# Salary-Prediction
This is a repository of the project Salary Predictions

# Files in Repo
salarypredictions.ipynb - Contains Python code for EDA and determining factors in predicting salary.
salaryprediction-eda-checkpoint.ipynb - Python notebook for machine learning concepts and various Statistical Models.

# Introduction
Employers and human resources professionals must consider many decisions carefully when  planning what they will pay employees on a job. This shouldn’t be a surprise as pay exerts important effects to employees and does account for a significant part of an organization’s cost structure. Chief among these decisions is determining the average amount the organization pays for a job.   

To determine salary ranges, many HR professionals consult trustworthy resources of salary research with the aim of determining market pay rates established through market pay studies for people doing similar work in similar industries in the same region or country in addition to accounting for attributes unique to employees such as educational level, skill, and experience, and regulatory requirements like Equal Pay and minimum wage requirements (Heathfield, 2019), which can take up a significant amount of time. According to a national study conducted by  Harris Poll on behalf of CareerBuilder in 2017,  HR managers loose up to 14 hours per week for the lack of automation. But thanks to improvements in machine learning and predictive analytics, HR professional no longer need to waste their valuable time calculating salary ranges. 

In this project I demonstrate building a salary prediction model for new job postings given some features of historical job postings. My aim is to demonstrate how machine learning could automate the salary determination task.

# Data Collection

To build our model, I use a dataset containing 1 million records of past postings with salaries and additional features specific to each job such as the required education level, major, years of experience, and job type.

The dataset had the following features:

-	jobId
-	salary
-	companyId
-	jobType
-	degree
-	major
-	industry
-	yearsExperience
-	milesFromMetropolis

# Exploratory Data Analysis

After loading the data in a Jupyter environment, I performed an exploratory data analysis (EDA) to understand  the structure and distribution of the dataset. 

I took the following steps and made the following observations:
 - Ensured no duplicated data by verifying that the dataset had one record per jobId
 - Checked for features with non-unique values but found none
 - Inspected outliers on salary (our target variable) and identified some jobs with no salaries
 - The target variable followed a normal distribution, giving us more algorithm options for modeling the data
 - No missing values were found


# Data Preprocessing

As part of data cleaning I implemented the following steps:
- Removed all jobs with no salaries
- Build a data transformation pipeline to:
    * Separate categorical and numerical features and transform those features in parallel:
      - For the categorical features:
           * Ordinal encoded the degree feature as
                  {'NONE': 0, 'HIGH_SCHOOL': 1, 'BACHELORS': 2, 'MASTERS': 3, 'DOCTORAL': 4}
           * Numerically encoded all remaining categorical features with pandas factorize method           
      - For numerical features:
           * Applied standardization to all numerical features
    * No additional steps were needed as the dataset was now clean and ready for modeling


# Data Modeling
To model the data, I implemented the following steps:
 - Engineered three more features:
    * less_than_HighSchool – an indicator for without high school completion
    * eduAndExp – indicates masters or higher education and more than five years of experience
    * notEduNotExp – indicates no college and less than one-year experience
- Fitted 3 models below with selected hyperparameters for tuning:
    * Random Forest Regressor:
        - n_estimators: [0,75,100,150,200,1000]
        - max_features: ['auto','sqrt', 'log2',  0.33]
    * Gradient Boosting Regressor:
        - n_estimators: [100,200]
        - learning_rate: [0.05,0.1,0.2]
        - max_depth: [1,3,5]
        - subsample: [0.5,0.7,1.0]
    * Lasso:
        - alpha: [0.001, 0.005, 0.01, 0.05, 0.1, 0.5, 1, 5, 10]
- Performed a 10 folds randomized search cross validation on the data and selected the best performing model with the least prediction error (i.e. lowest mean squared error)

        
# Results

The Gradient Boosting Regressor performed best on our data with a prediction error of 357.91, meaning if this model is to be implemented in a real world setting then predictions from this model will be between + or – $357.91 of the true yearly salary for the position which is practically reasonable.

# Conclusion

While these results could be improved with additional feature engineering, our results have demonstrated how machine learning could help automate the salary determination process.
