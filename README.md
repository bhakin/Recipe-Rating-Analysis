# Analysis On What Factors Get A Recipe To Get A Good/Bad Rating

By Bhakin Phanakesiri

---
## Introduction

Nowadays, learning new cooking recipes is easy and accessible since all we have to do is go on the internet. However, picking a recipe may be challenging since there might be tons of good recipes for us to choose from. So to help us decide, we would look at the rating of each recipe and see which one has the highest rating. But you might ask, **what makes this recipe have such a high rating compared to others?** This is the question we are trying to answer by using the recipes and review data since the year 2008.

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
1) **Converting data into correct types** - This is important because it allows us to perform tests and provide more accurate representation of the data. So I converted the `'submitted'` and `'dates'` column to `'datetime'`. \
2) **Assigning data to the correct columns** - The `'nutrition'`  column contains mutiple nutrition information on a recipe, so to make it easy to differentiate what nutrition it is referring to, I created `'calories (#)'`, `'total fat (PDV)'`, `'sugar (PDV)'`, `'sodium (PDV)'`, `'protein (PDV)'`, `'saturated fat (PDV)'`, `'carbohydrates (PDV)'` columns. \
3) **Filling in the null values** - Both recipe and review dataset contain missing values, so in order to not run into errors or wrong outcome, I filled in those values with 0, i.e `'review'` and `'rating'` has a lot of missing data, so I filled in 0 for those values. \
4) **Creating an `'avg_rating'` column** - Since we are analyzing the ratings of the recipe, I created an addition column, named `'avg_rating'` which tells us the average rating of each recipe. This is necessary since it will help us understand the rating of each recipe better which is vital for my test. \
5) **Merging the two dataframes** - I merged the review dataframe with the recipe dataframe. Merging the two dataframe together helps me analyzing them better since I don't have to go back and forth between the two dataframes. |
6) **Dropping irrelevant columns** - This helps keeping the dataframe small despite the merge and gets rid of the unnecessary information. 

After clearning my data, this is what the new **dataframe** looks like (this is the first five rows of the new dataframe):

