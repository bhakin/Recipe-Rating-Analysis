# Analysis On What Factors Get A Recipe To Get A Good/Bad Rating

By Bhakin Phanakesiri

---
## Introduction

Nowadays, learning new cooking recipes is easy and accessible since all we have to do is go on the internet. However, picking a recipe may be challenging since there might be tons of good recipes for us to choose from. So to help us decide, we would look at the rating of each recipe and see which one has the highest rating. But you might ask, what makes this recipe have such a high rating compared to others? This is the question we are trying to answer by using the recipes and review data since the year 2008

### Introduction to the Dataset

The recipe dataset contains 83782 recipes(rows) with 12 columns. Here is what the dataset looks like: 

|Column	                 |Description|
|---                     |---        |
|`'name'`                |Recipe name|
|`'id'`                  |Recipe ID|
|`'minutes'`             |Minutes to prepare recipe|
|`'contributor_id'`      |User ID who submitted this recipe|
|`'submitted'`           |Date recipe was submitted|
|`'tags'`                |Food.com tags for recipe|
|`'nutrition'`           |Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV)carbohydrates (PDV)]; PDV stands for “percentage of daily value”|
|`'n_steps'`             |Number of steps in recipe|
|`'steps'`               |Text for recipe steps, in order|
|`'description'`         |User-provided description|
|`'ingredients'`         |Ingredients needed for the recipe|
|`'n_ingredients'`       |Number of Ingredients|

\
The review dataset contains 731927 reviews(rows) with 5 columns. Here is what the dataset looks like:

|Column	                 |Description|
|---                     |---        |
|`'user_id'`             |User ID|
|`'recipe_id'`           |Recipe ID|
|`'date'`                |Date of interaction|
|`'rating'`              |Rating given|
|`'review'`              |Review text|


## Data Cleaning and Exploratory Data Analysis
### Data Cleaning

Now that we got our two dataset, we need to clean our data so we need to merge them so that all of the information are in the same dataset





