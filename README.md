# deep-learning-challenge
## Overview of Analysis
The goal of this Analysis is to use neural network models (tensorflow, keras) to genereate a predictive model that estimates the likelihood of certain charity fundings being successful.  The models we built with these libraries are designed to help identify factors in the dataset that contribute positively to funding approval.  These factors can then be used to improve selection and decisions for future charity candidates.

## Results of Analysis
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

  - ASK_AMT, STATUS : these numerical categories 
