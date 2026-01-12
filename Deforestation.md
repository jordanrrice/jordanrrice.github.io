## Deforestation across the world 

**Description:** 
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

Using Tableau, created graphics to clearly communicate information to potential end users. (Example screenshot pulled from dashboard)

![TreemapDeforest](https://github.com/jordanrrice/jordanrrice.github.io/assets/26234385/f3103b5e-629e-490b-9d27-70df22e99af6)

**When the "Continents" box is used as a filter within the dashboard, selecting specific continent will bring up the corresponding countries and subnational regions in the Bubble Chart and Tree Map.**

### Main Insights

There was not a marked increase in deforestation levels between 2000 and 2022 within the dataset, on the contrary a small decrease was noted in many of the most significant countries overall (Russia, Brazil, and Indonesia for example each had decreases in the single digit %s.) Potential drivers for this include international agreements such as the REDD+ (Reducing Emissions from Deforestation and Forest Degradation) and the Paris Agreement, as well as national policy changes within the countries themselves.

South America, sub-Saharan Africa, and Southeast Asia were the most outsized influences for high levels of tree coverage loss, with the biggest offenders relative to population size being Brazil, Indonesia, and the Democratic Republic of the Congo. Agricultural expansion is the likeliest source of blame for these countries' continued actions of large scale tree felling (including clearing land for grazing and ranching cattle, as well as palm oil and soy production.)

Population growth is the last major potential driver that can be inferred from the subnational information in the dataset. For the United States in particular, several states in the Sun Belt region (Georgia, Alabama, South Carolina, Texas, Florida, and Louisiana) all had outsized levels of coverage loss. This region is experiencing continued high levels of population growth and suburban development leads many of their urban areas to clear cut forests in order to make room for SFH style housing.

[Tableau Public Link]([(https://public.tableau.com/views/Deforestation_17167327247240/Dashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)])
