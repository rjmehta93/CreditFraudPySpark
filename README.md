# CreditFraudPySpark
Credit card fraud detection with PySpark


#########

# MOTIVATION
According to CreditDonkey.com, 46% of Americans have fallen victim to credit card fraud in the past five years, and it is estimated that losses from credit card fraud exceeded $24 billion in 2016. The number of fraudulent transactions is usually a very low fraction of the total transactions. Hence the task of detecting fraud transactions in an accurate and efficient manner is difficult and challengeable. Therefore, development of efficient methods which can distinguish rare fraud activities from billions of legitimate transactions is critical.  The data for the transactions by credit cards, is massive, sometimes in Petabytes. To store and analyze this data in a normal RDBMS is very difficult and inefficient way. By the time, a fraud is predicted, the transaction has already been processed. To deal with this issue, we explore how different statistical and machine learning models perform in terms of accuracy and scaling in the parallel distributed computing environment.

The motivation for doing an academic project on Credit Card Fraud Detection is because this use case is a befitting example of how Machine Learning can help us solve Big Data problems. With trillions of currency-less transactions being done every day, using machine learning to recognize patterns of transactions and detecting anomalies in them is a classic example of how technology can help us in day-to-day life.

# DATASET
The dataset contains transactions made by credit cards in September 2013 by European cardholders. This dataset presents transactions that occurred in two days, in which only 492 are fraud transactions out of 284,807 transactions.

The dataset is highly unbalanced, the positive class (frauds) account for 0.172% of all transactions. As it is an imbalanced classification problem, we would also like to understand how SMOTE techniques can be done in Spark RDD set up. This will basically over-sample the minority class and under-sample the majority class. With a more balanced dataset, we can get a better picture of false positives and false negatives of the analysis.

It contains only numerical input variables which are the result of a PCA transformation. Due to confidentiality issues, information about original features has not been provided. Features V1, V2, … V28 are the principal components obtained with PCA, the only features which have not been transformed with PCA are ‘Time’ and ‘Amount’. Feature ‘Time’ contains the seconds elapsed between each transaction and the first transaction in the dataset. The feature ‘Amount’ is the transaction Amount, this feature can be used for example-dependent cost-sensitive learning. Feature ‘Class’ is the response variable and it takes value 1 in case of fraud and 0 otherwise.1

ALGORITHMS USED
For classifying a transaction as fraudulent, we have implemented the following Machine learning models on Spark –

Decision Tree
Support Vector Machine
Gradient Boosting
Random Forest
Logistic Regression
To infer how the above models fare in the Big Data context, we scaled the data to try every model on 20%, 40%, 60%, 80% and 100% of the dataset.

Computational Time and the Area Under the ROC Curve are measured for different models and data proportions to understand the impact of the data size on model’s performance.


# PERFORMANCE OF ALGORITHMS
SPARK LOCAL MACHINE
Computational Time

We have explored the time taken by each model to train and predict the dependent variable – Class in this case. As mentioned above, this is done for 5 different scales of data – 0.20, 0.40, 0.60, 0.80 and 1.0(all data in this case)

# SPARK CLUSTER
To compare the performance of the Spark Local Machine and Cluster, we implement the following models on a cluster:

Decision Tree
Gradient Boosting
Random Forest
Logistic Regression
Support Vector Classification has not been done on the Cluster as the cluster did not support the Spark 2.3 version of SVC algorithm.

## Computational Time

On the Cluster, the time taken to train and predict the class values on test data is higher than that on local. This could be attributed to the difference in system configuration.

## Time Vs Scaling – Cluster

We find that the time to predict the fraud transactions increases almost linearly with scaling. The performance of Gradient Boost and Random Forest in terms of computational terms on scaling is better than Logistic Regression and Decision Tree. However, absolutely speaking Gradient Boost takes almost double the time as compared to other algorithms for the same scale factor.


### Model Behavior for Scaling

## AUC Vs Scaling – Cluster

In terms of performance of models in AUC metric, it is noticed that there is a consistent AUC score for all models except Decision Tree. Gradient Boost’s performance is consistent across scales and is the highest. Random Forest also has a good AUC with a benefit of having lesser computational time vis a vis Gradient Boost.

 

# CONCLUSION
The model has successfully classified fraudulent transactions with a good F1-Score. Models perform better on cluster vs the local if the data is big. As scale increases, the performance on cluster improves. It can be said that Random Forest is the recommended model based on above analysis. All the models are more robust on cluster than the Local machine.
With the above results, it is noted that models which have higher AUC metric take higher computational time. This is consistent with both local spark installation as well as distributed computing. Gradient Boosting outperforms other models in AUC but takes maximum time as well. In terms of AUC, it performs better in the distributed environment when compared
to single machine behavior. It is easy to note that Random Forest has the right balance of computational time and AUC – Its performance is robust across local machine and cluster. In terms of scaling, it can be inferred that as compared to Logistic Regression and Decision Tree, Random Forest and Gradient Boosting do an excellent job of scaling.
Thus, we concluded that the models perform better on cluster vs the local if the data is big. As scale increases, the performance on cluster improves. It can be said that Random Forest is the recommended model based on above analysis. All the models are more robust on cluster than the Local machine.
