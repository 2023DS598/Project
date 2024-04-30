# DS598 Final Project
This study aims to develop predictive models for mortality rates among critical care patients using neural networks, utilizing large-scale healthcare data from the United States. Additionally, we conduct a comparative analysis with classical machine learning techniques. While acknowledging the limitations of generalizing findings to other healthcare systems, we emphasize the significance of accurately predicting mortality rates for informed resource allocation and quality assessment in intensive care settings.

This repository contains the datasets used in the analysis, the Python code, slides summarizing the project, and the final report. Additionally, the references used for the project are stored in the "reference" folder.


1. Introduction

(Personal Motivation) Deep learning is widely applied in medical contexts, such as image diagnosis and intraoperative image recognition. However, there is currently limited evidence of deep learning analysis being utilized for national healthcare policy in Japan. By conducting a comparative analysis between deep learning and traditional machine learning methods, I seek to understand their respective strengths and weaknesses. My goal is to contribute to the advancement of data science in healthcare in Japan.

(Study Background) Predicting mortality rates for critically ill patients in intensive care units (ICUs) is crucial for various purposes, including the allocation of limited medical staff and equipment, assessment of treatment facility quality, and appropriate severity classification for clinical research. This study aims to develop a mortality prediction model for ICU admissions using both traditional machine learning methods and deep learning techniques.

2. Data and Methods

The dataset encompassed various domains, including patient demographics (age, gender, race, etc.), hospitalization details (ICU type, elective surgery, etc.), medical condition (Apache scores, blood pressure, etc.), and comorbidity information (diabetes, immunodeficiency, etc.). The dataset was partitioned into training data (70%) and test data (30%). From the initial 85 columns, 29 variables were selected as inputs based on exploratory data analysis and medical knowledge. Missing values of continuous/integer variables were imputed using mean values, while rows with missing values for categorical variables were excluded from the analysis. Due to the imbalance in binary outcomes, the models were evaluated using Receiver Operating Characteristic Area Under the Curve (ROC AUC) and Matthews Correlation Coefficient (MCC) instead of Accuracy. Three neural network models were fitted with varying numbers of hidden layers (1, 2, or 5). The optimizer used was Adam, and the loss function employed was Binary Cross-Entropy Loss. Certain hyperparameters were kept constant across all models, including the weight ratio of 12 (death) to 1 (survival). It is noted that hyperparameter tuning was not conducted for the learning rate and weight decay, given the use of the Adam optimizer. Hyperparameter tuning, performed using 5-fold cross-validation, focused on optimizing the dimensions of each hidden layer, dropout proportion, batch size, and number of epochs to enhance model performance.

3. Result

There was a bias toward binary variables, with 8.6% of deaths in the hospital in the total data. It was also suggested that mortality was lower after elective surgery, while mortality was higher in patients who were intubate, had liver failure, immunodeficiency, or metastatic solid tumors.
The classical methods used were Logistic Regression, Random Forests, Gradient Boosting, GAM (Generalized Additive Model), Support Vector Machine, and Neural Networks, the performance of models with one, two, and five hidden layers were examined. The results showed that GAM had the highest ROC AUC of 0.856 and Shallow Network had the highest MCC of 0.341.

4. Discussion

Among neural networks, models with shallower hidden layers demonstrated superior performance. While deep learning is increasingly utilized in medical applications, especially in diagnostic imaging, its superiority over classical machine learning models may not always be evident in simpler analyses like mortality prediction. However, the hyperparameters in this study were not exhaustively analyzed due to time and computational constraints. Better performance with deep learning may be achievable through more sophisticated tuning.
From a technical perspective, our initial attempt to fit a model using the Apache score included in the data did not yield good model fit. However, when a model was created that included some components of the Apache score, such as vital signs, as variables instead of using Apache score itself, the model performance improved. This enhancement is attributed to the increased flexibility of the model with the addition of more variables.
Furthermore, in terms of optimization, we compared SGD (Stochastic Gradient Descent) and Adam. As reported in various studies, Adam required less time for model convergence and exhibited better overall model performance compared to SGD.
Although the model's performance in this study was evaluated as good based on AUC, it did not perform well according to MCC. This discrepancy may be attributed to the unbalanced data.
