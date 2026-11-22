# Credit Card Fraud Detection

An end-to-end machine learning project exploring credit card fraud detection, starting with **unsupervised anomaly detection using Isolation Forest**. The first phase focuses on a careful, reproducible experiment; a supervised classification model is planned as a separate future phase.

> **Project status:** In progress. This README describes the intended workflow. Metrics and findings will be added after the experiments have been run and reviewed.

## Project goals

- Inspect and prepare the transaction dataset while preserving the fraud label for evaluation.
- Split data into training, validation, and test sets with a clear evaluation protocol.
- Fit Isolation Forest without using fraud labels during training.
- Compare contamination settings and examine anomaly scores.
- Choose a decision threshold using validation data, then evaluate the selected approach on held-out test data.
- Report useful metrics for an imbalanced classification problem, visualize model behavior, and investigate errors and limitations.

## Planned workflow

1. **Inspect the data** — review dimensions, columns, data types, missing values, duplicates, class balance, and feature distributions.
2. **Prepare and split** — define the feature columns and target label, then create reproducible train, validation, and test partitions. Keep the test set out of model and threshold selection.
3. **Establish a baseline** — document a simple reference point and the default Isolation Forest behavior.
4. **Run Isolation Forest experiments** — train without labels and compare selected `contamination` values. Record the settings and rationale for each run.
5. **Inspect anomaly scores** — examine score distributions and how rankings relate to known fraud labels on validation data.
6. **Select a threshold** — choose a decision threshold using validation data and a stated objective. Freeze that choice before the final test evaluation.
7. **Evaluate** — report the confusion matrix, precision, recall, F1 score, ROC-AUC, Average Precision, and precision-recall curve. Include the threshold and settings used, since threshold-dependent metrics depend on them.
8. **Understand errors and limits** — review false positives and false negatives, discuss class imbalance and dataset limitations, and note possible improvements.
9. **Prepare the project for reuse** — organize the code, document setup, and make the experiment reproducible.

## Learning setup

Isolation Forest is used in the first phase as an **unsupervised** detector: the training step uses transaction features only and does not learn from the fraud labels. The known labels are retained for validation-based threshold selection and evaluation. The label must not be included among the model input features.

The `contamination` parameter and the decision threshold play different roles in the experiment. Contamination informs the model's expected outlier proportion; the validation procedure will separately determine how anomaly scores are converted into fraud predictions. The selected settings will be recorded rather than chosen from test results.

## Planned evaluation

The evaluation will include:

- Confusion matrix
- Precision, recall, and F1 score at the selected threshold
- ROC-AUC
- Average Precision and a precision-recall curve
- Visualizations of score distributions and other relevant model behavior
- Error analysis of false positives and false negatives

Because fraud is rare in many transaction datasets, the report will interpret metrics in the context of class imbalance. No performance values are reported here; they belong in the results section after a reproducible run.

## Planned repository layout

The structure below is a target layout and may change as the project is implemented:

```text
credit-card-fraud-detection/
├── data/
│   ├── raw/                 # Local dataset; not committed
│   └── processed/           # Generated, reproducible intermediate data
├── notebooks/               # Exploration and experiment notes
├── src/                     # Reusable preprocessing and modeling code
├── reports/
│   └── figures/             # Generated plots for analysis
├── .gitignore
├── README.md
└── requirements.txt
```

The data folders and scripts will be added as the project takes shape. Keep downloaded or sensitive data out of version control; follow the dataset provider's terms when obtaining and sharing data.

## Reproducibility

The implementation will document the dataset source, required packages, random seeds, split strategy, preprocessing steps, Isolation Forest settings, threshold-selection rule, and commands needed to reproduce the reported results. These instructions will be completed alongside the runnable code.

## Planned future phase: supervised classification

A supervised classifier and a comparison with the anomaly-detection approach are planned for a later phase. **This phase has not been implemented.** No classifier, comparison, or result is claimed in this repository at this stage.

## Limitations to examine

- Transaction datasets may be highly imbalanced, so accuracy alone can hide poor fraud detection.
- Results depend on the dataset, split strategy, feature representation, contamination setting, and threshold-selection objective.
- Isolation Forest may flag unusual legitimate transactions and may miss fraud that resembles normal activity.
- Historical labels and anonymized features may not capture deployment conditions, changing fraud patterns, or real-world investigation costs.
- Test-set results estimate performance on the held-out split; they do not guarantee future or production performance.

## License and data

No license or dataset source is specified yet. Add the appropriate project license and dataset attribution once they have been confirmed. Do not redistribute the dataset unless its terms allow it.
