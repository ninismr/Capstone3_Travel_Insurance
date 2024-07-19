# Travel Insurance Analysis and Prediction
Capstone Project Module 3 - DTIDS Purwadhika (Mulya Fajar Ningsih Alwi)

## **Business Problem Understanding**
Travel insurance provides essential protection for travelers against unforeseen events such as medical emergencies, trip cancellations, and lost luggage. Companies like Allianz, Lippo, Zurich, Simasnet, and MNC offer these products, ensuring travelers are covered financially in case of unexpected incidents during their trips. Policyholders pay a premium based on the coverage, duration, and destination of their trip. Typically, the premium is a one-time payment that covers the entire trip duration as specified in the policy. In the event of a claim, policyholders can request reimbursement for covered expenses, up to the limits outlined in their policy.

The benefits of travel insurance include peace of mind, financial protection, and access to emergency assistance services. It ensures that travelers are not left stranded or financially burdened in the face of unexpected events. The coverage can include a wide range of incidents, from medical emergencies to trip interruptions, providing comprehensive support to the policyholder.

The profitability of travel insurance companies hinges on the balance between collected premiums and paid-out claims. Companies make a profit when the total premiums collected exceed the claims paid out and the administrative costs. Conversely, they incur losses when claim payouts and operational costs surpass the collected premiums. Effective risk management and accurate claim predictions are crucial for maintaining profitability.

## Business Problem Statement
A travel insurance company is facing significant financial risk due to its inability to accurately predict which policyholders will file claims. Despite the majority of policyholders (98.29 %) not filing claims, the small percentage that does (1.71 %) results in substantial financial losses.
 
