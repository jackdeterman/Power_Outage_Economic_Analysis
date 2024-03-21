# Power Outage Economic Analysis
**Author: Jack Determan**

## Project Overview
Originally for DSC80 at the University of California, San Diego, this project examines economic markers and potential explanatory economic trends in the context of major power outages in the United States. The original dataset can be accessed [in this article](https://www.sciencedirect.com/science/article/pii/S2352340918307182).

## Introduction
The reliability and resilience of power infrastructure play a pivotal role in ensuring smooth economic operations in the United States. Further, higher economic activity bolsters infrastructure, creating a fascinating mutualistic relationship. Through an analytical lens, this project seeks to unravel the complex characteristics that underpin this interaction, centered around the probing question: "How do the economic characteristics of a state or region influence the impact of major power outages, and conversely, how do such power outages affect the area's economy?" The relevance of this question extends beyond academic curiosity; it touches the core of the economic inequities in our country. Understanding the economic ramifications of power outages is paramount as our societies become increasingly dependent on stable electricity supply. This analysis aims to illuminate the direct effects of and shed light on how economic factors might amplify or mitigate these consequences.

The dataset used in this project, comprising 1534 rows and 56 columns, serves as a comprehensive canvas to explore this nuanced interconnectedness. Only a handful of columns were used for the bulk of this analysis, and they can be broken into a few categories;


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

