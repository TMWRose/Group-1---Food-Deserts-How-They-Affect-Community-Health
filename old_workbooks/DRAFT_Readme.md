# What Environmental Factors Contribute Most to Community Health?

## Outline of the Project

The root of the project was an interesting phenomenon that has been studied more and more in the past decade that researchers call 'Food Desserts'. 

These are defined by the communities access to nutritious food. A place is categorized as a food dessert depending on a number of factors including the amount and type of stores that sell food in the area. There is still much discussion and debate over what exactly should be called a “food dessert”

In an effort to define the term better the University of Michigan conducted a study in ten counties in Michigan that had areas within them that they believed to be food dessert. They broke down the counties into even smaller geographic areas, all the way down to individual neighborhoods, classified some as food desserts and collected extremely detailed information on the health metrics of the population. One thing was abundantly clear. Residents of these “food dessert” we in worse health than resident outside of the areas.

Initially we hoped to build a model off of this data that we could extrapolate to a larger, even nationwide dataset. After discussions with instructors we determined that It would be difficult to get meaningful insights that could be applied to a dataset as broad as the entire nation.

When we realized that the UofM data would be difficult if not impossible to draw any actionable conclusions from we shifted our focus to trying to learn something about what factors in community make it residents unhealthy. Thankfully the United States Department of Agriculture regularly publishes what it calls it Food Atlas. It contains data for the entire nation broken down to mostly the county level and includes statistics for many of the same factors UofM was studying.

Besides environment and socioeconomic statistics the Food Atlas also includes Two key indicators of health; obesity  and diabetes.udes Two key indicators of health; obesity  and diabetes. 

With the help of data in the USDA's Food Atlas we sought to understand what factors within a community were common among areas with poor health.

### Software and Tools Used: 


