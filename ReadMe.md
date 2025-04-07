README: Soccer Match Analysis and Prediction Using a Bivariate Poisson Model

Overview

This project involves analyzing FIFA World Cup match data to model team performance and predict match outcomes. The approach combines data processing, exploratory analysis, and statistical modeling, with a particular focus on using a Bivariate Poisson model to estimate team scoring rates and match outcomes. The workflow includes dataset preparation, visualization, model training, evaluation, and ranking prediction.

1. Data Loading and Preprocessing

The script begins by importing relevant libraries such as pandas, numpy, matplotlib, and seaborn, followed by reading two datasets:

Match Data (matches.csv): Contains information on match results, team performances, and match outcomes.

FIFA Ranking Data (fifa_ranking-2024-06-20.csv): Includes historical FIFA rankings of various teams.

After loading the datasets, the script:

Filters only FIFA Men’s World Cup matches.

Selects relevant columns for analysis.

Converts match_date to a datetime format for chronological sorting and time-based computations.

Checks for missing values.

2. Exploratory Data Analysis (EDA)

Several visualizations provide insights into match outcomes and scoring trends:

Home vs Away Performance: A bar plot showing win distributions for home teams, away teams, and draws.

Total Goals Distribution: A histogram displaying the distribution of total goals per match.

Goals Trend Over Time: A line plot illustrating how the average number of goals per match has evolved over the years.

Germany's FIFA Ranking Over Time: A line chart depicting Germany's FIFA ranking progression.

These analyses help in understanding past trends and inform the modeling phase.

3. Data Splitting and Time Weight Calculation

The dataset is split into training (80%) and testing (20%) subsets, ensuring chronological order is maintained. A time-weighting function is applied to account for recency effects:

Older matches receive exponentially lower weights.

Time decay is modeled using a half-period of 390 days.

Weights are calculated separately for training and test data.

This ensures that recent matches have a stronger influence on the predictive model.

4. Bivariate Poisson Model for Match Prediction

The core statistical model in this project is a Bivariate Poisson model, which estimates goal distributions based on:

Team-specific home and away scoring rates.

A common dependency factor that accounts for goal correlations between teams.

4.1 Model Formulation

The likelihood function is implemented using Maximum Likelihood Estimation (MLE):

Each team has a home (\lambda_{home}) and away (\lambda_{away}) scoring rate.

A common dependency factor (\lambda_{common}) models shared goal tendencies.

The probability of a match outcome is computed using Poisson probability mass functions for home and away teams.

The likelihood function is weighted by the time decay factor.

4.2 Parameter Estimation

Using the training dataset, parameters are optimized via the L-BFGS-B method:

The optimization minimizes the negative log-likelihood of observed match outcomes.

Bounds are set to ensure positive values for all Poisson rates.

The final model provides optimized scoring rates for each team.

4.3 Match Outcome Prediction

Using the trained model, match outcomes are predicted for the test dataset:

Goal probability matrices are computed for each match.

The most likely scoreline is determined from the matrix.

Predictions are stored and analyzed.

5. Model Evaluation: Rank Probability Score (RPS)

To assess model performance, the Rank Probability Score (RPS) is computed:

RPS measures how well predicted probabilities align with actual match outcomes.

A lower RPS indicates better predictive accuracy.

The final mean RPS score is displayed as a summary metric.

6. Germany’s Ranking Calculation vs. Actual FIFA Rankings

A secondary analysis evaluates Germany's predicted FIFA rankings:

Calculation are based on match results and FIFA's 2006-2018 ranking formula.

Match importance, opponent strength, and confederation coefficients are considered.

The predicted rankings are compared with actual historical rankings.

A ranking progression plot visualizes the prediction accuracy, with a focus on Germany's 2014 World Cup performance.



Outputs:

home_away_performance_annotated.png: Home vs Away win distribution

Distribution of Total Goals per Match.png: Goal distribution plot

Average Goals per Match Over Years.png: Goal trend plot

germany_rank_progression.png: Germany’s FIFA ranking over time

germany_ranking_2014.png: Germany's ranking comparison during the 2014 World Cup

