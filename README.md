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

To make the analysis better, I performed the following steps to clean the data:

1. Left merge the recipes and interactions datasets on id and recipe_id.

   - This helps match the unique recipes with their rating and review, leaving us with one combined dataset instead of two dataset.

1. Check data types of all the columns.

   - This step helps ensure that the data types are appropriate for the dataset and our analysis, or if we need to conduct data type conversion.
   - | Column             | Description |
     | :----------------- | :---------- |
     | `'name'`           | object      |
     | `'id'`             | int64       |
     | `'minutes'`        | int64       |
     | `'contributor_id'` | int64       |
     | `'submitted'`      | object      |
     | `'tags'`           | object      |
     | `'nutrition'`      | object      |
     | `'n_steps'`        | int64       |
     | `'steps'`          | object      |
     | `'description'`    | object      |
     | `'ingredients'`    | object      |
     | `'n_ingredients'`  | int64       |
     | `'user_id'`        | float64     |
     | `'recipe_id'`      | float64     |
     | `'date'`           | object      |
     | `'rating'`         | float64     |
     | `'review'`         | object      |

1. Fill all ratings of 0 with np.nan.

   - We do this step because rating is usually on a scale from 1 to 5, 1 being the lowest rating and 5 being the highest rating. So, a rating of 0 means missing values in rating. So, to avoid bias in the ratings, it is better to fill the values of 0 with np.nan.

1. Add column `'average_rating'`, which contains the average rating per recipe.

   - As recipes have different rating from different users, taking an average of all the ratings could help get a better understanding of the rating of a given recipe.

1. Split values in the nutrition column to individual columns of floats.

   - Although the values in the nutrition column look like a list, they are not. They are objects that behave like strings. Looking back at the desciption of the columns, we can see what each value in the list mean. So, we can apply a function that split the values in columns and set their type to floats. This way we can perform calculations using those columns. 

1. Convert date and submitted to datetime.

   - Those two columns are stored as objects, but it is better to convert them to datetime as it allows to perform analysis on trends over time.

1. Add `'protein_category'` to the dataframe

   - `'protein_category'` is a column that contains "proteiny" or "non-proteiny" depending on if the proportion of protein in the recipe is above or below the average proportion of protein in the dataset. This help separate the recipes into two groups, ones that are high in protein and ones that are low in protein. 

1. Add `'prop_protein'` to the dataframe
   - prop_sugar is the proportion of protein of the total calories in a recipe. To calculate this, we use the values in the protein (PDV) column and multiply by 4 since there are 4 calories in 1 gram of protein. Afterward, we get the number of calories of protein, then divide by the total amount of calories in the recipe to get the proportion of protein of the total calories. This makes our analysis more efficent as we would have the values between 0 and 1 instead of risking hacing extremely large or small. 

#### Result
Here are all the columns of the cleaned df.


| Column                  | Description    |
| :---------------------- | :------------- |
| `'name'`                | object         |
| `'id'`                  | int64          |
| `'minutes'`             | int64          |
| `'contributor_id'`      | int64          |
| `'submitted'`           | datetime64[ns] |
| `'tags'`                | object         |
| `'nutrition'`           | object         |
| `'n_steps'`             | int64          |
| `'steps'`               | object         |
| `'description'`         | object         |
| `'ingredients'`         | object         |
| `'n_ingredients'`       | int64          |
| `'user_id'`             | float64        |
| `'recipe_id'`           | float64        |
| `'date'`                | datetime64[ns] |
| `'rating'`              | float64        |
| `'review'`              | object         |
| `'average rating'`      | object         |
| `'calories (#)'`        | float64        |
| `'total fat (PDV)'`     | float64        |
| `sugar (PDV)'`          | float64        |
| `'sodium (PDV)'`        | float64        |
| `'protein (PDV)'`       | float64        |
| `'saturated fat (PDV)'` | float64        |
| `'carbohydrates (PDV)'` | float64        |
| `'protein_category'`    | object         |
| `'prop_protein'`        | float64        |


<iframe
  src="assets/fairness_analysis_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
