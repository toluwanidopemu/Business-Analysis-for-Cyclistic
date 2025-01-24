# Analyse
## Key Tasks
### 1. Set up Google Colab for SQLite (to write and execute SQL code):
- Install necessary libraries
- Mount Google Drive
- Upload the processed combined dataset 
- Create a SQLite database in memory 
- Write the dataset to the SQLite database
- Verify the data is loaded
```sql
import sqlite3
import pandas as pd
import os

from google.colab import drive
drive.mount('/content/drive')

file_path = '/content/drive/My Drive/CyclisticProject_raw_files/processed_data.csv'

conn = sqlite3.connect('cyclistic_data.db')

data.to_sql('cyclistic_data', conn, index=False, if_exists='replace')

query = "SELECT * FROM cyclistic_data LIMIT 5;"
result = pd.read_sql_query(query, conn)
print(result)
```
### 2. Run SQL queries
- Total rides by rider type
```sql
import sqlite3
import pandas as pd
import os
conn = sqlite3.connect('cyclistic_data.db')
data.to_sql('cyclistic_data', conn, index=False, if_exists='replace')
query = """
SELECT member_casual, COUNT(*) AS total_rides
FROM cyclistic_data
GROUP BY member_casual;
"""
df = pd.read_sql_query(query,conn)
print(df)
df.to_csv('/content/drive/My Drive/CyclisticProject_raw_files/Total_Ride_By_Rider_Type.csv', index=False)
print("total ride length  by rider type saved successfully!")
conn.close()
```
- Average ride length by rider type
```sql
import sqlite3
import pandas as pd
import os
conn = sqlite3.connect('cyclistic_data.db')
query = """
SELECT member_casual, AVG(ride_length) AS avg_ride_length
FROM cyclistic_data
GROUP BY member_casual
ORDER BY avg_ride_length DESC;
"""
df = pd.read_sql_query(query, conn)
print(df)
df.to_csv('/content/drive/My Drive/CyclisticProject_raw_files/Average_Ride_Length_By_Rider_Type.csv', index=False)
print("average ride length  by rider type saved successfully!")
conn.close()
```
- Frequency of rides by day of the week
```sql
import sqlite3
import pandas as pd
import os
conn = sqlite3.connect('cyclistic_data.db')
query = """
SELECT day_of_week_name, member_casual, COUNT(*) AS total_rides
FROM cyclistic_data
GROUP BY day_of_week_name, member_casual
ORDER BY day_of_week ASC
"""
df = pd.read_sql_query(query, conn)
print(df)
df.to_csv('/content/drive/My Drive/CyclisticProject_raw_files/Frequency_Of_Rides_By_Day_Of_The_Week.csv', index=False)
print("frequency of rides by day of the week saved successfully!")
conn.close()
```
- Popular start station
```sql
import sqlite3
import pandas as pd
import os
conn = sqlite3.connect('cyclistic_data.db')
query = """
SELECT start_station_name,start_lat, start_lng, member_casual, COUNT(*) AS total_rides
FROM cyclistic_data
GROUP BY start_station_name, start_lat, start_lng, member_casual
ORDER BY total_rides DESC
LIMIT 15;
"""
df = pd.read_sql_query(query, conn)
print(df)
df.to_csv('/content/drive/My Drive/CyclisticProject_raw_files/Popular_Start_Station.csv', index=False)
print("popular start station saved successfully!")
conn.close()
```
- Popular end station
```sql
import sqlite3
import pandas as pd
import os
conn = sqlite3.connect('cyclistic_data.db')
query = """
SELECT end_station_name,end_lat, end_lng, member_casual, COUNT(*) AS total_rides
FROM cyclistic_data
GROUP BY end_station_name, end_lat, end_lng, member_casual
ORDER BY total_rides DESC
LIMIT 15;
"""
df = pd.read_sql_query(query, conn)
print(df)
df.to_csv('/content/drive/My Drive/CyclisticProject_raw_files/Popular_End_Station.csv', index=False)
print("popular end station saved successfully!")
conn.close()
```
- Seasonal Trends (Monthly Ride Patterns)
```sql
import sqlite3
import pandas as pd
import os
conn = sqlite3.connect('cyclistic_data.db')
query = """
SELECT month_name, member_casual, COUNT(*) AS total_rides
FROM cyclistic_data
GROUP BY month_name, member_casual
ORDER BY month ASC;
"""
df = pd.read_sql_query(query, conn)
print(df)
df.to_csv('/content/drive/My Drive/CyclisticProject_raw_files/Seasonal_Trend__By_Rider_Type.csv', index=False)
print("seasonal trend (month) by rider type saved successfully!")
conn.close()
```
- Time of day of trip by rider type: Casual
```sql
import sqlite3
import pandas as pd
import os
conn = sqlite3.connect('cyclistic_data.db')
query = """
SELECT
    CASE
        WHEN CAST(STRFTIME('%H', started_at) AS INTEGER) BETWEEN 5 AND 11 THEN 'Morning'
        WHEN CAST(STRFTIME('%H', started_at) AS INTEGER) BETWEEN 12 AND 16 THEN 'Afternoon'
        WHEN CAST(STRFTIME('%H', started_at) AS INTEGER) BETWEEN 17 AND 20 THEN 'Evening'
        ELSE 'Night'
    END AS time_of_day,
    COUNT(*) AS total_rides
FROM cyclistic_data
WHERE member_casual = 'casual'
GROUP BY time_of_day
ORDER BY total_rides DESC;
"""
df = pd.read_sql_query(query, conn)
print(df)
df.to_csv('/content/drive/My Drive/CyclisticProject_raw_files/Time_Of_Day_Of_Trip_for_Casual_Rider.csv', index=False)
print("Time of day of trip for rider type:casual saved successfully!")
conn.close()
```
- Time of day of trip by rider type: Member
```sql
import sqlite3
import pandas as pd
import os
conn = sqlite3.connect('cyclistic_data.db')
query = """
SELECT
    CASE
        WHEN CAST(STRFTIME('%H', started_at) AS INTEGER) BETWEEN 5 AND 11 THEN 'Morning'
        WHEN CAST(STRFTIME('%H', started_at) AS INTEGER) BETWEEN 12 AND 16 THEN 'Afternoon'
        WHEN CAST(STRFTIME('%H', started_at) AS INTEGER) BETWEEN 17 AND 20 THEN 'Evening'
        ELSE 'Night'
    END AS time_of_day,
    COUNT(*) AS total_rides
FROM cyclistic_data
WHERE member_casual = 'member'
GROUP BY time_of_day
ORDER BY total_rides DESC;
"""
df = pd.read_sql_query(query, conn)
print(df)
df.to_csv('/content/drive/My Drive/CyclisticProject_raw_files/Time_Of_Day_Of_Trip_for_Member_Rider.csv', index=False)
print("Time of day of trip for rider type:member saved successfully!")
conn.close()
```
### 3. Save Queries: 
- Queries have been individually saved within each code block above into a unique file but shared folder in Google Drive 

*This analyse phase is about running queries that are to be visually represented in the share phase.*  
