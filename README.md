# Investigating-COVID-19-Impact-on-Flights-Delay-Time-For-The-Top-4-Airlines-in-US

# Investigating COVID-19 Impact on Flights Delay Time For The Top 4 Airlines in US

## Table of Contents
- [Introduction](#intro)
- [Dataset Overview](#Dataset)
- [Data Wrangling](#DR)
- [Data Exploration](#DE)
- [Conclusion](#conc)


<a id='intro'></a>
## Introduction

> www.transtats.bts.gov is a website contains various datasets for transportation means details. In this notebook, python popular data analysis packages are used to investigate the COVID-19 effect on flights and the airlines on-time performance for the top 4 airlines (carriers) in US. The data records are taken in May-2018, May-2019, and May-2020. The purpose is to compare 2018 and 2019 May season with the former in 2020 (during the global crisis). There are three datasets (one for each year) that need assessing cleaning. Also, they should be combined first in one DataFrame.

<a id='Dataset'></a>
## Dataset Overview

> The chosen dataset contains 11 columns, 6 of them are interesting features. Each record represents a flight between US states. All flights are on May but in different years (2018, 2019, and 2020). The columns and interesting features are illustrated as following (each is defined by the column name):
- `YEAR`: The year of flight (2018, 2019, or 2020).
- `MONTH`: The month of flight (all 5 (May)).
- `OP_UNIQUE_CARRIER` (carrier code) : Unique Carrier Code. Each code represents   a specific carrier (airline). For example, AA for American Airlines Inc.
- `ORIGIN_STATE_NM` (departure state name): Origin State Name.
- `DEST_STATE_NM` (arrival state name): Destination State Name.
- `DEP_DELAY`: Difference in minutes between scheduled and actual departure time.              Early departures show negative numbers.
- `DEP_DEL15`: If the flight delayed more than 15 minutes on departure, the value will be (1), else (0).
- `ARR_DELAY`: Difference in minutes between scheduled and actual arrival time.                Early arrivals show negative numbers.
- `ArrDel15`: If the flight delayed more than 15 minutes on arrival, the value will be (1), else (0).
- `CANCELLED`: If the flight is canceled, the value will be (1), else (0).
- `DISTANCE`: Distance between airports (miles).		

> The interesting feature are: `YEAR`, `OP_UNIQUE_CARRIER`, `DEP_DELAY`, `ARR_DELAY`, `CANCELLED`, and `DISTANCE`

<a id='DR'></a>
## Data Wrangling

> **Gathering:** Data are collected from [Reporting Carrier On-Time Performance](https://www.transtats.bts.gov/Fields.asp?Table_ID=236)  web page where the required date and features are selected. In this project, there are 3 CSV files downloaded each refers to May-2018, May-2019, and May-2020 flights in the US. Also, the selected features are illustrated in [Dataset Overview](#Dataset) section. 

> **Assessing**: In `exploration_template.ipynb` file, the assessment is applied to check the tidiness and quality of the data. 

> **Cleaning**: After data assessing and evaluation, the following modifications and corrections are applied: 
> - Joining the 3 datasets in one called `df_all` to work on.

> -  Delete the `MONTH` column as all flights are considered in May.
  
> -  Change column names to be more informative and apply lower case for all.

> -  Replace the carriers (airlines) unique codes by their commercial name.

> -  Choose the top 4 carriers that have the largest percent proportion of flights count in 2018 & 2019. All records for the other carriers are deleted.

> -  Order the carriers descendingly with respect to percent proportion of flights count in 2018 & 2019.

> -  Remove all records with `cancelled` = 1 (cancelled flights) from `df_all` and save them in new dataset called `df_cancelled`. The `df_all` now contains only completed flights. 

> -  Drop all records with null values. 

> -  Save the new datasets (`df_all` & `df_cancelled`) as CSV files. 

<a id='DE'></a>
## Data Exploration

> ### 1. Univariate Exploration
>         Q1: How do the delay durations distributed on may among the three years?

> By looking at the delay duration distribution using `seaborn FacetGrid` and `Matplotlib histogram` functions, the delay duration seems to be is skewed to the right (on both departure and arrival). Which means it flights tend to the low delay time. Besides, There are delays below 2000 minutes in 2018 and 2019. However, in 2020 some flights delayed more!

> ### 2. Bivariate Exploration
>        Q2.1: What is the relation between the traveled distance and delay on departure?

> By using `scatter plot` to find the relation between the delay on departure and the distance traveled, it seems to be overlapped in the center. That means most of departure delays fall in the interval [0,500] (in minutes) and appear on the flights with traveled distance between 100 and 3000 miles.

>        Q2.2: How does the cancellation rate changed over the 3 years (especially after COVID-19)?

> By inestigating the cancellation percent proportion for each year (2018, 2019, and 2020), the cancellation increased by approximately 1.5% in may 2019. Consequently, in 2020 the rate increased also by about 1.5%.

> ### 3. Multivariate Exploration
>        Q3.1: What is the flights count for each carrier in each year?

>  Interestingly, may 2018 and 2019 had nearly equal number of flights with respect to each carrier. Nevertheless, may 2020 had sharp decline in flights number (count). Actually the main reason is COVID-19 impact.

>        Q3.2: How do the delay durations differ between the three carriers in each year?

> The delay duration versus the carrier and the year shows something enthralling! The average delay duration for each carrier was positive but in 2020. This means that the flights was departing earlier than the scheduled.(negative value means earlier departure).

<a id='conc'></a>
## Conclusion

All in all, The show that the COVID-19 impact was obvious on sides like the average delay duration and the flights count. However, there are other sides that were not affected vividly like the cancellation rate.
