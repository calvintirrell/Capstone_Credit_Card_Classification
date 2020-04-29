# Credit Card Classification

## Business Problem Summary:
My project goal is try and shine some more light on the way credit card approval algorithms make their decision to approve or deny someone for a credit card.

For a long time these credit card algorithms have been a black box to everyone but a select few. The general public is on the outside trying to look in the boxes to see what exactly qualifies someone (or not) for a credit card.

I am testing out various models to see how well they work with a data set that contains information that would be submitted by someone applying for a credit card online. Then from each of the best perfoming alogorithms I display which features (columns of data) each model used the most to the least. I also have an overall look at feature importance for all the data.

After a best performing model has been selected and optimized as well as the top most relevant features selected, I aim to have a Flask web app that will act and look like an online credit card application website. This web app will allow users to input their information and 'run' the model to see if they would be approved or denied a credit card.

## Overview of Process:

### 1) Data Collection and Processing:
The data set my project utilizes is from: https://archive.ics.uci.edu/ml/datasets/credit+approval

The original form of the data set has columns and values that don't represent the information one might expect to see for credit card applications. 
My research led me to find (https://nycdatascience.com/blog/student-works/credit-card-approval-analysis/) a useful resource for what the columns are. From there it was easier to figure out what the values of each column represent. The data won't change itself to be useful for modeling, so here's some of what I did:

a) Fill in as much missing data as possible

b) Rename columns to have useful names

c) Columns like 'Gender' had 'a' or 'b'; changed those to be '1' or '0'

d) Change 'Age' values from values like '34.57' to '34'

e) Target column 'Approval' was '+' or '-', which changed to '1' or '0'

### 2) Feature Heatmaps and Model Building:
Before building various models to test the data with, I used heatmaps to see which columns might be strongly correlated to the target 'Approval' column. While this doesn't impact my initial modeling, it does start to help give a sense of what information might realistically be used (more heavily than others) in real world credit card application decision models.
Some columns that caught my eye with these heatmaps were: 'Debt', 'YearsWorked', 'PriorDefault', 'Employed', 'CreditScore' and 'Income'.

Initial models tested were: Logistic Regression, KNeighbors, Random Forest, Support Vector Machine, XGBoost, Multi-Layer Perceptron, AdaBoost, GaussianNB, GaussianProcess, QuadraticDiscriminant and GradientBoost. From here I narrowed down the choices to Logistic Regression, Random Forest, XGBoost, AdaBoost and GradientBoost simply based on these models having the best accuracy scores and overall results in their respective confusion matrices and classification reports. I then visualed these models' feature importances and coefficients, which essentially is how each model 'used' or 'favored' each column in the data set. My final two top models are Logistic Regression and Random Forest. The other models 'relied' too much on some columns which I don't believe should (and likely don't) have that much impact on an algorithm used in industry.

### 3) Model Evaluation
Lastly, by utilizing GridSearchCV I was able to optimize the top two models and perform cross validation to really evaluate the performance of each model. Logistic Regression currently has a 10 fold cross validated accuracy score of 86.14% and the Random Forest model has 88.61%. In terms of confusion matrices and classification report results, these two models are fairly close but the Random Forest model currently has overall better results.

For example, the confusion matrix for Logistic Regression had a larger number for False Positives. In the case of credit card application approvals, this means that the Logistic Regression model predicted application approvals but these were actually application denials. This could be costly to a company in real life usage because ultimately a company wouldn't want to approve someone who isn't supposed to be approved. One scenario could be that one specific applicant from this False Positives grouping could be considered a financial risk due to having a defaulted loan and/or a bad credit score.
