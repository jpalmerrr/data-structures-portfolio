pip install pyarrow
import pandas as pd

url = "https://github.com/nflverse/nflverse-data/releases/download/pbp/play_by_play_2021.parquet"

df = pd.read_parquet(url)

df.head()
# If these are not installed, uncomment this line:
# !pip install pandas numpy matplotlib scikit-learn pyarrow

import numpy as np
import matplotlib.pyplot as plt

from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.impute import SimpleImputer

from sklearn.dummy import DummyClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier

from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    roc_auc_score,
    confusion_matrix,
    ConfusionMatrixDisplay,
    classification_report,
    RocCurveDisplay
)

pd.set_option("display.max_columns", 100)
pd.set_option("display.max_rows", 100)
YEAR = 2021

url = (
    f"https://github.com/nflverse/nflverse-data/"
    f"releases/download/pbp/play_by_play_{YEAR}.parquet"
)

df = pd.read_parquet(url)

print("Original dataset shape:", df.shape)

df.head()
print("Number of rows:", df.shape[0])
print("Number of columns:", df.shape[1])

print("\nFirst 20 column names:")
print(df.columns[:20].tolist())

print("\nData types:")
print(df.dtypes.head(20))
print(df["season"].value_counts())
print(df["season_type"].value_counts())
df = df[df["season_type"] == "REG"].copy()

print("Regular season plays:", len(df))
passes = df[
    (df["pass_attempt"] == 1) &
    (df["sack"] == 0) &
    (df["qb_spike"] == 0)
].copy()

print("Pass attempts before removing missing targets:", len(passes))
passes = passes.dropna(subset=["complete_pass"])

print("Usable pass attempts:", len(passes))
print(passes["complete_pass"].value_counts())

print("\nPercentages:")
print(
    passes["complete_pass"]
    .value_counts(normalize=True)
    .mul(100)
    .round(2)
)
passes["completion_result"] = passes["complete_pass"].map({
    0: "Incomplete",
    1: "Complete"
})

passes[["complete_pass", "completion_result"]].head()
completion_counts = passes["completion_result"].value_counts()

plt.figure(figsize=(7, 5))

completion_counts.plot(kind="bar")

plt.title("NFL Pass Outcomes - 2021")
plt.xlabel("Pass Result")
plt.ylabel("Number of Pass Attempts")
plt.xticks(rotation=0)

plt.tight_layout()
plt.show()
numeric_summary_columns = [
    "air_yards",
    "ydstogo",
    "yardline_100",
    "game_seconds_remaining",
    "score_differential"
]

passes[numeric_summary_columns].describe().round(2)
features_to_check = [
    "complete_pass",
    "air_yards",
    "ydstogo",
    "down",
    "yardline_100",
    "qtr",
    "game_seconds_remaining",
    "score_differential",
    "shotgun",
    "no_huddle",
    "pass_location",
    "pass_length"
]

missing_table = pd.DataFrame({
    "Missing Count": passes[features_to_check].isnull().sum(),
    "Missing Percent":
        passes[features_to_check].isnull().mean() * 100
})

missing_table["Missing Percent"] = (
    missing_table["Missing Percent"].round(2)
)

missing_table.sort_values(
    "Missing Percent",
    ascending=False
)
duplicate_count = passes.duplicated(
    subset=["game_id", "play_id"]
).sum()

print("Duplicate plays:", duplicate_count)
passes = passes.drop_duplicates(
    subset=["game_id", "play_id"]
).copy()

print("Dataset after duplicate removal:", passes.shape)
plt.figure(figsize=(9, 5))

passes["air_yards"].dropna().plot(
    kind="hist",
    bins=40
)

plt.title("Distribution of Air Yards on NFL Pass Attempts")
plt.xlabel("Air Yards")
plt.ylabel("Number of Pass Attempts")

plt.tight_layout()
plt.show()
passes["air_yards"].describe()
passes[
    ["game_id", "week", "passer_player_name", "air_yards"]
].sort_values(
    "air_yards",
    ascending=False
).head(10)
air_yard_bins = [-100, 0, 5, 10, 15, 20, 30, 100]

air_yard_labels = [
    "Behind LOS",
    "1-5",
    "6-10",
    "11-15",
    "16-20",
    "21-30",
    "31+"
]

passes["air_yard_group"] = pd.cut(
    passes["air_yards"],
    bins=air_yard_bins,
    labels=air_yard_labels
)
air_yard_completion = (
    passes
    .groupby(
        "air_yard_group",
        observed=False
    )["complete_pass"]
    .mean()
    .mul(100)
)

