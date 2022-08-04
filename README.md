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
    - PCT_DIABETES_ADULTS08 - Diabetes Rate 2008
    - PCT_DIABETES_ADULTS13 - Diabetes Rate 2013
    - PCT_OBESE_ADULTS12 - Obesity Rate 2008
    - PCT_OBESE_ADULTS17 - Obesity Rate 2013
- SOCIOECONOMIC
    - MEDHHINC15 - Median Household Income
    - POVRATE15 - Poverty Rate
- RESTAURANTS
    - FFRPTH11 - Fast Food rest per 1000 population 2011
    - FFRPTH16 - - Fast Food rest per 1000 population 2016
    - PCH_FFRPTH_11_16 - - Fast Food rest per 1000 population Percent change
- STORES
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




FROM THE NEIGHBORHOOD HEALTH
GEOID10 - Census Tract ID 10-digit Census Tract ID
CountyCode - County Code County code; contained in Census Tract ID
CountyName - County Name

Diab_YearDX2009_2013 -  Number of deaths with diabetes listed as cause reported BY census tract from 2009-2013

Diab_YearDX2010_2014 - Number of deaths with diabetes listed as cause 2010 to 2014

Cardio_YearDX2009_2013 - 2009 to 2013 Number of deaths with cardiovascular disease listed as cause reported BY census tract from 2009-2013
Cardio_YearDX2010_2014 - 2010 to 2014 Number of deaths with cardiovascular disease listed as cause reported BY census tract from 2010-2014

AllCause_MortalityRate_09_13 - 2009 to 2013 All-cause mortality rate for the period 2009 to 2013 BY census tract
AllCause_MortalityRate_10_14 - 2010 to 2014 All-cause mortality rate for the period 2010 to 2014 BY census tract
Diab_MortalityRate_09_13 - 2009 to 2013 Diabetes mortality rate for the period 2009 to 2013 BY census tract
Diab_MortalityRate_10_14 - 2010 to 2014 Diabetes mortality rate for the period 2010 to 2014 BY census tract

Cardio_MortalityRate_09_13 - 2009 to 2013 Cardiovascular disease mortality rate for the period 2009 to 2013 BY census tract
Cardio_MortalityRate_10_14 - 2010 to 2014 Cardiovascular disease mortality rate for the period 2010 to 2014 BY census tract