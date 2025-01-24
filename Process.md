# Process
## Key Tasks
### 1. Set up Google Colab for Jupyter Notebook (to write and execute Python code in the cloud): 
```python
Ensure the Google Colab environment is ready by mounting Google Drive, installing necessary libraries, uploading the folder containing all 12 data files needed for the project, and combining all files as a single dataset
from google.colab import drive
drive.mount("/content/drive", force_remount=True)
folder_path = '/content/drive/My Drive/CyclisticProject_raw_files/CyclisticTripData2024'
print(folder_path)

import pandas as pd
import os

folder_path = '/content/drive/My Drive/CyclisticProject_raw_files/CyclisticTripData2024'
file_names = (
"202401DivvyTripdata.csv", "202402DivvyTripdata.csv", "202403DivvyTripdata.csv", "202404DivvyTripdata.csv", "202405DivvyTripdata.csv", "202406DivvyTripdata.csv", "202407DivvyTripdata.csv", "202408DivvyTripdata.csv", "202409DivvyTripdata.csv", "202410DivvyTripdata.csv", "202411DivvyTripdata.csv", "202412DivvyTripdata.csv"
)
all_files = [os.path.join(folder_path, file) for file in file_names]
dataframes = []
for  file in all_files:
    df = pd.read_csv(file, parse_dates=["started_at", "ended_at"])
    dataframes.append(df)
combined_data = pd.concat(dataframes, ignore_index=True)
print(combined_data.info())
print(combined_data.head())
```
### 2. Check for duplicated rows:
```python
print(f"Number of duplicated rows: {combined_data.duplicated().sum()}")
combined_data = combined_data.drop_duplicates()
print(f"Number of duplicate rows after cleaning: {combined_data.duplicated().sum()}")
Number of duplicated rows: 0
Number of duplicate rows after cleaning: 0
```
### 3. Handle Null (missing) values: 
- Identify which columns have missing values and how many
```python
print(combined_data.isnull().sum())
missing_percentage = combined_data.isnull().mean()*100
print(missing_percentage)
```
- Drop rows with missing critical values as this can skew analysis
```python
critical_columns = ["start_station_id", "end_station_id", "end_lat", "end_lng"]
combined_data = combined_data.dropna(subset=critical_columns)
print(combined_data.isnull().sum())
```
- Fill in missing non-critical values, if need be, and check there are no null values any longer 
```python
combined_data["start_station_name"] = combined_data["start_station_name"].fillna("Unknown Station")
combined_data["end_station_name"] = combined_data["end_station_name"].fillna("Unknown Station")
print(combined_data.isnull().sum())
print(combined_data.info())
```
### 4. Transform the data by creating ride_length, day_of_week_name, and month_name columns as these will be needed in the analyse phase
```python
combined_data["ride_length"] = (combined_data["ended_at"] - combined_data["started_at"]).dt.total_seconds()
combined_data["ride_length_hms"] = pd.to_timedelta(combined_data["ride_length"], unit="s")

combined_data["day_of_week"] = combined_data["started_at"].dt.dayofweek
combined_data["day_of_week_name"] = combined_data["started_at"].dt.day_name()

combined_data["month"] = combined_data["started_at"].dt.month
combined_data["month_name"] = combined_data["started_at"].dt.month_name()
```
### Save processed dataset
```python 
save_path = "/content/drive/My Drive/CyclisticProject_raw_files/processed_data.csv"
data.to_csv(save_path, index=False)
print(f"Processed dataset saved at: {save_path}")
```
*This process phase ensures the data is free from errors such as null values, properly transformed, and cleaned for the analysis phase*
