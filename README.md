<<<<<<< HEAD
# Group-1 Obesity Mortality Rate in Food Deserts

## Presentation
* Analysis of how food deserts can affect a communities diabetes/obesity mortality rate.
* We initially were going to focus on predicting if counties were food deserts or not based on countrywide zip codes, but that would have been a much bigger project than we could finish in 4 weeks, so we narrowed our focus to just diabetes. 
* Our data comes from the Food Atlas by the USDA and data we pulled from the MU study *“A ‘Big Data’ Approach to Understanding Neighborhood Effects in Chronic Illness Disparities.”*
* We are looking to predict the health of a county based on data from food deserts in Michigan. 

## Communication Protocols
* Slack is the main communication method
* Text is the secondary method of communication
* Email is the back-up method of communication in case the first two fail
* Meet as a team at 6PM, the hour before class, on Tuesday and Thursday to review progress

## ERD
![image](https://user-images.githubusercontent.com/100237685/183312296-1b115e6b-e4ea-4b6e-8326-334692879380.png)
=======
# Segment 2 update
## Communication protocols

* In this week's segment, all group members kept in touch via Slack and text messaging as a secondary option. 
* There was also group meetings on Tuesdays and Thursdays 1 hour before the class session.
 
 ##  Outline of the project

 * After multiple discussions among group members and advice from the instructor and teaching assistants, the dataset used for the machine learning process was a single excel file(FoodAtlasEnvironment.xls) derived from the USDA website. 
 * An update to the ERD was also done and it looks as shown below:
  <img width="1015" alt="Screen Shot 2022-08-14 at 9 13 31 PM" src="https://user-images.githubusercontent.com/101376325/184566417-605c43f7-058b-4581-801d-5aba305f5028.png">

  
 * The following 5 steps were followed and explanation in greater detail is included:

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
* We ran the RFR for two possible target variables. The first was the diabetes rate in the population. After scoring our model for predicting that rate we received a 0.9681 factor for our training score and 0.7639 for our test data score. This score does not indicate a particularly accurate model.
  <img width="1202" alt="Screen Shot 2022-08-14 at 8 39 52 PM" src="https://user-images.githubusercontent.com/101376325/184564340-cda36eb1-ee10-43c5-8754-7202cbfca7ef.png">
* When we changed our target feature to the obesity rate we were able to see our training score jump to .9999 and our testing score up to .9964
  <img width="1191" alt="Screen Shot 2022-08-14 at 8 40 53 PM" src="https://user-images.githubusercontent.com/101376325/184564406-3e0c9d08-2e36-4c17-b8c8-ccaa80757508.png">
## Summary
* Our preliminary data analysis yielded some interesting results. The RFR model found that the feature that most contributed to obesity rate was Expenditure per capita at full service restaurants. The measure of expenditure per person at fast food restaurants ranked fifth in our models weight of importance. 
* The categories that ranked second, third and fourth by order of importance all relate to the poverty level of the locale. Two were measure of the percentage of the population that receives federal food assistance in the form of WIC or SNAP benefits. The other measure the factor called Household Food Insecurity.
<img width="400" alt="Screen Shot 2022-08-14 at 8 42 11 PM" src="https://user-images.githubusercontent.com/101376325/184564432-6b5a3364-0144-4604-b52d-d23975be6f07.png">

* While it isn't surprising that many of the factors that contribute the most to bad health at the county level are poverty related. What is interesting and worthy of more exploration is why these three factors in particular stood out when there were a number of other metrics about poverty, including a few that directly measured the poverty rate. 
>>>>>>> d69401e5369ae2fba6229aa7a1442ed2f025862c

