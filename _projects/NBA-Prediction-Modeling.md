---
layout: single
classes: wide
author_profile: true
title: NBA Prediction
excerpt: Using machine learning to predict the outcome of NBA games.
header:
  teaser: assets/images/teasers/nba_arena.jpg
categories:
  - Project
tags:
  - NBA
  - machine learning
  - statistics
---
![nba_arena]({{site.url}}/assets/images/teasers/nba_arena.jpg)

For a more detailed analysis, check out the full Github repo here: [NBA-Prediction-Analysis](https://github.com/luke-lite/NBA-Prediction-Modeling/){: .btn .btn--warning} You can even copy the notebook and run the code yourself.

## Project Goal

The purpose of this project is to create a machine learning model that can accurately predict the outcome of NBA games using boxscore statistics from the past 10 seasons. In order to accomplish this, I:

* built a web-scraper from scratch to collect data on over 12,000 NBA games
* aggregated and processed multiple datasets to prepare them for modeling
* evaluated and iterated upon the models to improve accuracy

## Project Summary
All individual models fell short of the target accuracy of 68%. The best machine learning model was a Gaussian Naive-Bayes model that was trained on averaged team statistics from the past 20 games that underwent Principal Component Anaylsis to reduce dimensionality. The model had an accuracy of 63.5%. I then tested an algorithmic approach by creating an Elo rating system, which was the best performing model with an accuracy of 65.3%. With access to additional data and improved data aggregation techniques, I believe it is possible to create an ensemble model that can beat the 68% threshold.

<!-- ## Table of Contents

- [Understanding the Data](#Understanding-the-Data)
- [Exploratory Data Analysis](#Exploratory-Data-Analysis)
- [Time Series Modeling](#Time-Series-Modeling)
- [Results and Recommendation](#Results-and-Recommendations)
- [Appendix](#Appendix) -->

## Data

## Modeling

## Results

## Next Steps
