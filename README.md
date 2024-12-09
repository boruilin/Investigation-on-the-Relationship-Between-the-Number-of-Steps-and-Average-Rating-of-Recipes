# Investigation on the Relationship Between the Number of Steps and Average Rating of Recipes

Authors: Borui Lin, Junshu Xin

## Overview

This is the final project for DSC 80 at UCSD. Using the dataset on recipes and ratings, we plan to investigate the relationship between number of steps in a recipe and the average rating of a recipe

## Introduction 
Food is indispensable to everyone, a healthy eating habit can promote both mental and physical health significantly. Good food not only provides important nutrients, but also brings savory experiences that help us release dopamine that releases stress. For college students, eating at restaurants all the time can be very expensive, but cooking at home can bring delicious food and save a lot of money! To learn how to cook desirable dishes, recipes are important, and we love recipes with higher ratings. Each recipe consists of many factors,  some seems determinant to the rating of a recipe. We wonder if the number of steps of a recipe will affect the rating negatively or positively. The reason why we chose the number of steps is because we are not sure if people favor more or less: too little steps can be stress-free, but the dish may be rough due to the lack of process, while too many steps can be very time consuming and difficult to follow, the dish comes delicate and exquisite.  We are curious about the effect of the number of steps on recipe ratings. To achieve our goal, we analyze based on two datasets, recipes and ratings, from food.com. 
The first dataset, recipe, contains 83782 rows, representing 83872 unique recipes, with 10 columns recording the following information. 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dataset Overview</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f9f9f9;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            font-size: 16px;
        }
        th, td {
            padding: 12px;
            text-align: left;
            border: 1px solid #ddd;
        }
        th {
            background-color: #f4f4f4;
        }
    </style>
</head>
<body>
    <table>
        <thead>
            <tr>
                <th>Column</th>
                <th>Description</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td><code>name</code></td>
                <td>Recipe name</td>
            </tr>
            <tr>
                <td><code>id</code></td>
                <td>Recipe ID</td>
            </tr>
            <tr>
                <td><code>minutes</code></td>
                <td>Minutes to prepare recipe</td>
            </tr>
            <tr>
                <td><code>contributor_id</code></td>
                <td>User ID who submitted this recipe</td>
            </tr>
            <tr>
                <td><code>submitted</code></td>
                <td>Date recipe was submitted</td>
            </tr>
            <tr>
                <td><code>tags</code></td>
                <td>Food.com tags for recipe</td>
            </tr>
            <tr>
                <td><code>nutrition</code></td>
                <td>Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]</td>
            </tr>
            <tr>
                <td><code>n_steps</code></td>
                <td>Number of steps in recipe</td>
            </tr>
            <tr>
                <td><code>steps</code></td>
                <td>Text for recipe steps, in order</td>
            </tr>
            <tr>
                <td><code>ingredients</code></td>
                <td>Text for recipe ingredients</td>
            </tr>
            <tr>
                <td><code>n_ingredients</code></td>
                <td>Number of ingredients in recipe</td>
            </tr>
        </tbody>
    </table>



</body>
</html>

## Data Cleaning and Exploratory Data Analysis



## Assessment of Missingness
Within our merged dataset containing both columns from recipe and interaction, there are 3 columns that contain fair amounts of missing values, they are “ratings”, “reviews”, and “description”. Some other columns such as “user_id” and “name” also contain a few missing values; however, for the purpose of assessing missing values, we will only consider and examine the columns that contain a reasonable amount when determining the missing machisms. 
### NMAR Analysis
First, we will try to determine which of the columns above most likely has a missing mechanism of NMAR, meaning that the missing values are not dependent on anything else but the column itself. After we conducted some logical thinking and empirical testing, we concluded that the “review” column can both be NMAR. “review” is most likely NMAR because many users may avoid writing text reviews due to the effort involved, especially if they have a neutral feeling towards the results. To provide a similar example, when I have a very pleasant experience at a restaurant, I would usually write great reviews and give them a high star rating, but when I only have an average experience, I would not bother to write anything to provide my judgments on rating platforms. Some additional data that we can collect in order to make “review” MAR could be the number of times each recipe is used, since the more often a recipe is used, the more likely that it will have more reviews. 
### Missing Dependency
The column we selected to assess missing dependencies is the ‘ratings’. Some of the columns we thought ‘ratings could be MAR on are ‘n_steps”, “years_since_submission”, and “minutes”. Therefore, we decided to conduct some permutations using different test statistics for each case to determine their dependencies. In our analysis, we use the significance level of 0.05
#### Does the missingness of ‘ratings” depend on the “n_steps” column?
We decided to use KS stats as test statistics here, since n_steps is a numeric variable that contains a few outliers. Therefore, it is more appropriate to look at the difference in distributions rather than just the difference in means.

