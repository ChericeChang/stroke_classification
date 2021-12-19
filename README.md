# Stroke Prediction
###### Can we predict if a patient have stroke based on the features identified?
![stroke](/img/stroke.jpg)
## 1. Data
Data source: [Kaggle](https://www.kaggle.com/fedesoriano/stroke-prediction-dataset) <br>
Data updated date: 2021-01-26 <br>
Number of patients: 5110
* Stroke: 249
* No stroke: 4861
Features:
* Demographic: Gender, Age, Marital Status, Work Type, Residence Type
* Health history: Smoking Status, BMI, Average Glucose Level, Hypertension History, Heart Disease History

## 2. Method
There are many different types of classifier:
1. Decision tree Classifier
2. Logistic Regression
3. Random Forest
4. AdaBoost
5. XGBoost
6. SVM

## 3. Data Cleaning

Most of the columns are pretty clean, except for BMI.
> Treatment for BMI:<br>201 null values were replaced by average BMI from the dataset.

Minor data changes: <br>change values/column name to lower case

In general, this dataset could be pretty generalizable to the population data.
* In US, 2/3 adults were considered to be overweight or have obesity. The dataset has 28.1%, which is closer to the global average 39% of adults are overweight.
* The dataset (76%) contains more married people than US national average (48.2%)

## 4. EDA
#### 4.1 Numerical Features
![numerical_features](/img/numerical_features.png)
* The pearson correlation chart above shows that there's no significant relationship between each other.
* t-test was performed to the features (age, average glucose level, and bmi) and the result was to reject the null hypothesis that the means are equal.

#### 4.2 Categorical Features
Here's the percent of stroke in each category
![percentofstroke](/img/percentofstroke_features.png)
##### Chi-Squared Test
Chi-squared test result:<br>
![result](/img/chi2test.png)<br>
These features below look like they are statistically significant that they are dependent variables of stroke.
* **work type:** (2.9%) of people whose work type is private had stroke.
* **smoking status:** (1.8%) of people who has never smoked had stroke
* **hypertension:** (3.6%) of people who has no hypertension had stroke
* **heart disease:** (4%) of people who has no heart disease had stroke
* **ever_married:** (4.3%) of married people had stroke

While the features below didn't pass the chi-squared test
* Gender
* Residence_type


## 5. Data Preprocessing
Data is split into training dataset and testing dataset:
* training dataset is treated using SMOTE to resolve for issues that can be caused by having an imbalanced dataset
* both datasets are standardized using standard scaler and encoded using binary encoding.

## 5. Model Building
All of the model mentioned in method above were from sklearn library.

## 6. Conclusion
All performed okay on the test data, most likely due to original dataset is imbalanced.

If we make a rough guess that half of the people will get stroke, we will get the following confusion matrix:
tp: 42
fp: 725
tn: 724
fn: 42

making the recall score for stroke 0.5, balanced accuracy score of 0.5.

Logistic Regrssion shows the strongest performance without any other optimization currently. It has recall score for stroke: 0.36; balanced accuracy score of 0.63.

Balanced accuracy score of logistic regression performs better than benchmark (50% guess model). but recall score for stroke is weaker than benchmark.<br>
![result](/img/modelresults.png)<br>

### Optimization suggestion.

1. Data acquisition: get more data, especially stroke patients
2. Optimize SMOTE for imbalanced data (oversample the stroke data) and undersample the non-stroke data. [SMOTE](https://machinelearningmastery.com/smote-oversampling-for-imbalanced-classification/)
3. Feature selection:
    * remove some features that didn’t pass the significance testing (Gender, Residence Type)
    * BMI change it to categorical
4. Hyperparameter tuning: Use Cross Validation, Grid Search, and Random Search to find better hyperparameters.

