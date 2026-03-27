Cyclistic Bike Share Analysis | Google Data Analytics Capstone

This capstone project analyzes Cyclistic bike-share usage patterns using BigQuery SQL and Tableau Public to identify how casual riders and annual members use the service differently, with the aim of supporting membership growth strategies.

Ask, Prepare, Process, Analyze, Share, and Act

The purpose of this analysis is to understand how casual riders and annual members use Cyclistic bikes differently. The business goal is to use these insights to support marketing strategies that can encourage more casual riders to become annual members.

1. Ask
Business Task

Cyclistic’s marketing team wants to increase the number of annual memberships, since annual members are more profitable than casual riders. To support that goal, this analysis focuses on the following question:

How do annual members and casual riders use Cyclistic bikes differently?

The answer to this question can help the company design more targeted and effective marketing campaigns.

Stakeholders

The key stakeholders in this case study are:

Lily Moreno – Director of Marketing
Cyclistic Marketing Analytics Team
Cyclistic Executive Team

These stakeholders need clear, data-backed insights to approve future membership growth strategies.

2. Prepare
Background

Cyclistic is a bike-share company in Chicago with thousands of bikes and hundreds of docking stations. It offers flexible pricing options, including:

single-ride passes
day passes
annual memberships

Riders are grouped into two categories:

Casual riders: customers who use single-ride or day passes
Members: customers who purchase annual memberships

Cyclistic believes that attracting more annual members is important for long-term growth, and this case study aims to support that objective with data.

Data Source

The dataset used in this project consists of 12 months of Cyclistic trip data. It contains trip-level information such as:

ride ID
bike type
start and end timestamps
station names
geographic coordinates
rider type (member_casual)

The data was made available by Motivate International Inc. and is commonly used for this capstone project.

Tools Used

To complete the project, the following tools were used:

Google BigQuery (SQL) for data cleaning, transformation, and analysis
Tableau Public for dashboard creation and visualization
Data Storage

The 12 monthly datasets were uploaded into BigQuery and stored in the following project and dataset:

Project ID: project-324115b5-56af-44b5-a1a
Dataset: Capstone_cyclistic_data

Each month was imported as a separate table and later combined into a master table for analysis.

3. Process
Data Preparation and Cleaning

The first step in processing was to combine all 12 monthly datasets into a single annual table. This created one unified dataset that could be used for full-year analysis.

Initial Checks

Before analysis, the data was reviewed for:

missing values
invalid timestamps
abnormal ride durations
consistency of rider types
station data completeness
Observations During Cleaning

The timestamp columns (started_at and ended_at) had no missing values, which was a good sign for time-based analysis. However, the station name columns had a large number of null values. These were not removed because they likely reflect valid dockless or incomplete station records, and removing them would have excluded a large number of legitimate rides.

Ride Duration Validation

Ride duration was calculated using the difference between ended_at and started_at. During validation, the following issues were found:

some rides had negative durations
some rides had durations longer than 24 hours

These were treated as invalid or abnormal trips and excluded from the cleaned dataset.

New Fields Created

To support analysis, the following derived fields were created:

ride_length: trip duration in minutes
day_of_week: weekday name extracted from the trip start timestamp
month: month name extracted from the trip start timestamp
ride_hour: hour of day extracted from the trip start timestamp
Final Cleaned Dataset

The final cleaned table used for analysis was:

cyclistic_cleaned

This dataset became the foundation for all SQL analysis and Tableau visualizations.

4. Analyze

The main analysis focused on identifying behavioral differences between members and casual riders. To keep Tableau fast and efficient, aggregated summary tables were created in BigQuery and exported for dashboard creation.

Below is a detailed explanation of the findings shown across the dashboards.

Dashboard 1 Title
Cyclistic Rider Behavior and Usage Trends

This dashboard focuses on overall usage behavior, including ride volume, bike preference, seasonal trends, and peak riding hours.

A. Total Rides: Member vs Casual

This chart compares the total number of rides taken by members and casual riders.

Finding:
Members: 3,484,202 rides
Casual riders: 1,915,806 rides
Interpretation:

Members take significantly more rides overall than casual riders. This suggests that members use Cyclistic more regularly and may depend on the service as part of their routine transportation habits, such as commuting or recurring daily travel.

Casual riders, while still a large group, appear to use the service less frequently.

B. Bike Type Preference

This chart compares the types of bikes used by each rider group.

Finding:

Both groups use electric bikes and classic bikes, but electric bikes show especially high usage.

Interpretation:

Bike type preference appears strong across both groups, but usage is still higher among members simply because they ride more overall. The strong demand for electric bikes may indicate that convenience and ease of riding matter to both rider types. This could be useful for future promotions, especially if membership campaigns highlight flexible and convenient riding options.

C. Seasonal Usage Patterns

This chart shows total rides by month for members and casual riders.

Finding:
Ride activity increases steadily from spring into summer
Peak usage occurs in the warmer months, especially July and August
Activity drops sharply during winter
Interpretation:

Both groups are influenced by seasonality, but casual riders show stronger summer spikes. This suggests that casual riders may be more likely to use bikes for leisure, tourism, or recreational purposes during good weather. Members also increase usage in summer, but their riding pattern is more stable throughout the year.

This insight is important because it suggests that casual riders may be especially receptive to membership offers during peak season.

D. Peak Ride Hours

This chart shows hourly ride behavior throughout the day.

Finding:
Members show clear peaks during morning and evening hours
Casual riders have a more leisure-oriented pattern, with stronger activity later in the day
Interpretation:

