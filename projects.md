# Projects
This section documents my data science projects, research questions, and data stories I create throughout the semesters.
---
## Project 1
Research Question: How does home-field advantage affect the performance of the Charlotte 49ers football team in 2025?

Context: Home-field advantage is a well-documented phenomenon in sports, including college football. Previous research has found that college football teams tend to perform better at home, even after accounting for differences in team strength. For example, Wang et al. (2011) estimated a home advantage of approximately six points for home teams after controlling for team ability and other factors. More recent research has continued to find evidence of home-field advantage in American football while showing that its size can vary across levels and time periods.

For this project, I will focus specifically on the Charlotte 49ers and compare their performance in home and away games. This will allow me to determine whether Charlotte has a measurable home-field advantage and whether the difference remains after considering the strength of its opponents.

Planned Data Source: College Football Data (CFBD) API - https://collegefootballdata.com/key

### Conceptualization and Operationalization of Variables

| Variable               | Concept                                                   | Operationalization                                                         |
| ---------------------- | --------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Game Location**      | Where the game is played                                  | Categorical variable: **Home**, **Away**, or potentially **Neutral**       |
| **Win/Loss**           | Game outcome                                              | Binary variable: **1 = Charlotte win, 0 = Charlotte loss**                 |
| **Point Differential** | How well Charlotte performed relative to its opponent     | Charlotte points − opponent points                                         |
| **Win Probability**    | Estimated likelihood of winning based on game information | CFBD's postgame win probability                                            |
| **Opponent Strength**  | Relative quality of Charlotte's opponent                  | Opponent's pregame Elo rating compared with Charlotte's pregame Elo rating |
| **Season**             | Time period of the game                                   | Season/year from CFBD                                                      |
| **Opponent**           | Team Charlotte played                                     | Opposing team's name                                                       |

Main Independent Variable: Game Location is the primary independent variable. I will compare Charlotte's results when playing at home versus playing away.

Main Dependent Variable: The primary outcome will be whether Charlotte won the game. I will also examine point differential as a secondary measure of performance.

Control Variable: Opponent strength will be included because Charlotte could have a different schedule at home than on the road. Controlling for opponent strength makes the comparison more meaningful because a higher home winning percentage could otherwise simply reflect playing weaker teams at home.

CFBD's game data includes both teams' pregame Elo ratings, which makes this a useful measure for controlling for opponent strength.

### Planned Data Cleaning and Preparation

I first used Python to request Charlotte's 2025 game data from the CFBD API. I then converted the API's JSON response into a pandas DataFrame.

I checked the columns and first few rows to understand the data. I also removed games that did not have final scores because those games could not be used to calculate wins or point differential.

Next, I created new variables for game location, Charlotte's points, opponent points, point differential, and win/loss. These variables made the original API data easier to analyze.

I chose point differential because it gives more information than just looking at wins and losses. For example, winning by one point and winning by 30 points are both wins, but point differential shows the difference in how the team performed.

### Visualizations

Visualization 1: Home vs. Away Win Percentage

<img width="702" height="474" alt="Screenshot 2026-09-13 at 4 31 30 PM" src="https://github.com/user-attachments/assets/4fc8e103-3940-4409-8dba-4ccf6017d91a" />

Type: Bar chart

X-axis: Game Location
Y-axis: Charlotte Win Percentage (%)
Bars: Home and Away

Purpose: Directly answers your research question by showing whether Charlotte wins a greater percentage of games at home.

Example description for your writeup:

The first visualization compares Charlotte's winning percentage in home and away games. This graph directly measures the primary outcome of the research question. If Charlotte's home winning percentage is substantially higher than its away winning percentage, this would provide descriptive evidence of a home-field advantage.

Visualization 2: Point Differential by Location and Opponent Strength

<img width="708" height="475" alt="Screenshot 2026-09-13 at 4 31 56 PM" src="https://github.com/user-attachments/assets/9cda3b31-a371-4ec1-a56b-2e5d9afaf5a7" />

