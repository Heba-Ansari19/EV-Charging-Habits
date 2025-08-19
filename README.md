# EV-Charging-Habits

Exploring electric vehicle charging habits, focusing on patterns, peak usage times, charging station demand, and user behavior insights to support sustainable transportation.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Project Overview
As electric vehicles (EVs) become more popular, access to charging stations (ports) is becoming increasingly important. Many modern apartment buildings are retrofitting their parking garages with **shared charging stations** accessible to all tenants.  

However, with rising demand comes competition — it’s frustrating to come home and find no charging spots available!  

This project analyzes EV charging data to help **apartment building managers** better understand tenants’ charging habits and optimize charging station availability.  

---

## 🎯 Objectives / Key Questions
- Find the number of unique individuals that use each garage’s **shared charging stations**.  
- Identify the **top 10 most popular charging start times** (by weekday and hour) for shared charging sessions.  
- Find users whose **average charging duration exceeds 10 hours** on shared stations.  

---

## 🗂️ Dataset
**Source:** [Kaggle](https://www.kaggle.com/)  
**Table:** `charging_sessions`  

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

🔎 **Sample Preview**  
```sql
SELECT *
FROM charging_sessions
LIMIT 5;































































