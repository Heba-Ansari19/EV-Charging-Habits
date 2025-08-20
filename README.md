# EV-Charging-Habits

Exploring electric vehicle charging habits, focusing on patterns, peak usage times, charging station demand, and user behavior insights to support sustainable transportation.



## Project Overview
As electric vehicles (EVs) become more popular, access to charging stations (ports) is becoming increasingly important. Many modern apartment buildings are retrofitting their parking garages with **shared charging stations** accessible to all tenants.  

However, with rising demand comes competition — it’s frustrating to go home and find no charging spots available!  

This project analyzes EV charging data to help **apartment building managers** better understand tenants’ charging habits and optimize charging station availability.  

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Objectives / Key Questions
* Find the number of unique individuals that use each garage’s **shared charging stations**.  
* Identify the **top 10 most popular charging start times** (by weekday and hour) for shared charging sessions.  
* Find users whose **average charging duration exceeds 10 hours** on shared stations.  

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Dataset

* **Source:** [Kaggle](https://www.kaggle.com/)  
* **Table:** `charging_sessions`
* **Structure:**

| Column             | Definition                                      | Data Type |
|---------------------|------------------------------------------------|-----------|
| garage_id           | Identifier for the garage/building             | VARCHAR   |
| user_id             | Identifier for the individual user             | VARCHAR   |
| user_type           | Shared or Private station usage                | VARCHAR   |
| start_plugin        | Session start date & time                      | DATETIME  |
| start_plugin_hour   | Hour (0-23) session started                    | NUMERIC   |
| end_plugout         | Session end date & time                        | DATETIME  |
| end_plugout_hour    | Hour (0-23) session ended                      | NUMERIC   |
| duration_hours      | Session duration (hours)                       | NUMERIC   |
| el_kwh              | Electricity consumed (kWh)                     | NUMERIC   |
| month_plugin        | Month of session start                         | VARCHAR   |
| weekdays_plugin     | Day of week session started                    | VARCHAR   |
* **Sample Preview**  
```
sql

SELECT *
FROM charging_sessions
LIMIT 10;
```
This query displays the first 10 rows from the ```charging_sessions``` table to understand the kind of values present in each column and verify that the dataset has been loaded correctly. It helps us get an initial feel for how users interact with charging stations.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Tools & Skills Used

* **SQL (PostgreSQL) Concepts**: ``` SELECT, COUNT, DISTINCT, GROUP BY, HAVING, ORDER BY, LIMIT ```
* **Techniques**: Data exploration & aggregation

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Analysis & Approach

### 1. Exploring the Data
```
sql

SELECT *
FROM public.charging_sessions;
```
This query retrieves all records from the ```charging_sessions``` table, helping us inspect the dataset’s structure, verify data integrity, and understand how users interact with charging stations.

<img width="1223" height="632" alt="image" src="https://github.com/user-attachments/assets/2fa50369-f4e3-4e9a-9bb1-1460db856cc7" />


### 2. Understanding the Datatypes

```
sql

SELECT column_name, data_type
FROM information_schema.columns
WHERE table_name = 'charging_sessions';
```
This query lists all column names along with their respective data types in the ```charging_sessions``` table, helping us identify whether fields are numeric, text, or date/time, which is crucial for deciding how to clean and analyze them.

<img width="1221" height="458" alt="image" src="https://github.com/user-attachments/assets/2181c038-2cf3-4ac1-9feb-7b86d57e52d1" />


### 3. Unique Users per Garage

```
sql

SELECT 
	garage_id, 
	COUNT(DISTINCT user_id) AS num_unique_users
FROM charging_sessions
WHERE user_type = 'Shared'
GROUP BY garage_id
ORDER BY num_unique_users DESC;
```
This query calculates the number of distinct EV users for each garage that uses shared ```charging_stations```. It helps identify which garages experience the most diverse user activity, potentially signaling high demand and the need for more shared infrastructure.

<img width="1219" height="361" alt="image" src="https://github.com/user-attachments/assets/42d3d6fc-eba3-4e44-9ceb-1235d744b8ea" />


### 4. Top 10 Popular Charging Start Times

```
sql

SELECT 
	weekdays_plugin, 
	start_plugin_hour,
	COUNT(*) AS num_charging_sessions
FROM charging_sessions
WHERE user_type = 'Shared'
GROUP BY 
	weekdays_plugin, 
	start_plugin_hour
ORDER BY num_charging_sessions DESC
LIMIT 10;
```
This query reveals the top 10 most common start times for ```charging_sessions``` on shared stations, broken down by weekday and hour. It highlights peak demand periods, helping managers understand when charging stations are most likely to be occupied and plan scheduling or policy changes accordingly.

<img width="1219" height="435" alt="image" src="https://github.com/user-attachments/assets/4dea0a7a-96bf-4920-bbb9-1f45a2b4c3b4" />


### 5. Long Duration Shared Users

```
sql

SELECT 
	user_id, 
	AVG(duration_hours) AS avg_charging_duration
FROM charging_sessions
WHERE user_type = 'Shared'
GROUP BY user_id
HAVING AVG(duration_hours) > 10
ORDER BY avg_charging_duration DESC;
```
This query identifies users whose average ```charging_session``` exceeds 10 hours on shared stations. These users may be monopolizing the stations, reducing availability for others. Highlighting them allows building managers to consider implementing time limits or usage policies.

<img width="1224" height="291" alt="image" src="https://github.com/user-attachments/assets/494f59c2-f5d2-491a-9688-82df1c9f0f66" />

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Insights & Findings

* **High-demand garages**: Certain garages host a significantly higher number of unique EV users, indicating potential hotspots for congestion and the need for additional shared charging infrastructure.
* **Peak usage times**: Charging sessions are most frequently initiated during specific hours on weekdays, suggesting strong behavioral patterns. Building managers could use this insight to introduce time-based scheduling, reservation systems, or incentives for off-peak usage.
* **Long-duration users**: A subset of users consistently occupies shared charging stations for over 10 hours, reducing station availability for others. Identifying these users allows management to enforce usage guidelines or set session limits to ensure fair access for all tenants.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Final Notes

This project demonstrates how SQL can be applied to real-world infrastructure problems, translating raw data into actionable insights. Through this analysis, building managers gain visibility into user behavior, demand peaks, and resource allocation, supporting better planning for EV infrastructure in residential spaces.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------












































