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

Click [HERE](/Users/joshpalmer/Downloads/Studio_2_Projects) to access my code for this project.
Click [HERE](url) to access my GitHub for this project.
