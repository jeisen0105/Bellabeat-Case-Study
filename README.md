# Bellabeat-Case-Study

### Table of Contents
Introduction
Background
Scenario
Ask
Prepare
Process
Analyze
Share
Act


## Introduction 

In this project I will be examining the Bellabeat Wellness Technology Case Study which is a capstone project for the Google Data Analytics Professional Certificate. I will examine this case study and address key business questions using the different steps I learned from the course including; to ask, prepare, process, analyze, share and act.

## Background

Founded in 2013 by Urška Sršen and Sando Mur, Bellabeat is a high-tech company that specializes in manufacturing health-focused products designed to interact with one another for women. Bellabeat's products collect data on activity, sleep, stress, and reproductive health, empowering women with knowledge about their own health and habits. Since its inception, Bellabeat has quickly grown into a leading tech-driven wellness company for women. By 2016, Bellabeat had expanded its operations, opening offices worldwide and launching multiple products available on its company website and through various online retailers. 
Bellabeat offers a vast array of products, including the Bellabeat app which provides users with health data related to their activity, sleep, stress, menstrual cycle, and mindfulness habits. Their product line also features the Leaf, a versatile wellness tracker that can be worn as a bracelet, necklace, or clip; the Time, a wellness watch combining classic aesthetics with smart technology to track activity, sleep, and stress; and finally, the Spring, a smart water bottle that tracks daily water intake. These smart technology options can all connect, enabling data-driven insights. In addition, Bellabeat provides a subscription-based membership program offering 24/7 access to fully personalized guidance on nutrition, activity, sleep, health and beauty, and mindfulness, tailored to individual lifestyles and goals. 

## Scenario 

In this hypothetical case study I am working as a junior data analyst working on the marketing analyst team at Bellabeat and will be presenting my findings as well as possible solutions to the Bellabeat executive team. My report will specifically entail a clear statement on the business task, a description of data used, documentation of cleaning or manipulation of data, a summary of analysis, supporting visualizations and my top recommendations based on the analysis.

## Ask

## Prepare

```r
# Install and load necessary packages
install.packages("tidyverse")
library(tidyverse)
install.packages("ggplot2")
library(ggplot2)
install.packages("scales")
library(scales)
install.packages("dplyr")
library(dplyr)
install.packages("tidyr")
library(tidyr)

# Import datasets
daily_activity <- read.csv("dailyActivity_merged.csv")
daily_calories <- read.csv("dailyCalories_merged.csv")
daily_intensities <- read.csv("dailyIntensities_merged.csv")
daily_steps <- read.csv("dailySteps_merged.csv")
sleep <- read.csv("sleepDay_merged.csv")
hourly_intensities <- read.csv("hourlyIntensities_merged.csv")
hourly_steps <- read.csv("hourlySteps_merged.csv")
```

Process:

```r
# Cleaning and Formatting
daily_activity$Ymd <- as.Date( daily_activity$ActivityDate, format=" %m/%d/%Y")
str(daily_activity)

daily_steps$Ymd <- as.Date(daily_steps$ActivityDay, format=" %m/%d/%Y")
str(daily_steps)

daily_intensities$Ymd <- as.Date(daily_intensities$ActivityDay, format=" %m/%d/%Y")
str(daily_intensities)

daily_calories$Ymd <- as.Date(daily_calories$ActivityDay, format=" %m/%d/%Y")
str(daily_calories)

sleep$Ymd <- as.Date(sleep$SleepDay, format=" %m/%d/%Y")
str(sleep)

hourly_intensities$ActivityHour=as.POSIXct(hourly_intensities$ActivityHour, format="%m/%d/%Y %I:%M:%S %p", tz=Sys.timezone())
hourly_intensities$time <- format(hourly_intensities$ActivityHour, format = "%H:%M:%S")
hourly_intensities$date <- format(hourly_intensities$ActivityHour, format = "%m/%d/%y")
str(hourly_intensities)

hourly_steps$ActivityHour=as.POSIXct(hourly_steps$ActivityHour, format="%m/%d/%Y %I:%M:%S %p", tz=Sys.timezone())
hourly_steps$time <- format(hourly_steps$ActivityHour, format = "%H:%M:%S")
hourly_steps$date <- format(hourly_steps$ActivityHour, format = "%m/%d/%y")
str(hourly_steps)

# Verify the number of participants
n_distinct(daily_activity$Id)
n_distinct(daily_calories$Id)
n_distinct(daily_intensities$Id)
n_distinct(daily_steps$Id)
n_distinct(sleep$Id)
n_distinct(hourly_intensities$Id)
n_distinct(hourly_steps$Id)

# Look for any duplicates and remove them
sum(duplicated(daily_activity))
sum(duplicated(daily_calories))
sum(duplicated(daily_intensities))
sum(duplicated(daily_steps))
sum(duplicated(sleep))
sum(duplicated(hourly_intensities))
sum(duplicated(hourly_steps))

sleep <- sleep %>% # Remove duplicates
  distinct() %>%
  drop_na()

#Merge datasets sleep and daily activity
colnames(daily_activity) <- gsub("\\s", "", colnames(daily_activity))
colnames(sleep) <- gsub("\\s", "", colnames(sleep))

merged_data <- merge(sleep, daily_activity, by = "Id")
glimpse(merged_data)
```

Analyze:

Share:

Act:








