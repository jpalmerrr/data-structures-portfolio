import requests

API_KEY = "jJ3Pyhrf9pdrilfP2fCCP5l+RLSS5nJAmgMNNMZdCG7vUp92TNMeF7WyWazm3rny"

url = "https://api.collegefootballdata.com/games"

headers = {
    "Authorization": f"Bearer {API_KEY}"
}

params = {
    "year": 2025,
    "team": "Charlotte"
}

response = requests.get(url, headers=headers, params=params)

print(response.status_code)
print(response.json())

[{'id': 401761589, 'season': 2025, 'week': 1, 'seasonType': 'regular', 'startDate': '2025-08-29T23:00:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': True, 'conferenceGame': False, 'attendance': 35718, 'venueId': 3628, 'venue': 'Bank of America Stadium', 'homeId': 2429, 'homeTeam': 'Charlotte', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 11, 'homeLineScores': [3, 0, 0, 8], 'homePostgameWinProbability': 0.042695220559835434, 'homePregameElo': 1254, 'homePostgameElo': 1221, 'awayId': 2026, 'awayTeam': 'App State', 'awayClassification': 'fbs', 'awayConference': 'Sun Belt', 'awayPoints': 34, 'awayLineScores': [0, 17, 10, 7], 'awayPostgameWinProbability': 0.9573047794401646, 'awayPregameElo': 1428, 'awayPostgameElo': 1461, 'excitementIndex': 3.6672300484451488, 'highlights': '', 'notes': 'Duke’s Mayo Classic', 'playoff': None}, {'id': 401754527, 'season': 2025, 'week': 2, 'seasonType': 'regular', 'startDate': '2025-09-06T23:00:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': False, 'attendance': 19233, 'venueId': 4418, 'venue': 'Jerry Richardson Stadium', 'homeId': 2429, 'homeTeam': 'Charlotte', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 3, 'homeLineScores': [0, 3, 0, 0], 'homePostgameWinProbability': 0, 'homePregameElo': 1221, 'homePostgameElo': 1200, 'awayId': 153, 'awayTeam': 'North Carolina', 'awayClassification': 'fbs', 'awayConference': 'ACC', 'awayPoints': 20, 'awayLineScores': [10, 7, 0, 3], 'awayPostgameWinProbability': 1, 'awayPregameElo': 1417, 'awayPostgameElo': 1438, 'excitementIndex': 3.333886477580821, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762464, 'season': 2025, 'week': 3, 'seasonType': 'regular', 'startDate': '2025-09-13T22:00:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': False, 'attendance': 15681, 'venueId': 4418, 'venue': 'Jerry Richardson Stadium', 'homeId': 2429, 'homeTeam': 'Charlotte', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 42, 'homeLineScores': [0, 7, 21, 14], 'homePostgameWinProbability': 1, 'homePregameElo': 1170, 'homePostgameElo': 1170, 'awayId': 2405, 'awayTeam': 'Monmouth', 'awayClassification': 'fcs', 'awayConference': 'Coastal Athletic', 'awayPoints': 35, 'awayLineScores': [7, 7, 7, 14], 'awayPostgameWinProbability': 0, 'awayPregameElo': None, 'awayPostgameElo': None, 'excitementIndex': 8.551218092966522, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762468, 'season': 2025, 'week': 4, 'seasonType': 'regular', 'startDate': '2025-09-18T23:30:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': True, 'attendance': 13397, 'venueId': 4418, 'venue': 'Jerry Richardson Stadium', 'homeId': 2429, 'homeTeam': 'Charlotte', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 17, 'homeLineScores': [3, 6, 0, 8], 'homePostgameWinProbability': 0.13469073176383972, 'homePregameElo': 1200, 'homePostgameElo': 1183, 'awayId': 242, 'awayTeam': 'Rice', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 28, 'awayLineScores': [7, 7, 7, 7], 'awayPostgameWinProbability': 0.8653092682361603, 'awayPregameElo': 1271, 'awayPostgameElo': 1288, 'excitementIndex': 4.3486835794294665, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762475, 'season': 2025, 'week': 6, 'seasonType': 'regular', 'startDate': '2025-10-03T23:00:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': True, 'attendance': 34577, 'venueId': 3886, 'venue': 'Raymond James Stadium', 'homeId': 58, 'homeTeam': 'South Florida', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 54, 'homeLineScores': [23, 10, 0, 21], 'homePostgameWinProbability': 0.961682915687561, 'homePregameElo': 1482, 'homePostgameElo': 1521, 'awayId': 2429, 'awayTeam': 'Charlotte', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 26, 'awayLineScores': [0, 7, 3, 16], 'awayPostgameWinProbability': 0.038317084312438965, 'awayPregameElo': 1183, 'awayPostgameElo': 1144, 'excitementIndex': 3.245227656426531, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762483, 'season': 2025, 'week': 7, 'seasonType': 'regular', 'startDate': '2025-10-11T16:00:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': True, 'attendance': 31172, 'venueId': 3841, 'venue': 'Michie Stadium', 'homeId': 349, 'homeTeam': 'Army', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 24, 'homeLineScores': [7, 10, 7, 0], 'homePostgameWinProbability': 0.990699827671051, 'homePregameElo': 1551, 'homePostgameElo': 1552, 'awayId': 2429, 'awayTeam': 'Charlotte', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 7, 'awayLineScores': [0, 0, 0, 7], 'awayPostgameWinProbability': 0.009300172328948975, 'awayPregameElo': 1144, 'awayPostgameElo': 1143, 'excitementIndex': 2.926749973897242, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762489, 'season': 2025, 'week': 8, 'seasonType': 'regular', 'startDate': '2025-10-18T19:30:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': True, 'attendance': 13618, 'venueId': 4418, 'venue': 'Jerry Richardson Stadium', 'homeId': 2429, 'homeTeam': 'Charlotte', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 14, 'homeLineScores': [7, 0, 0, 7], 'homePostgameWinProbability': 0.0009986907243728638, 'homePregameElo': 1143, 'homePostgameElo': 1054, 'awayId': 218, 'awayTeam': 'Temple', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 49, 'awayLineScores': [7, 21, 21, 0], 'awayPostgameWinProbability': 0.9990013092756271, 'awayPregameElo': 1241, 'awayPostgameElo': 1330, 'excitementIndex': 3.3193001555565673, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762492, 'season': 2025, 'week': 9, 'seasonType': 'regular', 'startDate': '2025-10-24T23:00:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': True, 'attendance': 9626, 'venueId': 4418, 'venue': 'Jerry Richardson Stadium', 'homeId': 2429, 'homeTeam': 'Charlotte', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 20, 'homeLineScores': [10, 7, 3, 0], 'homePostgameWinProbability': 0.20414631068706512, 'homePregameElo': 1054, 'homePostgameElo': 1028, 'awayId': 249, 'awayTeam': 'North Texas', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 54, 'awayLineScores': [7, 10, 10, 27], 'awayPostgameWinProbability': 0.7958536893129349, 'awayPregameElo': 1648, 'awayPostgameElo': 1674, 'excitementIndex': 5.201038363476169, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762504, 'season': 2025, 'week': 11, 'seasonType': 'regular', 'startDate': '2025-11-08T20:00:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': True, 'attendance': 39096, 'venueId': 3699, 'venue': 'Dowdy-Ficklen Stadium', 'homeId': 151, 'homeTeam': 'East Carolina', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 48, 'homeLineScores': [21, 14, 10, 3], 'homePostgameWinProbability': 0.9722951054573059, 'homePregameElo': 1591, 'homePostgameElo': 1599, 'awayId': 2429, 'awayTeam': 'Charlotte', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 22, 'awayLineScores': [0, 14, 8, 0], 'awayPostgameWinProbability': 0.027704894542694092, 'awayPregameElo': 1028, 'awayPostgameElo': 1020, 'excitementIndex': 3.048260088986414, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762507, 'season': 2025, 'week': 12, 'seasonType': 'regular', 'startDate': '2025-11-15T17:00:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': True, 'attendance': 9831, 'venueId': 4418, 'venue': 'Jerry Richardson Stadium', 'homeId': 2429, 'homeTeam': 'Charlotte', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 7, 'homeLineScores': [0, 0, 0, 7], 'homePostgameWinProbability': 0.008371274918317795, 'homePregameElo': 1020, 'homePostgameElo': 1013, 'awayId': 2636, 'awayTeam': 'UTSA', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 28, 'awayLineScores': [7, 0, 7, 14], 'awayPostgameWinProbability': 0.9916287250816822, 'awayPregameElo': 1465, 'awayPostgameElo': 1472, 'excitementIndex': 3.426061002724206, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401752776, 'season': 2025, 'week': 13, 'seasonType': 'regular', 'startDate': '2025-11-22T17:45:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': False, 'attendance': 93033, 'venueId': 3917, 'venue': 'Sanford Stadium', 'homeId': 61, 'homeTeam': 'Georgia', 'homeClassification': 'fbs', 'homeConference': 'SEC', 'homePoints': 35, 'homeLineScores': [14, 14, 7, 0], 'homePostgameWinProbability': 0.9921115636825562, 'homePregameElo': 2070, 'homePostgameElo': 2048, 'awayId': 2429, 'awayTeam': 'Charlotte', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 3, 'awayLineScores': [0, 3, 0, 0], 'awayPostgameWinProbability': 0.007888436317443848, 'awayPregameElo': 1013, 'awayPostgameElo': 1035, 'excitementIndex': 2.676535798551931, 'highlights': '', 'notes': None, 'playoff': None}, {'id': 401762518, 'season': 2025, 'week': 14, 'seasonType': 'regular', 'startDate': '2025-11-30T00:30:00.000Z', 'startTimeTBD': False, 'completed': True, 'neutralSite': False, 'conferenceGame': True, 'attendance': 22245, 'venueId': 4729, 'venue': 'Yulman Stadium', 'homeId': 2655, 'homeTeam': 'Tulane', 'homeClassification': 'fbs', 'homeConference': 'American Athletic', 'homePoints': 27, 'homeLineScores': [14, 7, 0, 6], 'homePostgameWinProbability': 0.976479172706604, 'homePregameElo': 1575, 'homePostgameElo': 1587, 'awayId': 2429, 'awayTeam': 'Charlotte', 'awayClassification': 'fbs', 'awayConference': 'American Athletic', 'awayPoints': 0, 'awayLineScores': [0, 0, 0, 0], 'awayPostgameWinProbability': 0.023520827293395996, 'awayPregameElo': 1035, 'awayPostgameElo': 1023, 'excitementIndex': 2.8879023551198375, 'highlights': '', 'notes': None, 'playoff': None}]

