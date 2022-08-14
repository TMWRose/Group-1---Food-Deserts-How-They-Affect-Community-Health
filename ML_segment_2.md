# Segment Two deliverable

##Description of preliminary data processing

Our dataset came in the form a single excel file (FoodAtlasEnvironment.xls). The data was collected and publish by the USDA. 

The data we were looking to extract was spread over nine different sheets. We extracted each sheet as a seperate pandas dataframe and then exported each dataframe to a sperate csv file without doing any furthur processing withing pandas.

We chose to do it this way to furfil the rubrick requirement that we have multiple tables in our database and that we preform at least some kind of join within our database.

## Description of preliminary featyure engineering and feature selection
Across the nine sheets we created there were 73 distinct features. We selected columns from the Atlas data that would hopefully give us insights into the food enviroment for each row. These features included data related to the density food retailers in the county broken down by establishment type, data related to the overall health of the area, population data, and some socioeconomic factors.

After exploring the data we had we decided to drop a few column we had initially selected because they had too many null values to be of any use to us.

Also, for many of these measures we had matched pairs of data with resultes from 2 diffent years. Ultimately we decided to average those pairs as part of our standardizationa nd feature engineering.

Once the data was stanardized we split it using the train_test_split function from sklearn

The other engineering we did before feeding our data into the machine learning model was to standardize it using the StandardizedScaler from the sklearn module.

After a discussion with Kevin Lee we were convinced to try a Random Forrest Regressor to model our data. RFR is a supervised learning algorythm that allows us to test for a single target variable and through an ensamble learning method of using diverging desision trees arrives at a weeighted average for our independent varriables to give us an insight on what independent variables contribute the most to our target feature.

We ran the RFR for two possible target variables. The first was the diabetis rate in the population. after socring our model for predicting that rate we recieves a ____ factor for our traing score and ______ for our test data score

These score don't indicated a particularly accurate model

When we chaged our target feature to the obesisity rate we were happen to see our training score jump to .9999 and our testing score up to .9964





Description of how data was split into training and testing

Explanation of model choice including limitations and benifits
___
