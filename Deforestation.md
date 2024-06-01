## Deforestation across the world 

**Project description:** 
In a comprehensive project examining deforestation trends worldwide between 2000-2022, Tableau and SQL skills are leveraged to analyze and visualize data effectively. SQL queries are employed to extract and manipulate large datasets containing geographical and temporal information on forest coverage changes over this period. 

Utilizing Tableau, diverse visualizations are crafted, including bubble charts illustrating deforestation levels across different countries & subnational regions, treemaps demonstrating coverage loss between countries, and comparative bar graphs showcasing the relationship between coverage gain and carbon emissions. Furthermore, interactive dashboards are developed, allowing users to explore the data dynamically, enhancing understanding and facilitating informed decision-making towards sustainable forestry management.

### Data Cleaning

```sql
-- Combine datasets containing tree coverage loss data, carbon emissions, and total coverage using inner joins
SELECT 
    tc_loss.country,
    tc_loss.loss_data, 
    carbon_emissions.emission_data,
    tc_coverage.coverage_data 
FROM 
    tc_loss
INNER JOIN 
    carbon_emissions ON tc_loss.country = carbon_emissions.country
INNER JOIN 
    tc_coverage ON tc_loss.country = tc_coverage.country;
```

```sql
-- Typical validation check for duplicate countries, delete duplicates following this if present
SELECT 
    country, 
    COUNT(*) as count
FROM 
    (
        SELECT 
            tc_loss.country
        FROM 
            tc_loss
        LEFT JOIN 
            carbon_emissions ON tc_loss.country = carbon_emissions.country
        LEFT JOIN 
            tc_coverage ON tc_loss.country = tc_coverage.country
    ) as combined_data
GROUP BY 
    country
HAVING 
    COUNT(*) > 1;
```

### Using Tableau



### Main Insights






[Tableau Public Link](https://public.tableau.com/shared/FS2C53QSP?:display_count=n&:origin=viz_share_link)