Type: Scatter plot

X-axis: Opponent Elo Difference
Y-axis: Charlotte Point Differential
Different groups: Home vs. Away

Purpose: Shows whether Charlotte's performance changes based on both location and opponent strength.

Example description:

The second visualization examines the relationship between opponent strength and Charlotte's point differential. By separating home and away games, the visualization helps determine whether Charlotte performs differently depending on where the game is played after accounting for differences in opponent strength.

This is stronger than simply making two graphs that both show home vs. away because it brings your opponent-strength variable into the analysis.

### Ethics and Limitations

There are some limitations to my analysis. First, I am only looking at Charlotte's 2025 games, so one season may not represent how the team normally performs. Charlotte could have had an unusually easy or difficult schedule during this season.

Another limitation is that my current data does not account for the strength of each opponent. If Charlotte played stronger teams away from home, this could make its away record look worse even if location was not the main reason.

There are also other factors that could affect the results, such as injuries, weather, attendance, coaching, travel, and the quality of the team during that season.

Because of these limitations, my analysis can show a relationship between location and performance, but it cannot prove that playing at home directly causes Charlotte to perform better.

### Code and AI Transparency
#### Code Transparency

I used Python, pandas, Matplotlib, and the College Football Data API for this project. My complete code will be included in my Jupyter Notebook or GitHub repository so that the data cleaning and graphs can be viewed.

#### AI Usage Disclosure

I used ChatGPT to help me understand Python code, organize my project, and create ideas for my visualizations and written explanations. I reviewed the code and made sure I understood how it worked. I am responsible for checking the results and finalizing the analysis.

### Code Review

I will have my code reviewed by an instructor or TA. I will ask them to look at my API code, data cleaning, variables, and visualizations. I will make any necessary changes based on their feedback.

### Academic References

Wang, W., Johnston, R., & Jones, K. (2011). Home advantage in American college football games: A multilevel modelling approach. Journal of Quantitative Analysis in Sports, 7(3). https://doi.org/10.2202/1559-0410.1328

Fullagar, H. H. K., Delaney, J., Duffield, R., & Murray, A. (2019). Factors influencing home advantage in American collegiate football. Science and Medicine in Football, 3(2), 163–168. https://doi.org/10.1080/24733938.2018.1524581

Pollard, R., & Gómez, M. A. (2015). Comparison of home advantage in college and professional team sports in the United States. Collegium Antropologicum, 39(3), 583–589.

### Simple Overall Project Summary

My research question is: **How does home-field advantage affect the performance of the Charlotte 49ers football team in 2025?** I will use 2025 Charlotte football data from the College Football Data API to compare the team's performance in home and away games. My main variables are game location, wins and losses, Charlotte's points, opponent points, and point differential. I will use two graphs to compare home and away performance. The first graph will show Charlotte's win percentage at home versus away, while the second will compare average point differential. The goal is to determine whether Charlotte performs better when playing at home.

Click [HERE](code.md) to access my code for this project.

