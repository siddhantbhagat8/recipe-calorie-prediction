# recipe-calorie-prediction

## Exploratory Data Analsys
My majority exploratory data analsys can be found [here](https://siddhantbhagat8.github.io/recipe-calorie-analysis/)
In addition to the EDA done on the above website 6 new columns were created in the `recipes` dataset. This columns were extracted from the `nutrition` column and are as follows:
1. `total_fat`: total fat content of the recipe
2. `sugar`: total sugar in the recipe
3. `sodium`: total sodium in the recipe
4. `protein`: toal protein in the recipe
5. `saturated_fat`: total saturated fats in the recipe
6. `carbs`: total carbs in the recipe

For the purpose of the prediction column the columns involved during our prediction task are shown by the first few rows of the dataframe in use:

|    | name                                 |     id |   minutes |   n_ingredients |   year |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   carbs |   calories |
|---:|:-------------------------------------|-------:|----------:|----------------:|-------:|------------:|--------:|---------:|----------:|----------------:|--------:|-----------:|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |               9 |   2008 |          10 |      50 |        3 |         3 |              19 |       6 |      138.4 |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |              11 |   2011 |          46 |     211 |       22 |        13 |              51 |      26 |      595.1 |
|  2 | 412 broccoli casserole               | 306168 |        40 |               9 |   2008 |          20 |       6 |       32 |        22 |              36 |       3 |      194.8 |
|  3 | millionaire pound cake               | 286009 |       120 |               7 |   2008 |          63 |     326 |       13 |        20 |             123 |      39 |      878.3 |
|  4 | 2000 meatloaf                        | 475785 |        90 |              13 |   2012 |          30 |      12 |       12 |        29 |              48 |       2 |      267   |

## Framing the Problem

I am developing a regression model to predict the calorie content of a recipe. This model is based on observed correlations between `calories` and other **features** such as `total_fat`, `carbs`, `protein`, `sugar`, `year`, and `n_ingredients`. Understanding the calorie content is crucial for nutritional analysis and can be beneficial for individuals monitoring their dietary intake, as well as for culinary professionals who aim to design balanced recipes.

### Response Variable
Our chosen response variable is `calories`, which is a quantitative continuous variable. It's a vital component in nutritional information and of great interest in dietary planning and health-conscious cooking. Accurately predicting the calorie content of recipes can help in providing better dietary recommendations and in maintaining a balanced diet.

### Evaluation Metrics
Given that our task is a regression problem, I will evaluate our model using metrics such as Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and R-squared (R²). I have chosen R² as the primary metric for evaluating our model's performance. R² is a statistical measure that represents the proportion of the variance for the dependent variable (calories) that's explained by the independent variables in our model. A higher R² value indicates that the model explains a larger portion of the variance, which translates to better model performance.

### Model Selection
For this task, my baseline model will be **Linear Regression**. For the final model, I will compare and evaluate e two models: **Lasso Regression** and **RandomForestRegressor**. Lasso Regression is suitable for models where I expect some degree of regularization and feature selection. RandomForestRegressor, being a robust and versatile model, is suitable for capturing complex non-linear relationships without requiring extensive hyperparameter tuning.

### Information Known
At the time of prediction, I assume that features such as `total_fat`, `carbs`, `protein`, `sugar`, `year`, and `n_ingredients` are known. These are fundamental aspects of a recipe that can typically be determined or estimated during the recipe's creation. This information is essential for accurately predicting the calorie content and thus is integral to our model.