Based on [Average Costs and Benefits of Travel Insurance 2024](https://www.valuechampion.sg/travel-insurance/average-costs-and-benefits-travel-insurance-singapore#avecostTISG):
- **Average policy cost** paid by a policyholder for Annual Basic Plan Global Travel Insurance = **$524** per policy.
- **Average cost of insurance benefit** coverage for a Basic Plan = **$147,542** per policy.

Based on the dataset provided, the claim status proportion is:
- **Not Claim** (0) = **38,499** data points (98.29 %)
- **Claim** (1) = **668** data points (1.71 %)

Based on the above information, there is a potential for financial losses as calculated below:
- Revenue from premiums paid (policy cost) by policyholders who do not claim = 38,499 x $524 = $20,173,476
- Revenue from premiums paid (policy cost) by policyholders who claim = 668 x $524 = $362,056
- **Total revenue** from premiums paid (policy cost) by policyholders = $20,173,476 + $362,056 = **$20,535,532**
<br><br>
- Costs incurred for claims benefit = 668 x $147,542 = $98,558,056
- **Total potential financial loss** = $20,535,532 - $98,558,056 = **- $78,022,524**

The potential financial loss calculation highlights that even a few claims can lead to substantial losses for the company. Therefore, the company needs to better understand and predict which policyholders are likely to file claims to optimize resource allocation and minimize financial losses, ensuring sufficient funds are available to cover claims without unnecessary financial burden.

 ## **Goals**
 The goal is to develop a reliable predictive model that accurately identifies which policyholders are likely to file claims. This will enable the company to allocate funds more efficiently, minimizing financial losses from unpredicted claims while maintaining sufficient resources to cover potential claims.

 ## **Analytical Approach (Models and Evaluation Metrics)**
 Data analysis aims to identify patterns between policyholders who file claims and those who do not, as well as gain insights into what might lead policyholders to file claims. Then, we will develop a model to help the company predict the likelihood of a prospective policyholders filing a claim. Therefore, the model we will develop is a classification model. Modeling will be done using several classification algorithms such as Logistic Regression, K-Nearest Neighbors, and tree-based models like Decision Tree, Random Forest, AdaBoost, GradientBoost, and XGBoost.

To address the significant data imbalance, we will use various resampling methods, both oversampling and undersampling, such as RandomOverSampler, SMOTE (Synthetic Minority Over-sampling Technique), RandomUnderSampler, and NearMiss.

Here are the potential outcomes when the model classifies prospective policyholders' claim status:

<img src="https://images.datacamp.com/image/upload/v1701364260/image_5baaeac4c0.png" width="550" style="padding: 25px;">

- **True Positive (TP)**: The number of policyholders who correctly file claims.

- **True Negative (TN)**: The number of policyholders who correctly do not file claims.

- **Error type 1 - False Positive (FP)**: The number of policyholders incorrectly predicted to file claims but do not actually file claims.

  **Consequence**: Insurance funds may remain idle, affecting resource allocation and potential investment opportunities.
  
- **Error type 2 - False Negative (FN)**: The number of policyholders incorrectly predicted not to file claims but actually do file claims.

  **Consequence**: This error can lead to significant financial losses by reducing expected revenue from insurance premiums and using those funds unexpectedly to cover unpredicted claims. Such scenarios can result in negative cash flow, possibly necessitating the travel insurance company to seek loans from banks to cover unpredicted claims. Moreover, it can impact the company's trust and reputation.
 
Given the consequences of each error type, the model's primary focus will be to minimize Error type 2 (False Negative). This is because errors in predicting prospective policyholders who will file claims (FN) can lead to more serious financial losses than errors in predicting claims that do not actually occur (FP). Type 2 errors can potentially lead to significant financial losses by reducing expected revenue from insurance premiums and instead using it to pay for unpredicted claims, which can result in negative cash flow. Additionally, it affects the company's trust and reputation in the long term.

By prioritizing the minimization of False Negatives, the primary evaluation metric to be used is **Recall**. Recall is a metric that shows how well the model can identify all prospective policyholders who will actually file claims. Recall directly relates to the number of False Negatives. The higher the Recall, the lower the number of False Negatives, meaning the model is better at identifying all actual claim cases. 

Besides Recall, we will also consider the F2 Score (which gives more weight to Recall) and the Precision-Recall Area Under Curve (PR AUC) to ensure the model has reliable performance in identifying prospective claim-filing policyholders.

To determine the best resampling method and the most effective evaluation metrics, we will try all mentioned resampling methods and metrics and perform cross-validation to assess which resampling method and metric are the best based on the average value of their scenarios and their stability as seen from their mean and standard deviation of cross-validation. The models mentioned will also be selected based on this evaluation, and the best-performing model after benchmarking will proceed to the hyperparameter tuning stage to improve prediction recall accuracy and model performance in predicting prospective policyholders likely to file claims.

## **Model Limitation**
In developing the predictive model for travel insurance claims, we aimed to accurately identify policyholders likely to file claims. While the model, based on the XGBoost algorithm, successfully minimized false negatives, it exhibited a higher rate of false positives. This outcome highlights several limitations inherent in the current model and dataset, which are crucial to address for improving overall performance and reliability. Below, is the model limitations and suggest areas for further enhancement.

1. The model has issues with a high rate of false positives despite minimizing false negatives, suggesting that the dataset might have quality issues or imbalances. This affects the model's ability to generalize well.

2. To improve model reliability, additional data, especially from policyholders who have filed claims, is necessary. A more balanced dataset will help the model learn more effectively and reduce the incidence of both false positives and false negatives.

3. The current set of features may be insufficient to capture all the factors influencing claim status. The model's performance could be enhanced by adding more relevant features that better describe the policyholders' likelihood of filing claims.

4. The model is only valid for predictions within specific ranges of the input features:
    - Age: 0 to 88 years old
    - Net Sales: -357.5 to 682.0 dollars
    - Duration: 0 to 540 days
    - Commission: 0.0 to 262.76 dollars

    If the data points fall outside these ranges, the model's predictions may not be accurate.

5. The final model might not perform optimally yet. It would be helpful to reevaluate the model using different classification algorithms and a broader range of hyperparameters on this dataset. If the results still do not improve, enhancing the dataset with additional features related to claim status could be beneficial. Essentially, the model's performance depends on the quality of the data it uses, regardless of how advanced the model is.

These limitations emphasize the need for continued refinement and improvement of both the model and the data it relies on to achieve better predictive performance.

## **Conclusion**
**A. Final Model Performance**

The XGBoost Classifier, optimized through hyperparameter tuning, has demonstrated strong performance in identifying policyholders likely to file claims. The model achieves high recall, effectively identifying most actual claims. However, this focus on minimizing false negatives comes at the cost of a higher rate of false positives.
<br><br>

**B. Model Limitations**

1. **Imbalanced Dataset**: The high rate of false positives is influenced by the imbalanced nature of the dataset. With only 1.71% of policyholders filing claims, the model tends to predict claims more frequently, increasing the rate of false positives.

2. **Feature Limitations**: The current features and limited dataset may affect the model's accuracy. Enhancing the dataset with more relevant features and additional data could improve performance and reduce false positives.
<br><br>

**C. Problem Statement and Solution**

The travel insurance company faces significant financial risk due to the challenge of accurately predicting which policyholders will file claims. Given that only 1.71% of policyholders file claims but these claims result in substantial financial losses, there is a critical need for a reliable predictive model to manage these risks effectively.

**Predictive Model Impact**

**1. Without the Model**:
- **Potential Financial Loss**: $19,700,412

**2. With the Model**:
- **Financial Savings from True Positives (TP)**:
  - Premium revenue from TP: $66,024
  - Claim costs for TP: $18,590,292
  - **Net Savings**: $18,524,268

- **Financial Loss from False Negatives (FN)**:
  - Premium revenue from FN: $4,192
  - Claim costs for FN: $1,180,336
  - **Net Loss**: $1,176,144

- **Total Financial Savings: $18,524,268 (approximately 94% of the potential financial loss is saved)**

The predictive model significantly mitigates financial losses by accurately identifying policyholders likely to file claims. This allows the company to avoid substantial payouts for claims by focusing resources on high-risk policyholders, saving approximately 94% of potential losses compared to not using the model.

**Note: for a detailed analysis of the financial impact of the predictive model, please refer to the Cost Evaluation section.**
<br><br>

**D. Summary**

The model effectively addresses the problem of predicting claimants, resulting in substantial financial savings and improved risk management. However, to enhance its accuracy and reduce false positives, further refinement is needed, particularly by addressing the dataset imbalance and incorporating more comprehensive features.

## **Recommendation**
> ### **Recommendation For Predictive Model**

1. **Address Imbalanced Data:**
   - **Challenge:** The current model struggles with high false positive rates due to the imbalanced nature of the dataset, where only a small percentage of policyholders file claims.
   - **Recommendation:** Incorporate additional relevant features to improve model performance and balance. Features such as policy cost, trip history, claim history, and etc. can provide more context and improve the model’s ability to distinguish between claimants and non-claimants.
   <br><br>

2. **Enhance Feature Set:**
   - **Challenge:** The existing feature set may not capture all relevant factors influencing claim likelihood.
   - **Recommendation:** Add and evaluate new features:
     - **Policy Cost:** Understand the financial commitment of policyholders.
     - **Trip History:** Capture patterns in travel behavior that might correlate with higher risk.
     - **Claim History:** Include past claim information to identify patterns in claim behavior.
     - **Demographic Details:** More detailed demographic data, such as marital status or employment type, can offer additional insights into claim likelihood.
     - **Seasonality:** Incorporate time-of-year data to see if claims are more likely during specific travel seasons.
     <br><br>

3. **Model and Hyperparameter Tuning:**
   - **Challenge:** The model's performance may still need improvement.
   - **Recommendation:** Continue experimenting with different classification algorithms and a broader range of hyperparameters. Algorithms like Random Forest, Gradient Boosting, or even deep learning models could be explored. Fine-tuning these models can potentially lead to better performance.
   <br><br>

4. **Utilize Advanced Resampling Techniques:**
   - **Challenge:** Traditional resampling methods like NearMiss might not sufficiently address the imbalance.
   - **Recommendation:** Implement more advanced resampling techniques:
     - **SMOTEENN (SMOTE + Edited Nearest Neighbors):** Combine synthetic minority over-sampling and edited nearest neighbors cleaning to balance the dataset and remove noisy examples.
     - **SMOTETomek:** (combination of SMOTE and Tomek links) to generate synthetic samples and clean the dataset, improving the balance and model performance.
     - **ADASYN (Adaptive Synthetic Sampling):** Similar to SMOTE but focuses on generating harder-to-learn instances.
     - **Ensemble Methods:** Use ensemble techniques like EasyEnsemble or BalancedRandomForest to improve model performance on imbalanced datasets.
     - **Cost-Sensitive Learning:** Adjust the algorithm to account for the costs of misclassification, particularly false negatives.
     <br><br>

5. **Model Monitoring and Maintenance:**
   - **Challenge:** Model performance may degrade over time as new data is collected.
   - **Recommendation:** Regularly retrain the model with new data and monitor its performance to ensure it continues to make accurate predictions.
   <br><br>

By implementing these recommendations, it can enhance the predictive model’s performance, particularly in dealing with imbalanced data, and improve its ability to predict policyholders who are likely to file claims.

> ### **Recommendation For Business**

1. **High-Risk Policyholders:**
   - **Characteristics:** Long trip duration, high net sales, high commission, older age, airlines agency type, online distribution channel, female policyholders, comprehensive benefit product plan.

   - **Recommendations:**
     - Implement stricter underwriting policies.
     - Consider higher premiums or tailored products to mitigate risk.
     - Provide enhanced monitoring and support for claims processing.
     - Regularly review and adjust policies to match evolving risk profiles.
     - Offer risk management education and resources to policyholders.
     - Introduce deductible options to share the risk with policyholders.
     - Use predictive analytics to proactively identify and address potential high-risk claims.
     - Enhance fraud detection measures for this segment.
     <br><br>

2. **Low-Risk Policyholders:**
   - **Characteristics:** Short trip duration, lower net sales, lower commission, younger age, travel agency type, offline distribution channel, male policyholders, single benefit product plan.

   - **Recommendations:**
     - Offer incentives such as discounts or loyalty programs.
     - Streamline claims process to enhance customer satisfaction.
     - Provide additional benefits or coverage options to attract and retain low-risk policyholders.
     - Implement personalized marketing strategies to encourage policy renewals.
     - Develop reward programs for no-claim policyholders.
     - Enhance digital engagement with self-service options and mobile app features.
     - Offer bundled insurance products to increase value.
     - Conduct regular satisfaction surveys to gather feedback and improve services.
     <br><br>

3. **Overall Business Performance:**
   - **Recommendations:**
     - Continuously improve the predictive model by integrating more data and regularly updating it.
     - Adapt strategies to changing patterns and trends in the travel insurance market.
     - Maintain transparent communication with policyholders about their risk profiles and the benefits of tailored insurance plans to build trust and loyalty.
     <br><br>

4. **Policyholder Segmentation:**
   - **Characteristics:** More granular segmentation based on detailed policyholder profiles and claim history.
   
   - **Recommendations:**
     - Design targeted marketing campaigns for different policyholder groups.
     - Improve customer engagement through personalized communication and offers.
     - Optimize resource allocation for claims processing and fraud detection.
     - Develop customized insurance products and pricing strategies aligned with specific needs and risk profiles.
     - Regularly reassess and update segmentation criteria to reflect the latest data and trends.
