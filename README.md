# Business Analysis: Cyclistic Bike Sharing Program
This repository contains the Cyclistic bike-sharing business analysis project, exploring trends and insights for casual riders vs. annual members to maximize annual memberships, which will be key for the company's future growth.
## Introduction
In this case study, I will perform many real-world business analyst tasks at a fictional company, Cyclistic. To answer the business task, I will be following these steps of the data analysis process: 
- Ask
- Prepare
- Process
- Analyze
- Share
- Act
### Tools Used
- [Python](Process.md)
- [SQL]
- [Tableau](
## Background
### About Cyclistic
In 2016, Cyclistic launched a successful bike-share program. Since then, the program has grown
to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations
across Chicago. The bikes can be unlocked from one station and returned to any other station
in the system anytime.

Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to
broad consumer segments. One approach that helped make these things possible was the
flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships.
Customers who purchase single-ride or full-day passes are referred to as casual riders.
Customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable
than casual riders. Although the pricing flexibility helps Cyclistic attract more customers,
Moreno believes that maximizing the number of annual members will be key to future growth.

Rather than creating a marketing campaign that targets all-new customers, Moreno, the director of marketing and my manager, believes there is a solid opportunity to convert casual riders into members. She notes that casual riders
are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.

Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into
annual members. In order to do that, however, the team needs to better understand how
annual members and casual riders differ, why casual riders would buy a membership, and how
digital media could affect their marketing tactics. Moreno and her team are interested in
analyzing the Cyclistic historical bike trip data to identify trends.

### Scenario
I am assuming the role of a junior data analyst working on the marketing analyst team at Cyclistic, a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, my team wants to understand how casual riders and annual members use Cyclistic bikes differently. 

From these insights, my team and I will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve our recommendations, so they must be backed up with compelling data insights and professional data visualizations.

## [Ask](Ask.md)
The objective is to analyze Cyclistic’s historical trip data to identify patterns and differences between casual riders and annual members. These insights will inform marketing strategies to convert casual riders into annual members, which will be key to future growth.

## [Prepare](Prepare.md)
### Data Source 
Cyclistic’s historical trip data includes trip data from January 2024 to December 2024, provided by Motivate International Inc. via the Divvy public data license. This public dataset allows exploration of how annual members and casual riders use Cyclistic bikes differently. However, data privacy issues prohibit riders’ personally identifiable information (PII) from being included. As a result, it’s impossible to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

### Data Organization
The data is organized in CSV files for each month. Each file contains rows representing individual trips and columns describing trip details.
| Field Name         | Data Type | Description                                                    |
|--------------------|-----------|----------------------------------------------------------------|
| ride_id            | String    | Unique identifier for each trip                                |
| rideable_type      | String    | Type of bike (e.g., classic, electric)                         |
| started_at         | Timestamp | Date and time the trip started                                 |
| ended_at           | Timestamp | Date and time the trip ended                                   |
| start_station_name | String    | Name of the starting station                                   |
| start_station_id   | String    | Unique identifier for the station where the trip started       |
| end_station_name   | String    | Name of the ending station                                     |
| end_station_id     | String    | Unique identifier for the station where the trip ended         |
| start_lat          | Float     | Latitude coordinate of the station where the trip started      |
| start_lng          | Float     | Longitude coordinate of the station where the trip started     |
| end_lat            | Float     | Latitude coordinate of the station where the trip ended        |
| end_lng            | Float     | Longitude coordinate of the station where the trip ended      |
| member_casual      | String    | Indicates whether the rider is a casual rider or annual member |

### Data Credibility 
A trusted source provides the data, Motivate International Inc., under an open license, ensuring it is ethical and reliable to use. While the data is reliable, there are potential limitations such as missing or inconsistent data fields, which may need to be addressed during the process phase.

## [Process](Process.md)
The process phase was performed in a cloud-based Python environment on Google Colab. Python was used to write and execute the code necessary for data cleaning, manipulation, and transformation. 

- In this phase, the data files were first combined into a single dataset
- Checked the data is represented in the right data type, for example, started_at and ended_at are in datatime64[ns], start_lat/lng and end_lat/lng are in float
- Checked for duplicated rows
- Handled null (missing) values by dropping critical values that can skew the result as well as filling non-critical values
- Transformed the dataset by adding columns such as ride_length, day_of_week_name, and month_name as these will be needed in the analyse phase.