import requests
import pandas as pd
import matplotlib.pyplot as plt

### 1. Get Charlotte Football Game Data

API_KEY = "jJ3Pyhrf9pdrilfP2fCCP5l+RLSS5nJAmgMNNMZdCG7vUp92TNMeF7WyWazm3rny"

url = "https://api.collegefootballdata.com/games"

headers = {
    "Authorization": f"Bearer {API_KEY}"
}

params = {
    "year": 2025,
    "team": "Charlotte"
}

response = requests.get(
    url,
    headers=headers,
    params=params
)

print("Status Code:", response.status_code)

Turn API response into a pandas DataFrame
data = response.json()
df = pd.DataFrame(data)

Check the data
print(df.head())
print("\nColumns:")
print(df.columns)


### 2. Clean the Data
  
###Remove games that do not have final scores
df = df.dropna(
    subset=["homePoints", "awayPoints"]
).copy()

### Determine whether Charlotte played Home or Away
df["Location"] = df.apply(
    lambda row: "Home"
    if row["homeTeam"] == "Charlotte"
    else "Away",
    axis=1
)

### Determine Charlotte's score
df["Charlotte Points"] = df.apply(
    lambda row: row["homePoints"]
    if row["homeTeam"] == "Charlotte"
    else row["awayPoints"],
    axis=1
)