print(air_yard_completion.round(2))
plt.figure(figsize=(10, 5))

air_yard_completion.plot(
    kind="bar"
)

plt.title("Completion Percentage by Pass Distance")
plt.xlabel("Air-Yard Range")
plt.ylabel("Completion Percentage")
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
completion_by_down = (
    passes
    .groupby("down")["complete_pass"]
    .mean()
    .mul(100)
)

print(completion_by_down.round(2))
plt.figure(figsize=(7, 5))

completion_by_down.plot(
    kind="bar"
)

plt.title("NFL Completion Percentage by Down")
plt.xlabel("Down")
plt.ylabel("Completion Percentage")
plt.xticks(rotation=0)

plt.tight_layout()
plt.show()
print(passes["pass_location"].value_counts(dropna=False))
location_completion = (
    passes
    .groupby("pass_location")["complete_pass"]
    .mean()
    .mul(100)
)

print(location_completion.round(2))
plt.figure(figsize=(7, 5))

location_completion.plot(
    kind="bar"
)

plt.title("Completion Percentage by Pass Location")
plt.xlabel("Pass Location")
plt.ylabel("Completion Percentage")
plt.xticks(rotation=0)

plt.tight_layout()
plt.show()
length_completion = (
    passes
    .groupby("pass_length")["complete_pass"]
    .mean()
    .mul(100)
)

print(length_completion.round(2))
plt.figure(figsize=(7, 5))

length_completion.plot(
    kind="bar"
)

plt.title("Completion Percentage: Short vs. Deep Passes")
plt.xlabel("Pass Length")
plt.ylabel("Completion Percentage")
plt.xticks(rotation=0)

plt.tight_layout()
plt.show()
distance_bins = [0, 3, 6, 10, 15, 100]

distance_labels = [
    "1-3",
    "4-6",
    "7-10",
    "11-15",
    "16+"
]

passes["distance_group"] = pd.cut(
    passes["ydstogo"],
    bins=distance_bins,
    labels=distance_labels,
    include_lowest=True
)

distance_completion = (
    passes
    .groupby(
        "distance_group",
        observed=False
    )["complete_pass"]
    .mean()
    .mul(100)
)

print(distance_completion.round(2))
plt.figure(figsize=(8, 5))

distance_completion.plot(
    kind="bar"
)

plt.title("Completion Percentage by Yards to Go")
plt.xlabel("Yards Needed for First Down")
plt.ylabel("Completion Percentage")
plt.xticks(rotation=0)

plt.tight_layout()
plt.show()
numeric_features = [
    "air_yards",
    "ydstogo",
    "yardline_100",
    "game_seconds_remaining",
    "score_differential"
]

categorical_features = [
    "down",
    "qtr",
    "shotgun",
    "no_huddle",
    "pass_location",
    "pass_length"
]

target = "complete_pass"
leakage_variables = [
    "yards_gained",
    "epa",
    "success",
    "touchdown",
    "first_down",
    "interception",
    "cpoe",
    "passer_rating"
]
feature_columns = numeric_features + categorical_features

X = passes[feature_columns].copy()

y = passes[target].astype(int)

print("X shape:", X.shape)
print("y shape:", y.shape)
X.isnull().sum().sort_values(ascending=False)
train_mask = passes["week"] <= 14
test_mask = passes["week"] >= 15

X_train = X.loc[train_mask].copy()
X_test = X.loc[test_mask].copy()

y_train = y.loc[train_mask].copy()
y_test = y.loc[test_mask].copy()

print("Training observations:", len(X_train))
print("Testing observations:", len(X_test))

print(
    "Training percentage:",
    round(len(X_train) / len(X) * 100, 2)
)

print(
    "Testing percentage:",
    round(len(X_test) / len(X) * 100, 2)
)
print("Training target distribution:")
print(
    y_train.value_counts(
        normalize=True
    ).round(3)
)

print("\nTesting target distribution:")
print(
    y_test.value_counts(
        normalize=True
    ).round(3)
)
numeric_transformer = Pipeline(
    steps=[
        (
            "imputer",
            SimpleImputer(strategy="median")
        ),
        (
            "scaler",
            StandardScaler()
        )
    ]
)

categorical_transformer = Pipeline(
    steps=[
        (
            "imputer",
            SimpleImputer(strategy="most_frequent")
        ),
        (
            "onehot",
            OneHotEncoder(
                handle_unknown="ignore"
            )
        )
    ]
)

