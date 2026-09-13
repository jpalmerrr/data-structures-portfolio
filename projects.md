# Projects
This section documents my data science projects, research questions, and data stories I create throughout the semesters.
---
## Project 1
Research Question: How does home-field advantage affect the performance of the Charlotte 49ers football team?

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

Data from the College Football Data API was processed using Python and pandas to isolate completed Charlotte 49ers games and eliminate selection bias. To preserve a strict comparison of home versus away performance, neutral-site matchups and records with missing critical values (e.g., scores, location, Elo ratings) were excluded.Feature Engineering & FormattingThe finalized dataset was engineered with the following engineered features to support statistical modeling:is_home: A binary indicator mapping venue designation (\(1\) = Home, \(0\) = Away).win: A binary target outcome variable (\(1\) = Charlotte Victory, \(0\) = Loss).point_differential: Calculated as \(\text{Score}_{\text{Charlotte}} - \text{Score}_{\text{Opponent}}\).elo_differential: The difference between Charlotte’s and their opponent's pregame Elo ratings, serving as a control variable for relative team strength.
