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
Before starting analysis, I conducted data cleaning to create more convenience in the process.
**Replace Empty Strings with 'pd.NA'**
For both 'interactions_df' and 'recipes_df', I've replaced empty string values with 'pd.NA' This step is significant for several reasons:
1. Handling missing data: Empty strings in a dataset might represent missing or undefined values for a certain observation. By replacing it with 'pd.NA', it is now standardized. This is cruciel for the next data processing steps as I may need to differentiate between a genuinely empty string and a missing value.
2. Analysis Integrity: Using a consistent marker for missing data helps maintain the integrity of the analysis

**Convert Submission Dates to DateTime Objects**
In 'recipes_df', I've converted the 'submitted' column to datetime objects, storing the result in a new column 'submitted_date'. This transformation has several benefits:
1. Temporal Analysis: Converting date strings to datetime objects enables a wide range of temporal analyses, such as time-series analysis, calculating time intervals, and aggregating based on time periods
2. Ease of Use: DateTime objects are much more versatile and easier to work with compared to strings when performing date-related calculations.

**Calculate Recipe Age in Years**
I calculated age of each recipe by subtracting the submitted_date from current date, converting the result to days and then dividing by 365 to convert to years. This adds a new column 'recipe_age_years' to 'recipes_df'. This calculation is useful for:
1. Trend Analysis: Understanding how the popularity or ratings of recipes change over time. Older recipes might have more reviews or different ratings compared to newer recipes
2. Data Segnmentation: it is now possible to segment the age of the recipes, which migh reveal insights into how the characteristics of population recipes have evolved over time

**Convert Review Dates to DateTime Objects and Extract Review Year**
In 'interactions_df', I've converted the 'date' column to datetime objects and extracted the year of each review into a new column 'review_year'. This step is essential for:
1. Temporal Analysis: Similar to the conversion in 'recipes_df', converting review dates allows for detailed temporal analyses of user interactions. For instance, I can examine how user engagement or review patterns change over the years.
2. Cohort Analysis: By extracting the review year, I can perform cohort analyses to compare behavior among users who provided reviews in different years.

**Calculate Average Ratings per Recipe**
I aggregated ratings by recipe in 'interactions_df' to calculate an average rating for each recipe, then merged these averages with 'recipes_df'. This process is vital for:
1. Enhanced Recipe Metrics: Adding average ratings to recipes enriches the dataset with a key performance indicator, reflecting overall user satisfaction and enabling comparisons across recipes.
2. Data Enrichment for Analysis: This merged data set facilitates deeper analyses, such as correlating recipe features with user ratings

**Merge Detailed User Interactions with Recipes**
By merging 'recipes_df' with 'interactions_df', I created a comprehensive dataset that combines detailed recipe information with user interactions. This is for:
1. In-depth Behavioral Analysis: Understanding the relationship between recipe attributes and user interactions
2. Completeness and Engagement Analysis: Identifying missing reviews helps assess the completeness of the dataset and analyze patterns in user engagement.

