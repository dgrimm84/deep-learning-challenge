# deep-learning-challenge
## Overview of Analysis
The goal of this Analysis is to use neural network models (tensorflow, keras) to genereate a predictive model that estimates the likelihood of certain charity fundings being successful.  The models we built with these libraries are designed to help identify factors in the dataset that contribute positively to funding approval.  These factors can then be used to improve selection and decisions for future charity candidates.

## Results of Analysis
### Preprocessing the Data
- Target Variable 
  - IS_SUCCESSFUL : This variable shows whether a charity funding was successful (1) or not successful (0)

    ![image](https://github.com/user-attachments/assets/b9fb9655-ffd1-4ca2-bab0-ee777b619035)

- Feature Varibles:
  - APPLICATION_TYPE : this variable shows the type of application categorized with identification codes (T1, T2, etc.).  Rare results with fewer than 600 results are grouped and re-categorized as "Other" to not skew the prediction results

    ![image](https://github.com/user-attachments/assets/1386fdee-1317-4442-aabd-c689494f1142)

  - CLASSIFICATION : this variable categorizes each of these applications into larger groups of these APPLICATION_TYPES into classes which are identified with ID codes as well (C1000, C2000, etc.).  Similarly, to reduce skewing of rare occrances, any variable with fewer than 2000 results is re-categorized as "Other"

    ![image](https://github.com/user-attachments/assets/ca18c98f-b31a-4ea9-86ad-8dbb9bd9a9b3)

  - AFFILIATION, INCOME_AMT, SPECIAL_CONSIDERATIONS : these are factored into the prediction as categories of strings to see if they would factory in to making a charity application more likely to be successful
 
    ![image](https://github.com/user-attachments/assets/de403e3a-afe8-4b2c-879e-9b671961931b)

  - ASK_AMT, STATUS : these numerical features are factored into the X of the test data

    ![image](https://github.com/user-attachments/assets/af103884-d124-4e2e-aef3-8e3a17038cd9)

  - EIN, NAME, USE_CASE, ORGANIZATION : these features are dropped from the dataset as they don't contribute to the prediction models

    ![image](https://github.com/user-attachments/assets/b861d321-d687-4e0c-aa16-42a3fa2fc90d)

  - When splitting the dataset to compile the model and test it, the features above are grouped into "Y" (IS_SUCCESSFUL), and "X" APPLICATION_TYPE, CLASSIFICATION, AFFILIATION, INCOME_AMT, SPECIAL_CONSIDERATIONS, ASK_AMT, STATUS
 
### Compiling, Training, and Evaluating the Model

  - In the first iteration, I used the below combination of settings when creating the neural network model:
    - Two hidden layers (80 neurons, 30 neurons)
    - 100 Epochs
    - 2 layer activation functions (reLU) and 1 output activation function (sigmoid)
    - Optimizer Type: Adam
       
      ![image](https://github.com/user-attachments/assets/2aeee181-a033-462e-82e0-0423b8b5ddee)

    - the results of this prediction model was a 72.78% accuracy.  3% short of the 75% goal

      ![image](https://github.com/user-attachments/assets/b2e38c18-31a5-40ec-b17c-7b6137f4c3c4)

  - In the second iteration, more optimization was attempted by adjusting the combination of model settings to the below:
    - Three hidden layers (128 neurons, a batch normalization, 64 neurons, 32 neurons)
    - 200 epochs
    - 3 layer activation functions (reLU) and 1 output activation function (sigmoid)
    - Optimizer Type: Adam

      ![image](https://github.com/user-attachments/assets/6fe251c0-3280-45a6-8786-9ec6ac3526d3)

    - the results of this prediction model was a 72.69% accuracy.  Still 3% short of the 75% goal, without much of an improvement over the first iteration

      ![image](https://github.com/user-attachments/assets/d87c5eea-17e1-45c3-95b3-045ce9662c6b)

  - In the third iteration, even further optimization was attempted by adjusting the combination of model settings to the below:
    - Four hidden layers (256 neurons, a batch normalization, 128 neurons, a batch normalization, 64 neurons, 32 neurons)
    - 200 Epochs
    - Four layer activation functions (reLU) and 1 output activation function (sigmoid)
    - Optimizer Type: RMSprop

      ![image](https://github.com/user-attachments/assets/944f852a-878c-4ac0-ab09-10fd71890166)

    - The results of this prediction model was 72.50%.  Still 3% short of the 75% goal and actually worse than the previous model

      ![image](https://github.com/user-attachments/assets/cd871ffd-8795-415a-b206-fcc72da3d23b)

  - In the fourth iteration, a final optimization was attempted by adjusting the combination of model settings to the below:
    - Four hidden layers (256 neurons, a batch normalization, 128 neurons, a batch normalization, 64 neurons, 32 neurons)
    - 50 Epochs
    - Four layer activation functions (leakyRELU) and 1 output activation function (sigmoid)
    - In the preprocessing of the data, more unncessary columns were dropped (EIN, NAME, USE_CASE, ORGANIZATION)
    - Also, the upper limit of "rare" results for APPLICATION_TYPE was increased to 600 to remove more outliers
    - Similarly, the upper limit of CLASSIFICATION results was raised to 2000 to remove more rare outliers
    - Optimizer Type: SGD

      ![image](https://github.com/user-attachments/assets/80a9d5d6-1c29-46c7-bce4-7eb0bd1f6bb7)

    - The results of this prediction model was 72.18%.  Yet still 3% short of the 75% goal

      ![image](https://github.com/user-attachments/assets/52fe8882-41ab-436f-b2f0-65c291ded180)

## Analysis Summary

Overall, this model was moderately successful at predicting if certain application types were likely to be successfully funded.  There is definitely more room for improvement as an accuracy percentage of over 75% would be ideal to be able to apply the model to future application types and trust the likelihood results.  Even when tweaking the preprocessing data (removing more unnecessary columns, grouping more rare occrances into the "Other" category to reduce skewing) as well as tweaking the model properties (adding more epochs, using three different optimizers like SGD, Adam, and RMSprop, adding more layers and neurons to the models), the model accuracy was not improved by even a full percentage point.  There aren't many other tweaks that can be made to this model in order to resolve this.  These 4 iterations resulting in almost identical accuracy percentages of under 75% suggest that this model is just not sufficient for this dataset. 

It can be assumed that other types of neural network models need to be implemented to improve this accuracy.  These models could be:
  - XGBoost : this is an algorithm that in some cases outperforms neural networks for certain datasets
  - Logistic Regression or SVM : these are simpler models that may behave better for this particular dataset
  - Random Forest Classifier - this model may be better suited to the structure of this dataset becasue of all the categorical features in this dataset