#### **Null**: The missingness of ratings does not depend on the proportion of number of steps for a recipe

#### **Alternative**: The missingness of ratings does depend on the proportion of number of steps for a recipe

#### **Test Statistic**: KS statistic for the group of n_steps for rows with missing ratings and group of n_steps for rows with non-missing ratings

The graph below shows the distribution of n_steps for groups of missing and non-missing ratings respectively
<iframe
  src="https://boruilin.github.io/Number-of-Step-and-Ratings-in-Recipe/graphs/n_step_dist_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram below shows the distribution results of running the permutation 1000 times using the test statistic of KS stat
<iframe
  src="https://boruilin.github.io/Number-of-Step-and-Ratings-in-Recipe/graphs/n_step_ks_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The p_value we found is **(0.0)** and it is lower than the significance level. So we reject the null hypothesis. The missingness of “ratings” does depend on the ‘n_steps’ column

#### Does the missingness of ‘ratings” depend on the “years_since_submission” column?
We use TVD as the test statistic in this case since there are only 11 unique values in the “years_since_submission” column and they are ordinal. 
#### **Null**: The missingness of ratings does not depend on the number of years since the recipe was submitted for a recipe

#### **Alternative**: The missingness of ratings does depend on the the number of years since the recipe was submitted for a recipe

#### **Test Statistic**: Total Variance Distance for the group of years since submission for rows with missing ratings and group of years since submission for rows with non-missing ratings

The graph below shows the distribution of years since submission for groups of missing and non-missing ratings respectively
<iframe
  src="https://boruilin.github.io/Number-of-Step-and-Ratings-in-Recipe/graphs/years_dist_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The histogram below shows the distribution results of running the permutation 1000 times using the test statistic of TVD

<iframe
  src="https://boruilin.github.io/Number-of-Step-and-Ratings-in-Recipe/graphs/years_since_submission_tvd_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The p_value we found is **(0.0)** and it is lower than the significance level. So we reject the null hypothesis. The missingness of “ratings” does depend on the ‘years_since_submission’ column



## Hypothesis Testing
In the previous section, we conducted a permutation test and found evidence suggesting that the missingness of 'ratings' is dependent on the number of steps in a recipe. To further investigate the relationship between recipe ratings and the number of steps, we conducted an additional hypothesis test. Specifically, we divided the data based on the median number of steps **(9)**, categorizing recipes with more than 9 steps as "high_steps" and those with 9 or fewer steps as "low_steps." The goal of this analysis was to determine whether there is a relationship between the average rating of a recipe and its assigned step category. For this test, we used a significance level of 0.05 and performed 1,000 permutations to simulate the null distribution of the test statistic.
Hypotheses

#### **Null**: The average ratings for "high_steps" recipes and "low_steps" recipes are equal.

#### **Alternative**: The average ratings for "high_steps" recipes and "low_steps" recipes are not equal.

#### **Test Statistic**: We used the difference in mean ratings  as the test statistic.

To provide additional context for our null and alternative hypotheses, we considered that both "high_steps" and "low_steps" recipes might offer distinct advantages that could influence their ratings. "High_steps" recipes may receive higher ratings because the increased number of steps could result in more refined and complex flavors. Conversely, "low_steps" recipes might be rated highly due to their simplicity and convenience, which could appeal to users who prioritize ease of preparation. This reasoning motivated us to explore how these potential advantages align with the preferences of users reflected in our collected data.

### Results and Conclusion
The observed difference in mean ratings was **−0.0052**, and the resulting p-value was **0.007**, which is lower than the significance level of 0.05. Since the p-value is small, we reject the null hypothesis and conclude that the average ratings for "high_steps" recipes and "low_steps" recipes are not equal. This result suggests that the step categories do influence the average ratings of recipes in our dataset.

The histogram belows shows the distribution of difference in means of ratings for high steps recipes and low steps recipes

<iframe
  src="https://boruilin.github.io/Number-of-Step-and-Ratings-in-Recipe/graphs/n_steps_diff_means_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Framing a Prediction Problem


## Baseline Model



## Final Model


## Fairness Analysis


