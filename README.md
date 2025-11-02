# Data-Analysis-Capstone-Google

# Predicting Employee Attrition at Salifort Motors

## Overview

The goal of this project was to analyze an HR dataset to understand the key drivers of employee attrition and to build a predictive model that identifies employees who are likely to leave. This project utilized a dataset from Salifort Motors, a large consulting firm.

After a thorough exploratory data analysis (EDA) revealed complex, non-linear relationships, a **Random Forest** model was chosen. The final model performed with exceptional accuracy, achieving an **AUC score of 0.978** and an **F1-score of 0.957**. The model identified that **satisfaction level, number of projects, tenure, average monthly hours, and last evaluation score** were the most influential factors in predicting attrition.

## Business Understanding

Employee attrition is a significant cost for any company. It is expensive and time-consuming to find, interview, and train new employees, in addition to the loss of productivity and institutional knowledge.

The HR department at Salifort Motors wanted to move from a reactive to a **proactive retention strategy**. By understanding the key drivers of attrition and identifying "at-risk" employees, the company can implement targeted interventions—such as adjusting workloads, discussing career growth, or offering new incentives—to improve employee satisfaction and reduce costly turnover.

## Data Understanding

The dataset, provided by the HR department, consisted of 10 features for 14,999 employees. After cleaning duplicate entries, the final dataset for analysis contained **11,991 unique employee records**.

Key features included:
* `satisfaction_level` (0-1)
* `last_evaluation` (0-1)
* `number_project`
* `average_monthly_hours`
* `time_spend_company` (Tenure in years)
* `work_accident` (0 or 1)
* `left` (The target variable: 0 or 1)
* `promotion_last_5years` (0 or 1)
* `department`
* `salary` (Low, Medium, High)

A primary finding from the EDA was that the target variable, `left`, was **imbalanced**, with only **16.7%** of employees in the dataset having left the company. This imbalance guided the modeling strategy to focus on metrics like F1-score and AUC rather than simple accuracy.

``

Furthermore, the EDA revealed strong non-linear relationships. For example, employees with *both* very low and very high `average_monthly_hours` were more likely to leave, indicating two distinct "leaver" profiles: the **"Disengaged"** and the **"Burned Out."** This discovery was the key reason for choosing a tree-based model.

``

## Modeling and Evaluation

A standard Logistic Regression model was rejected because its assumptions (linearity, no outliers) were not met by this dataset.

A **Random Forest Classifier** was chosen for its ability to handle non-linear relationships, its robustness to outliers, and its high predictive power.

The final model's feature importance results confirmed our EDA findings, with `satisfaction_level` being the single most predictive factor.

``

The model's performance on the test set was excellent, achieving an **AUC of 0.978** and a **Recall of 0.927**.

Critically, we analyzed the model's errors in a business context:
* **False Positives (4):** The model predicted 4 employees would leave, but they stayed.
    * *Business Cost:* Low (e.g., wasted retention bonus).
* **False Negatives (29):** The model predicted 29 employees would stay, but they left.
    * *Business Cost:* High (lost talent, blindsided managers, recruiting costs).

The model's primary weakness is the 29 False Negatives. This indicates that while the model is strong, it should be further optimized to prioritize **Recall**—finding as many *actual* leavers as possible.

## Conclusion

This project successfully demonstrated that employee attrition at Salifort Motors is not a random event, but a highly predictable outcome driven by a specific set of factors.

By analyzing the HR dataset, we developed a Random Forest model that can predict whether an employee will leave with extremely high confidence, achieving an Area Under the Curve (AUC) of 0.978 and an F1-score of 0.957.

**Key Recommendations:**

1.  Don't wait for annual reviews. Implement lightweight, quarterly "pulse surveys" to get a real-time, predictive measure of company-wide satisfaction.
2.  Create workload alerts. Managers should be notified when an employee is assigned 5+ projects or logs over $\approx$280 hours, as these are top burnout indicators. The "sweet spot" for retention is 3-4 projects.
3.  Proactively engage with employees in the 4-6 year "burnout window." This is the critical time to discuss career growth, promotions, or new assignments to keep them engaged.

**Future Work:**
The model could be significantly improved by collecting **exit interview data**. This would provide a "ground truth" `reason_for_leaving` feature, moving our understanding from *what* is happening to *why* it's happening.
