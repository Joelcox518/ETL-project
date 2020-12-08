# ETL Project 6 - Analysis of Covid 19

## OVERVIEW

Utlizing data sets provided by *The New York Times* and the State of Indiana and Regenstrief Institute, we anaylzed Covid-19 case morbidity rates by Indiana county since March 1, 2020. Our goal is to find cases and hospitalizations by county; then examine death rates related to these figures to understand which counties had the worst case morbidity rates related to hospitalizations and cases

## EXTRACTING DATA 

We discovered *The New York Times* database through Kaggle (https://www.kaggle.com/fireballbyedimyrnmom/us-counties-covid-19-dataset). To understand the scope of the data, we loaded it to a CSV reader through Jupyter notebook. 

The Regenstrief data was in CSV format and was downloaded directly from the Regenstrief Institute's Covid-19 dashboard (https://www.regenstrief.org/data-downloads/). We looked at both data sets and preliminarily determined it was feasible to efficiently to conduct the analysis.

Later we added CSV-formatted from the Indiana State Department Health. Below we explain why we added this third data source. 

## TRANSFORMING DATA

### Regenstrief Institute/Indiana Hospitalization Database 

- We selected the Date and ED Visit columns and set "County" as the index. 
- Grouped the daily cases by Indiana County and summed Hospitalizations by "County"

### NY Times Covid-19 Database

After closer examination of this dataset, we realized that rather than the data being a day-by-day accounting of cases and deaths in each county; the figures provided were cumulative. This presented a challenge not easily overcome, as when we attempted to sum the cases and deaths per county, the output was the sum of the cumulative data points. As a result, we decided to abandon the use of NY Times Covid-19 database in favor of utilizing Indiana State Department of Health (ISDH) accounting deaths and cases by county.

### IDSH Indiana Data Hub - Covid-19 County Statistics 

- From the Indiana ISDH Data Hub we selected: Covid-19 County Statistics, then explored the Covid-19 County Statistics XLS, then filtered by County_Name.
- This produced cumulative, by-county data that included "Covid_Count" (cases) and "Covid_Deaths," 
  - https://hub.mph.in.gov/dataset/covid-19-county-statistics/resource/8b8e6cd7-ede2-4c41-a9bd-4266df783145.
- We chose those two columns and county; eliminating extraneous data ("Location_ID" and "Covid_Test"), which did not serve our purposes for this project.

## LOADING DATA

1. First, we created a database in PostGres, with two tables containing the respective columns of data we pulled from our two sources.
1. Next, we initiated a connection from Pandas to PostGres to allow for analysis of the our combined data.
  1. We chose PostGres because both sets of data were in the CSV format and similar enough that they easily combined.
1. The data is best formatted to be run using SQL queries.
1. We included use of the replace function which will allow future data to be easily added to our resulting database.

## ANALYSIS

- The purpose of this project was to examine Covid-19 morbidity rates in Indiana's 92 counties by analyzing:

    *Counties with the highest percentage of Covid-19 cases that resulted in hospitalization*
    
    1. Orange County
    1. Shelby County
    1. Fayette County
    1. Lagrange County
    1. Decatur County
   
    *Counties with the highest percentage of Covid-19 cases that resulted in death*
    
    1. Greene County
    1. Pulaski County
    1. Tipton County
    1. Orange County
    1. Pike County

- The cleaned and combined data set lends itself further analysis through the addition of further datasets. Potential questions for future study may include:
  - Is there a relationship between a county's predominant political party affiliation and Covid-19 rates?
  - How does a county's educational attainment level affect Covid-19 rates?
  - Is there a statistically-significant relationship between a county's Covid-19 case morbidity rate a its median income?
  
                                                                                *###*
  

 

