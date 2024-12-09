# Investigation on the Relationship Between the-Number of Steps and Average Rating of Recipes

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



