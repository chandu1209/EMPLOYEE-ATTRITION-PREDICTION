# Principal Component Analysis - IBM Employee Attrition

## A. Goal
Principal Component Analysis (PCA) is used to reduce the number of features needed to be used in a prediction model. In this exercise, we will see the impact of PCA – in terms of accuracy and time needed to train – on models: Logistic Regression, Decision Tree, Naive Bayes, and SVM.

## B. Data Source
https://www.ibm.com/communities/analytics/watson-analytics-blog/hr-employee-attrition/

## C. Summary
_Dataset Description_

‘Attrition’ (binary) is the target variable, which we will try to predict. We have 34 input variables – overall including factors such as demographics, travel, education, income, field, and number of years at the current company and role, and with current manager. The features have only 2 datatypes: integers and factors; however, it is important to note that many numerical variables (such as ‘DistanceFromHome’) are ordinal.

_Data Cleaning_

1. We did not have any missing values within the dataset.

![](PCA%20Images/MissingValues.png)

2. We mapped the yes/no in the target variable – Attrition – to 1/0.

3. We dropped ‘EmployeeNumber’ as it does not have any impact.

4. Further, after looking at the distribution of the numerical variables, we observed that ‘EmployeeCount’ and ‘StandardHours’ are constants; hence, we dropped these columns as well.

_Exploratory Data Analysis_

1. We can observe that ‘Attrition = 1’ is just 1/6th of ‘Attrition=0’; only 16% of the entire dataset is ‘0’. Thus, this is an unbalanced dataset. However, as we are focusing majorly on understanding the impact of PCA, we will not focus on methods needed to deal with unbalanced data (we have already discussed in one of the other repositories (https://github.com/Nickssingh/SMOTE-Unbalanced-Data-Bank Marketing/blob/master/Bank%20Marketing-Call%20Response%20Prediction.Rmd) how SMOTE can be used to deal with imbalance in data).
![](PCA%20Images/Attrition.png)

2. It appears that among the employees who discontinued, frequent travel is comparatively a larger portion of the group.

![](PCA%20Images/Travel.png)

3. We can see that among the employees who discontinued, the higher end of Monthly Income is comparatively sparse, and we visualized this information much more effectively using Kernel Density Estimate (KDE) plots.
![](PCA%20Images/Monthly_Income_Distribution.png)
![](PCA%20Images/Monthly_Income_KDE.png)


4. The proportion of employees from sales department seems to be higher among those who discontinued.
![](PCA%20Images/Department.png)


5. We also found that income does not vary widely with gender.
6. Single employees have income lower than those of married and divorced ones – probably because single employees are in young and thus in the initial stages of their careers.

![](PCA%20Images/Gender_and%20Marital_Income.png)


7. Employees from different education fields seem to have similar income levels; Nonetheless, it can be noted that employees from Life Sciences and Medical background have more number of outliers.
8. Research Director and Manager have the highest income levels, and Research Scientist, Laboratory Technician, and Sales Representatives have lowest income levels.
![](PCA%20Images/Education_and_Job_Role_Income.png)


_Machine Learning Models with and without Principal Component Analysis_

As mentioned in the goal, we developed 5 models. We developed a set of these 5 models without PCA and the other set with PCA. Then, we compared the results in the two sets, using train time and accuracy.

- ROC Curves
![](PCA%20Images/LogisticRegression.png)

![](PCA%20Images/DecisionTree.png)

![](PCA%20Images/KNN.png)

![](PCA%20Images/NaiveBayes.png)

![](PCA%20Images/SVM.png)


- Accuracy
![](PCA%20Images/Accuracy.png)

- Train Time
![](PCA%20Images/Train%20Time.png)

As shown above, the impact of PCA on Logistic Regression, KNN, and SVM was in alignment without our expectations – decrease in train time with negligible to small compromise on accuracy; the expected change in accuracy was not huge because the features, after reducing the number of variables using PCA, were good enough to explain 95% of the variation. However, the impact on Naive Bayes and Decision Tree was interesting.


- Naive Bayes

Impact on Naive Bayes was positive: computation time declined and accuracy increased. The performance of Naive Bayes classifier can be improved using preprocessing techniques, of which PCA is one. Correlated features can have a negative impact on Naive Bayes. PCA improves both accuracy and computational efficiency of Naive Bayes, as PCA tries to find uncorrelated variables and (depending upon the variation that needs to be retained) reduces number of features.


- Decision Tree

Impact of PCA on decision tree was negative: both computation time and accuracy suffered. Though the number of nodes did not change by huge amount (Before PCA: 237 & After PCA: 227), the depth of the tree increased quite visibly (Before PCA:14 & After PCA:23).

![](PCA%20Images/Tree_NoPCA.png)


![](PCA%20Images/Tree_PCA.png)