This is one of the strongest indicators of behavior differences.

Members appear to use Cyclistic in ways that resemble commuting behavior:

higher usage before work hours
higher usage after work hours

Casual riders appear less commute-driven and more flexible in timing, which supports the idea that they use bikes more for personal, social, or recreational trips.

Dashboard 2 Title
Cyclistic Ride Duration and User Behavior Analysis

This dashboard focuses on trip duration, weekday vs weekend differences, popular stations, and how rider behavior changes across the week.

E. Average Ride Duration

This chart compares the average ride duration between rider groups.

Finding:
Casual riders: about 19.4 minutes
Members: about 11.7 minutes
Interpretation:

Casual riders clearly take longer trips than members. This suggests that casual riders are more likely to use the bikes for relaxed or extended trips, while members use them for shorter, more practical journeys.

This is one of the most important findings in the entire case study because it directly shows a difference in how each group uses the service.

F. Weekday vs Weekend Rides

This chart compares usage during weekdays and weekends.

Finding:
Members dominate weekday rides
Casual riders are much more active on weekends
Interpretation:

This supports the idea that members are more likely to use Cyclistic for routine transportation, while casual riders are more likely to ride for leisure or social purposes.

This insight can directly influence marketing strategy. For example, campaigns targeting casual riders may perform better on weekends or before weekends, when those riders are most active.

G. Ride Duration Distribution

This chart groups rides into categories such as:

0–10 minutes
10–30 minutes
30–60 minutes
60+ minutes
Finding:
Members are heavily concentrated in shorter ride categories
Casual riders have a higher share of longer rides
Interpretation:

This reinforces the earlier average duration finding. Members are likely taking quick point-to-point trips, while casual riders are more likely to spend longer periods on the bikes.

A distribution chart is useful here because it shows that this is not just about averages — the entire shape of rider behavior is different between the two groups.

H. Top 10 Start Stations

This chart highlights the most frequently used start stations.

Finding:

The most active start stations are concentrated around prominent urban areas.

Interpretation:

This can suggest that heavily used start points may be near central business areas, waterfronts, entertainment districts, or other popular destinations. These locations may attract different rider groups for different reasons.

Although this chart alone does not prove rider motivation, it adds location context and could be useful for future marketing or station-level promotions.

I. Average Ride Duration by Weekday

This chart compares average ride duration across different days of the week.

Finding:
Casual riders have longer rides across all days
Casual riders especially show longer rides on weekends
Members remain relatively stable and short throughout the week
Interpretation:

This is another strong indicator of recreational versus routine usage. Weekend ride duration for casual riders suggests freer, longer trips, while members continue to use Cyclistic more consistently for practical travel.

5. Share
Dashboard Titles

Here are polished titles you can use for your Tableau pages:

Dashboard 1
Cyclistic Rider Behavior and Usage Trends

Alternative:

Cyclistic Usage Overview: Members vs Casual Riders
Cyclistic Rider Trends and Bike Usage Analysis
Dashboard 2
Cyclistic Ride Duration and User Behavior Analysis

Alternative:

Cyclistic Ride Duration, Weekday Patterns, and Station Insights
Cyclistic Rider Time Patterns and Duration Analysis
Visualization Summary

The dashboards together communicate the following:

overall ride frequency
ride duration differences
weekday vs weekend usage
seasonal changes
peak hour behavior
bike type preference
location patterns

They provide a clear visual story showing that members and casual riders use Cyclistic in different ways.

6. Key Findings
Similarities
Both groups ride more during warmer months
Both groups use the same core bike types
Both groups show seasonal fluctuation in demand
Differences
Members take more rides overall
Casual riders take longer rides
Members ride more during weekdays and commute hours
Casual riders are more active on weekends and during leisure hours
Members show more routine and stable usage
Casual riders show stronger recreational patterns
7. Act
Recommendations

Based on the analysis, the following recommendations can support Cyclistic’s goal of converting casual riders into members.

1. Launch Weekend Membership Campaigns

Casual riders are heavily active on weekends, so this is a strong window for targeted conversion offers. Cyclistic could promote:

weekend-to-membership upgrades
limited-time weekend discounts
free trial membership upgrades after repeated weekend usage
2. Run Seasonal Promotions During Peak Months

Because casual usage rises significantly during summer, Cyclistic can introduce:

summer membership campaigns
tourist-targeted membership bundles
digital promotions during peak riding months
3. Highlight Cost Savings for Frequent Casual Riders

Casual riders who take repeated long trips may be good membership prospects. Marketing should emphasize:

savings compared to repeated pass purchases
convenience of unlimited access
membership value for frequent users
4. Use Digital Media Based on Rider Timing

Since casual riders appear more active during leisure periods, digital campaigns can be timed for:

Friday afternoons
weekends
summer travel periods

This increases the chance of reaching riders when they are most likely to engage.

8. Conclusion

This case study shows that members and casual riders behave very differently.

Members use Cyclistic more frequently and in a way that suggests practical, routine, commute-based travel. Casual riders use the service less often but for longer, more leisure-oriented trips, especially on weekends and in warmer months.

These findings provide a strong basis for marketing strategies aimed at converting casual riders into annual members. By targeting weekend, seasonal, and frequent leisure riders with personalized membership messaging, Cyclistic can improve conversion and support long-term growth.

9. Skills Demonstrated

This project demonstrates practical skills in:

SQL querying in BigQuery
data cleaning and validation
deriving calculated fields
descriptive and comparative analysis
dashboard design in Tableau Public
business recommendation development
storytelling with data
