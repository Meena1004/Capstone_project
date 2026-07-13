# Part 2 – Supervised Machine Learning Model
# Project Overview
This is Part 2 of my Applied AI & ML Essentials Capstone Project.
After cleaning the dataset in Part 1, I used the cleaned dataset to build Machine Learning models.
In this part I created one Regression model one Classification model. 
I trained different algorithms, compared their performance and evaluated the results using different evaluation metrics.
The cleaned dataset from Part 1 is used as the input for this part.

# Dataset Used 
Dataset: **cleaned_data.csv**
This dataset was created on Part 1 after completing all data cleaning and preprocessing steps.
The dataset contains no missing values.
I selected Sales Price as the regression target because it is a continuous numerical value.
If SalePrice > Median - Class 1
If SalePrice <= Median - Class 0
This created an almost balanced dataset.
Class 0 = 1467
Class 1 = 1463
Since both classes are almost equal, I did not use SMOTE or class balancing methods.

# Data Preprocessing 
Before training the models I performed the following preprocessing steps.
  -	Loaded cleaned_data.csv.
  -	Selected SalePrice as the regression target.
  -	Created a binary classification target from SalePrice.
  -	Selected all remaining columns as input features.
  -	Converted categorical columns using One-Hot Encoding.
I used One-Hot Encoding because the categorical columns have no natural order.
If Label Encoding was used, the model may think one category is greater than another even when they are not related.
I used drop_frist = True to avoid multicollinearity by removing one dummy variable from each category.
  -	Split the dataset into 80% training data and 20% testing data.
  -	Applied StandardScaler for feature scaling.
The scaler was fitted only on the training data and then used to transform both training and testing data.
If the scaler was fitted on the whole dataset before splitting, it would cause data leakage because the testing data information would already be available during training.

# Regression Models
# Linear Regression 
Linear Regression was used as the baseline regression model.
**Results**
**Mean Squared Error (MSE)** : 850,429,170.20
**R^2Score** : 0.8939
The model explains nearly 89% of the variation in house prices.

# Ridge Regression 
I also trained Ridge Regression with alpha – 0.1.
**Results**
**Mean Squared Error (MSE)** : 843,062,500
**R^2Score** : 0.8948
Ridge Regression performed slightly better than Linear Regression.
Ridge Regression adds L2 Regularization which reduces overfitting and handles multicollinearity better.
The alpha parameter controls the strength of regularization.
A higher alpha means stronger regularization while a smaller alpha behaves more like normal Linear Regression.

# Important Features 
After training the Linear Regression model I checked the coefficients.
Top 3 important features were
-	BsmtFin SF 1
-	Bsmt Unf SF
-	Total Bsmt SF
A positive coefficient means increasing the feature increase the predicted SalePrice.
A negative coefficient means increasing that feature decrease the predicted SalePrice.
These basement related features had the strongest influence on predicting house prices.

# Classification Model 
For the classofocation task I trained a Logestic Regression model.
The dataset was already balanced. 
**Class 0 = 1467
Class 1 = 1463**
Since no class had less than 35% od the data, I did not apply SMOTE or class_weight.
The default Logistic Regression model worked well on this dataset.

# Model Evaluation
The Logistic Regression model produced the following results.
**-	Accuracy = 93%
-	Precision = 0.93
-	Recall = 0.93
-	F1 Score = 0.93
-	ROC-AUC = 0.9788**
The confusion matrix also showed only a small number of incorrect predictions.
The ROC curve was plotted and saved as roc_curve.png.
The high ROC-AUC value shows that the model can seprate both classes very well.

# Precision and Recall
Precision Formula : **Precision = TP / (TP + FP)**
Recall Formula : **Recall = TP / (TP + FN) **
For this project both precision and recall are important because predicting house prices incorrectly in either direction can reduce model realiability.

# Decision Threshold Comparision
I treated different probability thresholds.
Thresholds tested
  0.30
  0.40
  0.50
  0.60
  0.70
The highest F1 Score was obtained at approximately 0.40.
When the threshold increases,
-	Precision increases.
-	Recall decreases.
When the threshold decreases,
-	Recall increases.
-	False Positive prediction also increase.
The default threshold of 0.50 also produced very good performance.

# Logistic Regression Regularization
I trained another Logistic Regression model using 
C = 0.01
The C parameter controls the amount of regularization.
Smaller C means stronger regularization.
Results
C = 1.0
Precisoon = 0.9311
AUC = 0.9788
C = 0.01
Precisopn = 0.9630
Recall = 0.9493
The model with C = 0.01 produced slightly higher Precision nut lowe ROC-AUC.
Overall, the default model (C =1.0) gave better overall classification performance.

# Bootstrap Confidence Interval
To compare both Logistic Regression models, I performed Bootstrap Sampling.
I generated 500 bootstrap samples from the testing data.
For every sample I calculated the difference between the AUC values of both models.
**Results**
**Mean AUC Difference**  -0.0111
95% Confidence Interval
**Lower BOUND ** -0.0181
**Upper Bound** -0.0055
The confidence interval does not include zero.
This means the difference between the two models is consistent across different bootstrap samples.

# Conclusion
In this part I successfully built Regression and Classification models using yhe cleaned Ames Housinh dataset.
Linear Regression and Ridge Regression produced good regression performance.
Logistic Regression achieved about 93% accuracy and an AUC of 0.9788, showing very good classification performance.
The trained  model and processed data will be used in Part 3 for Ensemble Learning, Hyperparameter Tuning and Mchine Learning Pipeline.
