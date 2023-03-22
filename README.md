![Alt text](https://github.com/antonyjiss/Bellabeat-Case-Study/blob/main/Visulization/GitHub%20Cover%20Bellabeat1.png)

# **Bellabeat-Case Study**
### [**Google Data Analyst Certificate - Capstone**](https://www.coursera.org/professional-certificates/google-data-analytics)
---

## Introduction
I work for [Bellabeat](https://bellabeat.com/), a high-tech manufacturer of health-focused products for women, as part of the marketing analysis team. Our Chief Creative Officer, Urška Sršen, is a firm believer in the potential of smart device fitness data to unlock new growth opportunities for our company.

To this end, we decided to analyze data from a competitor's (FitBit) device to gain insight into how consumers use smart devices. Using these insights, we aim to apply them to improve the performance of our own products. As part of this process, I was tasked with analyzing Fitbit data and presenting my findings and recommendations to the team.

My goal is to identify opportunities to improve one of Bellabeat's products using the insights gained from the analysis of competitor's data. By leveraging the data, we hope to enhance our product offerings and better meet the needs of our customers.

### Case Study Strategy
As I embark on the Google Data Analyst Course, I will utilize a comprehensive six-step data analysis process to accomplish the goal of this case study. The process begins with posing the right questions (Ask), followed by gathering data and ensure it is ready for analysis (Prepare), then cleaning relevant data and using statistical and computational methods to derive valuable insights (Process). The main part is, analyzing the processed data to uncover patterns, trends, and other valuable insights (Analyze). Once the data is analyzed, I will share my findings and insights with stakeholders (Share) and identify actionable steps to achieve the desired outcome (Act).
<br>
<br>

## Ask
> ### **Business Task**
1. What are the latest trends in smart device usage?
2. How can we apply these trends to better serve Bellabeat customers?
3. In what ways can these trends inform and enhance Bellabeat's marketing strategy?

> ### **Key Stakeholders**
1. Urška Sršen: Bellabeat's Chief Creative Officer and cofounder
2. Sando Mur: Mathematician and cofounder of Bellabeat
3. Bellabeat marketing analytics team: A team of skilled data analysts tasked with collecting, analyzing, and interpreting data that informs and guides Bellabeat's marketing strategy

> ### **Data**

 &nbsp;&nbsp; The data set is publicly available in [Kaggle, FitBit Fitness Tracker Data](https://www.kaggle.com/datasets/arashnic/fitbit)
 
 > ### **Tools**
 
&nbsp;&nbsp; Excel, SQL and Tableau
<br>
<br>

## Prepare
> ### **Summary Of Data**

&nbsp;&nbsp; The Kaggle database contains a wealth of information, comprising of eighteen different files, each detailing various aspects of activity, such as steps, intensity, calories burned, sleep patterns, heart rate and weight, among other metrics. The data pertains to approximately 33 Fitbit users and covers a two-month period in 2016.

> ### **Limitations of Data**
1.	Data has only two months of records and it is recorded in 2016, we can say it is out-dated
2.	User participation is inconsistent, few data have only below 30 IDs recorded
3.	The sample size is too small, considering [FitBit has approximately 30 million users.](https://www.statista.com/statistics/472600/fitbit-active-users/) 
<br>

## Process
Cleaning and sorting would be done with Excel for normal data sets and SQL will be used for large data sets. 

> ### **Below is the summary table of Excel data cleaning**


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

> ### **Below is the summary table for SQL cleaning**

| File name                       | Format issues | Duplicates | Null values & Empty rows | Inconsistent ID/data | Total Users recorded |
|--------------------------------|---------------|------------|--------------------------|----------------------|----------------------|
| heartrate_seconds_merged       | Yes           | No         | No                       | No                   | 15                   |
| minuteCaloriesNarrow_merged    | Yes           | No         | No                       | No                   | 34                   |
| minuteIntensitiesNarrow_merged | Yes           | No         | No                       | No                   | 34                   |
| minuteMETsNarrow_merged        | Yes           | No         | No                       | No                   | 34                   |
| minuteStepsNarrow_merged       | Yes           | No         | No                       | No                   | 34                   |
<br>

*	While uploading the data file in Big Query for creating the table, it shows an error and it was unsuccessful. After checking in [the discussion form of Google data analyst capstone](https://www.coursera.org/learn/google-data-analytics-capstone/discussions) and after research, I have decided to give ‘Edit as text – Schema’

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
  <br>
  
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
 <br>
 
 * Find duplicates
 
 ```SQL
 --To find duplicates
SELECT DISTINCT * 
FROM 
 `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.minuteIntensitiesNarrow_merged` ;


--If the file shows any duplicates, the below query is used for saving a new table without duplicates 
CREATE TABLE
  bellabeat_capstone_fitbitdata.minuteIntensitiesNarrow_distict
AS
SELECT DISTINCT *
FROM 
 `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.minuteIntensitiesNarrow_merged`;
```
 <br>
 
 * Find null values
 
 ```SQL
 
SELECT *
FROM 
 `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.minuteIntensitiesNarrow_merged`
WHERE Id IS NULL OR Date IS NULL OR Time IS NULL OR Value IS NULL
```
<br>

* Check the consistency of length of ID, since we will be using ID as primary key for joins, so it is important to make sure that it has no error values.

```SQL
SELECT 
 Id,
 LENGTH(Id) AS id_column_length,
 COUNT (*) AS count

 FROM 
 bellabeat-fitbit-data-cleaning.bellabeat_capstone_cleaned_datab1.c1_heartrate_seconds

GROUP BY
 Id,
 id_column_length
HAVING                             --This means that only the groups of records whose Id column lengths differ will be returned
 COUNT (DISTINCT LENGTH(Id)) > 1
 ```
 <br>
 
 * To count the IDs recorded
  
  ```SQL
  SELECT 
COUNT (DISTINCT Id) AS no_of_ids
FROM 
 bellabeat-fitbit-data-cleaning.bellabeat_capstone_cleaned_datab1.c1_heartrate_seconds
 ```
  <br>
 
![Alt text](https://github.com/antonyjiss/Bellabeat-Case-Study/blob/main/Visulization/Screenshot%202023-03-21%201224211.png)
 
  ## Analyze
  
  > ### **Features & Particopation**
  
From the data key features of the FitBit device is identified as Step, Sleep, Heart rate and Weight monitoring
The below table tells the total proportion of participation numbers grouped by key device features 

<div class='tableauPlaceholder' id='viz1679458293728' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;6_&#47;6_16793679130260&#47;Sheet1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='6_16793679130260&#47;Sheet1' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;6_&#47;6_16793679130260&#47;Sheet1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /></object></div> 


### :mag: Key Findings

* Weight and Heart rate monitoring participation is comparatively very low, as we can see there are only 8 IDs logged in weight records
* Since the sample participation is way too low, data related Weight and Heart rate will not be considered for analyses.
* Bellabeat should work on the least taken features of our competitor, combined with [advanced technologies](https://www.edumed.org/spotlight/wearable-tech-smart-devices/)
 <br>
 
> ### **Total hourly sleep analysis**

SQL Query for calculating hourly sleep per person

```SQL
SELECT Id, 
 ROUND(SUM((TotalMinutesAsleep) / 31)/60, 2) AS Total_assleepminuts,  --Total 31 days recorded & divided by 60 - for getting horly sleep
 ROUND(SUM ((TotalTimeInBed) / 31)/60, 2) AS Total_timeinBed
FROM 
 `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.sleepDay_merged_fixed`

GROUP BY
 Id
```
![Alt text](https://github.com/antonyjiss/Bellabeat-Case-Study/blob/main/Table%20Extract/Sleen%20table%20SH.png)

![Alt text](https://github.com/antonyjiss/Bellabeat-Case-Study/blob/main/Visulization/Sleep%20Analysis.png)

### :mag: Key Findings

* Getting sufficient sleep every day is crucial for overall well-being, [Centres for Disease Control and Prevention](https://www.cdc.gov/sleep/about_sleep/how_much_sleep.html) recommends a minimum of 7 hours of sleep for the age range of 18-60. As per record analyses only 5 to 6 people only getting recommended sleep among 24 participants. 
* The resulting pattern shows inconsistent records, here we should consider a few possibilities, 1) The sleep monitoring system with Fitbit is not user-friendly.  2) Most customers have the least concern for the importance of sound sleep as a healthy habit and show little interest in tracking their sleeping patterns. Based on the analysis, the sleeping records of the last 10-11 customers appear that they are averaging less than 4 hours of sleep per day.
 <br>
 
> ### Target Customers
The objective is to determine the group of customers who use health tracking devices consistently.

<div class='tableauPlaceholder' id='viz1679457999724' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;3_&#47;3_16793583274750&#47;Dashboard1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='3_16793583274750&#47;Dashboard1' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;3_&#47;3_16793583274750&#47;Dashboard1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /></object></div>
<br>

### :mag: Key Findings

* The analysis in this context is based on the criterion of [high-intensity activity](https://www.cdc.gov/physicalactivity/basics/measuring/index.html), which is typically recorded as distinct physical activity separate from regular daily activity and requires a dedicated amount of time. This criterion can aid in filtering and scheduling different categories of customers based on their engagement in high-intensity activities.
* Based on the visualization, it is evident that Tuesday and Wednesday are the days when people tend to participate in high-intensity activities more frequently
* Two distinct peaks in high-intensity activity are observed during the day, specifically at 12 pm and 7 pm
* Both of the aforementioned trends point towards the workout schedule of office workers. [Research indicates](https://www.perfectgym.com/en/blog/club-owners/when-gym-least-busy) that office workers tend to have a higher tendency to exercise in the middle of the week, which is consistent with the high-intensity activity observed on Tuesday and Wednesday. Additionally, the peak intensity time at 7 pm aligns with after-office hours, [further supporting](https://www.theladders.com/career-advice/this-is-the-day-of-the-week-people-are-most-likely-to-workout) this trend
<br>

> ### Ratio of Activity Classification
This analysis is to understand customers' daily activity intensity to better understand their activity behavioral patterns.

```SQL
--To find the percentage of each catagory activity
SELECT

  (AVG(SedentaryMinutes)/(AVG(SedentaryMinutes)+AVG(LightlyActiveMinutes)+AVG(FairlyActiveMinutes)+AVG    (VeryActiveMinutes))) * 100 AS Sedentary_percentage,
  (AVG(LightlyActiveMinutes)/(AVG(SedentaryMinutes)+AVG(LightlyActiveMinutes)+AVG(FairlyActiveMinutes)+AVG(VeryActiveMinutes))) * 100 AS Lightly_Active_percentage,
  (AVG(FairlyActiveMinutes)/(AVG(SedentaryMinutes)+AVG(LightlyActiveMinutes)+AVG(FairlyActiveMinutes)+AVG(VeryActiveMinutes))) * 100 AS Fairly_Active_percentage,
  (AVG(VeryActiveMinutes)/(AVG(SedentaryMinutes)+AVG(LightlyActiveMinutes)+AVG(FairlyActiveMinutes)+AVG(VeryActiveMinutes))) * 100 AS Very_Active_percentage

FROM 
 `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.dailyIntensities_merged_fixed`
```

![Alt text](https://github.com/antonyjiss/Bellabeat-Case-Study/blob/main/Visulization/Proportion%20of%20activity.png)
<br>

### :mag: Key Findings
* The largest portion of activity minutes belongs to sedentary activities, accounting for 81.3% of total minutes recorded. The [Fitbit website](https://community.fitbit.com/t5/Web-API-Development/Sedentary-Time-Explanation/td-p/1945560#:~:text=Sedentary%2FActive%20time%20is%20calculated,article%20for%20Hourly%20Activity%20Goals.) explains what is sedentary minutes, it is technically the total inactive minutes of activity recorded. 
* These statistics shows that users are mainly utilizing the FitBit app to record daily routine activities such as commuting, minor movements throughout the day, rather than tracking fitness activities like running.
<br>

> ### Quality Sleep Vs Daily Activity

Attempting to identify any correlations between weekly physical activity and sleep patterns, specifically focusing on the timing of sleep.
<br>
To facilitate analysis, the data from the Daily sleep and Daily intensity datasets were imported into Tableau, and a new data source was created using the 'Dates' column as the primary key. This allowed for easy merging of the two datasets and enabled analysis of the combined data using Tableau's data visualization and analysis tools.

<div class='tableauPlaceholder' id='viz1679458079831' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;5_&#47;5_16793681595090&#47;Sheet6&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='5_16793681595090&#47;Sheet6' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;5_&#47;5_16793681595090&#47;Sheet6&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /></object></div>
<br>

### :mag: Key Findings

* The daily sleep time and daily activity has positive correlation relationship
* This relationship can be used as one of the marketing strategies through the company’s interest in customer’s health and well-being.
<br>

> ### Calories and Intensity

This analysis will focus on calories burned as the main parameter, investigating whether regular daily activities contribute significantly to calorie burn.
In view of three data sets 1) Daily calories 2) Daily steps 3) Daily high-intensive activity.

```SQL
--Creating Inner Join with Daily Calories and Daily Steps, Id - as primary key
SELECT 
    a.Id,
    a.ActivityDay,
    a.Calories,
    b.stepTotal
FROM 
    `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.dailyCalories` AS a
JOIN 
    `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.dailySteps` AS b
ON 
    a.Id = b.Id
    
--Creating Inner Join with Daily Calories and Daily Intensive Activity
SELECT 
    a.Id, 
    a.ActivityDay, 
    a.Calories, 
    b.VeryActiveMinutes
FROM 
    `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.dailyCalories` AS a
JOIN 
    `bellabeat-fitbit-data-cleaning.bellabeat_capstone_fitbitdata.dailyIntensities_merged_fixed` AS b
ON 
    a.Id = b.Id AND a.ActivityDay = b.ActivityDay
```

Two tables results were imported into Tableau and a new data source was created using calories as the primary key.

<div class='tableauPlaceholder' id='viz1679458153338' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;6_&#47;6_16793679130260&#47;Dashboard2&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='6_16793679130260&#47;Dashboard2' /><param name='tabs' value='yes' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;6_&#47;6_16793679130260&#47;Dashboard2&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /></object></div>
<br>

### :mag: Key Findings

* Calories, steps, and intensity activity show consistent momentum until the second day, but after that, steps exhibit a negative correlation while intensity activity exhibits a positive correlation with time.
* While normal daily routines contribute less to burning calories, and intensive activities show a strong positive correlation with calorie burning.
* We can encourage and promote customers to engage in intensive activities to burn more calories.

## Share

The final visulization and presentation available in [Tableau/Jiss](https://public.tableau.com/app/profile/jiss6941)

## Act

> ### Conclusion
* Weight and heart rate monitoring participation is very low, with only 8 IDs logged in weight records. Therefore, data related to weight and heart rate will not be considered for analysis due to the small sample size
* Out of 24 participants, only a few (5-6) achieved recommended sleep. The sleep patterns of the last 10-11 participants indicate they are averaging less than 4 hours of sleep per day, which is unreliable.
* The visualization indicates that high-intensity activities are more frequent on Tuesdays and Wednesdays, with two distinct peaks at 12 pm and 7 pm.e assume that most of our customers are working-class individuals.
* The visualization shows that high-intensity activities are most frequent on Tuesdays and Wednesdays, with two distinct peaks at 12 pm and 7 pm. This led us to assume that our customers are mostly working-class individuals.
* Users primarily use the Fitbit device to track daily routine activities such as commuting and minor movements throughout the day, rather than tracking fitness activities like running and aerobic exercise.
* There is a positive correlation between daily sleep time and daily activity. Additionally, when there is a high-intensity activity, we observe that the duration and quality of sleep is also high
* Regular daily routines have a lower impact on calorie burning, whereas [high-intensity activities](https://thestrongkitchen.com/blog/post/aerobic-vs-anaerobic-exercise-how-to-burn-the-most-fat-and-carbohydrates#:~:text=That%20being%20said%2C%20high%2Dintensity,from%20fat%20during%20anaerobic%20exercise.) show a strong positive correlation with calorie burning. Therefore, focusing on intensive activities is more effective for burning calories.
<br>

> ### Recommendations
* The device features:

We should more focus on underused features of our competitors, we can conduct research on the sleep monitoring, heart rate monitoring, and weight monitoring capabilities of smart devices. By exploring [innovative ideas](https://www.edumed.org/spotlight/wearable-tech-smart-devices/), we can enhance these features and create devices that offer unique advantages and more userfriendly. 
For instance, [wifi connected weight scales](https://www.familyhandyman.com/article/about-smart-scales/#:~:text=Once%20it%20measures%20your%20weight,app%20to%20store%20this%20data.), thereby eliminating the need for manual weight tracking.

* Target Customers:
 
Based on our analysis, we have identified that Fitbit's primary customer base consists of working-class individuals who typically work 9-6 jobs. To expand our reach, Bellabeat can explore the preferences of other customer categories and introduce an application program tailored to [their needs](https://www.thebump.com/a/9-ways-to-work-out-when-you-have-toddler). However, we can still provide support to the working-class category by expanding our marketing efforts.

*	Encouragement and educate customers:

Developing a [motivational](https://www.inkin.com/blog/en/How-A-Fitness-Tracker-Creates-Motivation-And-Accountability) application platform is crucial to encourage customers and help then to be in track, especially since many people do not use FitBit for aerobic exercise. A marketing strategy can be created to emphasize the importance of health also how Bellabeat can help individuals establish healthy routines and [how fitness trackers can boost the health](https://www.webmd.com/fitness-exercise/news/20220726/more-evidence-fitness-trackers-can-boost-your-health).
<br>
This can involve implementing a point system to track activity milestones such as calorie burning and steps taken. Users can receive motivational notes each time they reach a milestone to inspire them to achieve more.
