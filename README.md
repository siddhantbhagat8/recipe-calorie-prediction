# recipe-calorie-prediction

## Exploratory Data Analsys
My majority exploratory data analsys can be found ![here](https://siddhantbhagat8.github.io/recipe-calorie-analysis/)
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