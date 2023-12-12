# recipe-calorie-prediction

## Exploratory Data Analysis
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
Given that our task is a regression problem, I will evaluate our model using metrics such as Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and R-squared (R²). I have chosen **R²** as the primary metric for evaluating our model's performance. R² is a statistical measure that represents the proportion of the variance for the dependent variable (calories) that's explained by the independent variables in our model. A higher R² value indicates that the model explains a larger portion of the variance, which translates to better model performance.

### Model Selection
For this task, my baseline model will be **Linear Regression**. For the final model, I will compare and evaluate e two models: **Lasso Regression** and **RandomForestRegressor**. Lasso Regression is suitable for models where I expect some degree of regularization and feature selection. RandomForestRegressor, being a robust and versatile model, is suitable for capturing complex non-linear relationships without requiring extensive hyperparameter tuning.

### Information Known
At the time of prediction, I assume that features such as `total_fat`, `carbs`, `protein`, `sugar`, `year`, and `n_ingredients` are known. These are fundamental aspects of a recipe that can typically be determined or estimated during the recipe's creation. This information is essential for accurately predicting the calorie content and thus is integral to our model.

## Baseline Model

### Description
In our baseline model: **Linear Regression**, I am using three predictor features: `total_fat` **(quantitative continuous)**, `carbs` **(quantitative continuous)**, and `year` **(categorical)**. `Year` is one-hot encoded to capture the potential varying impacts of different years on the calorie content, while `total_fat` and `carbs` are used as is. This model aims to establish a fundamental understanding of how these features relate to the calorie content of a recipe.

### Feature Transformations
The feature transformations in this baseline model include:
- One-hot encoding for the `year` feature, given its categorical nature.
- `total_fat` and `carbs` are kept in their original numeric form without transformation, maintaining their raw values for simplicity in this initial model.

### Performance
The baseline model's performance is evaluated using the R-squared metric, which indicates the proportion of the variance in the dependent variable that is predictable from the independent variables:

| Metric       | Train Score         | Test Score         |
| ------------ | ------------------- | ------------------ |
| R-squared    | 0.9728244840452863  | 0.9718240324704646 |

These metrics suggest that my baseline LLinear Regression model is **'good'** because it has a high R² value for both the training set and the test set. This means that not only does it explain the varianve of the dataset well but is also good a generalizing when tested with unseen data. However, being a baseline, it serves as a starting point for further model development and refinement.

## Final Model Description

### Feature Selection and Transformation
For the final model, I added `protein`, `sugar`, and `n_ingredients` to the existing features (`total_fat`, `carbs`, `year`):

- **Protein and Sugar**: Key nutritional components in recipes that can significantly influence calorie content. Including them helps the model capture more of the nutritional profile of a recipe.
- **Number of Ingredients (n_ingredients)**: This feature potentially correlates with the complexity and type of recipe, impacting the calorie content.

The feature transformations applied are as follows:
- **Log Transformation for `sugar`**: Applied to normalize the distribution, as sugar content can be skewed in recipe data.
- **Min-Max Scaling for `protein`**: To normalize this feature, ensuring it's on the same scale as other variables.
- **Standard Scaling for `total_fat` and `carbs`**: To standardize these features for better model performance.
- **One-Hot Encoding for `year`**: To capture any categorical effects of the year on the recipes.

### Modeling Algorithm and Hyperparameters
#### Lasso Regression
- **Strengths**: Lasso Regression is particularly effective in scenarios where feature selection is crucial. It adds a penalty equivalent to the absolute value of the magnitude of coefficients, which helps in reducing overfitting and in handling multicollinearity by shrinking less important feature coefficients to zero.
- **Application**: In our context, Lasso helps identify which features (out of `total_fat`, `carbs`, `protein`, `sugar`, `year`, and `n_ingredients`) are most predictive of calorie content, potentially simplifying the model by excluding less important predictors.

