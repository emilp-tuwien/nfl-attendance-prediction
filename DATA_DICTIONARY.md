# DATA_DICTIONARY.md

## Dataset Descriptions

---

### `attendance_df` (from `attendance.csv`)

| Variable           | Class     | Description                                                         |
|--------------------|-----------|---------------------------------------------------------------------|
| team               | character | Team City                                                          |
| team_name          | character | Team name                                                          |
| year               | integer   | Season year                                                        |
| total              | double    | Total attendance across 17 weeks (1 week = no game)                |
| home               | double    | Home attendance                                                    |
| away               | double    | Away attendance                                                    |
| week               | character | Week number (1–17)                                                 |
| weekly_attendance  | double    | Weekly attendance number                                           |

---

### `standings_df` (from `standings.csv`)

| Variable               | Class     | Description                                                                                      |
|------------------------|-----------|--------------------------------------------------------------------------------------------------|
| team                   | character | Team city                                                                                        |
| team_name              | character | Team name                                                                                        |
| year                   | integer   | Season year                                                                                      |
| wins                   | double    | Wins (0–16)                                                                                      |
| loss                   | double    | Losses (0–16)                                                                                    |
| points_for             | double    | Points scored (offensive performance)                                                            |
| points_against         | double    | Points allowed (defensive performance)                                                           |
| points_differential    | double    | Point differential (points_for – points_against)                                                 |
| margin_of_victory      | double    | (Points scored – points allowed) / Games played                                                  |
| strength_of_schedule   | double    | Average quality of opponents (SRS)                                                               |
| simple_rating          | double    | Team quality relative to average (SRS = margin_of_victory + strength_of_schedule)                |
| offensive_ranking      | double    | Team offense quality relative to average (SRS)                                                   |
| defensive_ranking      | double    | Team defense quality relative to average (SRS)                                                   |
| playoffs               | character | Made playoffs (“Yes”/“No”)                                                                       |
| sb_winner              | character | Won Super Bowl (“Yes”/“No”)                                                                      |

---

### `games_df` (from `games.csv`)

| Variable           | Class     | Description                                     |
|--------------------|-----------|-------------------------------------------------|
| year               | integer   | Season year (note: playoff games still counted in previous season)  |
| week               | character | Week number (1–17, plus playoffs)               |
| home_team          | character | Home team code                                 |
| away_team          | character | Away team code                                 |
| winner             | character | Winning team code                             |
| tie                | character | Losing team if a tie                           |
| day                | character | Day of the week                                |
| date               | character | Date (MM-DD)                                   |
| time               | character | Game start time (HH:MM AM/PM)                  |
| pts_win            | double    | Points scored by winning team                  |
| pts_loss           | double    | Points scored by losing team                   |
| yds_win            | double    | Yards gained by winning team                   |
| turnovers_win      | double    | Turnovers by winning team                      |
| yds_loss           | double    | Yards gained by losing team                    |
| turnovers_loss     | double    | Turnovers by losing team                       |
| home_team_name     | character | Home team full name                            |
| home_team_city     | character | Home team city                                 |
| away_team_name     | character | Away team full name                            |
| away_team_city     | character | Away team city                                 |

---

### `merged_df` (cleaned merge, before encoding & scaling)

| Column Name                   | Description                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| `team_name_home`              | Name of the home team                                                     |
| `team_name_away`              | Name of the away team                                                     |
| `year`                        | Year the game was played                                                  |
| `week`                        | Week of the season (1–17 regular season)                                  |
| `weekly_attendance_home`      | **Target variable** – Number of attendees at the home game                |
| `points_for_home`             | Total points scored by the home team throughout the season                |
| `points_against_home`         | Total points allowed by the home team throughout the season               |
| `points_differential_home`    | Point differential for the home team across the season                    |
| `simple_rating_home`          | Home team’s overall performance rating (SRS)                              |
| `margin_of_victory_home`      | Average margin of victory for the home team                               |
| `wins_home`                   | Total wins by the home team                                               |
| `offensive_ranking_home`      | Offensive performance rank of the home team                               |
| `defensive_ranking_home`      | Defensive performance rank of the home team                               |
| `points_for_away`             | Total points scored by the away team throughout the season                |
| `points_against_away`         | Total points allowed by the away team throughout the season               |
| `points_differential_away`    | Point differential for the away team across the season                    |
| `simple_rating_away`          | Away team’s overall performance rating                                    |
| `wins_away`                   | Total wins by the away team                                               |
| `offensive_ranking_away`      | Offensive performance rank of the away team                               |
| `defensive_ranking_away`      | Defensive performance rank of the away team                               |

---
