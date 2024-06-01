## MTA Ridership

**Description:** In a comprehensive project delving into mass transit usage within NYC's MTA subway system, Tableau and SQL skills are instrumental in analyzing and visualizing ridership data. SQL queries are deployed to aggregate and manipulate vast datasets encompassing station-specific ridership metrics and inter-station travel patterns. 

Leveraging Tableau, a variety of visualizations are crafted, ranging from dynamic line graphs illustrating ridership trends over time to geographical maps pinpointing station hotspots and connectivity. Additionally, interactive dashboards are developed, empowering users to explore ridership patterns, peak hours, and popular routes, thus facilitating informed decision-making for optimizing transit services and infrastructure.

### Data Cleaning

```sql
--Combine initial datasets with station information, then those containing ridership by station for weekdays and weekends.

SELECT *
FROM mta_stations AS s
JOIN mta_2017weekend AS w ON s.station = w.station
JOIN mta_2017weekday AS d ON s.station = d.station;
```

```sql
--Follow this with typical validation checks for potential null values, duplicates, and/or irrational outliers.

SELECT COUNT(*) AS null_count
FROM mta_combined
WHERE station IS NULL OR weekend_column IS NULL OR weekday_column IS NULL;


--Query checking for potential duplicates 
SELECT COUNT(*) - COUNT(DISTINCT station) AS duplicate_count
FROM combined_table;

--Query removing duplicates
DELETE FROM mta_combined
WHERE ROWID NOT IN (SELECT MIN(ROWID) FROM combined_table GROUP BY station);

--Query checking for potential outliers
SELECT station, MAX(weekend) AS max_weekend_riders, MIN(weekday) AS min_weekday_riders
FROM mta_combined
GROUP BY station;

-- Example of removing potential outliers
DELETE FROM mta_combined
WHERE weekend > 1000000 OR weekday > 1000000;

```

Using Tableau's innate functionality, UNION combine all datasets to then shape into graphics for end users.

### Using Tableau

Using Tableau, create graphics to clearly communicate information to potential end users.
(Example screenshot pulled from dashboard)

![MTARidership2017](https://github.com/jordanrrice/jordanrrice.github.io/assets/26234385/cf1ef8bb-f4bf-4990-9e33-11851ed9fd00)

**When the Treemap is used as a filter within the dashboard, selecting an individual station (or multiple using CTRL+click) will highlight the corresponding location on the map.**

### Main Insights

Comparison of ridership levels between weekdays and weekends reveals a (rather obvious) insight that weekday ridership is dramatically higher, with weekdays having 96% higher levels of passenger activity.

Evaluation of ridership distribution across the five boroughs (Manhattan, Brooklyn, Queens, the Bronx, and Staten Island), also indicates that Manhattan & Brooklyn significantly outperform their counterparts. Staten Island comes in last unsurprisingly with its single line.

Stations found in Midtown Manhattan (Times Square 42nd, Grand Central 42nd, & Herald Square) are solidly in the top three positions. There are only two stations in the top 10 that fall outside of Midtown Manhattan at all (Fulton Street & 14th Street Union Square), and Flushing - Main Street is the only line outside of the borough of Manhattan that comes anywhere close to the highest with less than 1/3rd of the top spots passengers.

See link below for full dashboard on Tableau Public:

[Tableau Public Link](https://public.tableau.com/views/NYCSubwayMTARidership-2017/Summary?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link)