### Data Source
 **The United States Department of Agriculture Food Atlas:**

 Last updated: Friday, December 18, 2020

 **Homepage:** [USDA Food Atlas Documentation](https://www.ers.usda.gov/data-products/food-environment-atlas/data-access-and-documentation-downloads/)
 **Raw Excel File:** [HERE](https://www.ers.usda.gov/webdocs/DataFiles/80526/FoodEnvironmentAtlas.xls?v=3274.7)
 



## Preliminary Data Processing
The data we were looking to extract was spread over nine different sheets within the MS Excel file that contained the entire Food Atlas. We extracted each sheet as a separate pandas dataframe and then exported each dataframe to a separate csv file without doing any further processing within pandas.

```

    ### USE THE LISTS ABOVE TO CREATE DATAFRAMES FROM EACH SHEET ###

population_df = global_dict['Supplemental Data - County'][POPULATION_LIST]
access_df = global_dict['ACCESS'][ACCESS_LIST]
store_df = global_dict['STORES'][STORES_LIST]
restaurants_df = global_dict['RESTAURANTS'][RESTAURANTS_LIST]
assistance_df = global_dict['ASSISTANCE'][ASSISTANCE_LIST]
insecurity_df = global_dict['INSECURITY'][INSECURITY_LIST]
local_df = global_dict['LOCAL'][LOCAL_LIST]
health_df = global_dict['HEALTH'][HEALTH_LIST]
socioeconomic_df = global_dict['SOCIOECONOMIC'][SOCIOECONOMIC_LIST]


## Output the dataframes to csv files ##

population_df.to_csv('data/ATLAS/population.csv')
access_df.to_csv('data/ATLAS/access.csv')
store_df.to_csv('data/ATLAS/stores.csv')
restaurants_df.to_csv('data/ATLAS/restaurants.csv')
assistance_df.to_csv('data/ATLAS/assistance.csv')
insecurity_df.to_csv('data/ATLAS/insecurity.csv')
local_df.to_csv('data/ATLAS/local.csv')
health_df.to_csv('data/ATLAS/health.csv')
socioeconomic_df.to_csv('data/ATLAS/socioeconomic.csv'
```

## Entity Relationship Diagram (ERD)
### A map of the realtionships within our database

We then created a SQL database by importing each csv sheet into postgres/pgAdmin as a seperate table. We chose to do it this way to fulfil the rubric requirement that we perform at least some kind of join within our database.

```
## Load the individual dataframes into the database ##

population_df.to_sql('population', engine, index = False, if_exists='replace')
access_df.to_sql('access', engine, index = False, if_exists='replace')
store_df.to_sql('stores', engine, index = False, if_exists='replace')
restaurants_df.to_sql('restaurants', engine, index = False, if_exists='replace')
assistance_df.to_sql('assistance', engine, index = False, if_exists='replace')
insecurity_df.to_sql('insecurity', engine, index = False, if_exists='replace')
local_df.to_sql('local', engine, index = False, if_exists='replace')
health_df.to_sql('health', engine, index = False, if_exists='replace')
socioeconomic_df.to_sql('socioeconomic', engine, index = False, if_exists='replace')

```

We also needed to furfil a requirement that our data be hosted on the cloud. For this task we chose to create an remote database on Amazon Web Services and connect it to out local database

```
### Dependencies and Setup ###
### LOAD DATAFRAME FROM AWS SERVER

import pandas as pd
import sqlalchemy as sql
import config

endpoint=config.aws_endpoint
username='postgres'
password=config.aws_password
engine=sql.create_engine(f'postgresql://{username}:{password}@{endpoint}:5432/postgres')
df=pd.read_sql_table('final_merged', con=engine)
df.head()
```




## Feature Selection
* Across the nine sheets we created, there were 73 distinct features. We selected columns from the Atlas data that would hopefully give us insights into the food environment for each row. These features included data related to the density food retailers in the county broken down by establishment type, data related to the overall health of the area, population data, and some socioeconomic factors.
* After exploring the data we had we decided to drop a few columns we had initially selected because they had too many null values to be of any use to us.


## Feature Engineering
* For many of these measures we had matched pairs of data with results from 2 different years. Ultimately, we decided to average those pairs as part of our standardization and feature engineering.
<img width="813" alt="Screen Shot 2022-08-14 at 8 53 47 PM" src="https://user-images.githubusercontent.com/101376325/184564926-ddba6130-6ec8-494d-a652-cbce77e1f9e3.png">

* The other engineering we did before feeding our data into the machine learning model was to standardize it using the StandardizedScaler from the sklearn module. We then used the train_test_split function from sklearn to split our data into training and testing sets. We used the standard parameters to do the split.


## Model Selection and EDA
* After a discussion with the instructor, we were convinced to try a Random Forest Regressor to model our data. RFR is a supervised learning algorithm that allows us to test for a single target variable and through an ensemble learning method of using diverging decision trees arrives at a weighted average for our independent variables to give us an insight on what independent variables contribute the most to our target feature.

We ran the RFR for two possible target variables. 

When we targeted obesity rate saw some off the charts accuracy scores
![obesity score](images/obesity_test_score.png)
![obesity factores](images/obesity_top_factors.png)

The problem with this approach is that the dataset only had obesity rates at the state level. 


When we changed the target to diabetes rate, which we had values for at the county level the model score predictably fell.

![diabetes score](images/diabetes_test_score.png)
![diabetes factors](images/diabetes_top_factors.png)


A score of .81 is not optimal but when we considered the scope data and the difficulty of predicting such a difficult variable we felt that some insights might still be gained from our imperfect model. 

Unfortunately the time frame of the project meant we were unable to continue to work on the model. In an ideal situation we would have been able to try different paramenters for our RFR model and been able to go back to the data engineering phase to compile different sets of factors and run them through to look for a better fit and stronger relationships. 


## Conclutions

While both of our models were imperfect for the reasons mentioned above by looking at the results of both we were able to make some interesting conclusions. There were a number of factors that were shared between the two models. Most of the factors identified in both models were related to the socioeconomic makeup of the area. 

The thing that stood out to us were the shared factors that didn't have an obvious tie to the socioeconomic makeup of the county.  In fact two of the top contributing factors for both obesity and diabetes rates that we identified seemed to be in conflict with the simple conclution.


![formatted list](images/top_factors_presentation.png)

Our analysis suggested that areas that spend more money on prepaired food, either at food food or full service restaurants were more likely to be unhealthy.

 We chose to focus on this relationship to focus on in the reporting phase of the project.


When realized that spending on prepaired food per capita, either from a fast food establishment and/or a full service restuarant, was closely tied to the key health metrics of the community. We descided that this concultion seemed worthy of summary and visualization.

## Summary

When looking at ways to summarize our findings we first tried creating simple summary plots using seaborn and matplotlib within python.

Eventually we settled on using Tableau Public because of it's robust mapping capabilities, built in styles, and it's ability to easily integrate with HTML could not be matched by any other free-to-use tools we found 

In order to better display the connection between spending at fast food and full service restuarants we divided the per capita spending by the median household income for the area. When we did it was clear that areas where residents spend more of their income on food prepaired outside of the home had significantly worse health than other areas where this factor was lower. 

Using Tableau we created six maps to display on the website.

A factor that has been identified by other researchers as systematic issue that contributes to poor community health is gennerational poverty. 

The Food Atlas dataset we used included a classification that marked a community as a having Persistant Overall Poverty and Persistant Child Poverty

The definitaion of persistant poverty from USDA:
![poverty def](images/Poverty_definitions.png)

Because we see a corrilation between these metrics and the poor health factors we decided to include the option for users to toggle this factor in our visualizations.


 persistant poverty so we have made that factor togglable in the maps marked by an *

1. Obesity Rate By State: The percentage of residents in each state catagorized as 'obese'
2. *Diabetes Rate: The percentage of residents of each county that have been diagnosed with diabetes
3. *Median Household Income: A general measure of poverty at the county level
4. Child Poverty Rate - The percentage of children living in poverty with a filter to toggle between counties that had been classified as being a Persistant Poverty Area
5. *Prepaired Food Spending - This highlights areas where spending on ready to eat food is high in realtion to the median income of the community
6. *Prepaired Food Spending in Areas with High Rates of Diabetes - Top Quartile of Diabetes Rates

A factor that has been identified as systematic issue that contributes to poor community health is economic stagnation. The Food Atlas data we used included a factor that classifies a community as one that faces gnnerational persistant poverty. 

Three of theses maps were configured to allow the user to toggle on an of

### Example Images
#### Diabetes Rate for Adults
![diatese map](images/adult_diabetes_rate.png)


#### Spending on Prepaired Food as Percentage of Income
![food spending](images/food_spending_vs_income.png)

### Website Creation
We created a website using  VS Code, HTML5,  JavaScript, and CSS github pages was used to deploy the website.

[Project Summary Website](https://tmwrose.github.io/Group-1---Food-Deserts-How-They-Affect-Community-Health/)




We created a website using  VS Code, HTML5,  JavaScript, and CSS github pages 