### Determine opponent's score
df["Opponent Points"] = df.apply(
    lambda row: row["awayPoints"]
    if row["homeTeam"] == "Charlotte"
    else row["homePoints"],
    axis=1
)

### Calculate point differential
df["Point Differential"] = (
    df["Charlotte Points"] -
    df["Opponent Points"]
)

### Create Win variable
### 1 = Win
### 0 = Loss
df["Win"] = (
    df["Point Differential"] > 0
).astype(int)


### 3. View Cleaned Data

print("\nCleaned Data:")

print(
    df[
        [
            "homeTeam",
            "awayTeam",
            "Location",
            "Charlotte Points",
            "Opponent Points",
            "Point Differential",
            "Win"
        ]
    ]
)


### 4. Visualization 1:
### Home vs. Away Win Percentage

win_percentage = (
    df.groupby("Location")["Win"]
    .mean() * 100
)

print("\nWin Percentage:")
print(win_percentage)


plt.figure(figsize=(8, 5))

plt.bar(
    win_percentage.index,
    win_percentage.values
)

plt.title(
    "Charlotte Win Percentage: Home vs. Away"
)

plt.xlabel(
    "Game Location"
)

plt.ylabel(
    "Charlotte Win Percentage (%)"
)

plt.ylim(0, 100)

