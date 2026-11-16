# Bank Marketing ML

**An end-to-end data science project using the UCI Bank Marketing dataset to explore customer campaigns and predict term-deposit subscriptions.** The notebook covers exploratory analysis, data preparation, feature pipelines, and a comparison of logistic regression and random forest models.

[Open the notebook](bank_marketing_project.ipynb) · [View the presentation](https://www.canva.com/design/DAG80w25nWk/yRy2_kMG-sbzizxxhf9C-A/view?utm_content=DAG80w25nWk&utm_campaign=designshare&utm_medium=link2&utm_source=uniquelinks&utlId=h8d16597c7a) · [Open in Google Colab](https://colab.research.google.com/drive/1KeQcz1L9QXra-GVRTcy8cWQCwmeInPSM?usp=sharing)

> **Educational project only.** The analysis is for coursework and should not be used as the sole basis for real-world marketing, customer, or financial decisions.

## What is inside?

The notebook follows a complete classification workflow: it explores the data and target distribution, checks missing values, duplicates, and outliers, prepares numerical and categorical features with scikit-learn, then trains and evaluates two classifiers. The repository also includes the CSV required by the notebook, the PowerPoint presentation, and the course assignment brief.

## Run the notebook

Use Python 3.10 or later from the repository root:

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
python -m pip install -r requirements.txt
jupyter notebook bank_marketing_project.ipynb
```

Run the cells in order. The notebook reads `bank-full.csv` from the repository root; the file is included here and uses semicolon delimiters. In Google Colab, upload both the notebook and CSV to the same session, or clone this repository before running the notebook.

## Methodology

1. Explore the 45,211 customer records, summarize numeric and categorical features, visualize distributions and relationships, and inspect the imbalanced subscription target.
2. Check data quality and convert categorical columns for modeling. Numerical features are scaled with `StandardScaler`, while categorical features are one-hot encoded with `OneHotEncoder`.
3. Combine preprocessing and model fitting in a scikit-learn `ColumnTransformer` and `Pipeline`. Split data into training and test sets with a stratified 80/20 split and `random_state=42`.
4. Compare logistic regression and random forest using accuracy, class-level precision, recall and F1, along with ROC/AUC analysis.

The notebook excludes call duration (`duration`) from the selected numeric predictors. The target is imbalanced: roughly 11.7% of records are `yes` and 88.3% are `no`, so accuracy alone does not describe how well the models identify likely subscribers.

## Results shown in the saved notebook

The notebook's saved evaluation outputs report **89.33% accuracy and 18% recall for the `yes` class** for logistic regression. The random forest reports **81.71% accuracy, 61% recall for `yes`, and 0.84 weighted F1**. The results illustrate a trade-off: the random forest identifies more subscribers in this test split, while logistic regression has higher overall accuracy. Re-run all notebook cells to regenerate the metrics in your environment.

## Dataset

The included `bank-full.csv` is the full Bank Marketing dataset from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/222/bank+marketing). It contains 45,211 rows and 17 columns. The prediction target, `y`, indicates whether a client subscribed to a term deposit.

## Reproducibility note

There is a mismatch between the notebook's cleaning narrative and its executable cells: the narrative mentions capping outliers (Winsorization), while the code detects outliers and keeps them. Review and resolve this discrepancy before treating the preprocessing description as final. The saved notebook outputs may also differ from a fresh run depending on the software environment.

## Presentation and assignment

The PowerPoint file is available as [`presentation.pptx`](presentation.pptx), and the assignment requirements are in [`docs/course_assignment.pdf`](docs/course_assignment.pdf). The presentation can also be viewed through the Canva link at the top of this page.

## Contributors

Omar Aljerbi, Faraj Alarabi, Abd Albari Abd Alsamad, and Ali Bie.

## License

No license was supplied for the project code. The code and presentation remain with their respective rights holders unless a license is added. The dataset is a separate resource; refer to its [UCI source page](https://archive.ics.uci.edu/dataset/222/bank+marketing) for dataset details and terms.
