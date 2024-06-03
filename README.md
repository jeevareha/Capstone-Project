# Capstone-Project
# Data Analysis Case Study - Bellabeat

# BELLA BEAT - FITBIT FITNESS TRACKER DATA ANALYSIS


Bellabeat is a high-tech women health products manufacturer. This company owns a list of health specific smart devices. The below analysis is regarding the usage of smart devices by the customers and to explore the possibilities of recommendations for Bellabeat’s marketing strategy.

# ASK

# BUSINESS TASK:
1. What are some trends in smart device usage? 
2. How could these trends apply to Bellabeat customers? 
3. How could these trends help influence Bellabeat marketing strategy?

# STAKEHOLDERS:
○ Urška Sršen: Bellabeat’s cofounder
○ Sando Mur: Mathematician and Bellabeat’s cofounder
○ Bellabeat marketing analytics team


# PREPARE

Data considered for this analysis is a public data that explores smart device users’ daily habits for FitBit Fitness Tracker

● FitBit Fitness Tracker Data (CC0: Public Domain, dataset made available through Mobius): This data set is obtained from Kaggle. It includes     
  information about daily activity, steps, and heart rate that can be used to explore users’ habits  of 30 Fitbit users who consented to the 
  submission of personal tracker data.

  ### List of tables in the data 
     1 daily_activity_merged
     2 dailyCalories_merged
     3 daily_intensities_merged
     4 dailySteps_merged
     5 heartrate_seconds_merged
     6 hourlyCalories_merged
     7 hourlyIntensities_merged
     8 hourlySteps_merged
     9 minuteCaloriesNarrow_merged
    10 minuteCaloriesWide_merged
    11 minuteIntensitiesNarrow_merged
    12 minuteIntensitiesWide_merged
    13 minuteMETsNarrow_merged
    14 minuteSleep_merged
    15 minuteStepsNarrow_merged
    16 minuteStepsWide_merged
    17 sleepDay_merged
    18 weightLogInfo_merged


● There are 18 tables in the data set.

● The tables considered for analysis are 
  - Daily_activity_merged - This table has the consolidated data from the tables like dailyCalories_merged, daily_intensities_merged,                     dailySteps_merged and the corresponding hourly and minute based data tables.
  - sleepDay_merged - This table has the daily sleep data. This is merged with Daily_activity_merged table for analysis purpose
  - weightLogInfo_merged - This table has Weight, FAT and BMI. This has 67 records with mostly NULL values for FAT


# Process

● Downloaded the complete data set available.

● Identified the time frame of the available data (12 Apr 2016 - 12 May 2016)

● Used Google Sheets, BigQuery and Tableau for the analysis.

● Removed duplicates using google sheets

<img width="436" alt="Screenshot 2024-06-03 at 12 38 21 PM" src="https://github.com/jeevareha/Capstone-Project/assets/32441508/0ef19805-d798-4eb7-9167-f675c6fd646a">

● Verified the data types of all the columns.
● Observed too many null values in the “weightLogInfo_merged” when LEFT joined with the primary table “dailyActivity_merged”. Also “weightLogInfo_merged” has very limited data points. Hence the table “weightLogInfo_merged” is not considered for this analysis.

● Imported all the 18 tables into Big Query for merging data for analysis. 

● Merged the “dailyActivity_merged”, “sleepDay_merged” using Big Query.

```
SELECT
   dailyActivity_merged.*,
   sleepDay_merged.SleepDay,
   sleepDay_merged.TotalSleepRecords,
   sleepDay_merged.TotalMinutesAsleep,
   sleepDay_merged.TotalTimeInBed,
  
 FROM
   `bellabeat-fitbit-data-analysis.bellabeat_data.dailyActivity_merged` AS dailyActivity_merged
  LEFT JOIN `bellabeat-fitbit-data-analysis.bellabeat_data.sleepDay_merged` AS sleepDay_merged
   ON dailyActivity_merged.Id = sleepDay_merged.Id
   AND CAST(dailyActivity_merged.ActivityDate AS DATE) = CAST( sleepDay_merged.SleepDay AS DATE)

```
For learning purpose, uploaded and merged the same data using Tableau as well.


<img width="616" alt="Screenshot 2024-06-03 at 12 36 29 PM" src="https://github.com/jeevareha/Capstone-Project/assets/32441508/33eb9bbf-907f-43ae-a818-d9b2ad31c821">


# Analyze

### 1. Figured out usage percentage of the smart devices.
	To do this, used the calculated fields to filter the records that has value > 0 in the “Total Distance” field.
	Then split the filtered records into 3 categories such as “LOW”, “MEDIUM”, “HIGH” and “VERY HIGH”.
	
<img width="351" alt="Screenshot 2024-06-03 at 12 40 03 PM" src="https://github.com/jeevareha/Capstone-Project/assets/32441508/ca60a5d5-fe1a-4c41-9c18-86858166a2a3">
	

#### => Observed that very less percentage of customers are in “LOW USAGE” category.





### 2. Validated the calories burnt against different levels of active minutes.

<img width="544" alt="Screenshot 2024-06-03 at 12 41 38 PM" src="https://github.com/jeevareha/Capstone-Project/assets/32441508/4c035a90-710e-4015-88d2-f606dd5d6f57">

The Calories are split across different buckets such as “LOW”, “MEDIUM”, “HIGH” and “VERY HIGH”.


#### =>  Observed that a good amount of calories are burnt during the “Light Active Minutes” and the “Moderate Active Minutes” as well. (and not just during high active hours)





