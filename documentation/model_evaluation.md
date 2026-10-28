# AI Hiring Classification — Model Evaluation Report

## 1. Project Overview

This project demonstrates a machine learning classification workflow for predicting hiring decisions using Dataiku DSS, with Power BI used to explore candidate predictions and supporting metrics.

The objective is to evaluate a Decision Tree classifier, compare it with Logistic Regression, and examine potential differences in model outcomes across gender and experience subgroups.

**Important:** This is a portfolio prototype, not a validated or production-ready hiring system.

## 2. Model Evaluation Dataset

| Item | Details |
|---|---|
| Classification task | Binary classification |
| Selected model | Decision Tree |
| Comparison model | Logistic Regression |
| Test-set size | 289 records |
| Evaluation platform | Dataiku DSS |
| Decision threshold | 0.5, as configured for candidate scoring |

The reported test metrics relate to the held-out evaluation dataset. Predictions generated for the separate synthetic candidate dataset must not be treated as test-set evaluation results.

## 3. Classification Performance

The following values were recorded during the project workflow and should be verified against the final saved-model evaluation in Dataiku DSS before publication.

| Metric | Decision Tree |
|---|---:|
| Accuracy | 89.97% |
| Precision | 83.13% |
| Recall | 82.14% |
| F1-score | 82.63% |
| ROC-AUC | Approximately 0.889 |

### Interpretation

- **Accuracy:** Approximately 90% of test records were classified correctly.
- **Precision:** Approximately 83% of records predicted as positive were positive in the test data.
- **Recall:** Approximately 82% of actual positive records were identified.
- **F1-score:** The harmonic mean of precision and recall was approximately 82.63%.
- **ROC-AUC:** A value near 0.889 indicates good ranking discrimination on the evaluated data, but does not establish that the model is suitable for real hiring decisions.

These metrics depend on the dataset, target-label coding, test split, and model configuration.

## 4. Confusion Matrix

The recorded confusion matrix is:

| Actual outcome | Predicted 1 | Predicted 0 |
|---|---:|---:|
| Actual 1 | 69 | 15 |
| Actual 0 | 14 | 191 |

Where:

- **True positives (69):** Actual positive records predicted as positive.
- **False negatives (15):** Actual positive records predicted as negative.
- **False positives (14):** Actual negative records predicted as positive.
- **True negatives (191):** Actual negative records predicted as negative.

The matrix contains 289 records. Its diagonal contains 260 correct classifications, corresponding to approximately 89.97% accuracy.

The meaning of class 1 must be confirmed from the original target encoding. It should not automatically be described as “hired” or “selected” until that mapping has been verified.

## 5. Model Comparison

| Model | ROC-AUC |
|---|---:|
| Decision Tree | Approximately 0.889 |
| Logistic Regression | Approximately 0.871 |

The Decision Tree had the higher recorded ROC-AUC in this evaluation. The difference is approximately 0.018.

This supports selecting the Decision Tree for further investigation within this prototype. However, model selection should consider more than ROC-AUC, including calibration, error costs, stability, subgroup performance, explainability, and validation on representative data.

## 6. Fairness Diagnostics

A fairness analysis was performed using Gender as the sensitive attribute, with gender values 0 and 1 compared in the evaluation report.

| Fairness diagnostic | Recorded disparity |
|---|---:|
| Demographic parity | 0.022 |
| Equalized odds | 0.061 |
| Equality of opportunity | 0.061 |
| Predictive rate parity | 0.063 |

### Group-level observations

| Measure | Gender = 0 | Gender = 1 |
|---|---:|---:|
| Group size | 156 | 133 |
| Positive prediction rate | 35.3% | 33.1% |
| False-positive rate | 12.8% | 14.6% |
| True-positive rate | 87.2% | 81.1% |
| Positive predictive value | 74.5% | 68.2% |

These results show differences in prediction outcomes between the two groups in this dataset. The recorded disparity values should be interpreted using the definitions and calculation settings in the Dataiku fairness report.

**Limitations:** These diagnostics do not prove that the model is fair or unbiased. Group sample sizes, label quality, feature selection, data representativeness, and the suitability of the fairness metrics all affect interpretation. The gender encoding must also be verified before assigning human-readable labels.

Gender and other protected or sensitive characteristics should not be used to make real employment decisions without appropriate legal, ethical, and governance review.

## 7. Subgroup Performance

The project also examined ROC-AUC across groups of candidates with different levels of experience.

The observed subgroup results varied substantially. Some groups had ROC-AUC values near 0.50, while others had values close to 1.00.

These extreme results require caution. They may reflect small subgroup sample sizes, limited variation in outcomes, or unstable estimates rather than genuine differences in predictive ability.

Before drawing conclusions, record each subgroup's sample size and positive/negative class counts, and verify that each group contains enough examples to support meaningful evaluation.

## 8. Synthetic Candidate Scoring

A separate dataset containing 15 fictional candidate records was scored using the deployed Dataiku prediction model.

The workflow generated predicted classes and class probabilities, including `prediction`, `proba_0`, and `proba_1`. The recorded output contained 10 class-1 predictions and 5 class-0 predictions.

These are predictions for synthetic examples, not verified hiring outcomes. The proportion of positive predictions is not a measure of model accuracy because the true outcomes for these new records are not known.

The synthetic scoring dataset is intended to demonstrate the scoring workflow and Power BI reporting, not to demonstrate real-world hiring performance.

## 9. Limitations and Risks

1. **Dataset representativeness:** Performance may not generalize to other organizations, job roles, applicant populations, or recruitment processes.
2. **Historical labels:** Historical hiring decisions can reflect past biases and may not represent objective job suitability.
3. **Fairness:** A small difference in one fairness metric does not establish equitable treatment across all groups.
4. **Subgroup sample sizes:** Small groups can produce unreliable performance estimates.
5. **Prediction probabilities:** Model probabilities should not automatically be interpreted as calibrated probabilities of job success.
6. **Feature validity:** Features should be reviewed for job relevance, data quality, proxy discrimination, and potential privacy concerns.
7. **Human oversight:** Automated predictions should not be used as the sole basis for rejecting or selecting candidates.

## 10. Recommended Next Steps

- Verify all reported metrics against the final Dataiku saved-model evaluation.
- Confirm the target-label mapping for classes 0 and 1.
- Document the train/test split, random seed, preprocessing steps, and model parameters.
- Evaluate calibration and precision-recall performance in addition to ROC-AUC.
- Review subgroup sample sizes and confidence intervals.
- Investigate fairness across relevant groups and job-related criteria.
- Test on representative, independently collected data before considering any real-world use.
- Retain meaningful human oversight and conduct legal, privacy, and employment-impact reviews.

## 11. Conclusion

The Decision Tree achieved a recorded ROC-AUC of approximately 0.889, compared with approximately 0.871 for Logistic Regression. Its recorded classification metrics suggest promising performance on the project's held-out test set.

The fairness and subgroup analyses highlight the importance of examining model behavior beyond overall accuracy. However, the results are preliminary and dataset-specific. Further validation, transparent documentation, and careful assessment of potential harms are necessary before any practical use.

**Project status:** Educational portfolio prototype. Not approved or validated for real-world hiring decisions.