preprocessor = ColumnTransformer(
    transformers=[
        (
            "num",
            numeric_transformer,
            numeric_features
        ),
        (
            "cat",
            categorical_transformer,
            categorical_features
        )
    ]
)
baseline = DummyClassifier(
    strategy="most_frequent"
)

baseline.fit(
    X_train,
    y_train
)

baseline_predictions = baseline.predict(
    X_test
)
baseline_accuracy = accuracy_score(
    y_test,
    baseline_predictions
)

print(
    "Baseline Accuracy:",
    round(baseline_accuracy, 4)
)
logistic_model = Pipeline(
    steps=[
        (
            "preprocessor",
            preprocessor
        ),
        (
            "classifier",
            LogisticRegression(
                max_iter=1000
            )
        )
    ]
)
logistic_model.fit(
    X_train,
    y_train
)
logistic_predictions = logistic_model.predict(
    X_test
)

logistic_probabilities = (
    logistic_model.predict_proba(X_test)[:, 1]
)
logistic_accuracy = accuracy_score(
    y_test,
    logistic_predictions
)

logistic_precision = precision_score(
    y_test,
    logistic_predictions
)

logistic_recall = recall_score(
    y_test,
    logistic_predictions
)

logistic_f1 = f1_score(
    y_test,
    logistic_predictions
)

logistic_auc = roc_auc_score(
    y_test,
    logistic_probabilities
)

print("LOGISTIC REGRESSION")

print(
    "Accuracy:",
    round(logistic_accuracy, 4)
)

print(
    "Precision:",
    round(logistic_precision, 4)
)

print(
    "Recall:",
    round(logistic_recall, 4)
)

print(
    "F1 Score:",
    round(logistic_f1, 4)
)

print(
    "ROC-AUC:",
    round(logistic_auc, 4)
)
print(
    classification_report(
        y_test,
        logistic_predictions
    )
)
ConfusionMatrixDisplay.from_predictions(
    y_test,
    logistic_predictions,
    display_labels=[
        "Incomplete",
        "Complete"
    ]
)

plt.title(
    "Logistic Regression Confusion Matrix"
)

plt.tight_layout()
plt.show()
results = pd.DataFrame({
    "Model": [
        "Baseline",
        "Logistic Regression",
        "Random Forest"
    ],

    "Accuracy": [
        baseline_accuracy,
        logistic_accuracy,
        rf_accuracy
    ],

    "Precision": [
        np.nan,
        logistic_precision,
        rf_precision
    ],

    "Recall": [
        np.nan,
        logistic_recall,
        rf_recall
    ],

    "F1 Score": [
        np.nan,
        logistic_f1,
        rf_f1
    ],

    "ROC-AUC": [
        np.nan,
        logistic_auc,
        rf_auc
    ]
})

results.round(3)
accuracy_results = results[
    ["Model", "Accuracy"]
].set_index("Model")

plt.figure(figsize=(9, 5))

accuracy_results.plot(
    kind="bar",
    legend=False
)

plt.title("Model Accuracy Comparison")
plt.xlabel("Model")
plt.ylabel("Accuracy")
plt.xticks(rotation=0)

plt.tight_layout()
plt.show()
auc_results = results.dropna(
    subset=["ROC-AUC"]
)

plt.figure(figsize=(8, 5))

plt.bar(
    auc_results["Model"],
    auc_results["ROC-AUC"]
)

plt.title("ROC-AUC Comparison")
plt.xlabel("Model")
plt.ylabel("ROC-AUC")

plt.tight_layout()
plt.show()
plt.figure(figsize=(8, 6))

RocCurveDisplay.from_predictions(
    y_test,
    logistic_probabilities,
    name="Logistic Regression"
)

RocCurveDisplay.from_predictions(
    y_test,
    rf_probabilities,
    name="Random Forest"
)

plt.title("ROC Curves for NFL Pass Completion Models")

plt.tight_layout()
plt.show()
log_preprocessor = (
    logistic_model.named_steps[
        "preprocessor"
    ]
)

feature_names = (
    log_preprocessor
    .get_feature_names_out()
)

coefficients = (
    logistic_model
    .named_steps["classifier"]
    .coef_[0]
)

coefficient_table = pd.DataFrame({
    "Feature": feature_names,
    "Coefficient": coefficients
})

coefficient_table[
    "Absolute Coefficient"
] = coefficient_table[
    "Coefficient"
].abs()

