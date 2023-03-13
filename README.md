# **Bellabeat-Case Study**
### [**Google Data Analyst Certificate - Capstone**](https://www.coursera.org/professional-certificates/google-data-analytics)
---

## Introduction
I work for Bellabeat, a high-tech manufacturer of health-focused products for women, as part of the marketing analysis team. Our Chief Creative Officer, Urška Sršen, is a firm believer in the potential of smart device fitness data to unlock new growth opportunities for our company.

To this end, we decided to analyze data from a competitor's (FitBit) device to gain insight into how consumers use smart devices. Using these insights, we aim to apply them to improve the performance of our own products. As part of this process, I was tasked with analyzing Fitbit data and presenting my findings and recommendations to the team.

My goal is to identify opportunities to improve one of Bellabeat's products using the insights gained from the analysis of competitor's data. By leveraging the data, we hope to enhance our product offerings and better meet the needs of our customers.

### Case Study Strategy
As I embark on the Google Data Analyst Course, I will utilize a comprehensive six-step data analysis process to accomplish the goal of this case study. The process begins with posing the right questions (Ask), followed by gathering data and ensure it is ready for analysis (Prepare), then cleaning relevant data and using statistical and computational methods to derive valuable insights (Process). The main part is, analyzing the processed data to uncover patterns, trends, and other valuable insights (Analyze). Once the data is analyzed, I will share my findings and insights with stakeholders (Share) and identify actionable steps to achieve the desired outcome (Act).
<br>
<br>

## Ask
> **Business Task**
1. What are the latest trends in smart device usage?
2. How can we apply these trends to better serve Bellabeat customers?
3. In what ways can these trends inform and enhance Bellabeat's marketing strategy?

> **Key Stakeholders**
1. Urška Sršen: Bellabeat's Chief Creative Officer and cofounder
2. Sando Mur: Mathematician and cofounder of Bellabeat
3. Bellabeat marketing analytics team: A team of skilled data analysts tasked with collecting, analyzing, and interpreting data that informs and guides Bellabeat's marketing strategy

> **Data**

 &nbsp;&nbsp; The data set is publicly available in [Kaggle, FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit)
 
 > **Tools**
 
&nbsp;&nbsp; Excel, SQL and Tableau
<br>
<br>

## Prepare
> **Summary Of Data**

&nbsp;&nbsp; The Kaggle database contains a wealth of information, comprising of eighteen different files, each detailing various aspects of activity, such as steps, intensity, calories burned, sleep patterns, heart rate and weight, among other metrics. The data pertains to approximately 33 Fitbit users and covers a two-month period in 2016.

> **Limitations of Data**
1.	Data has only two months of records and it is recorded in 2016, we can say it is out-dated
2.	User participation is inconsistent, few data have only below 30 IDs recorded
3.	The sample size is too small, considering [FitBit has approximately 30 million users.](https://www.statista.com/statistics/472600/fitbit-active-users/) 
<br>

## Process
Cleaning and sorting would be done with Excel for normal data sets and SQL will be used for large data sets. 

> **Below is the summary table of Excel data cleaning**


| File name                  | Format issues | Duplicates | Null values & Empty rows | Inconsistent data | ID String count | Total IDs recorded |
|----------------------------|---------------|------------|--------------------------|------------------|--------------|-------------------|
| weightLogInfo_merged       | Yes           | No         | No                       | Yes              | 10           | 8                 |
| sleepDay_merged            | Yes           | Yes        | No                       | Yes              | 10           | 24                |
| dailyCalories_merged       | Yes           | No         | No                       | No               | 10           | 33                |
| dailySteps_merged          | Yes           | No         | No                       | No               | 10           | 33                |
| dailyIntensities_merged    | Yes           | No         | No                       | Yes              | 10           | 33                |
| dailyActivity_merged       | Yes           | No         | No                       | No               | 10           | 33                |
| hourlySteps_merged         | Yes           | No         | No                       | No               | 10           | 33                |
| hourlyCalories_merged      | Yes           | No         | No                       | No               | 10           | 33                |
| hourlyIntensities_merged   | Yes           | NO         | No                       | Yes              | 10           | 33                |
| minuteIntensitiesWide_merged | Yes         | No         | No                       | No               | 10           | 33                |
| minuteStepsWide_merged      | Yes         | No         | No                       | No               | 10           | 33                |
| minuteSleep_merged          | Yes         | Yes        | No                       | No               | 10           | 24                |
| minuteCaloriesWide_merged   | Yes         | No         | No                       | Yes              | 10           | 33                |


*	 All files have format issues with date/time: for clearing that, I have changed the format into custom date/time as ‘dd:mm:yyy hh:mm:ss’, then used the ‘Text in to column’ function to split the date and time.
*	Duplicates: only two files have duplicate issues, used ‘Remove duplicate’ in ‘Data’ tab
*	Null values & empty rows: checked the empty and null values with ‘Special – find & select' function from ‘Home’ tab
*	Inconsistent data: Few files have issues with decimal points, used the number group to standardize the decimal points. 
*	To find the inconsistent ID numbers, I have used ‘=LEN’ formula, and used ‘filter’ function to check the inconsistency
*	To count the IDs recorded, I have followed this method: the copied the full ID column to new column, and used the ‘remove duplicate’ function from ‘Data’ tab
<br>

> **Below is the summary table for SQL cleaning**

| File name                       | Format issues | Duplicates | Null values & Empty rows | Inconsistent ID/data | Total Users recorded |
|--------------------------------|---------------|------------|--------------------------|----------------------|----------------------|
| heartrate_seconds_merged       | Yes           | No         | No                       | No                   | 15                   |
| minuteCaloriesNarrow_merged    | Yes           | No         | No                       | No                   | 34                   |
| minuteIntensitiesNarrow_merged | Yes           | No         | No                       | No                   | 34                   |
| minuteMETsNarrow_merged        | Yes           | No         | No                       | No                   | 34                   |
| minuteStepsNarrow_merged       | Yes           | No         | No                       | No                   | 34                   |

*	While uploading the data file in Big Query for creating the table, it shows an error and it was unsuccessful. After checking in [the discussion form of Google data analyst capstone]( Google Data Analytics Capstone: Complete a Case Study - Discussions | Coursera) and after research, I have decided to give ‘Edit as text – Schema’

```SQL
[
 {    "description" : "Customer ID",
      "name": "Id",
      "type": "STRING",
      "mode": "NULLABLE"
  },
  {   "description" : "Activity time & date",
      "name": "ActivityMinute",
      "type": "TIMESTAMP",
      "mode": "NULLABLE"
  },
  {   "description" : "Activity intensity",
      "name": "Intensity",
      "type": "FLOAT",
      "mode": "NULLABLE"
   }
  ]
  ```
  
  * Split the date and time into different columns
 
```SQL
--The query is extracting the Id, ActivityMinute, and Value columns from a table called heartrate_seconds in the bellabeat_capstone_fitbitdata dataset.

SELECT 
 Id,
TRIM(SUBSTR(ActivityMinute, 1, instr(ActivityMinute,' '))) AS Date,
TRIM(SUBSTR(ActivityMinute, instr(ActivityMinute,' '))) AS Time, Value
FROM 
 `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.heartrate_seconds`
 ```
 
 
  
   
