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
