# Recipe Analysis
This is a project for DSC 80 at UCSD
By Hana Tjendrawasi

## Introduction
In an era where culinary exploration and home cooking have surged in popularity, understanding the components that make a recipe stand out is more important than ever. This project dives into an extensive dataset sourced from Food.com, a platform renowned for its vast collection of recipes and user interacions. 

The data comprises of two primary datasets: recipes and interactions. The recipes dataset includes the columns: name, ID, minutes, contributor ID, submission date, tags, nutrition information, number of steps, steps text, description, ingredients and number of ingredients. The interactions dataset includes the columns: user ID, recipe ID, date, rating, and review.

Recipes dataframe has 12 columns and 83783 rows, which means it contains 83782 recipes.The interactiions dataframe has 5 columns and 731927 rows, each consisting of a review for a particular recipe. This rich dataset not only showcases the popularity of recipes but also offers a direct insight into the preferences and opinions of the cooking community.

The question I will use for this project for further investigation will be: "What are the common characteristics of highly rated recipes?" I sparked interest to this question because it can provide insights into what makes a recipe successful, potentially guiding both home cooks and professional chefs in creating dishes that are likely to be well-received. By analyzing factors such as cooking time, number of ingredients, nutritional information, and the presence of specific tags or ingredients, we can uncover trends and patterns that characterize well-loved recipes

Understanding the characteristics of highly rated recipes can be beneficial for multiple reasons. For recipe developers and food bloggers, this insight helps in crafting content that resonates with their audience. Additionally, this analysis can shed light on broader culinary trends, such as preferences for certain cuisines, dietary restrictions, or ingredient trends.

To carry out this investigation, I'll focus on data from both datasets, paying particular attention to columns such as 'rating', 'nutrition', 'n_ingredients', 'tags', and 'minutes from recipes dataset, and correlating these with the ratings and reviews from the interactions dataset

## Data Cleaning and Exploratory Data Analysis
Describe, in detail, the data cleaning steps you took and how they affected your analyses. The steps should be explained in reference to the data generating process. Show the head of your cleaned DataFrame (see Part 2: Report for instructions).

Embed at least one plotly plot you created in your notebook that displays the distribution of a single column (see Part 2: Report for instructions). Include a 1-2 sentence explanation about your plot, making sure to describe and interpret any trends present. (Your notebook will likely have more visualizations than your website, and that’s fine. Feel free to embed more than one univariate visualization in your website if you’d like, but make sure that each embedded plot is accompanied by a description.)

Embed at least one plotly plot that displays the relationship between two columns. Include a 1-2 sentence explanation about your plot, making sure to describe and interpret any trends present. (Your notebook will likely have more visualizations than your website, and that’s fine. Feel free to embed more than one bivariate visualization in your website if you’d like, but make sure that each embedded plot is accompanied by a description.)

Embed at least one grouped table or pivot table in your website and explain its significance.

## Assessment of Missingness
State whether you believe there is a column in your dataset that is NMAR. Explain your reasoning and any additional data you might want to obtain that could explain the missingness (thereby making it MAR). Make sure to explicitly use the term “NMAR.”
Present and interpret the results of your missingness permutation tests with respect to your data and question. Embed a plotly plot related to your missingness exploration; ideas include: The distribution of column Y when column X is missing and the distribution of column Y when column X is not missing, as was done in Lecture 8.
The empirical distribution of the test statistic used in one of your permutation tests, along with the observed statistic

To proceed with a meaningful NMAR (Not Missing At Random) analysis within the context of the RAW_interactions.csv and RAW_recipes.csv datasets, we must first conceptualize how missingness in these datasets could depend on unobserved or unrecorded data, rendering it NMAR.
Identifying a Potential NMAR Column
One common candidate for NMAR in datasets similar to the ones provided could be the review column from RAW_interactions.csv. It's reasonable to speculate that the missingness in review might not be completely random but instead depend on factors not captured in the dataset. For example, users who feel neutral or indifferent about a recipe might neither rate it nor leave a review, whereas users with strong positive or negative opinions are more likely to do both. If this indifference or mild satisfaction is not captured by other variables in the dataset, the missingness in review could be considered NMAR.
Transforming NMAR to MAR
To transform this analysis from NMAR to Missing At Random (MAR), we would need additional data that could explain the missingness. This might include user engagement metrics, such as the number of times they viewed the recipe or if they added it to a collection without leaving a review. With such data, we could potentially link the missingness in review to observed data, thereby classifying it as MAR.
Analysis of Missingness Dependency
For the second part of your request, which involves performing permutation tests to analyze the dependency of the missingness of a selected column on other columns, let's conceptualize an approach using review missingness as the focus.
Conceptual Approach to

## Hypothesis Testing
Clearly state your null and alternative hypotheses, your choice of test statistic and significance level, the resulting p-value, and your conclusion. Justify why these choices are good choices for answering the question you are trying to answer.
Optional: Embed a visualization related to your hypothesis test in your website.
Tip: When making writing your conclusions to the statistical tests in this project, never use language that implies an absolute conclusion; since we are performing statistical tests and not randomized controlled trials, we cannot prove that either hypothesis is 100% true or false.

Hypotheses Null Hypothesis: The average rating of recipes is independent of the number of steps required to prepare them. Any observed difference in average ratings across recipes with varying numbers of steps is due to random chance. Alternative Hypothesis: There is a dependency between the average rating of recipes and the number of steps required to prepare them. Specifically, recipes with fewer steps have significantly different average ratings compared to those with more steps
Test Statistic: The difference in mean ratings between recipes with above-median number of steps (considered complex) and recipes with at or below-median number of steps (considered simple) Significance Level: 0.05

## Framing a Prediction Problem
Clearly state your prediction problem and type (classification or regression). If you are building a classifier, make sure to state whether you are performing binary classification or multiclass classification. Report the response variable (i.e. the variable you are predicting) and why you chose it, the metric you are using to evaluate your model and why you chose it over other suitable metrics (e.g. accuracy vs. F1-score).

Note: Make sure to justify what information you would know at the “time of prediction” and to only train your model using those features. For instance, if we wanted to predict your final exam grade, we couldn’t use your Project 4 grade, because Project 4 is only due after the final exam! Feel free to ask questions if you’re not sure.

## Baseline Model
Describe your model and state the features in your model, including how many are quantitative, ordinal, and nominal, and how you performed any necessary encodings. Report the performance of your model and whether or not you believe your current model is “good” and why.

Tip: Make sure to hit all of the points above: many projects in the past have lost points for not doing so.

## Final Model
State the features you added and why they are good for the data and prediction task. Note that you can’t simply state “these features improved my accuracy”, since you’d need to choose these features and fit a model before noticing that – instead, talk about why you believe these features improved your model’s performance from the perspective of the data generating process. 

Describe the modeling algorithm you chose, the hyperparameters that ended up performing the best, and the method you used to select hyperparameters and your overall model. Describe how your Final Model’s performance is an improvement over your Baseline Model’s performance.

Optional: Include a visualization that describes your model’s performance, e.g. a confusion matrix, if applicable.

## Fairness Analysis
Clearly state your choice of Group X and Group Y, your evaluation metric, your null and alternative hypotheses, your choice of test statistic and significance level, the resulting 
p
-value, and your conclusion.

Optional: Embed a visualization related to your permutation test in your website.