coefficient_table = coefficient_table.sort_values(
    "Absolute Coefficient",
    ascending=False
)

coefficient_table.head(15)
top_coefficients = (
    coefficient_table
    .head(15)
    .sort_values("Coefficient")
)

plt.figure(figsize=(10, 7))

plt.barh(
    top_coefficients["Feature"],
    top_coefficients["Coefficient"]
)

plt.title(
    "Most Influential Logistic Regression Features"
)

plt.xlabel("Coefficient")

plt.tight_layout()
plt.show()
rf_preprocessor = (
    random_forest_model
    .named_steps["preprocessor"]
)

rf_feature_names = (
    rf_preprocessor
    .get_feature_names_out()
)

rf_importance = (
    random_forest_model
    .named_steps["classifier"]
    .feature_importances_
)

importance_table = pd.DataFrame({
    "Feature": rf_feature_names,
    "Importance": rf_importance
})

importance_table = (
    importance_table
    .sort_values(
        "Importance",
        ascending=False
    )
)

importance_table.head(15)
top_features = (
    importance_table
    .head(15)
    .sort_values("Importance")
)

plt.figure(figsize=(10, 7))

plt.barh(
    top_features["Feature"],
    top_features["Importance"]
)

plt.title(
    "Random Forest Feature Importance"
)

plt.xlabel("Feature Importance")

plt.tight_layout()
plt.show()
prediction_results = passes.loc[
    test_mask,
    [
        "game_id",
        "week",
        "posteam",
        "defteam",
        "passer_player_name",
        "air_yards",
        "down",
        "ydstogo",
        "complete_pass"
    ]
].copy()

prediction_results[
    "Predicted Completion"
] = rf_predictions

prediction_results[
    "Completion Probability"
] = rf_probabilities

prediction_results.head(20)
prediction_results[
    "Completion Probability"
] = (
    prediction_results[
        "Completion Probability"
    ] * 100
).round(1)

prediction_results.head(10)
errors = prediction_results[
    prediction_results[
        "complete_pass"
    ] !=
    prediction_results[
        "Predicted Completion"
    ]
].copy()

print(
    "Number of incorrect predictions:",
    len(errors)
)

errors.head(20)
false_positives = prediction_results[
    (prediction_results["complete_pass"] == 0) &
    (
        prediction_results[
            "Predicted Completion"
        ] == 1
    )
]

false_positives.head(10)
false_negatives = prediction_results[
    (prediction_results["complete_pass"] == 1) &
    (
        prediction_results[
            "Predicted Completion"
        ] == 0
    )
]

false_negatives.head(10)
surprising_completions = (
    prediction_results[
        prediction_results[
            "complete_pass"
        ] == 1
    ]
    .sort_values(
        "Completion Probability"
    )
)

surprising_completions.head(10)
surprising_incompletions = (
    prediction_results[
        prediction_results[
            "complete_pass"
        ] == 0
    ]
    .sort_values(
        "Completion Probability",
        ascending=False
    )
)

surprising_incompletions.head(10)
qb_stats = (
    passes
    .groupby("passer_player_name")
    .agg(
        Pass_Attempts=("complete_pass", "count"),
        Completions=("complete_pass", "sum"),
        Completion_Rate=("complete_pass", "mean")
    )
)

qb_stats[
    "Completion_Rate"
] = qb_stats[
    "Completion_Rate"
] * 100

qb_stats = qb_stats[
    qb_stats["Pass_Attempts"] >= 200
]

qb_stats = qb_stats.sort_values(
    "Completion_Rate",
    ascending=False
)

qb_stats.head(15)
top_qbs = qb_stats.head(15)

plt.figure(figsize=(10, 7))

plt.barh(
    top_qbs.index[::-1],
    top_qbs["Completion_Rate"][::-1]
)

plt.title(
    "Completion Percentage Among QBs With 200+ Attempts"
)

plt.xlabel("Completion Percentage")
plt.ylabel("Quarterback")

plt.tight_layout()
plt.show()
results.to_csv(
    "model_results.csv",
    index=False
)

importance_table.to_csv(
    "random_forest_feature_importance.csv",
    index=False
)

coefficient_table.to_csv(
    "logistic_regression_coefficients.csv",
    index=False
)

prediction_results.to_csv(
    "pass_predictions.csv",
    index=False
)

print("Files successfully saved.")
print("NFL PASS COMPLETION PROJECT")
print("-" * 40)

print(
    "Total pass attempts analyzed:",
    len(passes)
)

print(
    "Training plays:",
    len(X_train)
)

