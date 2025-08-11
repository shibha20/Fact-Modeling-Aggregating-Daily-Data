# Fact-Modeling-Aggregating-Daily-Data
array_metrics Table and Data Aggregation
This SQL script manages monthly aggregated user metrics by building and maintaining arrays of daily site hits per user.
Overview


Clear Existing Data:
Deletes all rows from the array_metrics table to reset the data.



Table Creation:
Creates the array_metrics table with the following columns:
user_id (NUMERIC): Unique identifier for the user.
month_start (DATE): First day of the month for which metrics are aggregated.
metric_name (TEXT): Name/type of the metric, e.g., 'site_hits'.
metric_array (REAL[]): An array storing daily metric values within the month.
The primary key is a composite of (user_id, month_start, metric_name).


Daily Aggregation:
Aggregates the number of site hits per user for a specific day (2023-01-04) from an events table.
Combining with Previous Data:
Joins aggregated data with the previous day's metric arrays (2023-01-03) from array_metrics.
If an existing array is found, today's count is appended; otherwise, a zero-filled array is created up to the current day, and today's count is added.


Upsert Behavior:
Inserts new records or updates existing ones in array_metrics based on the primary key.
On conflict, the metric_array is updated with the new combined data.
Usage Notes
Modify the date filters in the query ('2023-01-04' and '2023-01-03') as needed to process different days.
The script assumes the existence of an events table with columns user_id and event_time.
This approach builds a cumulative array metric for each user, growing daily as new data is processed.
<img width="566" height="321" alt="Screenshot 2025-08-11 at 12 34 37 PM" src="https://github.com/user-attachments/assets/6355b951-e417-4457-a733-195ec19808ac" />
