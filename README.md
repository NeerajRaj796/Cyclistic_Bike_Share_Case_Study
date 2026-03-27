# Cyclistic Bike Share Analysis | Google Data Analytics Capstone

This capstone project analyzes Cyclistic bike-share usage patterns using BigQuery SQL and Tableau Public to identify how casual riders and annual members use the service differently, with the aim of supporting membership growth strategies.

Ask, Prepare, Process, Analyze, Share, and Act

The purpose of this analysis is to understand how casual riders and annual members use Cyclistic bikes differently. The business goal is to use these insights to support marketing strategies that can encourage more casual riders to become annual members.

---

## Ask

### Business Task

Cyclistic’s marketing team wants to increase the number of annual memberships, since annual members are more profitable than casual riders. To support that goal, this analysis focuses on the following question:

**How do annual members and casual riders use Cyclistic bikes differently?**

The answer to this question can help the company design more targeted and effective marketing campaigns.

### Stakeholders

The key stakeholders in this case study are:

- Lily Moreno – Director of Marketing
- Cyclistic Marketing Analytics Team
- Cyclistic Executive Team

These stakeholders need clear, data-backed insights to approve future membership growth strategies.

---

## Prepare

### Background

Cyclistic is a bike-share company in Chicago with thousands of bikes and hundreds of docking stations. It offers flexible pricing options, including:

- single-ride passes
- day passes
- annual memberships

Riders are grouped into two categories:

- Casual riders: customers who use single-ride or day passes
- Members: customers who purchase annual memberships

Cyclistic believes that attracting more annual members is important for long-term growth, and this case study aims to support that objective with data.

### Data Source

The dataset used in this project consists of 12 months of Cyclistic trip data. It contains trip-level information such as:

- ride ID
- bike type
- start and end timestamps
- station names
- geographic coordinates
- rider type (`member_casual`)

The data was made available by Motivate International Inc. and is commonly used for this capstone project.

### Tools Used

To complete the project, the following tools were used:

- Google BigQuery (SQL) for data cleaning, transformation, and analysis
- Tableau Public for dashboard creation and visualization

### Data Storage

The 12 monthly datasets were uploaded into BigQuery and stored in the following project and dataset:

- Project ID: `project-324115b5-56af-44b5-a1a`
- Dataset: `Capstone_cyclistic_data`

Each month was imported as a separate table and later combined into a master table for analysis.

---

## Process

### Data Preparation and Cleaning

The first step in processing was to combine all 12 monthly datasets into a single annual table. This created one unified dataset that could be used for full-year analysis.

### Initial Checks

Before analysis, the data was reviewed for:

- missing values
- invalid timestamps
- abnormal ride durations
- consistency of rider types
- station data completeness

### Observations During Cleaning

The timestamp columns (`started_at` and `ended_at`) had no missing values, which was a good sign for time-based analysis. However, the station name columns had a large number of null values. These were not removed because they likely reflect valid dockless or incomplete station records, and removing them would have excluded a large number of legitimate rides.

### Ride Duration Validation

Ride duration was calculated using the difference between `ended_at` and `started_at`. During validation, the following issues were found:

- some rides had negative durations
- some rides had durations longer than 24 hours

These were treated as invalid or abnormal trips and excluded from the cleaned dataset.

### New Fields Created

To support analysis, the following derived fields were created:

- `ride_length`: trip duration in minutes
- `day_of_week`: weekday name extracted from the trip start timestamp
- `month`: month name extracted from the trip start timestamp
- `ride_hour`: hour of day extracted from the trip start timestamp

### Final Cleaned Dataset

The final cleaned table used for analysis was:

**`cyclistic_cleaned`**

This dataset became the foundation for all SQL analysis and Tableau visualizations.

---

## Analyze

The main analysis focused on identifying behavioral differences between members and casual riders. To keep Tableau fast and efficient, aggregated summary tables were created in BigQuery and exported for dashboard creation.

Below is a detailed explanation of the findings shown across the dashboards.

---

## Cyclistic Rider Behavior and Usage Trends

![Cyclistic Rider Behaviour and Usage Overview](Cyclistic_Rider_Behaviour_and_Usage_Overview.png)

This dashboard focuses on overall usage behavior, including ride volume, bike preference, seasonal trends, and peak riding hours.

### A. Total Rides: Member vs Casual

![Member Vs Casual](Member_Vs_Casual.png)

This chart compares the total number of rides taken by members and casual riders.

**Finding:**
- Members: 3,484,202 rides
- Casual riders: 1,915,806 rides