print(
    "Testing plays:",
    len(X_test)
)

print()

print(
    "Baseline Accuracy:",
    round(baseline_accuracy, 3)
)

print(
    "Logistic Regression Accuracy:",
    round(logistic_accuracy, 3)
)

print(
    "Random Forest Accuracy:",
    round(rf_accuracy, 3)
)

print()

print(
    "Logistic Regression ROC-AUC:",
    round(logistic_auc, 3)
)

print(
    "Random Forest ROC-AUC:",
    round(rf_auc, 3)
)
if rf_auc > logistic_auc:
    print(
        "Random Forest had the higher ROC-AUC."
    )

elif logistic_auc > rf_auc:
    print(
        "Logistic Regression had the higher ROC-AUC."
    )

else:
    print(
        "The models had the same ROC-AUC."
    )
# ==========================================
# NFL PASS COMPLETION MACHINE LEARNING MODEL
# ==========================================

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.impute import SimpleImputer

from sklearn.dummy import DummyClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier

from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    roc_auc_score,
    ConfusionMatrixDisplay
)


# ------------------------------------------
# 1. LOAD DATA
# ------------------------------------------

url = "https://github.com/nflverse/nflverse-data/releases/download/pbp/play_by_play_2021.parquet"

df = pd.read_parquet(url)

print("Original dataset:", df.shape)


# ------------------------------------------
# 2. CLEAN DATA
# ------------------------------------------

# Regular season only
df = df[df["season_type"] == "REG"].copy()

# Keep actual pass attempts
df = df[
    (df["pass_attempt"] == 1) &
    (df["sack"] == 0) &
    (df["qb_spike"] == 0)
].copy()

# Remove plays without a known pass result
df = df.dropna(subset=["complete_pass"])

# Remove duplicate plays
df = df.drop_duplicates(
    subset=["game_id", "play_id"]
)

print("Pass attempts after cleaning:", len(df))


# ------------------------------------------
# 3. TARGET DISTRIBUTION
# ------------------------------------------

print("\nCompletion Distribution:")

print(
    df["complete_pass"]
    .value_counts(normalize=True)
    .mul(100)
    .round(2)
)


# Simple visualization
df["complete_pass"].map({
    0: "Incomplete",
    1: "Complete"
}).value_counts().plot(
    kind="bar"
)

plt.title("NFL Pass Outcomes")
plt.xlabel("Pass Result")
plt.ylabel("Number of Passes")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()


# ------------------------------------------
# 4. SELECT FEATURES
# ------------------------------------------

numeric_features = [
    "air_yards",
    "ydstogo",
    "yardline_100",
    "game_seconds_remaining",
    "score_differential"
]

categorical_features = [
    "down",
    "qtr",
    "shotgun",
    "no_huddle",
    "pass_location",
    "pass_length"
]

features = numeric_features + categorical_features

X = df[features].copy()

y = df["complete_pass"].astype(int)


# ------------------------------------------
# 5. TRAIN / TEST SPLIT
# ------------------------------------------

# Earlier weeks = training
# Later weeks = testing

train = df["week"] <= 14
test = df["week"] >= 15

X_train = X.loc[train]
X_test = X.loc[test]

y_train = y.loc[train]
y_test = y.loc[test]

print("\nTraining plays:", len(X_train))
print("Testing plays:", len(X_test))


# ------------------------------------------
# 6. PREPROCESS DATA
# ------------------------------------------

numeric_process = Pipeline([
    (
        "missing",
        SimpleImputer(strategy="median")
    ),
    (
        "scale",
        StandardScaler()
    )
])

categorical_process = Pipeline([
    (
        "missing",
        SimpleImputer(strategy="most_frequent")
    ),
    (
        "encode",
        OneHotEncoder(handle_unknown="ignore")
    )
])

preprocessor = ColumnTransformer([
    (
        "numeric",
        numeric_process,
        numeric_features
    ),
    (
        "categorical",
        categorical_process,
        categorical_features
    )
])


# ------------------------------------------
# 7. BASELINE MODEL
# ------------------------------------------

baseline = DummyClassifier(
    strategy="most_frequent"
)

baseline.fit(
    X_train,
    y_train
)

baseline_predictions = baseline.predict(
    X_test
)

baseline_accuracy = accuracy_score(
    y_test,
    baseline_predictions
)


# ------------------------------------------
# 8. LOGISTIC REGRESSION
# ------------------------------------------

