# Part 3 - Advanced Modeling, Ensemble Methods and Pipeline
# Project Description
In this part i build advanced machine learning models using the cleaned dataset from part 1 and the processed features from part2. 
The main aim is not only getting good accuracy but also finding which model is more stable and reliable.
I compare different models, perform hyperparameter tuning, create a complete sklearn pipeline and save best model for later use.

# Dataset
I continue using the **Ames Housing Dataset**.
I did not change the dataset because all preprocessing and feature engineering were already completed in the previous parts.
Using the same dataset helps keep every experiment fair and consistent.
The dataset contains enough records and many features, so it is suitable for comparing different machine learning models.

# These are the Steps:
**1.Decision Tree Baseline:**
  First i trained a Decision Tree classifier.
  I used it as a baseline model because it issimple and easy to understand.
  After training i evaluated the model using - Accuracy
                                             - Precision
                                             - Recall
                                             - F1-score
                                             - ROC-AUC
  This model helped me compare the performance of more advanced ensemble models.
**2.Random Forest:**
  After the Decision Tree, I trained a Random Forest classifier.
  Random Forest combines many Decision Trees instead of using only one tree.
  This usuallly gives - Better accuracy
                      - Less overfitting
                      - More stable predictions
  I evaluate it using the same performance metrics.
**3.Bagging Classifier:**
  Next i trained a Bagging Classifier.
  Bagging creates multiple models using different random samples of the training data.
  The final prediction comes from combining all individual models.
**  This helps reduce variance and improve prediction stability
4.Hyperparameter Tuning:**
  After training the models, i performed hyperparameter tuning using **GridSearchCV**
  Different parameter combinations were tested automatically.
  The best parameter combination was selected based on crosss-validation performance.
  This helped improve the model without manually testing many values.
**5.Cross Validation:**
  I used cross-validation to evaluate the model on multiple splits of the training data.
  Instead of checking performanace on only one train-test split, cross-validation gives a more reliable estimate of model performance.
  This makes the comparison between models more trustworthy.
**6.Model Comparison:**
  After training all models, i compared their performance.
  I compared - Accuracy
             - Precision
             - Recall
             - F1-score
             - ROC-AUC     based on these results, i selected the best-performing model.
**7.Machine Learning Pipeline:**
  After selecting the best model, i created a complete Scikit-learn Pipeline.
  The pipeline combines preprocessing and model prediction into one workflow.
  Using a pipeline makes the project  - Easier to reuse
                                      - Easier to deploy
                                      - reduces preprocessing mistakes
                                      - keeps every prediction consistent
**8.Saving the Best Model:**
  The final trained model was saved using joblib.
  Saved file as : **"best_model.pkl"**
  Saving the model means i do not need to train it again every time.
  The saved model can be loaded directly for prediction.
**9.Reloading the model:**
  After saving, i loaded the model again using Joblib.
  I tested predictions using the loaded model.
  The loaded model produced the same predicitions as the original trained model.
  This confirms the model was saved correctly.
  
**Why I Selected the Final Model**
I selected the final model because it performed better than the other models on the evaluation metrics.
It also showed more stable performance during cross-validation.
The model generalized well on unseen data and had lower risk of overfitting compared to a single Decision Tree.
  
**Files in this Folder**
  part3.ipynb
  best_model.pkl
  README.md

**Libraries Used**
  - Pandas
  - Numpy
  - Scikit-learn
  - Joblib
  - Matplotlib
  - Seaborn

**What I learned**
From this part i learned
  - How Decision Tree works
  - How Random Forest improves performance
  - How Bagging reduces variance
  - How GridSearchCV finds better parameters
  - How Cross Validation gives better model evaluation
  - How to create a Scikit-learn pipeline
  - How to save and reload a trained machine learning model

**Conclusion**
In this part i trained multiple machine learning models and compared their performance.
After hyperparameter tuning and cross-validation, i selected the best model and saved it using joblib.
Finally i created a reusable machine learning pipeline,making the project easier to use in the next part where the model is integrated with an LLM.
