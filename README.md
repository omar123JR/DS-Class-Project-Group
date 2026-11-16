# Bank Marketing Subscription Prediction

**A practical data-science project exploring how historical bank campaign data can help identify clients who may subscribe to a term deposit.** The notebook covers exploratory analysis, feature preparation, and a comparison of logistic regression and random forest on an imbalanced classification problem.

[Open the notebook](bank_marketing_project.ipynb) · [Open the notebook in Colab](https://colab.research.google.com/github/omar123JR/DS-Class-Project-Group/blob/main/bank_marketing_project.ipynb) · [View the presentation](https://www.canva.com/design/DAG80w25nWk/yRy2_kMG-sbzizxxhf9C-A/view?utm_content=DAG80w25nWk&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h8d16597c7a)

> **Educational project.** The analysis is not a validated marketing system and should not be used as the sole basis for customer or financial decisions.

## The question

Can information available about a client and previous campaign interactions help identify clients who subscribe to a term deposit? The target, `y`, records whether the client subscribed (`yes`) or did not (`no`). The practical challenge is class imbalance: only 11.70% of records are positive.

## What the project demonstrates

The notebook explores a real-world tabular dataset, checks data quality, and compares two classification approaches. It uses scikit-learn preprocessing pipelines to scale numeric features and encode categorical features, and evaluates the models with class-level precision, recall, and F1 rather than relying on accuracy alone.

## Results from the saved test run

The stratified test set contains 9,043 records: 7,985 `no` cases and 1,058 `yes` cases.

- **Logistic regression:** 89.33% accuracy. For the `yes` class, precision is 66%, recall is 18%, and F1 is 28%. Weighted F1 is 87%.
- **Random forest:** 81.71% accuracy. For `yes`, precision is 34%, recall is 61%, and F1 is 44%. Weighted F1 is 84%.

The results show a useful trade-off in this split. Logistic regression has higher overall accuracy and higher precision among its positive predictions. The class-weighted random forest finds more subscribers, but its lower precision means more of its positive predictions are incorrect. The preferred model depends on the relative cost of missing a potential subscriber versus making an unnecessary follow-up call. These are saved results from one held-out split, not evidence of performance on future campaigns.

## Methodology

The included `bank-full.csv` has 45,211 records and 17 columns: 16 input features and the target. The notebook uses a stratified 80/20 train/test split with `random_state=42`. Numeric features are scaled with `StandardScaler`; categorical features are one-hot encoded with `OneHotEncoder`. Both transformations are combined with the estimators in a scikit-learn `ColumnTransformer` and `Pipeline`.

The models are logistic regression and a random forest with 100 trees, maximum depth 10, and balanced class weights. The notebook excludes `duration` from the predictors. Because call duration is only known after a client has been contacted, excluding it is appropriate when the intended use is to prioritize clients before making a call.

## Run the notebook

Use Python 3.10 or later from the repository root:

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
python -m pip install -r requirements.txt
jupyter notebook bank_marketing_project.ipynb
```

The notebook reads `bank-full.csv` from the repository root. The included CSV uses semicolon delimiters. In Colab, open the notebook using the link above and ensure the CSV is available in the runtime before running the cells.

## Dataset and attribution

The project uses the `bank-full.csv` variant of the UCI Bank Marketing dataset. It describes phone-based campaigns from a Portuguese banking institution. The target `y` indicates whether a client subscribed to a term deposit. The included file contains no blank missing fields; values such as `unknown` are retained as categories.

Moro, S., Rita, P., & Cortez, P. (2014). *Bank Marketing* [Dataset]. UCI Machine Learning Repository. [https://doi.org/10.24432/C5K306](https://doi.org/10.24432/C5K306). The dataset is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## Project files

- [`bank_marketing_project.ipynb`](bank_marketing_project.ipynb) — analysis, preprocessing, model training, and evaluation.
- [`bank-full.csv`](bank-full.csv) — dataset used by the notebook.
- [`presentation.pptx`](presentation.pptx) — project presentation; also available through the Canva link above.
- [`docs/course_assignment.pdf`](docs/course_assignment.pdf) — course project requirements.
- [`requirements.txt`](requirements.txt) — Python dependencies.

## Limitations and reproducibility notes

- The notebook's saved ROC/AUC cell did not complete (`NameError: y_test is not defined`). Its code also calls `roc_auc_score` without importing it. No AUC value is reported here; that cell needs to be fixed and rerun before ROC/AUC results can be cited.
- The final test cell imports a course helper named `testcases`, but `testcases.py` is not included in the repository. That cell requires the instructor-provided helper.
- The cleaning narrative says outliers were capped with Winsorization, while the executable cells detect and retain them. Align the narrative and implementation before presenting that step as completed.
- The reported model metrics come from one test split. Further validation across splits or later campaign data would be needed before using the model operationally.

## Presentation and contributors

The presentation is available as [`presentation.pptx`](presentation.pptx), in the [Canva viewer](https://www.canva.com/design/DAG80w25nWk/yRy2_kMG-sbzizxxhf9C-A/view?utm_content=DAG80w25nWk&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h8d16597c7a), and through the [Google Colab notebook](https://colab.research.google.com/github/omar123JR/DS-Class-Project-Group/blob/main/bank_marketing_project.ipynb).

**Contributors:** Omar Aljerbi, Faraj Alarabi, Abd Albari Abd Alsamad, and Ali Bie.

## License

The UCI dataset is licensed under CC BY 4.0. No separate license has been added for the project's original code or presentation.
