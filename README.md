# Credit Card Classification

[Presentation](https://docs.google.com/presentation/d/1KAX45m0vJLl9hF3pMOYaTrom7tYX2pT7DlNWmYQPaZs/edit?usp=sharing)

## Navigation

1) 'data' folder contains the data set used. Link to the data set is below.
2) 'notebooks' folder contains the iterations of my project. 'final_notebook' is the latest version.
3) 'visualizations' folder contains some saved visualizations from the 'final_notebook' notebook.
4) All other files are used internally for the project as a whole.

## Business Problem Summary:
The project goal is to try and replicate the way credit card approval algorithms make their decision to approve or deny someone for a credit card. My project is three fold:

1) Train a computer model to simulate a credit card application algorithm

2) Use the trained model on a web app that simulates an online credit card application

3) People less familiar with credit cards will have a better idea of what factors impact decisions

Testing out various models to see how well they work with a data set that contains information that would be submitted by someone applying for a credit card online. Then from each of the best perfoming alogorithms, display which features (columns of data) each model used the most to the least. There is also an overall look at feature importance for all the data.

A best performing model has been selected and optimized as well as the top most relevant features selected. A Flask web app has been deployed and utilizes the trained computer model. Users can now choose 1 of 4 pre-defined people to see if that person will be approved or not. Along with the results of the application, each of these 4 people also has different explanations as to why that person is being approved or denied a credit card. In reading these 4 unique scenarios, people can see that there are some overlapping factors that can help or hurt someone when applying for a credit card.

## Overview of Process:

### 1) Data Collection and Processing:
The project data set is provided by U.C. Irvine and was submitted anonymously. The data set itself has also been anonymized due to the possibility that this data is from an actual credit card company or bank. This is also partly why the data set is rather limited in size as well and how well the data can be used by computer models without further manipulation. [The UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/credit+approval)

The original form of the data set has columns and values that don't represent the information one might expect to see for credit card applications. Research led me to find this [data science blog using R](https://nycdatascience.com/blog/student-works/credit-card-approval-analysis/), which is a useful resource for describing what the columns are. From there it is easier to figure out what most of the values of each column represent. Some steps taken to convert the data to be usable in modeling include:

a) Fill in as much missing data as possible

b) Rename columns to have useful names

c) Columns like 'Gender' had 'a' or 'b'; changed those to be '1' or '0'

d) Change 'Age' values from values like '34.57' to '34'

e) Target column 'Approval' was '+' or '-', which changed to '1' or '0'

### 2) Feature Heatmaps and Model Building:
Before building various models to test the data with, using heatmaps to see which columns might be strongly correlated to the target 'Approval' column helps with the initial exploratory data analysis (EDA). While this doesn't impact initial modeling, it does start to help give a sense of what information might realistically be used (more heavily than others) in real world credit card application decision models. Some columns that stood out on the heatmaps were: 'Debt', 'YearsWorked', 'PriorDefault', 'Employed', 'CreditScore' and 'Income'. 'BankClient' and 'Married' had a very strong connection which was unexpected.

Initial models tested were: Logistic Regression, KNeighbors, Random Forest, Support Vector Machine, XGBoost, Multi-Layer Perceptron, AdaBoost, GaussianNB, GaussianProcess, QuadraticDiscriminant and GradientBoost. From there the selected was narrowed down to Logistic Regression, Random Forest, XGBoost, AdaBoost and GradientBoost simply based on these models having the best accuracy scores and overall results in their respective confusion matrices and classification reports. These models then had feature importances and coefficients (Logistic Regression) visualized. The final two top models are Logistic Regression and Random Forest, with Random Forest being the final choice.

### 3) Model Evaluation
Lastly, by utilizing GridSearchCV the final two models can be cross validated to really evaluate the performance of each. Logistic Regression currently has a 10 fold cross validated accuracy score of 86.14% and the Random Forest model has 88.61%. In terms of confusion matrices and classification report results, these two models are fairly close but the Random Forest model has overall better results.

For example, the confusion matrix for Logistic Regression has a larger number for False Positives. In the case of credit card applications, this means that the Logistic Regression model predicted application approvals but these should actually be application denials. This could be costly to a company because a company wouldn't want to approve someone who isn't supposed to be approved. One scenario could be that a specific applicant from this grouping could be considered a financial risk due to having a defaulted loan and/or a bad credit score.
