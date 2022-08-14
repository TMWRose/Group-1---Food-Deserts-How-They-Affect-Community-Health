# Group-2---Food-Deserts-How-They-Affect-Community-Health
Analysis of data from an MU study in Detroit about how food deserts affect a communities’ health

## 7/30/2022

I wrote a short jupyter notebook to pair down the csv files into smaller pandas dataframes

there is also code in there to send the data into a sql database but that code will need to be modified a little bit to get it to work on your machines.


# NOTES 8/4/2022
##

From the Large FoodEnviromental access dataset. 

places are designated by FIPS code, first two digits are for state, next tree digits are for county. there can be up to seven digits total to get down to the place level. Need connect this to the GEOIS10 code or county code feom the neighborhood effects health status table

we would be able to aggrigate everything down to the county level to match the food atlas set



from the food atlas we want the following columns
- ACCESS TABLE
    - FIPS
    - LACCESS_POP10 - Low access population 2010
    - LACCESS_POP15 - Low access population 2015
    - LACCESS_LOWI10 - Low access + Low income population 2010
    - LACCESS_LOWI15 - Low access + Low income population 2015
    - LACCESS_HHNV10 - Low access + Low income population + No Car 2010
    - LACCESS_HHNV15 - Low access + Low income population + No Car 2015
- HEALTH TABLE
    - FIPS
    - PCT_DIABETES_ADULTS08 - Diabetes Rate 2008
    - PCT_DIABETES_ADULTS13 - Diabetes Rate 2013
    - PCT_OBESE_ADULTS12 - Obesity Rate 2008
    - PCT_OBESE_ADULTS17 - Obesity Rate 2013
- SOCIOECONOMIC
    - FIPS
    - MEDHHINC15 - Median Household Income
    - POVRATE15 - Poverty Rate
- RESTAURANTS
    - FIPS
    - FFRPTH11 - Fast Food rest per 1000 population 2011
    - FFRPTH16 - - Fast Food rest per 1000 population 2016
    - PCH_FFRPTH_11_16 - - Fast Food rest per 1000 population Percent change
- STORES
    - FIPS
    - GROCPTH11 - Grocery stores/1,000 pop, 2011	
    - GROCPTH16 - Grocery stores/1,000 pop, 2016	
    - PCH_GROCPTH_11_16 - Grocery stores/1,000 pop (% change), 2011-16	





FROM THE NEIGHBORHOOD FOOD ENVIRONMENT
    GEOID10 - Census Tract ID 10-digit Census Tract ID
    CountyCode - County Code County code; contained in Census Tract ID
    CountyName - County Name

    Food_Desert_Pct_Lowa_Pop -  Percentage of people with low access to a supermarket or large grocery store 2011
    Food_Desert_lowa_Pop -  Number of people with low access to a supermarket or large grocery store 2011
    Food_Desert_Pct_Lowi - Percentage of total population that is low-income and has low access to a supermarket or large grocery store 2011
    Food_Desert_Lowi - Number of low-income people with low access to a supermarket or large grocery store 2011

    Spatial_Measures_grocerystore_Density - Full-Line Grocery stores - Kernel Density by census tract 2016 
        
    Spatial_Measures_fastfood_density - Fast food stores- Kernel Density by census tract 2
            - would need to transform these column to compair them to the ATLAS data. ATLAS data is fast food per 1000 people. this is average distance to a fast foor / grocery store . 
                - might be doable - transform this into an estimate of stores per 1000 using population data for the census tract so it matches the ATLAS data



FROM THE NEIGHBORHOOD HEALTH
    GEOID10 - Census Tract ID 10-digit Census Tract ID
    CountyCode - County Code County code; contained in Census Tract ID
    CountyName - County Name

    Diab_YearDX2009_2013 -  Number of deaths with diabetes listed as cause reported BY census tract from 2009-2013

    Diab_YearDX2010_2014 - Number of deaths with diabetes listed as cause 2010 to 2014

    Cardio_YearDX2009_2013 - 2009 to 2013 Number of deaths with cardiovascular disease listed as cause reported BY census tract from 2009-2013
    Cardio_YearDX2010_2014 - 2010 to 2014 Number of deaths with cardiovascular disease listed as cause reported BY census tract from 2010-2014

    AllCause_MortalityRate_09_13  2009 to 2013 All-cause mortality rate for the period 2009 to 2013 BY census tract
    AllCause_MortalityRate_10_14 - 2010 to 2014 All-cause mortality rate for the period 2010 to 2014 BY census tract
    Diab_MortalityRate_09_13 - 2009 to 2013 Diabetes mortality rate for the period 2009 to 2013 BY census tract
    Diab_MortalityRate_10_14 - 2010 to 2014 Diabetes mortality rate for the period 2010 to 2014 BY census tract

    Cardio_MortalityRate_09_13 - 2009 to 2013 Cardiovascular disease mortality rate for the period 2009 to 2013 BY census tract
    Cardio_MortalityRate_10_14 - 2010 to 2014 Cardiovascular disease mortality rate for the period 2010 to 2014 BY census tract




# Thursday 8/4/2022 notes
## Dashboard
This sundays submission if just going to be graded on the readme . they want a clear discription of what we are doing. an erd . links to where we found the data sets are also encouraged

Set up a google sheets to do the dashboard layout as Kevin described on thursday 8/4

We will be using a REGRESSION MODEL

TARGET IDEA: We are doing a regression model trying to predict the number of people who die per county.
    - build the prediction model off the data from the 10 michigan counties.
    - We have neighborhood level data for 10 counties that are considered food desserts
        -  we have the population and the diabeties mortality rate (as well as many other mortality rates) 
        - we have fast food
    - We have a county level dataset for the entire nation
        - county level data has population data and data on population that is classified as having low access to quality food as well as low income people who have low access to quality food. We also have the same data at the neighborhood level

## For the neighborhood datasets

- need to add FIPS key to eachline in the neighborhood data
    - lookup fips key based on county name
        - use the fips key to connect in overall diabities and obesity rate for the county to the neighborhood health effects 

### End of night notes Thursday

workbook code now stiches together the ATLAS data from the seperate csv files into a joined dataframe. That dataframe is outputed as mederg_df.csv

### Friday brainstorm

# Not nessisary The CountyCode column is actually the FIPS code, just renamed the column
To grab the FIPS codes and add them to I think we are going to use a for loop and a collection of if elif statements. There are only 10 counties so there will only be a need for that many statements - if CountyCode = _____ then FIPS = ____
elif County Code = ______ then FIPS = _____ and so on.

There is probably a more elegent way to do this with code and if there were more than the 10 different FIPS we were trying to assign it would be worth looking into this more


#### NOTES 8/11/22

