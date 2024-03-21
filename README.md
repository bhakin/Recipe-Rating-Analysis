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

---

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning

Now that we got our two dataset, we need to clean our data in order for us to analyze them. This were the steps I took to clean them: \
1) **Converting data into correct types** - This is important because it allows us to perform tests and provide more accturate representation of the data. So I converted the `'submitted'` and `'dates'` column to `'datetime'`. \
2) **Assigning data to the correct columns** - The `'nutrition'`  column contains mutiple nutrition information on a recipe, so to make it easy to differentiate what nutrition it is referring to, I created `'calories (#)'`, `'total fat (PDV)'`, `'sugar (PDV)'`, `'sodium (PDV)'`, `'protein (PDV)'`, `'saturated fat (PDV)'`, `'carbohydrates (PDV)'` column. \
3) **Filling in the null values** - Both recipe and review dataset contain missing values, so in order to not run into errors or wrong outcome, I filled in those values with 0, i.e `'review'` has a lot of missing data, so I filled in 0 for those values. \
4) **Creating an `'avg_rating'` column** - Since we are analyzing the ratings of the recipe, I created an addition column, named `'avg_rating'` which tells us the average rating of each recipe. This is necessary since it will help us understand the rating of each recipe better. \
5) **Merging the two dataset** - I merged the review dataset with the recipe dataset. Merging the two dataset together helps analyzing them better since I don't have to go back and forth between the two dataset. \

### Exploratory Data Analysis