| name | id | &nbsp;minutes&nbsp; | &nbsp;n_steps&nbsp;| &nbsp;n_ingredients&nbsp; | &nbsp;calories (#)&nbsp; | &nbsp;total fat (PDV)&nbsp; | &nbsp;sugar (PDV)&nbsp; | &nbsp;sodium (PDV)&nbsp; | &nbsp;protein (PDV)&nbsp; | &nbsp;saturated fat (PDV)&nbsp;| &nbsp;carbohydrate (PDV)&nbsp; | &nbsp;rating&nbsp; | &nbsp;avg_rating&nbsp; | 
|------|----|---------|---------|---------------|-------------|----------------|------------|-------------|--------------|-------------------|-------------------|-------|------------|
|1 brownies in the world    best ever |333281 |40 |10 |9 |138.4 |10.0 |50.0 |3.0 |3.0 |19.0 |6.0 |4 |4.0 |
|1 in canada chocolate chip cookies |453467 |45 |12 |11 |595.1 |46.0 |211.0 |22.0 |13.0 |51.0 |26.0 |5 |5.0 |
|412 broccoli casserole    |306168   |40  |6  |9  |194.8   |20.0   |6.0   |32.0   |22.0   |   36.0   |3.0    |5   |5.0   |
|412 broccoli casserole    |306168   |40  |6  |9  |194.8   |20.0   |6.0   |32.0   |22.0   |   36.0   |3.0    |5   |5.0   |
|412 broccoli casserole    |306168   |40  |6  |9  |194.8   |20.0   |6.0   |32.0   |22.0   |   36.0   |3.0    |5   |5.0   |

### Exploratory Data Analysis

Now that we cleaned our data, we can start visualizing what the data we have look like. 

#### Univariate Analysis

This figure below is the distribution of `'rating'` from our dataset. This figure represents the amount of time each rating is given to the recipe. We can see that there are over 160,000 recipes that have 5 ratings and less than 3000 recipes have a rating 1 or a rating 2. Moreover, it shows to us that there about 15,000 recipes that did not get a rating which is why it is 0.

<iframe
  src="assets/rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Bivariate Analysis

This figure below is the distributions of `'minutes'` in log and`'avg_rating'` from our dataset. The reason why I **log(minutes)** is because the data was too big so it was hard to visualize what was going on. Based on the figure, we can see that most of the data are located in the **bottom right of the figure.** This shows us that recipe that takes a short amount of time tend to have a **higher** average rating (around 4 - 5).

<iframe
  src="assets/log_mins.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


#### Interesting Aggregates

Now, let's see if the rating of a recipe has some connections with the amount of steps:

| rating | max_n_steps | mean_n_steps | median_n_steps | min_n_steps | count_nsteps |
|--------|-------------|--------------|----------------|-------------|--------------|
| 0      | 93.0        |11.270968     |9.0             |1.0          |15035.0       |
| 1      | 55.0        |10.629965     |9.0             |1.0          |2870.0        |
| 2      | 61.0        |10.697635     |9.0             |1.0          |2368.0        |
| 3      | 88.0        |9.992052      |9.0             |1.0          |7172.0        |
| 4      | 88.0        |9.577425      |9.0             |1.0          |37307.0       |
| 5      | 100.0       |9.984901      |9.0             |1.0          |169676.0      |



Based on this pivot table, we can see that there are some connections between `'rating'` and `'n_steps'`. If we look at the mean of each n_step, it tells us that a large n_steps tends to have a lower rating than a small n_steps. However, if we look at the max column, we can see that the rating 5 has a max of 100 steps whereas the rating 1 has only 55 steps, but the mean for rating 5 is smaller than the mean for rating 1. This implies that the 100 may have been an outlier. 

---

## Assessment Missingness

As mentioned in the **Data Cleaning**, there are values in our dataset that are missing so in this section, I will evaluate and test why those values are missing. 

### NMAR Analysis

In the dataset, the most missing values are from the `'rating'` column with over 15,000 recipes and this is possibly due to NMAR (Not Missing At Random). This is because some people might choose not to rate the recipe if they don't feel strongly aganist or for the recipe so they would leave it blank. Additionally, people might just forget to rate a recipe after they finish making it because it is not something they are required to do. Both of these points are the reasons why `'rating'` might be NMAR.  

However, if we want the missingness of `'rating'` to be MAR (Missing At Random), we could add another column where people would say **Good** if the recipe was good, **Meh** if the recipe was so so, and **Bad** if the recipe was bad. Having this column would show that whether the missingess of `'rating'` is dependent on this new column, making this MAR instead of NMAR.

### Missingness Dependency

Now, I will test the dependency of the missingness of `'rating'`. To do this, I will perform a permutation test 1000 times to test the dependency of `'rating'` on `'carbohydrates (PDV)'` and `'n_steps'` 

**Rating and Carbohydrates (PDV)**

**Null Hypothesis**: The missingness of `'rating'` **does NOT depends on** `'carbohydrates (PDV)'`
**Alternative Hypothesis**: The missingness of `'rating'` **does depends on** `'carbohydrates (PDV)'`  
**Test Statistic** : Difference in Means \
**Significance Level**: 0.05

<iframe
  src="assets/emp_missing1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

From the figure above, the **p-value = 0.184.** Since the significance level is 0.05 then the p-value is larger the significance level because 0.184 > 0.05. Therefore, I **fail to reject** the null hypothesis. This means that the missingness of `'rating'` **does not depends on** `'carbohydrates (PDV)'` which shows that this missingness is **MCAR (Missing at Completely At Random).**

**Rating and Number of Steps**

**Null Hypothesis**: The missingness of `'rating'` **does NOT depends on** `'n_steps'` \
**Alternative Hypothesis**: The missingness of `'rating'` **does depends on** `'n_steps'`  
**Test Statistic** : Difference in Means \
**Significance Level**: 0.05

<iframe
  src="assets/emp_missing2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

From the figure above, the **p-value = 0.0**. Since the significane level is 0.5 then the p-value is smaller than the significance level because 0.0 < 0.05. Therefore, I **reject** the null hypothesis. This means that the missingness of `'rating'` **does depends on** `'n_steps'` which shows that this missingness is **MAR (Missing At Random).**

---

## Hypothesis Testing

In the **Bivariate Analysis** section, we looked at the distributions between `'avg_rating'` and `'minutes'` and noticed that there might be some connections between these two, specically on how shorter time length of a recipe tend to have a higher average rating. So in this section, I will perfom a permutation test and see whether this is true or not. 

**Null Hypothesis**: There is no effect of cooking time under under 1 hour (60 minutes) on the average rating of recipes. \
**Alternative Hypothesis**: Cooking time under 1 hour (60 minutes) have an effect on the average rating of recipes. \
**Test Statistic**: Difference in Means since I am comparing two numerical distributions. \
**Signficance Level**: 0.05 so that I can get an accuracy result from this test.

<iframe
  src="assets/hypothesis_test.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Conclusion**: After performing permutation 1000 times, I got the resulting figure above. The **p-value = 0.223.** Since the significance level is 0.5 then then the p-value is larger than the significance level because 0.223 > 0.05. So, I **fail to reject** the hypothesis. This means that there is no effect of cooking time under 1 hour (60 minutes) on the average rating of recipes. However, I can not conclude that this is 100% true considering how this is only one sample and this is not a controlled trials. There might be other factors that come into play that I don't know so hence I can not conclude that `'minutes'` has no absolutely effect on `'avg_rating'`.

---

## Framing a Prediction Problem

Now that we have some understanding on what factors cause good rating and bad rating, for the rest of this analysis, I will shift gear and try to **predict the rating of each recipe**. Now, as we saw in the **Univariate Analysis** section that the majority of the ratings in this dataset are 5 so if I continue to use this dataset, my model will tend to predict 5 no matter what the features are. So to fix this issue, I created a new dataset by sampling 2000 recipes per rating and combined them to a new dataset. This will allow my model to preict the ratings based on the features not the occurences of each rating. Then to do this, I will use the relevant information from the dataset to predict such as `'minutes'`, `'n_steps'`, `'n_ingredients'`, `'calories (#)'`, `'total fat (PDV)'`, `'sugar (PDV)'`, `'sodium (PDV)'`, `'protein (PDV)'`, `'saturated fat (PDV)'`, and `'carbohydrates (PDV)'`. This is a **multiclass classification** prediction problem since we are trying to predict an oridnal data. The **response variable** is `'rating'` because it is the variable I am trying to predict. The evaluation metric for my model is R<sup>2</sup>. Even though this is a classification problem, I am using R<sup>2</sup> because it is more efficient and best summarize the accuracy of my model, whereas, for precision and recall, I have to perform it for each rating which is not efficient. 

---

## Baseline Model

My baseline model consists of only the **DecisionTreeClassifier**. The features I decided to use are `'minutes'` and `'n_steps'`. All of theese features are quantitative since there are all numerical so there are no ordinal and nominal data. Because they are all quantitative data, I did not perform any encoding since I was able to perform **DecisionTreeClassifier** on those features. After performing **DecisionTreeClassifier**, the R<sup>2</sup> of my model is **0.3858333333333333** on my training set and **0.17541666666666667** on my testing set. Based on the R<sup>2</sup>, I believe that my current model is bad considering how it is pretty close to 0. This means that the the prediction of my models are not quite accurate. 

---

## Final Model

For my final model, I added two additional features which are `'calories (#)'` and `'n_ingredients'`. So in total, my final models have 4 features which are `'minutes'`, `'n_steps'`, `'calories (#)'`, and  `'n_ingredients'`. The reason why I added calories and number of ingredients to my final model is because these two informations are vital when it comes to rating a recipe. Both of these features will help the final model's performance since calories are essential information espeically for people who are trying to gain or lose weight. People would tend to rate good if the calories of a food are approriate, but bad if the calories are too much or too little. On the other hand, ingredients are also important because without it, there will be nothing for people to cook with. So knowing the number of ingredents will allow people to jugde whether this recipe was worth it or not, thus rating it high if the number of ingredients are appropriate and low if the number of ingredients are too much.

My final model consists of the **DecisionTreeClassifier**, **PolyFeatures of degree 4**, and **StandardScaler**. In order to find the best hyperparameters for my **DecisionTreeClassifier**, I used **GridSearchCV**. After I ran, **GridSearchCV**, I found that the best hyperparameters to run are `'max_depth: None'`, `'min_samples_split: 2'`, and `'criterion: 'gini'`. With this algorithm and hyperparameters, the R<sup>2</sup> of my model is **0.8955208333333333** on my traning set and **0.21208333333333335** on my testing set. Based on this, my final model's performance improved from my baseline model. This shows that adding 2 new features, `'calories (#)'` and `'n_ingredients'`, and perfrom **StandardScaler** and **PolyFeatures** on them improve the accuracy of my final model. 


---

## Fairness Analysis

Finally, in this section, I will be testing the fairness of my final model. To do this I decided to separate my dataset into two groups where the first group is the **short recipe** which consists of 8 steps or less and the second group is the **long recipe** which consists of 9 or more steps. To evaluate this, I am going to use the R<sup>2</sup> since it best summarizes what is going on in our final model than using precision or recall.

**Null Hypothesis**: Our model is fair. Its R<sup>2</sup> for short recipes and long recipes are roughly the same, and any difference are due to random chance. \
**Alternative Hypothesis**: Our model is unfair. Its R<sup>2</sup> for short recipes is lower than its R<sup>2</sup> for long recipes. \
**Test Statistic**: Difference in Accuracy since I am trying to find the accuracy of the final model. \
**Significane Level**: 0.05

<iframe
  src="assets/fairness.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

**Conclusion**: After performing permutation 1000 times, I got the resulting figure above. The **p-value = 0.737**. Since the significane level is 0.05, the p-value is much larger than the significance because 0.737 > 0.05. So, I **fail to reject** the null hypothesis. This means that our model is fair. Its R<sup>2</sup> for short recipes and long recipes are roughly the same, and any difference are due to random chance. 

---

