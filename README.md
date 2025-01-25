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
- [SQL](Analyse.md)
- [Tableau](https://public.tableau.com/views/CyclisticBusinessAnalysisVisualizations/WhyWouldCasualRidersWouldBuyMemberships?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
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

## [Analyse](Analyse.md)
The Analyze phase was performed in a cloud-based SQL environment on Google Colab. SQL was used to write and execute queries, uncovering insights for this portion of the project.

The queries ran during this phase include: 
- Total rides by rider type
- Average ride length by rider type
- Frequency of rides by day of the week
- Popular start station
- Popular end station
- Seasonal Trends (Monthly Ride Patterns)
- Time of day of trip by rider type: Casual
- Time of day of trip by rider type: Member

## Share
[View Interactive Dashboard of the Key Insights Below on Tableau Public](https://public.tableau.com/views/CyclisticBusinessAnalysisVisualizations/WhyWouldCasualRidersWouldBuyMemberships?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
 
This phase visualizes key insights derived from the data analysis. These findings include:
1. Total Rides by Rider Type:
- Cyclistic’s current user base consists of approximately 36.16% casual riders and 63.84% annual members, as of 2024.
- This highlights a significant opportunity to target casual riders for membership conversion.
2. Average Ride Length Per Trip by Rider Type:
- Casual riders have an average ride length nearly double that of annual members per trip.
- This suggests that casual riders may primarily use Cyclistic for leisure or tourism, likely to explore the city, resulting in longer trip durations.
3. Time of Day by Rider Type:
- Casual riders take significantly fewer trips in the morning and evening compared to annual members, but the gap closes during the afternoon and night.
- This indicates that annual members are likely commuting professionals who use Cyclistic for work-related travel during peak commute hours.
4. Popular Stations:
- Casual riders frequently use stations densely located along the coastline, while annual members’ usage is more evenly distributed across office and residential areas.
- This suggests that casual riders might favor scenic or leisure-focused routes, whereas members’ trips align more with practical commuting needs.
5. Frequency of Rides by Day of Week:
- During weekdays, casual riders take significantly fewer trips than members. However, this difference narrows during the weekends, suggesting casual riders are more active during their leisure time.
6. Seasonal Trends (Monthly Ride Patterns):
- Casual riders take the majority of their trips between May and October, aligning with warmer weather and tourist activity.
- In contrast, annual members exhibit a steady increase in trips over the year, with a gradual decline between October and December. This consistency reflects year-round commuting patterns.

## Act
Moreno’s goal is to convert casual riders into annual members. Based on the analysis of Cyclistic’s historical bike trip data, here are three actionable strategies:

1. Highlight Cost Savings for Casual Riders to Drive Membership Conversion
- Key Insight: Casual riders account for 36.16% of Cyclistic’s user base and take significantly more rides during May–October, with their total spending on single-day passes during these months potentially exceeding the cost of an annual membership.
- Actionable Strategy:
  - Develop campaigns using data-backed visuals to illustrate how casual riders could save money as annual members, particularly during their peak riding season.
  - Integrate personalized in-app analytics to notify casual riders of their potential savings, factoring in their historic ride patterns (e.g., frequency, duration, and distance).
  - Offer limited-time membership discounts in late spring to capture casual riders’ attention before peak season begins.
2. Introduce Exclusive Benefits for Annual Members Without Impacting Profitability
- Key Insight: Casual riders’ average ride length is nearly double that of annual members, indicating they often use Cyclistic for leisure or tourism. Their frequency also spikes on weekends and during warmer months, aligning with recreational activities.
- Actionable Strategy:
  - Allow annual members to rent a second bike at a reduced rate during non-peak hours, appealing to casual riders who ride for leisure with companions.
  - Implement a free trial membership that includes perks like access to popular stations, discounts on group rentals, and detailed cost-savings reports. Use the trial period to show casual riders their potential annual savings and exclusive benefits they’d miss out on without a membership.
  - Capitalize on the longer average ride lengths of casual riders by offering scenic ride recommendations exclusively for annual members.
3. Leverage Digital Media to Target Casual Riders at Key Locations and Times
- Key Insight: Popular stations and peak ride times differ significantly between casual and annual riders, presenting targeted advertising opportunities.
- Actionable Strategy:
  - Use digital ads (Google, Instagram, and YouTube) geo-targeted to stations most frequented by casual riders.
  - Highlight member benefits such as cost savings and exclusive perks during these campaigns.
  - Deploy app notifications that dynamically track casual riders’ behavior, prompting them to upgrade to membership at high-use points or seasonal trends.