**Here is the cleaned dataframe**
| name  |     id |   minutes |   contributor_id | submitted   | tags   | nutrition  |   n_steps | steps | description   | ingredients   |   n_ingredients | submitted_date      |   recipe_age_years |   recipe_id |   average_rating | time_category   |   is_highly_rated |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------|----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|:--------------------|-------------------:|------------:|-----------------:|:----------------|------------------:|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]      |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']   | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 | 2008-10-27 00:00:00 |            15.4055 |      333281 |                4 | medium          |                 1 |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                      | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0]  |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !'] | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 | 2011-04-11 00:00:00 |            12.9507 |      453467 |                5 | medium          |                 1 |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]     |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 | 2008-05-30 00:00:00 |            15.8164 |      306168 |                5 | medium          |                 1 |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] | [878.3, 63.0, 326.0, 13.0, 20.0, 123.0, 39.0] |         7 | ['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']  | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                              | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 | 2008-02-12 00:00:00 |            16.1123 |      286009 |                5 | long            |                 1 |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  | ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                             | [267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2.0]    |        17 | ['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 | 2012-03-06 00:00:00 |            12.0466 |      475785 |                5 | long            |                 1 |

**This plot shows the distribution of average recipe ratings**
<iframe
  src="assets/dist_averageratings.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
The distribution is left-skewed and shows that there is a high amount of 5 star ratings and 4 star ratings coming in second highest. This shows that there are more highly rated recipes than not highly rated ones.


**This plot shows the correlation between average recipe ratings and cooking times**
<iframe
  src="assets/ratingsvscooking.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This visualization explores the relationship between the time it takes to prepare a recipe and its average rating. There is a negative slope which shows that the longer the cooking time (minutes) the lower the reviews tend to be.


**This is the pivot table**
<iframe
  src="assets/pivot_table.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
The pivot table would help us understand if there's a sweet spot in terms of recipe complexity and preparation time that correlates with higher average ratings.
These analyses are significant because they can offer valuable insights for recipe developers, culinary bloggers, and home cooks alike. For instance, if we find that simpler recipes with fewer ingredients and shorter cooking times tend to have higher average ratings, this could suggest a preference among users for recipes that are quick and easy to prepare. Conversely, if recipes with more ingredients and longer preparation times tend to be rated higher, this might indicate a user base that appreciates more complex, potentially flavorful dishes.

## Assessment of Missingness
In this part, I will conduct an assessment of missingness on the dataframe.
### NMAR Analysis
In the context of the datasets RAW_interactions.csv and RAW_recipes.csv, identifying Not Missing At Random (NMAR) data requires a consideration of the nature of missingness and how it might be intrinsically related to the unobserved data itself. NMAR occurs when the reason data is missing is related to the missing data itself, and not to the observed data.

One potential NMAR scenario in our dataset could involve the rating column in the interactions dataset. Users might choose not to leave a rating for a recipe because they had a negative experience or did not actually prepare the recipe, but this reason for the missing rating is directly related to the value of the missing data (i.e., what their rating would have been). If users are less likely to rate recipes they dislike or don't bother trying, then the missing ratings are not at random but are tied to their potential low value or the user's lack of engagement with the recipe.

**To further investigate and possibly address the NMAR nature of rating:**
**Additional Data:**
It would be beneficial to have access to more detailed user interaction data, such as whether a user viewed a recipe but chose not to rate it, or if they added it to a list (e.g., "Favorites" or "To Try") without subsequent feedback. Such data could provide insights into the user's intentions and preferences, even in the absence of a rating. 

**Qualitative Feedback:**
Including optional qualitative feedback for users who choose not to leave a numerical rating could also help understand the reasons behind missing ratings. If users frequently mention reasons like "did not try" or "not interested enough to make," this feedback could explain the missingness as NMAR but also give context that transforms it into Missing At Random (MAR), assuming the feedback is captured as part of the observed data. 

### Analysis of Missingness Dependency
For the second part, I conducted a permutation tests to analyze the dependency of the missingness of reviews depends on the rating.
<iframe
  src="assets/permutation_ratingdiffdist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

P-value for dependency of review missingness on rating: 0.0
Observed difference in mean ratings: 0.3834305990286735

## Hypothesis Testing
**Null Hypothesis**
The average rating of recipes is independent of the number of steps required to prepare them. Any observed difference in average ratings across recipes with varying numbers of steps is due to random chance.

**Alternative Hypothesis**
There is a dependency between the average rating of recipes and the number of steps required to prepare them. Specifically, recipes with fewer steps have significantly different average ratings compared to those with more steps

**Test Statistic**
The difference in mean ratings between recipes with above-median number of steps (considered complex) and recipes with at or below-median number of steps (considered simple)
**Significance Level:** 0.05

**These are the results from the test:**
Observed difference: 0.027238616956376305
P-value: 0.4552

Based on this, the p-value is 0.4552 which is above the significance level of 0.05, and hence we fail to reject the null hypothesis. This outcome indicates that there is no statistically significant evidence to support the claim that the average rating of recipes is dependent on the number of steps required to prepare them. 

**Statistical Significance:**
The choice of significance level of 0.05 is standard in many field of research, by adhering to this convention, the analysis ensures the risk of committing a Type I error is limited to 5%.

**Test Statistic Choice:**
The decision to use the difference in mean ratings between recipes categorized as complex and simple as the test statistic is a rational approach to investigating the hypothesis. 

**Interpretation of Results**
Emphasizing that the failure to reject the null hypothesis does not prove it true is critical in scientific communication. Instead, it suggests that, within the limitations of this dataset and analysis, there is insuffiecient evidence to assert a significant relatioinship between recipe complexity and average recipe ratings.

## Framing a Prediction Problem
**Prediction Problem**
Predicting whether a recipe will be highly rated based on its characteristics before any user interaction.

**Problem Type:** Binary Classification

**Prediction Goal**
Determine if a recipe will be highly rated (average rating >= 4) based on its pre-interaction characteristics

**Response Variable**
A binary variable indicating whether a recipe is highly rated 
('1' for average rating >= 4, '0' for average rating < 4)

### Why ? 
Choosing to predict whether a recipe will be highly rated before any user interaction allows us to focus on intrinsic recipe characteristics that may contribute to its success. This aligns with culinary creators' and platforms' interest in understanding what makes a recipe appealing to a broad audience.

**Cooking Time (minutes):** Indicates how long a recipe takes to prepare and cook. Both quick and slow-cooked recipes have potential appeal but might cater to different audiences.
**Number of Ingredients (n_ingredients):** Reflects recipe complexity. Simpler recipes might be more universally appealing due to accessibility and ease of preparation.
**Tags (tags):** Categorical data indicating recipe attributes like meal type (breakfast, dessert), dietary preferences (vegan, gluten free), and occassion(Christmas, summer) which could influence a recipe's popularity.

**Time of Prediction Consideration**
As the time of prediction, we assume no user ratings or reviews are available for the recipe, thus solely focusing on the recipe's content and metadata submitted by the author.

**Evaluation Metric Choice:** F1-score
In a binary classification problem, focusing on predicting highly rated recipes, it's crucial to balance precision and recall. The F1-score harmonically combines these metrics, providing a more nuanced evaluation than accuracy alone. 
Achieving a high F1-score requires the model not only to accurately identify highly rated recipes but also to minimize false positives and false negatives.

## Baseline Model
**Prediction Problem Type:** Binary classification

**Response Variable:** Whether a recipe is highly rated (1) or not (0). A recipe is considered highly rated if its average rating is 4 or above

**Reason for Choice:** Predicting the potential success of a recipe can be valuable for content creators, culinary websites, and users looking for quality recipes. It provides insights into what characteristics contribute to a recipe's popularity and satisfaction among users.

### Features Used
**Numerical:**
1. minutes (cooking time)
2. n_ingredients (number of ingredients)
**Categorical:**
1. tags (dessert, quick-easy)

**Feature Transforms and Encoding:**
Numerical features will be left as-is.
Categorical features (tags) will be transformed using one-hot encoding to handle the nominal nature of the data

**Metric for Evaluation**
Accuracy is chosen as the initial metric for simplicity and because the dataset is assumed to be fairly balanced between highly and not highly rated recipes.
In further iterations, the F1-score could be considered to balance precision and recall, especially if the dataset turns out to be imbalanced.

### Baseline Model:
**Logistic Regression**
A simple and interpretable model for this baseline classification task. 
The model will be implemented in an sklearn pipeline that includes feature transformation (one-hot encoding for categorical variables) and the logistic regression model itself.

### Model and Performance Discussion
After performing the test:
Baseline Model Accuracy: 0.8425732529689085

This baseline model uses a straightforward logistic regression to predict the likelihood of a recipe being highly rated based on its cooking time, number of ingredients, and tags

The performance of this model as indicated by accuracy provides a benchmark for future models. Since the accuracy is significantly better than random guessing (50% for a balanced binary classification problem), the model can be considered a good starting point. 
Further model iterations might explore additional features, more complex models, and more nuanced evaluation metrics to improve predictive power and relevance to the prediction task.

## Final Model
### Feature Engineering
**Cooking Time Bins:** Recipes might have different appeal based on their cooking time. Quick recipes might be more appealing to some users, while others might associate longer cooking times with more sophisticated dishes. We'll categorize minutes into bins (Quick, Medium, Long) and encode these categories.
**Ingredient Density:** The ratio of the number of ingredients to cooking time might indicate recipe complexity in a way that's more informative than the number of ingredients alone. We'll create a new feature ingredient_density = n_ingredients / minutes.

### Modeling Algorithm and Hyperparameter Tuning
**Model Chosen:** RandomForestClassifier. 
It's a versatile model that can capture complex relationships between features without requiring linear assumptions.

### Hyperparameters to Tune
**n_estimators:** The number of trees in the forest. More trees can increase accuracy but also computational cost.
**max_depth:** The maximum depth of the trees. Controls overfitting by limiting how detailed the model can get.
**Method for Hyperparameter Selection:** GridSearchCV. It systematically explores a range of values for each parameter to find the combination that performs the best according to a specified metric, which in this case, will be accuracy.

### Model Performance and Improvement
The final model's performance, as measured by accuracy or another appropriate metric (e.g., F1-score for imbalanced classes), should be compared against the baseline model to assess improvement. The choice of features and model adjustments are informed by an understanding of the data and the prediction task, aiming to capture more nuances in how recipes' attributes might influence their ratings.

## Fairness Analysis
**Group X (Quick Recipes):**
Recipes with a cooking time of 30 minutes or less
**Group Y (Long Recipes):**
Recipes with a cooking time of more than 30 minutes

**Evaluation Metric**
We will choose accuracy as our evaluation metric since our final model is a binary classifier prediciting whether a recipe is highly rated or not.

**Hypotheses**
**Null Hypothesis**:
The model is fair regarding recipe cooking time. The accuracy for predicting highly rated recipes is roughly the same for quick recipes (Group X) and long recipes (Group Y), and any differences are due to random chance.
**Alternative Hypothesis**:
The model is unfair regarding recipe cooking time. There's a significant difference in the accuracy of predicting highly rated recipes between quick recipes (Group X) and long recipes (Group Y).

**Test Statistic and Significance Level**
**Test Statistic**: The difference in model accuracy between Group X and Group Y
**Significance Level**: 0.05

**After conducting a permutation test:**
Observed Difference in Accuracy: 0.028093212070608997
P-value: 0.0
Based on the p-value:
As p ≤ 0.05, We reject the null hypotheses and conclude that the model performs significantly differently for quick recipes compared to long recipes, indicating a potential fairness issue. 