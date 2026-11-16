# Bank Marketing ML

**An end-to-end data science project using the UCI Bank Marketing dataset to explore customer campaigns and predict term-deposit subscriptions.** The notebook covers exploratory analysis, data preparation, feature pipelines, and a comparison of logistic regression and random forest models.

[Open the notebook](bank_marketing_project.ipynb) · [View the presentation](https://www.canva.com/design/DAG80w25nWk/yRy2_kMG-sbzizxxhf9C-A/view?utm_content=DAG80w25nWk&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h8d16597c7a) · [Open in Google Colab](https://colab.research.google.com/drive/1KeQcz1L9QXra-GVRTcy8cWQCwmeInPSM?usp=sharing)

> **Educational project only.** The analysis is for coursework and should not be used as the sole basis for real-world marketing, customer, or financial decisions.

## What is inside?

The notebook explores the data and target distribution, checks missing values, duplicates, and outliers, prepares numerical and categorical features with scikit-learn, then trains and evaluates two classifiers. The repository also includes the CSV required by the notebook, the PowerPoint presentation, and the course assignment brief.

## Run the notebook

Use Python 3.10 or later from the repository root:

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
python -m pip install -r requirements.txt
jupyter notebook bank_marketing_project.ipynb
```

The notebook reads `bank-full.csv` from the repository root. The CSV is included and uses semicolon delimiters. Run the analysis and model cells in order. In Google Colab, upload both the notebook and CSV to the same session, or clone this repository before running the notebook.

## Methodology

The included `bank-full.csv` contains 45,211 records and 17 columns: 16 input features and the target `y`. The notebook uses a stratified 80/20 train/test split with `random_state=42`, which yields 9,043 test records in the saved run. It excludes `duration` from the selected numeric predictors.

Numerical features are scaled with `StandardScaler`, while categorical features are one-hot encoded with `OneHotEncoder`. The transformations are combined with model fitting in a scikit-learn `ColumnTransformer` and `Pipeline`. The models are logistic regression and a random forest with 100 trees, maximum depth 10, and `class_weight="balanced"`.

## Results in the saved notebook

The test set has 7,985 `no` cases and 1,058 `yes` cases. For logistic regression, the saved classification report shows **89.33% accuracy**. For the `yes` class it reports **66% precision, 18% recall, and 28% F1**; weighted F1 is **87%**.

For the random forest, the saved report shows **81.71% accuracy**. For the `yes` class it reports **34% precision, 61% recall, and 44% F1**; weighted F1 is **84%**. These outputs show a trade-off on this test split: logistic regression has higher overall accuracy, while the class-weighted random forest finds more subscribers. The target is imbalanced: 39,922 records are `no` (88.30%) and 5,289 are `yes` (11.70%), so accuracy alone is not a sufficient model-selection measure.

## Reproducibility notes

The saved ROC/AUC analysis cell did not complete: its stored output is `NameError: y_test is not defined`. In addition, the cell's code calls `roc_auc_score` without importing it. Therefore this README does not report numeric AUC results, and the ROC/AUC cell needs correction and a successful rerun before those results can be cited.

The notebook's cleaning narrative says outliers were capped with Winsorization, but its executable cells detect outliers and keep them. Also, the final test cell imports `testcases`, but the required `testcases.py` helper is not included in this repository. Provide the course helper to run that cell. The reported model metrics are the saved outputs; re-run the successful model cells to regenerate them in your environment.

## Dataset

This is the UCI `bank-full.csv` variant of the Bank Marketing dataset, based on phone campaigns of a Portuguese banking institution. Its target `y` indicates whether a client subscribed to a term deposit. The UCI page describes 16 input features and the target, for 17 columns in total. The included dataset has no missing fields.

**Citation:** Moro, S., Rita, P., & Cortez, P. (2014). *Bank Marketing* [Dataset]. UCI Machine Learning Repository. [https://doi.org/10.24432/C5K306](https://doi.org/10.24432/C5K306).

The UCI dataset is licensed under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). This dataset license is separate from the license for the project's original code and presentation.

## Presentation and assignment

The PowerPoint file is available as [`presentation.pptx`](presentation.pptx), and the assignment requirements are in [`docs/course_assignment.pdf`](docs/course_assignment.pdf). The presentation can also be viewed through the Canva link at the top of this page.

## Contributors

Omar Aljerbi, Faraj Alarabi, Abd Albari Abd Alsamad, and Ali Bie.

## Project license

No license has yet been assigned to the project's original code or presentation. The UCI dataset is separately licensed under CC BY 4.0, as noted above. A project license should be added only with the contributors' approval and should not be assumed to cover the UCI dataset.