### Add percentage labels
for i, value in enumerate(win_percentage.values):
    plt.text(
        i,
        value + 2,
        f"{value:.1f}%",
        ha="center"
    )

plt.show()


### 5. Visualization 2:
### Point Differential by Location


### Calculate average point differential
point_difference = (
    df.groupby("Location")["Point Differential"]
    .mean()
)

print("\nAverage Point Differential:")
print(point_difference)


plt.figure(figsize=(8, 5))

plt.bar(
    point_difference.index,
    point_difference.values
)

plt.title(
    "Charlotte Average Point Differential: Home vs. Away"
)

plt.xlabel(
    "Game Location"
)

plt.ylabel(
    "Average Point Differential"
)

### Add values above bars
for i, value in enumerate(point_difference.values):
    plt.text(
        i,
        value + 1,
        f"{value:.1f}",
        ha="center"
    )

plt.axhline(
    0,
    linestyle="--"
)

plt.show()

Status Code: 200
          id  season  week seasonType                 startDate  startTimeTBD  \
0  401761589    2025     1    regular  2025-08-29T23:00:00.000Z         False   
1  401754527    2025     2    regular  2025-09-06T23:00:00.000Z         False   
2  401762464    2025     3    regular  2025-09-13T22:00:00.000Z         False   
3  401762468    2025     4    regular  2025-09-18T23:30:00.000Z         False   
4  401762475    2025     6    regular  2025-10-03T23:00:00.000Z         False   

   completed  neutralSite  conferenceGame  attendance  ...     awayConference  \
0       True         True           False       35718  ...           Sun Belt   
1       True        False           False       19233  ...                ACC   
2       True        False           False       15681  ...   Coastal Athletic   
3       True        False            True       13397  ...  American Athletic   
4       True        False            True       34577  ...  American Athletic   

  awayPoints  awayLineScores awayPostgameWinProbability awayPregameElo  \
0         34  [0, 17, 10, 7]                   0.957305         1428.0   
1         20   [10, 7, 0, 3]                   1.000000         1417.0   
2         35   [7, 7, 7, 14]                   0.000000            NaN   
3         28    [7, 7, 7, 7]                   0.865309         1271.0   
4         26   [0, 7, 3, 16]                   0.038317         1183.0   

  awayPostgameElo  excitementIndex highlights                notes  playoff  
0          1461.0         3.667230             Duke’s Mayo Classic     None  
1          1438.0         3.333886                            None     None  
...
Location
Away     0.000000
Home    14.285714
Name: Win, dtype: float64

<img width="702" height="474" alt="Screenshot 2026-09-13 at 4 31 30 PM" src="https://github.com/user-attachments/assets/d93e1405-b0ef-4a8c-9eb0-bc122d3dc698" />

Average Point Differential:
Location
Away   -26.000000
Home   -19.142857
Name: Point Differential, dtype: float64

<img width="708" height="475" alt="Screenshot 2026-09-13 at 4 31 56 PM" src="https://github.com/user-attachments/assets/3fecbf0c-38d3-4492-9248-3e88766bf400" />