logistic = Pipeline([
    (
        "preprocessing",
        preprocessor
    ),
    (
        "model",
        LogisticRegression(
            max_iter=1000
        )
    )
])

logistic.fit(
    X_train,
    y_train
)

log_predictions = logistic.predict(
    X_test
)

log_probabilities = logistic.predict_proba(
    X_test
)[:, 1]


# ------------------------------------------
# 9. RANDOM FOREST
# ------------------------------------------

random_forest = Pipeline([
    (
        "preprocessing",
        preprocessor
    ),
    (
        "model",
        RandomForestClassifier(
            n_estimators=300,
            max_depth=10,
            min_samples_leaf=10,
            random_state=42,
            n_jobs=-1
        )
    )
])

random_forest.fit(
    X_train,
    y_train
)

rf_predictions = random_forest.predict(
    X_test
)

rf_probabilities = random_forest.predict_proba(
    X_test
)[:, 1]


# ------------------------------------------
# 10. MODEL EVALUATION FUNCTION
# ------------------------------------------

def evaluate_model(name, actual, predictions, probabilities=None):

    results = {
        "Model": name,
        "Accuracy": accuracy_score(
            actual,
            predictions
        ),
        "Precision": precision_score(
            actual,
            predictions,
            zero_division=0
        ),
        "Recall": recall_score(
            actual,
            predictions,
            zero_division=0
        ),
        "F1": f1_score(
            actual,
            predictions,
            zero_division=0
        )
    }

    if probabilities is not None:

        results["ROC-AUC"] = roc_auc_score(
            actual,
            probabilities
        )

    else:
        results["ROC-AUC"] = np.nan

    return results


# ------------------------------------------
# 11. COMPARE MODELS
# ------------------------------------------

results = pd.DataFrame([

    {
        "Model": "Baseline",
        "Accuracy": baseline_accuracy,
        "Precision": np.nan,
        "Recall": np.nan,
        "F1": np.nan,
        "ROC-AUC": np.nan
    },

    evaluate_model(
        "Logistic Regression",
        y_test,
        log_predictions,
        log_probabilities
    ),

    evaluate_model(
        "Random Forest",
        y_test,
        rf_predictions,
        rf_probabilities
    )
])

print("\nMODEL RESULTS")

print(
    results.round(3)
)


# ------------------------------------------
# 12. MODEL COMPARISON VISUALIZATION
# ------------------------------------------

results.set_index(
    "Model"
)["Accuracy"].plot(
    kind="bar"
)

plt.title("NFL Pass Completion Model Accuracy")
plt.ylabel("Accuracy")
plt.xlabel("Model")
plt.xticks(rotation=0)
plt.tight_layout()
plt.show()


# ------------------------------------------
# 13. RANDOM FOREST CONFUSION MATRIX
# ------------------------------------------

ConfusionMatrixDisplay.from_predictions(
    y_test,
    rf_predictions,
    display_labels=[
        "Incomplete",
        "Complete"
    ]
)

plt.title(
    "Random Forest Confusion Matrix"
)

plt.tight_layout()
plt.show()


# ------------------------------------------
# 14. FEATURE IMPORTANCE
# ------------------------------------------

feature_names = (
    random_forest
    .named_steps["preprocessing"]
    .get_feature_names_out()
)

importance = (
    random_forest
    .named_steps["model"]
    .feature_importances_
)

importance_df = pd.DataFrame({
    "Feature": feature_names,
    "Importance": importance
})

importance_df = importance_df.sort_values(
    "Importance",
    ascending=False
)

print("\nTOP FEATURES")

print(
    importance_df.head(10)
)


# Visualize top features

top_features = (
    importance_df
    .head(10)
    .sort_values("Importance")
)

plt.figure(figsize=(9, 6))

plt.barh(
    top_features["Feature"],
    top_features["Importance"]
)

plt.title(
    "Most Important Features for Predicting Pass Completion"
)

plt.xlabel("Feature Importance")

plt.tight_layout()
plt.show()


# ------------------------------------------
# 15. EXAMPLE PREDICTIONS
# ------------------------------------------

prediction_table = df.loc[
    test,
    [
        "week",
        "posteam",
        "defteam",
        "passer_player_name",
        "air_yards",
        "down",
        "ydstogo",
        "complete_pass"
    ]
].copy()

prediction_table[
    "Prediction"
] = rf_predictions

prediction_table[
    "Completion Probability"
] = (
    rf_probabilities * 100
).round(1)

print("\nEXAMPLE PREDICTIONS")

print(
    prediction_table.head(10)
)
