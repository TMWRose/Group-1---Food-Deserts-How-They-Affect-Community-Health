## Outline of the Project

The root of the project was an interesting phenomenon that has been studied more and more lately called Food Desserts. 

These are defined by the communities access to nutritious food. A place is categorized as a food dessert depending on a number of factors including the amount and type of stores that sell food in the area. There is still much discussion and debate over what exactly should be called a “ffood dessert”
In an effort to define the term better the University of Michigan conducted a study in ten counties in Michigan that had areas within them that they believed to be food dessert. They broke down the counties into even smaller geographic areas, all the way down to individual neighborhoods, classified some as food desserts and collected extremely detailed information on the health metrics of the population. One thing was abundantly clear. Residents of these “food dessert” we in worse health than resident outside of the areas.

Initially we hoped to build a model off of this data that we could extrapolate to a larger, even nationwide dataset. After discussions with instructors we determined that It would be difficult to get meaningful insights that could be applied to a dataset as broad as the entire nation.

When we realized that the UofM data would be difficult if not impossible to draw any actionable conclusions from we shifted our focus to trying to learn something about what factors in community make it residents unhealthy. Thankfully the United States Department of Agriculture regularly publishes what it calls it Food Atlas. It contains data for the entire nation broken down to mostly the county level and includes statistics for many of the same factors UofM was studying.

Besides environment and socioeconomic statistics the Food Atlas also includes Two key indicators of health; obesity  and diabetes.udes Two key indicators of health; obesity  and diabetes. 

With the help of data in the USDA's Food Atlas we sought to understand what factors within a community were common among areas with poor health.


## DRAFTS

#### Data Source#### Data Source

### Preliminary Data Processing


* The data we were looking to extract was spread over nine different sheets. We extracted each sheet as a separate pandas dataframe and then exported each dataframe to a separate csv file without doing any further processing withing pandas.
* We chose to do it this way to fulfil the rubric requirement that we have multiple tables in our database and that we perform at least some kind of join within our database.
### Feature Selection
* Across the nine sheets we created, there were 73 distinct features. We selected columns from the Atlas data that would hopefully give us insights into the food environment for each row. These features included data related to the density food retailers in the county broken down by establishment type, data related to the overall health of the area, population data, and some socioeconomic factors.
* After exploring the data we had we decided to drop a few columns we had initially selected because they had too many null values to be of any use to us.
### Feature Engineering
* For many of these measures we had matched pairs of data with results from 2 different years. Ultimately, we decided to average those pairs as part of our standardization and feature engineering.
<img width="813" alt="Screen Shot 2022-08-14 at 8 53 47 PM" src="https://user-images.githubusercontent.com/101376325/184564926-ddba6130-6ec8-494d-a652-cbce77e1f9e3.png">

* The other engineering we did before feeding our data into the machine learning model was to standardize it using the StandardizedScaler from the sklearn module. We then used the train_test_split function from sklearn to split our data into training and testing sets. We used the standard parameters to do the split.


### Model Selection and EDA
* After a discussion with the instructor, we were convinced to try a Random Forest Regressor to model our data. RFR is a supervised learning algorithm that allows us to test for a single target variable and through an ensemble learning method of using diverging decision trees arrives at a weighted average for our independent variables to give us an insight on what independent variables contribute the most to our target feature.

* We ran the RFR for two possible target variables. 

When we targeted obesity rate we were able to saw some off the charts accuracy scores
![obesity score](\images\obesity_test_score.png)

The RFR model identified these as the top factors contributing to high obesity

Our model showed these as the top factors that lead to a high obesity rate:
1. Full Service Resturant Spending Per Capita ($)
2. Population with "Low Food Security" (%)
3. SNAP participants (% pop)
4. Households, no car & low access to store (%)
5. Infant participation in WIC (% pop)
6. Population with "Very Low Food Security" (%)
7. WIC Participation  Overall (% pop)
8. Fast Food Resturant Spending Per Capita ($)

![obesity factores](\images\obesity_top_factors.png)

The problem with this approach is that the dataset only had obesity rates at the state level. 

When we changed the target to diabetes rate, which we had values for at the county level the model score predictably fell
![diabetes score](\images\diabetes_test_score.png)


A score of .79 is not optimal but when we considered the scope data and the difficulty of predicting such a difficult variable we felt that some insights might still be gained from our imperfect model. 

The top contributing factors in our diabetes model were:

1. Median household income, 2015
2. SNAP participants (% pop)
3. Child Poverty Rate (% pop)
4. Households, no car & low access to store (%)
5. SNAP Spending Per Capita ($)
6. Full Service Resturant Spending Per Capita ($)
7. High schoolers physically active (%)
8. Population with "Very Low Food Security" (%)
9. Fast Food Sales Per Capita ($)


![diabetes factors](\images\diabetes_top_factors.png)

### DRAFT

Our preliminary data analysis yielded some interesting results. The RFR model found that the feature that most contributed to obesity rate was Expenditure per capita at full service restaurants. The measure of expenditure per person at fast food restaurants ranked fifth in our models weight of importance. 

The categories that ranked second, third and fourth by order of importance all relate to the poverty level of the locale. Two were measure of the percentage of the population that receives federal food assistance in the form of WIC or SNAP benefits. The other measure the factor called Household Food Insecurity.

* While it isn't surprising that many of the factors that contribute the most to bad health at the county level are poverty related. What is interesting and worthy of more exploration is why these three factors in particular stood out when there were a number of other metrics about poverty, including a few that directly measured the poverty rate. 


## Summary and Conclutions

////TABLAUE BOOK

