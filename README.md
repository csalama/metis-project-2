# Betting Against the Spread - NBA Score Prediction

#### Status: Active

The initial iteration of this project was completed.  The current general goals of this project are as follows:

- Organize the code into more accessible python files
- Modify the analysis using a variety of regression methods
- Interpret the model using a wider variety of metrics
- Modify the data  to include a wider dataset or a different set of features
- Calculate the probability that a game will beat the spread using our chosen model
- Backtest our method to find the profits gained if this method is followed


#### Background

The goal of this project is to predict the score differential within any NBA game for the purpose of betting on NBA spreads.  The model uses the following two data sources:

- Weighted RAPTOR differential by team/season, where RAPTOR player scores are taken from [FiveThirtyEight](https://github.com/fivethirtyeight/data/tree/master/nba-raptor).
- NBA game data, including home and away teams, scores, and win ATS, as scraped from Oddsshark.com.

#### Method

Multiple models were separated into training and testing sets, and models were validated using 5-Fold Cross Validation including a simple linear regression and a 2-degree polynomial regression.  To correct for potential collinearity within the features, Ridge and Lasso regularization methods were used.  A Ridge regression model resulted in the highest $R^2$.

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
