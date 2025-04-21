---
layout: default
title: Predicting Calories from Online Recipes
---

## Introduction

This project analyzes the **Recipes and Ratings** dataset to explore how recipe characteristics (e.g. prep time, ingredient count) influence **calories**. We aim to build a regression model that predicts calorie content based solely on features a user would see before cooking.

**Name:** Alyssa Rodriguez  
**Email:** alyssa@umich.edu  

---

## Data Cleaning and Exploratory Data Analysis

### Histogram of Calories

<iframe
  src="assets/calories_hist.html"
  width="800"
  height="500"
  frameborder="0">
</iframe>

This plot shows that most recipes fall between 100–800 kcal, but there are some very high outliers.

### Calories vs. Prep Time

<iframe
  src="assets/calories_vs_minutes.html"
  width="800"
  height="500"
  frameborder="0">
</iframe>

Longer cook times correlate with slightly higher calories. Many high-calorie recipes are desserts or stews with long simmering durations.

### Interesting Aggregates Table

<iframe
  src="assets/calorie_table.html"
  width="600"
  height="300"
  frameborder="0">
</iframe>

Here we group recipes by number of ingredients and show average calories — more ingredients tends to mean more calories.

---

## Framing a Prediction Problem

We treat this as a **regression** problem: calories are a continuous value with meaningful differences (e.g., 300 vs 900 kcal).  
**Target Variable:** `calories`  
**Metric:** RMSE (Root Mean Squared Error)  
We only use features that are known at “time of prediction” — prep time, ingredient count, tag length, etc.

---

## Baseline Model

- **Features Used:** `minutes`, `n_steps`, `n_ingredients`, `tag_count`, `step_length_avg`
- **Model:** Linear Regression
- **Baseline RMSE:** 664 kcal

---

## Final Model

- **New Features:** `minutes_per_step`, `ingredient_density`
- **Model:** Random Forest + hyperparameter tuning (`max_depth`, `n_estimators`, `min_samples_split`)
- **Final RMSE:** 512 kcal

### Predicted vs. Actual Scatterplot

<iframe
  src="assets/pred_vs_actual.html"
  width="800"
  height="500"
  frameborder="0">
</iframe>

---

## Key Takeaways

- Recipes with more ingredients and longer descriptions tend to have higher calorie counts.
- A basic model using time and step count gives decent estimates, but adding smart features improves results by ~23%.
- The tool can help users quickly gauge nutritional impact without logging into food tracking apps.
