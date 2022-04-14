# CARDIO CATCH DISEASES COMPANY - HEALTHCARE AND ARTIFICIAL INTELLIGENCE

![](img/cardio.png)

# 1.0. CONTEXT

Cadio Catch Diseases is a company that specializes in detecting heart disease in the early stages.The company offers an early diagnosis of cardiovascular disease for a certain price. Currently, the diagosis is made manually. The currently accuracy used to be between 55% and 60%, because of the complex diagnostics and the team's tiredness, there's a another employees on other shifts.

This is a project was developed within the DS community created by Meigarom Lopes (https://www.comunidadedatascience.com/)

# 2.0. BUSINESS PROBLEM

There are some points that is important to know:

- Each diagnosis costs about $1000,00

- The price will vary according to the precision, the customer pays $500.00 for every 5% accuracy above 50%.

- If the diagnostic precision is 50% or below, the customer doesn't pay for it.

What is the objective?
- Build a predictive model to classify cardiovascular diseases.

Why is this necessary?
- Because the price will vary according the precision.

What do we need to show?
- The accuracy and precision of the model.
- How much profit will Cardio Catch Diseases have after the project?
- How reliable is our result?

# 3.0. DATA DESCRIPTION 

## 3.1. Data Dimensions

> **print(f'Number of rows: {df.shape[0]} ')**

> Number of rows: 70000

> **print(f'Number of columns: {df.shape[1]} ')**

> Number of Columns: 13


## 3.2. Data Types

![](img/data_types.PNG)

As we can see above, we have 2 data types: int64 and float64. It's important to explain that machine learning algorithms usually build a better learning with numerical data, this is one of the premises that we will assume.

## 3.3. Change Types

The "id" column is a "int64" but, we won't execute any mathmatical operation because it is just a indentifying column. Therefore, we could change it to a categorical data or maybe to drop it, but let's to change the type to "object". Another point that we need to note is that our "age" column has an "days" format, so let's switch to the "age" format.

#Converting the age to year format

> df1 ['age_year'] = df1['age'].apply(lambda x: x/365)

#age year convert

> df1 ['age_year'] = df1['age_year'].astype(int)

#Changing id type

> df1 ['id'] = df1['id'].astype(int)

![](img/change_types.png)

## 3.4. Statistical Descriptive

### 3.4.1. Numerical Attributes

 
|  | Attributes    | min     |  max   | range  | mean          | median | std         | skew     | kurtosis |
|--| ------------- | ------- | ------ |------  |--------       |-----   |-----        |--------  |--------  |
| 0| Age           | 10798.0 | 23713  | 12915  |  19468.875    | 19703  |   2467.2340 |  -0.3070 |  -0.8234 |
| 1| Gender        | 1       | 2      | 1      |  1.34         | 1      |   0.470     |   0.630  |  -1.60   |
| 2| Height        | 55      | 250    | 195    |  164.359      | 165    |   8.21      |  -0.630  |  7.943   |
| 3| Weight        | 10      | 200    | 190    |  74.205       | 72     |   14.395    |  1.01    |  2.586   |
| 4| AP_HI         | -150    | 16020  | 16170  |  128.81       | 120    |   154.01    |  85.296  |  7580.074| 
| 5| AP_LO         | -70     | 11000  | 11070  |  96.630       | 80     |   188.471   |  32.114  |  1425.914|
| 6| Age_year      | 29      | 64     | 35     |  52.840       | 53     |   6.766     |  -0.305  |  -0.8189 |
     


From this table, we can get some informations:

- There aren't children included in the dataset
- The minimum value for the "height" column is 55, but the minimum value for the age_year column is 29. As we said, we don't have children included in the data set
- "ap_hi" and "ap_lo have a high skew, this probably means that we have a non-symmetric graph shifted to the right.
- If we remember that a person who has systolic blood pressure of 180mmHg must urgently go to the doctor and with a diastolic pressure greater than 120mmHg. However, we have as maximum values in the columns "ap_hi" and "ap_lo" the values 16020.0 and 11000.0 respectively. This is a strange value that needs to be analyzed soon, but it could indicates that it is an outlier.
- There are also negative values for the columns "ap_hi" and "ap_lo", this represents an inconsistent value.

### 3.4.1. Binary and Ordinal Attributes

![](img/binary_ord.PNG)

From these plots we can get some informations:

- There is much more data from people with normal glucose levels.

- Our target variable has balanced data, which is very good, it will avoid a lot of work.

- The number of people who do physical activities is considerably greater than those who don't.

# 4.0. MINDMAP HYPOTHESIS

![](img/MindMapHypothesis.png)

From the mind map above, we created some features to validate the hypotheses.

# 5.0. EXPLORATORY DATA ANALYSIS 

## 5.1. Univariate Analysis

### 5.1.1. Response Variable

![](img/univariate_analysis.PNG)

- As we can see, we have our classes balanced.

### 5.1.2. Numerical Varibles

![](img/num_attributes.PNG)

From the graphs above, we can get some conclusions:

- gender
  - Our class that has the gender "1" has almost twice the gender class "2".
- height
  - It has a distribution similar to a normal one.
- weight
  - It has a distribution similar to a normal one.
- bmi
  - It has a distribution similar to a normal one.
  
### 5.1.3. Categorical Attributes

![](img/cat_attributes.PNG)

From these plots, we've got some informations:

- The number of people with normal weight and overweight are very close. The number of obese people is half the number of people with normal weight.
- There are twice as many people between 50-65 than 0-50.
- There are almost twice as many people of gender 1 compared to 2.
- The number of hypertensive people is half that of normal people.

## 5.2. Bivariate Analysis 

### 5.2.1. Hypothesis

**H1. There are more cases of cardiovascular diseases in older people.**
True -  It is true until the age of 59, after that, there is a drop in the number of people with cardiovascular diseases.

![](img/h1.PNG)

From these plots, we can get some informations:

- There is a growing trend between age and the number of people with cardiovascular disease.
- After 59 years, we can see a drop in the number of people with cardiovascular disease.
- The "age" variable has a low correlation with our target variable.

**H3. There are more cases of cardiovascular disease in people with high diastolic and systolic pressure.**
True Although the number of people with hypertension is higher, there are more cases of people with normal blood pressure than with high blood pressure.

![](img/h2.PNG)

![](img/h22.PNG)

What can we get about the plots above?

- There are many people with hypertension and cardiovascular disease. However, there are also a lot of people without hypertension and with cardiovascular disease.
- In scatterplots, we can see some points with a very high number of cases of cardiovascular diseases. For example, there are almost 10,000 people with 120mmHg of systolic blood pressure with CVD.
- In both types of blood pressure, we have a positive correlation with our target variable. Systolic blood pressure has a moderate correlation and diastolic blood, a weak correlation.

**H6. There are more cases of cardiovascular disease in people who are overweight.**
True However, the number of cases in obese people is less than the number of cases of people with normal weight. The number of extremely obese people with cardiovascular disease is almost half the number of people with a normal person.

![](img/h3.PNG)

- The number of cases in obese people is less than the number of cases of people with normal weight.
- The number of extremely obese people with cardiovascular disease is almost half the number of people with a normal person.
- There's a low positive correlation between bmi and cardio.

## 5.3. Multivariate Analysis

![](img/multi_analysis.PNG)

# 6.0. DATA PREPARATION

![](img/data_prep.PNG)

- RobustScaler
  - ap_lo
  - ap_hi
  - bmi
  - Weight
  
- MinMaxScaler
  - age_year
  - height
  
 # 7.0. MACHINE LEARNING MODELLING
 
 ## 7.1. Single Performance
 
 ![](img/machine_leraning1.PNG)
 
 We obtained the following results, however, in order for our model to be reliable, we applied the cross-validation technique.
 
 ## 7.2. Real Performance - Cross-Validation
 
|                  | Model                    | Accuracy      |  Standard Deviation 
|  -------------   | -------------            | ------------- | --------        
| 0                | Logistc regression       | 0.748         | 0.003           
| 0                | Support Vector Machine   | 0.750         | 0.003           
| 0                | Xboost Classifier        | 0.757         | 0.005           
| 0                | K Nearest Neighbor       | 0.730         | 0.005           
| 0                | LGBM Classifier          | 0.759         | 0.003           
| 0                | Random Forest Classifier | 0.741         | 0.004           

  
 ## 7.3. ROC Curve
 
 ![](img/roc_curve.PNG)
 
 ## 7.4. Hyperparameter Fine Tunning
 
 In machine learning, hyperparameter optimization or tuning is the problem of choosing a set of optimal hyperparameters for a learning algorithm. A hyperparameter is a parameter whose value is used to control the learning process. By contrast, the values of other parameters (typically node weights) are learned.

Therefore, we will use the RandomSearchCV algorithm beacuse, the method described herein is a type of local random search, where every iteration is dependent on the prior iteration's candidate solution. So, we will spend less time to obtain the result.

In our best algorithm, we apply the technique to find the best parameters. Below, we can see its performance with the chosen parameters.


| Model             | Best Score    |  Accuracy  |Kappa Score     | Recall | F1-Score | ROC AUC | Precision Score
| -------------     | ------------- | --------   | -------        |------- | -------  | ------- | -------
| LGBM Classifier   | 0.761         | 0.758      | 0.515          | 0.751  | 0.755    | 0.825   |0.762


|                  |Confidente Interval  | Worst Scenario|  Best Scenario 
|  -------------   | -------------       | ------------- | --------        
| 0                | 0.00769             | 0.2461        | 0.231           


|                  |Model   | Worst Scenario|  Best Scenario | Gain
|  -------------   | -------------       | ------------- | --------        | --------
| 0                | LGBM Classifier             | $ 35,000,000.00        | 175,000,000.00 - 140,000,000.00| 500%


![](img/machine_learning4.PNG)

# 8.0. BUSINESS PERFORMANCE


Let's remember what is our business problem:

- Each diagnosis costs about $1000,00
- The price will vary according to the precision, the customer pays $500.00 for every 5% precision above 50%.
- If the diagnostic precision is 50% or below, the customer doesn't pay for it.

What did we get?

- Precision = 76.04%
- 5% above 50% = $500,00
- 25% above 50% = $2500,00

With a data set of 70000 people and each exam costing approximately \$ 2500.00, our financial return will be, in the worst case, \$ 35,000,000.00 and in the best case, \$ 175,000,000.00

