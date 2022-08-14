# Segment Two deliverable
## Machine Learning portion


## Preliminary Data Processing

Our dataset came in the form a single excel file (FoodAtlasEnvironment.xls). The data was collected and publish by the USDA. 

The data we were looking to extract was spread over nine different sheets. We extracted each sheet as a separate pandas dataframe and then exported each dataframe to a sperate csv file without doing any further processing withing pandas.

We chose to do it this way to fulfil the rubric requirement that we have multiple tables in our database and that we preform at least some kind of join within our database.

### Feature Selection
Across the nine sheets we created there were 73 distinct features. We selected columns from the Atlas data that would hopefully give us insights into the food environment for each row. These features included data related to the density food retailers in the county broken down by establishment type, data related to the overall health of the area, population data, and some socioeconomic factors.

After exploring the data we had we decided to drop a few column we had initially selected because they had too many null values to be of any use to us.

## Feature Engineering
For many of these measures we had matched pairs of data with results from 2 different years. Ultimately we decided to average those pairs as part of our standardization and feature engineering.

The other engineering we did before feeding our data into the machine learning model was to standardize it using the StandardizedScaler from the sklearn module. We then used the train_test_split function from sklearn to split our data into training and testing sets. We used the standard parameters to do the split.

### Model Selection and EDA
After a discussion with Kevin Lee we were convinced to try a Random Forrest Regressor to model our data. RFR is a supervised learning algorithm that allows us to test for a single target variable and through an ensemble learning method of using diverging decision trees arrives at a weighted average for our independent variables to give us an insight on what independent variables contribute the most to our target feature.

We ran the RFR for two possible target variables. The first was the diabetes rate in the population. after scoring our model for predicting that rate we receives a 0.9681 factor for our training score and 0.7639 for our test data score

These score don't indicated a particularly accurate model

When we changed our target feature to the obesity rate we were happen to see our training score jump to .9999 and our testing score up to .9964

### Summary

Our preliminary data analysis yielded some interesting results. The RFR model found that the feature that most contributed to obesity rate was Expenditure per capita at full service restaurants. The measure of expenditure per person at fast food restaurants ranked fifth in our models weight of importance. 

The categories that ranked second, third and fourth by order of importance all relate to the poverty level of the locale. Two were measure of the percentage of the population that receives federal food assistance in the form of WIC or SNAP benefits. The other measure the factor called Household Food Insecurity.

![top five output](/images/prelim_top_five_reversed.png)
While it isn't surprising that many of the factors that contribute the most to bad health at the county level are poverty related. What is interesting and worthy of more exploration is why these three factors in particular stood out when there were a number of other metrics about poverty, including a few that directly measured the poverty rate.
