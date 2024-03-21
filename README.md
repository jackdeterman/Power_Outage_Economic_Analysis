# Power Outage Economic Analysis
**Author: Jack Determan**

## Project Overview
Originally for DSC80 at the University of California, San Diego, this project examines economic markers and potential explanatory economic trends in the context of major power outages in the United States. The original dataset can be accessed [in this article](https://www.sciencedirect.com/science/article/pii/S2352340918307182).

___
## Introduction
The reliability and resilience of power infrastructure play a pivotal role in ensuring smooth economic operations in the United States. Further, higher economic activity bolsters infrastructure, creating a fascinating mutualistic relationship. Through an analytical lens, this project seeks to unravel the complex characteristics that underpin this interaction, centered around the probing question: "How do the economic characteristics of a state or region influence the impact of major power outages, and conversely, how do such power outages affect the area's economy?" The relevance of this question extends beyond academic curiosity; it touches the core of the economic inequities in our country. Understanding the economic ramifications of power outages is paramount as our societies become increasingly dependent on stable electricity supply. This analysis aims to illuminate the direct effects of and shed light on how economic factors might amplify or mitigate these consequences.

The dataset used in this project, comprising 1534 rows and 56 columns, serves as a comprehensive canvas to explore this nuanced interconnectedness. It represents detailed information on every major power outage in the United States from 2000 to 2016. Only a handful of columns were used for the bulk of this analysis, and they can be broken into a few categories;


#### Geographic / Climate Data

|Column	                 |Description|
|---                     |---        |
|`'State'`            |The state in which the outage occurred|
|`'NERC Region'`	           |The North American Electric Reliability Corporation (NERC) Region in which the outage occurred|
|`'Climate Region'`	           |The U.S. Climate region, as specified by National Centers for Environmental Information, in which the outage occurred|
|`'Climate Category'`	           |The climate episode (Warm, Normal, Cold) corresponding to the year|
|`'Year'`	         |The year in which the outage occurred|

#### Event-Specific Data

|Column	                 |Description|
|---                     |---        |
|`'Duration'`	            |The length of the outage|
|`'Cause Category'`	         |The cause of the outage|
|`'Hurricane Name'`	     |The name of the hurricane that caused the outage, if applicable|
|`'Customers Affected'`	              |The number of customers affected by the outage|

#### Economic Data

|Column	                 |Description|
|---                     |---        |
|`'Demand Loss'`	          |The peak electricity demand loss during the outage|
|`'GSP Relative to USA'`	          |The state's Gross State Product (GSP) per capita, relative to the Gross Domestic Product (GDP) of the United States. Expressed as a fraction.|
|`'Change in GSP'`	              |The percentage change of GSP per capita from the previous year|
|`'Utility Percent of GSP'`	     |The percentage of GSP contributed by utility industry|
|`'Residential Price'`	     |The average price of electricity in the residential sector|

 Now that we have familiarized ourselves with the data, let's continue with our project's set up.

___
## Data Cleaning and Exploratory Data Analysis
### Data Cleaning

While I already presented the columns of the DataFrame that will be valuable to my analysis, the DataFrame required significant cleaning to arrive at a usable state. These are the first five rows of the raw DataFrame __(Make sure to scroll!)__

|    |   OBS |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | OUTAGE.START.DATE         | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE    | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND |
|---:|------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:--------------------------|:--------------------|:---------------------------|:--------------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|
|  0 |     1 |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | Friday, July 1, 2011      | 5:00:00 PM          | Sunday, July 3, 2011       | 8:00:00 PM                | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 | 2.33292e+06 | 2.11477e+06 | 2.11329e+06 |   6.56252e+06 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |         0.4112 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|  1 |     2 |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | Sunday, May 11, 2014      | 6:38:00 PM          | Sunday, May 11, 2014       | 6:39:00 PM                | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 | 1.58699e+06 | 1.80776e+06 | 1.88793e+06 |   5.28423e+06 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |         0.3748 |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|  2 |     3 |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | Tuesday, October 26, 2010 | 8:00:00 PM          | Thursday, October 28, 2010 | 10:00:00 PM               | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 | 1.46729e+06 | 1.80168e+06 | 1.9513e+06  |   5.22212e+06 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |         0.3924 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|  3 |     4 |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | Tuesday, June 19, 2012    | 4:30:00 AM          | Wednesday, June 20, 2012   | 11:00:00 PM               | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 | 1.85152e+06 | 1.94117e+06 | 1.99303e+06 |   5.78706e+06 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |         0.4224 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |
|  4 |     5 |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | Saturday, July 18, 2015   | 2:00:00 AM          | Sunday, July 19, 2015      | 7:00:00 AM                | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 | 2.02888e+06 | 2.16161e+06 | 1.77794e+06 |   5.97034e+06 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |         0.367  |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |

While a daunting DataFrame to clean, I split the process into four steps:
- Remove redundant or valueless columns,
- Perform necessary datatype transformations,
- Create new features using existing data,
- Rename existing columns for readability.

Then, I divided the dataset into components for the data cleaning process to familiarize myself with all of the information conveyed in the dataset. For this, I generally defaulted to the categorizations used by Sayanti Mukherjee, Roshanak Nateghi, and Makarand Hastak in their explanation of the variables in their article [Data on major power outage events in the continental U.S.](https://www.sciencedirect.com/science/article/pii/S2352340918307182). However, this came with numerous adjustments. Within each component, I walked through the four steps I described above.

- __Geographic / Climate Data__: The climate data in the raw dataset was generally very well organized and formatted. In cleaning these columns, I first dropped redundancies present in the `'U.S._STATE'` and `'ANOMALY.LEVEL'` columns. They contained the same information as the `'State'` and `'Climate Category'` columns of the cleaned DataFrame, respectively, and were unnecessary to include. Then, I aggregated the time-related columns in the raw DataFrame into the `'Year'` column of the cleaned DataFrame. This entailed converting one of the columns to a DateTime datatype, extracting its year, and removing the resulting redundancies. I renamed the columns for readability and moved forward.
- __Event-Specific Data__: There was no mechanically challenging data cleaning on any event-specific columns in the raw DataFrame. I removed repetitive columns, renamed the existing ones to the versions you were introduced to, and moved on.
- __Economic Data__: Once again, the economic data in the raw DataFrame was presented very well. There were unnecessary redundancies in the data, so I removed them, renamed the columns, and concluded cleaning the data.

__Note__: Originally, I divided the DataFrame into seven components, and performed data cleaning on all 58 features of the original DataFrame. This resulted in a 36-column DataFrame, but it is unnecessary to include details on the entire data cleaning process for this analysis. As such, I only included data cleaning on portions relevant to my following analysis. But don't worry, _no stone was left unturned!_

The first five rows of the cleaned DataFrame look like this:

|    | State   | NERC Region   | Climate Region     | Climate Category   |   Year |   Duration | Cause Category     | Hurricane Name   |   Customers Affected |   Demand Loss |   GSP Relative to USA |   Change in GSP |   Utility Percent of GSP |   Residential Price |
|---:|:--------|:--------------|:-------------------|:-------------------|-------:|-----------:|:-------------------|:-----------------|---------------------:|--------------:|----------------------:|----------------:|-------------------------:|--------------------:|
|  0 | MN      | MRO           | East North Central | normal             |   2011 |       3060 | severe weather     | None             |                70000 |           nan |               1.07738 |             1.6 |                  1.75139 |               11.6  |
|  1 | MN      | MRO           | East North Central | normal             |   2014 |          1 | intentional attack | None             |                  nan |           nan |               1.08979 |             1.9 |                  1.79    |               12.12 |
|  2 | MN      | MRO           | East North Central | cold               |   2010 |       3000 | severe weather     | None             |                70000 |           nan |               1.06683 |             2.7 |                  1.70627 |               10.87 |
|  3 | MN      | MRO           | East North Central | normal             |   2012 |       2550 | severe weather     | None             |                68200 |           nan |               1.07148 |             0.6 |                  1.93209 |               11.79 |
|  4 | MN      | MRO           | East North Central | warm               |   2015 |       1740 | severe weather     | None             |               250000 |           250 |               1.09203 |             1.7 |                  1.6687  |               13.07 |

### Exploratory Data Analysis

To further our understanding of the information, let's examine some visualizations related to our dataset.

##### Outages over Time
The most fundamental unit of our dataset is power outages, and understanding how their frequency has changed over time is a crucial piece of context to have when conducting any form of analysis on this data. Below, we see the frequency of power outages in every month in our dataset. There is a visible spike in the summer of 2011, when the United States experienced one of the most active hurricane seasons in its history. Climaxing with Hurricane Irene in August but containing a total of 19 named storms, this spike in our dataset makes sense.

<iframe
  src="assets/outages_over_time.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

##### Cause Distribution
Another critical feature in our dataset is the `'Cause Category'` of a power outage. The visualization below displays the distribution of `'Cause Category'`, showing `'Severe Weather'` as the most common cause. While this is intuitive, it is interesting that `'Intentional Attack'` was the second leading cause of major power outages from 2000-2016 in the United States.

<iframe
  src="assets/cause_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

With the more basic, yet critical, visualizations completed, let's explore a few more nuanced relationships before continuing.

##### Cause by Climate Region
This table displays the distribution of `'Cause Category'` between the different `'Climate Region'`s present in our DataFrame. While much of the information is intuitive, it is interesting to note that the West North Central region has a markedly low number of major power outages. Further, I found it interesting that in the South, the second-leading cause of major power outages was `'Public Appeal'`.

<iframe
  src="assets/climate_region_cause.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


##### Power Outages per State per Year
This interactive choropleth displays the number of major power outages per state per year. There are lots of interesting features in this visualization (Look at Washington in 2011, for example), and I welcome you to explore the plot on your own and observe the trends over time!

<iframe
  src="assets/outages_by_year.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Now, let's continue with our analysis.

___
## Assessment of Missingness

### NMAR Data
Data that is Not Missing At Random (NMAR) is data in which the missingness of a value is likely dependent on the value itself. A common example of NMAR data is missing data in a survey about education level. In this example, individuals with lower education levels are less likely to reply to the survey, and as such, the missingness of a value likely depends on what the value would have been.

Let's apply this definition to our dataset to determine whether we have any NMAR data.

First, 