#### RandomForestRegressor
- **Strengths**: This is an ensemble learning method based on decision tree regressors. It's known for its high accuracy, ability to run efficiently on large datasets, and capability to handle thousands of input variables without variable deletion. It's particularly good at capturing non-linear relationships and interactions between features.
- **Application**: Given the diverse range of ingredients and cooking methods that can influence the calorie content of a recipe, RandomForestRegressor's ability to handle complex, non-linear relationships makes it well-suited for our prediction task.

### Hyperparameter Tuning
For the RandomForestRegressor, I performed hyperparameter tuning using GridSearchCV. I experimented with different values for `n_estimators` (the number of trees in the forest) and `max_depth` (the maximum depth of the trees). 

- **Best Parameters**: The best-performing hyperparameters were found to be {'max_depth': 10, 'n_estimators': 50}. This configuration balances the model's complexity with its ability to generalize, avoiding both underfitting and overfitting.
- **Method**: GridSearchCV was used for its exhaustive search over the specified parameter grid. This method is beneficial for systematically working through multiple combinations of parameter tunes, cross-validating as it goes to determine which tune gives the best performance.

### Performance Comparison
The performance metrics for both models are as follows:

#### Lasso Regression
| Metric          | Train R-Squared    | Test R-Squared    |
| --------------- | ------------------ | ----------------- |
| R-squared       | 0.9722494053815499 | 0.9718028743643612|

#### RandomForestRegressor
| Metric          | Train R-Squared    | Test R-Squared    |
| --------------- | ------------------ | ----------------- |
| R-squared       | 0.9899919142508882 | 0.9788770164864619|

The RandomForestRegressor with the best parameters (`max_depth`: 10, `n_estimators`: 50) achieved a GridSearchCV best R^2 score of 0.9460395035205833.

**The RandomForestRegressor is chosen as the final model** due to its superior performance in both training and testing phases. This model effectively captures the complexity of the relationships between the various features and the calorie content of the recipes. Its ability to handle non-linear relationships and interactions between features makes it well-suited for this task.

The improvements in R-squared values from the baseline to the final model indicate that the additional features and chosen transformations have contributed significantly to the model's ability to predict calorie content accurately.

| Model           | Metric          | Train R-Squared    | Test R-Squared    |
|---------------- | --------------- | ------------------ | ----------------- |
|Random Forest    | R-squared       | 0.9899919142508882 | 0.9788770164864619|
|Linear Regression| R-squared       | 0.9728244840452863 | 0.9718240324704646|

## Fairness Analysis

### Group Definition
- **Group X**: Recipes submitted before 2013.
- **Group Y**: Recipes submitted in 2013 or later.

### Evaluation Metric
- The chosen evaluation metric for this analysis is the **Root Mean Squared Error (RMSE)**. It quantifies the difference between the predicted and actual calorie values, making it suitable for assessing model accuracy across different groups.

### Hypotheses
- **Null Hypothesis**: The model predicts calorie content with equal accuracy for recipes submitted before and after 2013, indicating no bias in prediction based on the year of submission.
- **Alternative Hypothesis**: The model's accuracy in predicting calorie content significantly differs for recipes submitted before 2013 compared to those submitted from 2013 onward, suggesting a potential bias in prediction based on the year of submission.

### Test Statistic and Significance Level
- The test statistic used is the absolute difference in RMSE between Group X and Group Y.
- The significance level is set at 0.05.

### Permutation Test and P-value
- A permutation test was performed to evaluate the fairness of the model. The model used to make predictions in the permutation test was the same RandomForestRegressor model that I obtained in the Final Model section. It contains the same column transformations and the same pipeline The p-value obtained from this test is **0.825**.

### Conclusion
- With a p-value of 0.825, I **fail to reject** the null hypothesis. This is considerably higher than our significance level of 0.05, I do not find sufficient evidence to reject the null hypothesis. This outcome suggests that, based on our dataset and analysis, there is no strong statistical indication of bias in the model's calorie predictions with respect to the year of recipe submission. However, it's important to acknowledge that statistical tests have limitations and cannot conclusively prove the absence of bias. Further investigations, possibly with different methodologies or additional data, could provide more insights.
