# ETL Project 6 - Analysis of Covid 19

## OVERVIEW

Utlizing data sets provided by the New York Times and the State of Indiana and Regenstrief Institute, we anaylzed Covid-19 case morbidity rates by Indiana county since March 1, 2020. Our goal is to find cases and hospitalizations by county; then examine death rates related to these figures to understand which counties had the worst case morbidity rates related to hospitalizations and cases

## FINDING DATA

We discovered the New York Times database through Kaggle (https://www.kaggle.com/fireballbyedimyrnmom/us-counties-covid-19-dataset). To understand the scope of the data, we loaded it to a CSV reader through Jupyter notebook. The State of Indiana/Regenstrief data was downlaoded directly from the Regenstrief Institute's Covid-19 dashboard (https://www.regenstrief.org/data-downloads/). We looked at both data sets and preliminarily determined it was feasible to efficiently to conduct the analysis.

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

## BUILDING THE COMBINED DATABASE

1. First, we created a database in PostGres, with two tables containing the respective columns of data we pulled from our two sources.
1. Next, we initiated a connection from Pandas to PostGres.