**Interpretation:**

Members take significantly more rides overall than casual riders. This suggests that members use Cyclistic more regularly and may depend on the service as part of their routine transportation habits, such as commuting or recurring daily travel.

Casual riders, while still a large group, appear to use the service less frequently.

### B. Bike Type Preference

![Bike Type Preferences](Bike_Type_Preferences.png)

This chart compares the types of bikes used by each rider group.

**Finding:**

Both groups use electric bikes and classic bikes, but electric bikes show especially high usage.

**Interpretation:**

Bike type preference appears strong across both groups, but usage is still higher among members simply because they ride more overall. The strong demand for electric bikes may indicate that convenience and ease of riding matter to both rider types.

### C. Seasonal Usage Patterns

![Seasonal Usage Patterns](Seasonal_Usage_Patterns.png)

This chart shows total rides by month for members and casual riders.

**Finding:**
- Ride activity increases steadily from spring into summer
- Peak usage occurs in July and August
- Activity drops during winter

**Interpretation:**

Casual riders show stronger seasonal spikes, suggesting leisure or recreational use. Members show more stable usage.

### D. Peak Ride Hours

![Peak Ride Hours](Peak_Ride_Hours.png)

This chart shows hourly ride behavior throughout the day.

**Finding:**
- Members peak in morning and evening
- Casual riders peak later in the day

**Interpretation:**

Members show commuting behavior, while casual riders show leisure-based usage.

---

## Cyclistic Ride Duration and User Behavior Analysis

![Ride_Duration_&_User_Behavior_Analysis](Ride_Duration_&_User_Behavior_Analysis.png)

This dashboard focuses on trip duration, weekday vs weekend differences, popular stations, and how rider behavior changes across the week.

### E. Average Ride Duration

![Average Ride Duration](Average_Ride_Duration.png)

This chart compares the average ride duration between rider groups.

**Finding:**
- Casual riders: about 19.4 minutes
- Members: about 11.7 minutes

**Interpretation:**

Casual riders clearly take longer trips than members. This suggests that casual riders are more likely to use the bikes for relaxed or extended trips, while members use them for shorter, more practical journeys.

### F. Weekday vs Weekend Rides

![Weekday Vs Weekend Ride](Weekday_Vs_Weekend_Ride.png)

This chart compares usage during weekdays and weekends.

**Finding:**
- Members dominate weekdays
- Casual riders dominate weekends

**Interpretation:**

Members = routine usage  
Casual riders = leisure usage

### G. Ride Duration Distribution

![Ride Duration Distribution](Ride_Duration_Distribution.png)

This chart groups rides into categories such as:

- 0–10 minutes
- 10–30 minutes
- 30–60 minutes
- 60+ minutes

**Finding:**
- Members → short rides
- Casual riders → longer rides

**Interpretation:**

Clear difference in usage patterns.

### H. Top 10 Start Stations

![Top 10 Start Stations](Top_10_Start_Stations.png)

This chart highlights the most frequently used start stations.

**Finding:**
Stations are concentrated in urban and popular areas.

### I. Average Ride Duration by Weekday

![Average Ride Duration On Weekdays](Average_Ride_Duration_On_Weekdays.png)

This chart compares average ride duration across different days of the week.

**Finding:**
Casual riders have longer rides, especially on weekends.

---

## Share

### Dashboard Titles

- Cyclistic Rider Behavior and Usage Trends
- Cyclistic Ride Duration and User Behavior Analysis

### Visualization Summary

The dashboards show:

- ride frequency
- duration differences
- weekday vs weekend usage
- seasonal trends
- peak hours
- bike preferences
- location patterns

---

## Key Findings

### Similarities
- Both groups ride more in summer
- Both prefer similar bike types

### Differences

- Members ride more frequently
- Casual riders ride longer
- Members ride weekdays
- Casual riders ride weekends
- Members show routine usage
- Casual riders show leisure patterns

---

## Act

### Recommendations

1. Launch weekend membership campaigns
2. Run seasonal promotions during summer
3. Highlight cost savings for frequent riders
4. Use time-based digital marketing

---

## Conclusion

Members use Cyclistic for routine, short, commute-based trips. Casual riders use it for longer, leisure-based rides, especially on weekends and in summer.

These insights help Cyclistic design strategies to convert casual riders into members.

---

## Skills Demonstrated

- SQL (BigQuery)
- Data cleaning and validation
- Data analysis
- Tableau dashboards
- Business insights
- Data storytelling

---

## Author

**Neeraj Raj Srinivasa Raju**