Click [HERE](https://github.com/jpalmerrr/data-structures-portfolio) to access my GitHub for this project.

---

## Project 2

# Predicting NFL Pass Completions Using Machine Learning

## Project Overview

Football statistics such as completion percentage are useful for evaluating quarterbacks, but they do not account for how difficult each individual throw is. A short pass behind the line of scrimmage and a deep pass downfield both count equally as either a completion or an incompletion, even though the difficulty of those throws can be very different.

For this project, I will use NFL play-by-play data and machine learning to investigate whether characteristics of a pass and the game situation can predict whether the pass will be completed. The overall goal is to develop and compare classification models that estimate the probability of an NFL pass being completed.

---

# 1. Problem Definition

## Research Question

**Can machine learning predict whether an NFL pass attempt will be completed based on characteristics of the pass and game situation?**

The prediction problem is determining whether an NFL pass attempt will result in a completion or an incompletion.

## Target Variable

My target variable is:

**`complete_pass`**

The variable will be measured as:

* `1` = completed pass
* `0` = pass was not completed

Because the outcome contains two categories, this is a **binary classification problem**.

## Primary Model

The model I am primarily using to answer my research question is **Logistic Regression**.

Logistic Regression is appropriate because my dependent variable has two possible outcomes: complete or incomplete. It also allows me to examine coefficients to understand how different game and pass characteristics affect the estimated probability of a completion.

## Second Model

The second model I will use is a **Random Forest Classifier**.

Random Forest is appropriate because football plays may contain nonlinear and more complicated relationships that Logistic Regression may not capture. For example, the influence of air yards may depend on the down, field position, or yards needed for a first down.

## Who Could Benefit From This Model?

NFL teams, football analysts, coaches, scouts, broadcasters, and researchers could potentially benefit from this type of model.

Rather than evaluating quarterbacks strictly through raw completion percentage, a completion-probability model can help provide more context about the difficulty of the throws they attempt.

## Why This Problem Matters

Traditional completion percentage treats every pass equally even though not every pass has the same level of difficulty.

The NFL has developed its own Completion Probability metric for this reason. NFL Next Gen Stats uses machine learning and tracking information to estimate how likely a pass is to be completed given the circumstances surrounding the throw.

My project explores whether publicly available play-by-play data can also be used to make useful predictions about pass completion.

---

# 2. Background and Context

Machine learning is becoming increasingly important in football analytics because it allows analysts to evaluate plays beyond traditional box-score statistics.

The NFL's Completion Probability model estimates the likelihood that a pass will be completed using information about the difficulty of the throw. Factors used by the NFL include air distance, air yards, receiver separation, pass-rush separation, quarterback speed, and time to throw.

One limitation of my project is that many of those variables come from proprietary NFL player-tracking data. My project instead investigates how much prediction can be accomplished using publicly available game and play information.

Previous academic work also shows that publicly available NFL play-by-play data can support advanced statistical modeling. Yurko, Ventura, and Horowitz used public NFL play-by-play information to develop reproducible models for expected points, win probability, and player evaluation.

This research supports the idea that open NFL data can be used to develop meaningful football analytics models.

---

# 3. Data Description

## Data Source

The dataset for this project comes from the **nflverse NFL play-by-play database**.

nflverse provides publicly available NFL play-by-play information that can be loaded in formats including CSV and Parquet.

For this project, I am using the **2021 NFL season**.

The complete 2021 nflverse dataset contains approximately:

**49,922 plays and 372 variables.**

## Unit of Analysis

Each row in the original dataset represents an individual NFL play.

After cleaning and filtering the data, each observation in my machine-learning dataset will represent **one NFL pass attempt**.

Running plays, punts, field goals, kickoffs, sacks, quarterback spikes, and other non-pass observations will not be used in the final model.

## Key Variables

My target variable is:

**`complete_pass`**

My primary predictor variables are:

| Variable                 | Meaning                                                     |
| ------------------------ | ----------------------------------------------------------- |
| `air_yards`              | Distance the pass travels relative to the line of scrimmage |
| `ydstogo`                | Yards needed to earn a first down                           |
| `down`                   | Current offensive down                                      |
| `yardline_100`           | Distance from the opponent's end zone                       |
| `qtr`                    | Quarter of the game                                         |
| `game_seconds_remaining` | Number of seconds remaining in the game                     |
| `score_differential`     | Offensive team's score advantage or deficit                 |
| `shotgun`                | Whether the offense is using a shotgun formation            |
| `no_huddle`              | Whether the offense is operating without a huddle           |
| `pass_location`          | Whether the pass is directed left, middle, or right         |
| `pass_length`            | Whether the pass is classified as short or deep             |

The nflverse documentation contains definitions for 372 different play-by-play variables.

---

# 4. Conceptualization and Operationalization

## Complete Pass

**Conceptualization:** A successful forward pass in which an eligible offensive receiver catches the ball.

**Operationalization:** `complete_pass = 1` represents a completion and `complete_pass = 0` represents a pass that was not completed.

## Air Yards

**Conceptualization:** The distance the football travels downfield before reaching the intended receiver.

**Operationalization:** Measured using the numerical `air_yards` variable contained in nflverse.

## Yards to Go

**Conceptualization:** The distance the offense needs to gain to earn a new set of downs.

**Operationalization:** Measured using `ydstogo`.

## Down

**Conceptualization:** The offensive attempt within the team's current series of downs.

**Operationalization:** Measured numerically from first through fourth down.

## Field Position

**Conceptualization:** Where the offense is located relative to the opponent's end zone.

**Operationalization:** Measured using `yardline_100`, which represents yards from the opponent's end zone.

## Game Time Remaining

**Conceptualization:** How much regulation game time remains when the play begins.

**Operationalization:** Measured in seconds using `game_seconds_remaining`.

## Score Differential

**Conceptualization:** Whether the offensive team is winning, losing, or tied at the time of the play.

**Operationalization:** Measured using the numerical difference between the offense's score and its opponent's score.

## Shotgun Formation

**Conceptualization:** Whether the quarterback receives the snap from a shotgun position.

**Operationalization:** Treated as a binary variable, where 1 represents shotgun and 0 represents another formation.

## No-Huddle Offense

**Conceptualization:** Whether the offense begins the play without using a traditional huddle.

**Operationalization:** Treated as a binary variable.

## Pass Location

**Conceptualization:** The horizontal area of the field toward which the pass is thrown.

**Operationalization:** Categorized as left, middle, or right.

## Pass Length

**Conceptualization:** A general classification of the depth of the pass.

**Operationalization:** Categorized by nflverse as either short or deep.

---

# 5. Data Understanding and Exploration

Before training machine-learning models, I will explore the data to understand its structure and identify important patterns.

I will calculate descriptive statistics including the mean, median, standard deviation, minimum, maximum, and quartiles for numerical variables such as air yards, yards to go, field position, score differential, and game time remaining.

One important step will be examining the distribution of the target variable. If completions occur much more frequently than incompletions, the dataset will contain some class imbalance.

This is important because a model could achieve relatively high accuracy by simply predicting the most common outcome.

## Visualizations

The main exploratory visualizations for the project will include:

1. **Completed vs. Incomplete Passes**
   This visualization will show the distribution of my target variable and help identify class imbalance.

2. **Distribution of Air Yards**
   This histogram will show how pass depth is distributed and identify unusually short or deep throws.

3. **Completion Percentage by Pass Distance**
   Pass attempts will be grouped into air-yard ranges to determine whether completion percentage changes as throws become deeper.

4. **Completion Percentage by Down**
   This visualization will examine whether completion rates differ on first, second, third, and fourth down.

5. **Completion Percentage by Pass Location**
   This chart will compare passes thrown to the left, middle, and right areas of the field.

6. **Completion Percentage by Yards to Go**
   This chart will examine whether passes become more difficult in longer-distance situations.

Based on football knowledge and previous research, I expect pass distance to have a meaningful relationship with completion probability. NFL Next Gen Stats has found that the probability of completion generally decreases as the distance of a throw increases.

However, my final conclusions will be based on the results from my own dataset rather than assuming this relationship beforehand.

---

# 6. Data Preparation and Feature Selection

## Filtering

I will first limit the dataset to regular-season games.

I will then keep only plays identified as pass attempts while removing sacks and quarterback spikes.

Observations without a known value for `complete_pass` will be removed because the model cannot be trained without knowing the actual outcome.

## Duplicate Observations

Potential duplicate plays will be checked using the combination of:

**`game_id` + `play_id`**

These fields identify individual plays within the dataset.

Any true duplicate observations will be removed before modeling.

## Missing Values

I will calculate both the number and percentage of missing observations for every feature selected for the model.

For numerical predictors, missing observations will be handled using **median imputation**.

For categorical predictors, missing observations will be replaced with the **most frequent category**.

This preprocessing will occur inside a machine-learning pipeline so that information from the test dataset is not used when preparing the training dataset.

## Feature Selection

The numerical features selected are:

`air_yards`, `ydstogo`, `yardline_100`, `game_seconds_remaining`, and `score_differential`.

The categorical features selected are:

`down`, `qtr`, `shotgun`, `no_huddle`, `pass_location`, and `pass_length`.

These variables were selected because they describe the circumstances surrounding the pass without directly revealing what happened after the pass was thrown.

## Data Leakage

Avoiding data leakage is especially important for this project.

I will intentionally exclude variables such as:

`yards_gained`, `epa`, `success`, `touchdown`, `first_down`, `interception`, and `cpoe`.

These variables contain information that becomes known during or after the play. Allowing the model to use these variables could make its performance appear artificially strong because it would indirectly know the outcome it is supposed to predict.

## Encoding

Categorical variables such as pass location and pass length will be converted into machine-readable values using **one-hot encoding**.

## Scaling

Numerical features will be standardized for Logistic Regression using `StandardScaler`.

Random Forest does not require feature scaling, but preprocessing the features consistently allows the two models to be compared through the same workflow.

---

# 7. Training and Testing Strategy

Instead of randomly splitting plays throughout the season, I will use a **chronological train/test split**.

Plays from approximately **Weeks 1–14** will be used for training, while plays from **Weeks 15–18** will be reserved for testing.

This strategy is appropriate because it more closely represents a real-world forecasting situation. The model learns from football games that have already happened and is then evaluated on later games it has never seen.

The test dataset will not be used during model training or preprocessing.

This helps reduce the possibility of data leakage and provides a more realistic evaluation of model performance.

---

# 8. Baseline and Model Development

## Baseline Model

Before evaluating machine-learning models, I will establish a baseline using a **Dummy Classifier**.

The baseline will predict the most common outcome for every play.

For example, if completed passes are the majority outcome, the baseline will predict that every pass is completed.

A useful machine-learning model should outperform this simple strategy or provide significantly better discrimination between completions and incompletions.

## Model 1: Logistic Regression

My first machine-learning model is Logistic Regression.

Logistic Regression is useful because it predicts probabilities for binary outcomes and provides interpretable coefficients.

This model will help answer both whether pass completions can be predicted and which characteristics are associated with increases or decreases in completion probability.

## Model 2: Random Forest

My second machine-learning model is Random Forest.

Random Forest combines many decision trees and is capable of identifying nonlinear relationships and interactions among variables.

This may be beneficial because the effect of one football variable may depend on other game conditions.

For example, a 15-yard pass on first-and-10 may have a different level of difficulty than a 15-yard pass on fourth-and-15.

## Model Comparison

Both models will use the same training and testing observations and the same pre-play predictor information.

This ensures that their results can be compared fairly.

---

# 9. Model Evaluation and Selection

My models will be evaluated using several different measures rather than accuracy alone.

## Accuracy

Accuracy measures the percentage of all predictions that are correct.

## Precision

Precision measures how frequently passes predicted as completions are actually completed.

## Recall

Recall measures how many actual completed passes the model correctly identifies.

## F1 Score

F1 combines precision and recall into a single measure.

## ROC-AUC

ROC-AUC measures how effectively the model separates completed passes from incomplete passes across different probability thresholds.

A model with an ROC-AUC closer to 1 demonstrates stronger ability to distinguish between the two classes.

## Confusion Matrix

I will also create a confusion matrix for each model.

The confusion matrix will show:

* Correctly predicted completions
* Correctly predicted incompletions
* False positives
* False negatives

### Model Results

The final results table will compare:

| Model               |  Accuracy | Precision |    Recall |  F1 Score |   ROC-AUC |
| ------------------- | --------: | --------: | --------: | --------: | --------: |
| Baseline            | Run model |         — |         — |         — |         — |
| Logistic Regression | Run model | Run model | Run model | Run model | Run model |
| Random Forest       | Run model | Run model | Run model | Run model | Run model |

I will select my final model based primarily on performance on the unseen test set, particularly ROC-AUC and F1 score, while also considering interpretability.

**These numbers should only be filled in after running the Python notebook. I will not report invented model results.**

---

# 10. Model Interpretation and Insights

Once the models have been trained, I will examine what they learned about pass completion.

For Logistic Regression, I will examine the model's coefficients.

Positive coefficients indicate variables associated with a higher estimated probability of completion, while negative coefficients indicate variables associated with a lower probability.

For Random Forest, I will examine **feature importance** to identify which variables contribute the most to predictions.

I expect air yards to be important based on existing football analytics research, but the final conclusion will depend on my actual model output.

I will also conduct error analysis by examining individual false-positive and false-negative predictions.

A **false positive** occurs when the model predicts that a pass will be completed but the pass is actually incomplete.

A **false negative** occurs when the model predicts an incompletion but the pass is actually completed.

Examining these errors could reveal circumstances that the model has difficulty capturing.

---

# 11. Example Predictions

For the final Random Forest model, I will create an output table showing individual pass attempts.

The table will include:

| Quarterback  |    Air Yards |         Down |  Yards to Go | Actual Result | Model Prediction | Completion Probability |
| ------------ | -----------: | -----------: | -----------: | ------------- | ---------------- | ---------------------: |
| From dataset | From dataset | From dataset | From dataset | From dataset  | From model       |             From model |

This will make the machine-learning results easier for a nontechnical reader to understand.

For example, the model might determine that a certain throw has a 75% probability of being completed. If the pass is actually incomplete, that observation could become an interesting example for error analysis.

---

# 12. Limitations, Ethics, and Reflection

The largest limitation of this project is that traditional NFL play-by-play data cannot capture everything that happens on the field.

Important variables that are unavailable include detailed measurements of:

* Receiver separation
* Defensive coverage
* Pass-rush pressure
* Route design
* Quarterback movement
* Player speed
* Exact location of defenders
* Pass placement

NFL Next Gen Stats uses player-tracking information for several of these factors in its own Completion Probability model.

Because my dataset does not include all of these factors, two passes that appear similar in the play-by-play dataset may actually have very different levels of difficulty.

## Potential Bias

Different quarterbacks play in different offensive systems and attempt different types of passes.

For example, one quarterback may regularly attempt short, high-percentage throws while another quarterback may be asked to throw farther downfield.

A model that does not fully capture these differences could unfairly evaluate certain players.

## Consequences of Incorrect Predictions

Incorrect predictions would have limited consequences in an academic project.

However, if a similar model were used by NFL organizations for scouting, coaching, contract evaluation, or personnel decisions, inaccurate predictions could affect how players are evaluated.

For this reason, a model like this should be considered one piece of information rather than a replacement for coaches, scouts, or film analysis.

## Real-World Use

I would not recommend using this model as the sole method for evaluating quarterbacks or receivers.

Football performance depends on many variables that are not captured in traditional play-by-play information.

The model is better viewed as an analytical tool for adding context to football performance.

## Future Improvements

A stronger future version of the project could add NFL player-tracking information such as receiver separation, quarterback pressure, defender distance, quarterback movement, and time to throw.

I could also test additional machine-learning methods such as Gradient Boosting or XGBoost and compare them with Logistic Regression and Random Forest.

Hyperparameter tuning and cross-validation could also improve model performance.

---

# 13. Main Visualizations for the Portfolio

For the final portfolio page, I will focus on visualizations that tell a clear story rather than displaying every graph created during analysis.

The most important figures will be:

**Pass Outcome Distribution** — shows completed versus incomplete passes.

**Completion Percentage by Pass Distance** — demonstrates how passing depth relates to completion rate.

**Completion Percentage by Down** — examines differences based on game situation.

**Model Performance Comparison** — compares the baseline, Logistic Regression, and Random Forest.

**Confusion Matrix** — shows where my final model predicts correctly and incorrectly.

**Feature Importance** — identifies the variables that have the largest influence on the final Random Forest model.

Together, these visualizations move from understanding the data to evaluating the models and finally interpreting what the selected model learned.

---

# 14. Project Code Summary

The Python workflow for this project follows these stages:

**Data Loading → Data Cleaning → Exploratory Analysis → Feature Selection → Preprocessing → Train/Test Split → Baseline Model → Logistic Regression → Random Forest → Model Evaluation → Model Interpretation**

The code loads the 2021 nflverse dataset, filters it to legitimate pass attempts, handles missing information, encodes categorical variables, scales numerical features, trains two classification models, compares their performance, creates confusion matrices, and examines feature importance.

The complete code will be available through my GitHub repository.

**GitHub Repository:**
[INSERT MY GITHUB PROJECT LINK HERE]

---

# 15. Questions I Still Have

As I complete the modeling portion of this project, I still want to determine which predictors have the strongest relationship with pass completion.

I also want to determine whether Random Forest provides a meaningful improvement over Logistic Regression or whether the simpler and more interpretable Logistic Regression model performs similarly.

Another question is how much predictive performance is lost because public play-by-play information does not contain detailed player-tracking variables such as receiver separation and pass-rush pressure.

---

# 16. Conclusion

This project examines whether publicly available NFL play-by-play information can be used to predict whether a pass will be completed.

Using the nflverse dataset, I will compare Logistic Regression and Random Forest models using variables describing pass depth, down, yards to go, field position, game situation, formation, and pass location.

The project goes beyond simply trying to achieve the highest possible accuracy. It also focuses on understanding what characteristics influence completion probability, evaluating where the models make mistakes, avoiding data leakage, and recognizing the limitations of using publicly available football data.

Ultimately, the project demonstrates how machine learning can be applied to a real sports analytics question while also showing why predictive models should be interpreted carefully.

---

# References

NFL Next Gen Stats Analytics Team. (2018). *Introduction to Completion Probability.* National Football League. The NFL describes Completion Probability as a machine-learning approach for contextualizing the difficulty of individual throws using play and player-tracking information.

nflverse. (2026). *nflreadr: Download nflverse Data.* The nflverse documentation provides access to NFL play-by-play data and documentation for its variables.

nflverse. (2026). *Data Dictionary: Play by Play.* The play-by-play dictionary documents the variables available in the nflverse dataset.

Yurko, R., Ventura, S., & Horowitz, M. (2018). *nflWAR: A reproducible method for offensive player evaluation in football.* The authors demonstrate how publicly available NFL play-by-play data can support reproducible football analytics and statistical modeling.

---

# AI Usage Disclosure

I used **OpenAI ChatGPT (GPT-5.6)** as a support tool during this project. I used ChatGPT to help brainstorm and refine the research question, identify relevant variables, organize the project structure, explain machine-learning concepts, assist with Python code development and troubleshooting, and improve the clarity of written explanations.

I reviewed the generated material and made the final decisions regarding my research question, feature selection, data preparation, modeling strategy, model evaluation, and interpretation. Final numerical results and conclusions will be based on the output of my own Python analysis rather than generated or assumed results.

Click [HERE](code2.md) to access my code for this project.

Click [HERE]() to access the visuals for this project.

Click [HERE](https://github.com/jpalmerrr/data-structures-portfolio) to access my GitHub for this project.
