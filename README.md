# my-AI-Course-exercis
### Experimental Results: Hyperparameter Tuning

| Vectorizer | Model | Best Hyperparameters Found | CV Best Score | Test Accuracy |
| :--- | :--- | :--- | :--- | :--- |
| **CountVectorizer** | Logistic Regression | `{'C': 1}` | 0.9473 | 0.9378 |
| | KNN | `{'n_neighbors': 3, 'weights': 'distance'}` | 0.9359 | 0.9474 |
| | Random Forest | `{'max_depth': None, 'n_estimators': 100}` | 0.9479 | 0.9593 |
| | Gradient Boosting | `{'learning_rate': 0.1, 'n_estimators': 200}` | 0.9545 | 0.9545 |
| | SVM | `{'C': 10, 'kernel': 'rbf'}` | 0.9503 | 0.9569 |
| | Naïve Bayes (Bernoulli) | `{'alpha': 0.5, 'force_alpha': True}` | 0.9443 | 0.9426 |
| **HashingVectorizer** | Logistic Regression | `{'C': 10}` | 0.9509 | 0.9641 |
| | KNN | `{'n_neighbors': 7, 'weights': 'uniform'}` | 0.9401 | 0.9330 |
| | Random Forest | `{'max_depth': None, 'n_estimators': 200}` | 0.9694 | 0.9641 |
| | Gradient Boosting | `{'learning_rate': 0.1, 'n_estimators': 200}` | 0.9647 | 0.9641 |
| | **SVM** | **`{'C': 10, 'kernel': 'rbf'}`** | **0.9688** | **0.9833** |
| | Naïve Bayes (Bernoulli) | `{'alpha': 0.1, 'force_alpha': True}` | 0.9143 | 0.9306 |
| **TfidfVectorizer** | Logistic Regression | `{'C': 0.1}` | 0.9521 | 0.9545 |
| | KNN | `{'n_neighbors': 5, 'weights': 'uniform'}` | 0.9155 | 0.9330 |
| | Random Forest | `{'max_depth': None, 'n_estimators': 200}` | 0.9515 | 0.9689 |
| | Gradient Boosting | `{'learning_rate': 0.1, 'n_estimators': 100}` | 0.9521 | 0.9593 |
| | SVM | `{'C': 1, 'kernel': 'linear'}` | 0.9503 | 0.9569 |
| | Naïve Bayes (Bernoulli) | `{'alpha': 0.5, 'force_alpha': True}` | 0.9443 | 0.9426 |


# Next-Stop Arrival Delay Prediction — Stockholm Bus Routes 176 and 177

AH2179 Applied Artificial Intelligence in Transportation · KTH Royal Institute of Technology
Group 4: Alemayehu Abadi & Saad Alhmmada

Predicts the observed arrival delay at the next stop from information available when a bus
departs its current stop, using 2024 GTFS Schedule and GTFS-Realtime data.

## Contents

`AH2179_Final_Project.ipynb` — full pipeline, Sections 0–22:

- data download, filtering to routes 176 and 177, quality assessment
- next-stop target construction and cleaning audit
- feature engineering and a chronological train/validation/test split
- baselines, Ridge regression, XGBoost
- tabular neural networks with a history-feature ablation
- five-stop LSTM sequence models with verified trip boundaries
- weather ablation across four model families
- stop-level error diagnostics, grouped permutation importance and early-warning evaluation

## Results

Test period: November–December 2024, 448,566 rows.

| Model | Test MAE (minutes) |
|---|---|
| Five-stop LSTM, no weather | 0.3342 |
| History-enhanced network | 0.3392 |
| Ridge regression | 0.3836 |
| XGBoost | 0.5261 |
| Persistence baseline | 0.6303 |

The LSTM's advantage over the tabular network is 0.30 seconds of MAE, while the two models
differ in input representation, architecture and runtime. They are treated as comparable
rather than ranked; see Section 11 of the report for the full discussion.

## Running

Built with Python 3.11 and TensorFlow 2.21. Required packages:

numpy, pandas, pyarrow, scikit-learn, xgboost, tensorflow,
matplotlib, seaborn, openpyxl, joblib

Raw data is not included. Download the monthly 2024 GTFS-Realtime files and the static
GTFS reference tables from the KTH Data Repository (DOI: 10.71775/kth.f50j9-fkg32) and place
them in `data/raw/`. The optional weather extension requires the SLB Analys hourly export at
`data/external/torkel_2024.xlsx`.

## Notes

- All preprocessing is fitted on training rows only.
- The split is chronological by service date, never random.
- `next_segment_distance_km` holds cumulative route progress, not link length.
- Weather timestamp semantics are unverified; treat that experiment as offline only.
