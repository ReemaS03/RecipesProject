# Evaluating the Relationship Between the Amount of Protein and Average Rating of Recipes

Author: Reema 

## Overview

This is a data science project for DSC80 at UCSD that focuses on evaluating the relationship between the rating of a recipe and the proportion of protein in that recipe

## Introduction

Food is a huge part of our lives, as we spend a lot of time eating and cooking everyday. Also, many see eating or cooking as a hobby they enjoy. While some might be indifferent to the amount of protein in their food, some care about the amount of protein. As some see that a healthier recipe is the one with a high amount of protein. Considering that high protein in food could mean a healthier food, and better for you, I want to evaluate the relationship between the rating of a recipe and the proportion of protein in that recipe. **I wonder if people would rate a high-protein recipe higher due to the perceived health benefits of protein.**. To check this, I am going to use two datasets consisting of recipes and ratings from [food.com](https://www.food.com/) that was posted since 2008.

The first dataset, `recipe`, contains 83782 rows, which means we have 83782 unique recipes, with 10 columns recording the following information:

| Column             | Description                                                                                                                                                                                       |
| :----------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `'name'`           | Recipe name                                                                                                                                                                                       |
| `'id'`             | Recipe ID                                                                                                                                                                                         |
| `'minutes'`        | Minutes to prepare recipe                                                                                                                                                                         |
| `'contributor_id'` | User ID who submitted this recipe                                                                                                                                                                 |
| `'submitted'`      | Date recipe was submitted                                                                                                                                                                         |
| `'tags'`           | Food.com tags for recipe                                                                                                                                                                          |
| `'nutrition'`      | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| `'n_steps'`        | Number of steps in recipe                                                                                                                                                                         |
| `'steps'`          | Text for recipe steps, in order                                                                                                                                                                   |
| `'description'`    | User-provided description                                                                                                                                                                         |
| `'ingredients'`    | Text for recipe ingredients                                                                                                                                                                       |
| `'n_ingredients'`  | Number of ingredients in recipe                                                                                                                                                                   |

The second dataset is `interactions`, which consist of 731927 rows and each row is a review from the user on a specific recipe. The columns it includes are:

| Column        | Description         |
| :------------ | :------------------ |
| `'user_id'`   | User ID             |
| `'recipe_id'` | Recipe ID           |
| `'date'`      | Date of interaction |
| `'rating'`    | Rating given        |
| `'review'`    | Review text         |

**Given the datasets, I am evaluating whether people rate recipes with high-protein and recipes with low-protein on the same scale.** The most relevant columns to answer our question are `'calories(#)'`, which is the amount fo calories in a recipe, `'protein (PDV)'`, which is the amount of protein in a recipe in percent daily value, showing how much a nutrient in a serving of food contributes to the daily diet, `'prop_protein'`, which is the proportion of protein in terms of calories using the total calories of a  recipe, `'rating'`, which is the rating that a user left on a recipe, and `'average rating'`, which are the average of the ratings on each unique recipe.

By trying to analyze my question to find an answer, it can lead us to getting insights on what people prefer in terms of protein, which can help contribute websites such as Food.com to edit their recipes to be more in line with what people prefer.

## Data Cleaning and Exploratory Data Analysis




<iframe
  src="assets/fairness_analysis_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
