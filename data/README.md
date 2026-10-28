# AI Hiring Classification & Candidate Prediction Dashboard

## Project Overview
An end-to-end machine learning prototype that predicts hiring decisions using candidate attributes and presents the results through an interactive Power BI dashboard.

The project demonstrates a workflow combining data preparation, classification modelling, model evaluation, prediction explainability, and candidate-level reporting.

## Business Problem
Recruitment teams assess candidates using multiple attributes, including experience, education, interview performance, skills, personality scores, and recruitment strategy. This project explores how machine learning can support structured analysis of hiring decisions.

## Tools & Technologies
- **Dataiku DSS:** Data preparation, model training, scoring, and model evaluation
- **Power BI:** Interactive dashboards and candidate prediction analysis
- **Machine Learning:** Decision Tree and Logistic Regression
- **Data:** Synthetic candidate data

## Machine Learning
Two classification models were explored:
- Logistic Regression
- Decision Tree

The Decision Tree achieved a reported ROC AUC of approximately **0.889** on a held-out test set of 289 records. Its reported accuracy was approximately **89.97%**, with precision of **83.13%**, recall of **82.14%**, and an F1 score of **82.63%** at the evaluated threshold.

These metrics describe performance on the test set, not guaranteed performance on real recruitment data.

## Power BI Dashboard
The dashboard contains two pages:

### Page 1 — Model & Hiring Insights
Summarises model performance and relevant hiring patterns.

### Page 2 — Candidate Prediction Analysis
Includes:
- Candidate prediction probability distribution
- Prediction breakdown by education level
- Prediction breakdown by gender
- Prediction breakdown by recruitment strategy
- Candidate-level predicted outcomes and probabilities
- Interactive slicers for candidate exploration

## Explainability & Fairness
Dataiku was used to explore feature importance, model explanations, and fairness metrics across demographic groups.

Fairness metrics are exploratory. Results based on small synthetic samples cannot establish that a model is fair or suitable for actual hiring decisions.

## Key Limitations
- Synthetic data does not represent the complexity of real recruitment.
- Model performance may differ substantially on unseen real-world data.
- Predictions reflect patterns in the training data and may reproduce existing biases.
- The prototype is not intended to make autonomous hiring decisions.

## Future Improvements
- Validate the model using representative, appropriately governed recruitment data.
- Compare additional classification algorithms.
- Improve probability calibration and threshold selection.
- Conduct more robust subgroup and fairness testing.
- Develop monitoring and human-review workflows.

## Model Evaluation

The Decision Tree model achieved a ROC-AUC of approximately 0.889 on the recorded evaluation dataset. It was compared with Logistic Regression using Dataiku DSS.

### Model Comparison
![Model comparison](screenshots/01_model_comparison.png)

### Confusion Matrix
![Confusion matrix](screenshots/03_confusion_matrix.png)

### ROC Curve
![ROC curve](screenshots/04_roc_curve.png)

For additional details, see [Model Evaluation Report](documentation/model_evaluation.md).

**Note:** This is an educational portfolio prototype. Results are dataset-specific and do not establish suitability for real-world hiring decisions.


## Disclaimer
This project is an educational portfolio prototype. It is not a validated recruitment system and should not be used to make real employment decisions.

