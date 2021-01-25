# Betting Against the Spread - NBA Score Prediction

#### Background

The goal of this project is to predict the score differential within any NBA game for the purpose of betting on NBA spreads.  The model uses the following two data sources:

- Weighted RAPTOR differential by team/season, where RAPTOR player scores are taken from [FiveThirtyEight](https://github.com/fivethirtyeight/data/tree/master/nba-raptor).
- NBA game data, including home and away teams, scores, and win ATS, as scraped from Oddsshark.com.

#### Model

The following is the primary model of interest:
$$
Score\_Diff = \alpha + \beta_1Value\_Diff + \beta_2Last\_N\_ATS\_Diff + \beta_3Season+ \beta_4 ATL + \beta_5 BOS +...+\beta_{33}WAS
$$

- $Score\_Diff$: Difference between home and away scores within a game
- $Value\_Diff$: Difference between home and away weighted wins above replacement (as described by [FiveThirtyEight](https://fivethirtyeight.com/features/how-our-raptor-metric-works/)). The weighted average of wins above replacement by minutes played was taken to given a team's "value" within a season.
- $Last\_N\_ATS\_Diff$: Difference between the Last $N$ wins against the spread for the home and away teams.  $N = 5$ by default, but can be edited within data_import.
- $Season$: Season year.  Seasons 2017-2021 were used for this analysis.
- $ATL,...,WAS$: Dummy variables for the team playing the game.  Equal to 1 if the team is home, -1 if the team is away, and 0 if the team didn't play in this game.

#### Method

Multiple models were separated into training and testing sets, and models were validated using 5-Fold Cross Validation including a simple linear regression and a 2-degree polynomial regression.  To correct for potential colinearity within the features, Ridge and Lasso regularization methods were used.  A Ridge regression model resulted in the highest $R^2$.

Different models for each season were also considered as an option, but $R^2$ within the test data signified over-fitting.

#### File Descriptions

**Jupyter Notebooks**

- data_import: Scrapes oddsshark.com pages using BeautifulSoup, and creates clean tables for seasons 2017-2021 saved within the season_data folder.
- main_analysis: Merges together all NBA game data scraped from data_import.ipynb, performs the described regression analysis, and creates multiple descriptive graphs.

**input-data**

- latest_RAPTOR_by_team: FiveThirtyEight RAPTOR scores within 2021.
- modern_RAPTOR_by_team: FiveThirtyEight RAPTOR scores from 2014 - 2020.
- aggregate-modern_RAPTOR_by_team: Aggregation of latest_RAPTOR_by_team and modern_RAPTOR_by_team.
- nba_abbr_map.csv: Map used to convert between different NBA team name abbreviations.

**season-data**

- nba_spreads_*: Output files of data_import for seasons 2017-2021.

**Presentation**

- betting_against_the_spread-presentation: Deck for the presentation given within Metis.





