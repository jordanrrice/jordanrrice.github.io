## Netflix Show and Movie Popularity

**Project description:** 
Embarking on a project exploring the popularity of Netflix shows and movies, we dive into data analysis with Tableau and SQL. SQL helps gather and organize vast amounts of data, like viewer ratings and reviews, while Tableau turns this data into easy-to-understand visuals. Imagine colorful charts showing which shows are trending, graphs comparing viewer ratings over time, and maps revealing which regions love certain genres. 

Interactive dashboards let you explore viewer demographics and genre preferences with a simple click. By using these tools, we unlock insights that guide Netflix in creating the shows and movies we love to binge-watch.

### Data Cleaning

We begin by joining together data from several sources pulled from Kaggle. These sources include information provided by Netflix covering their catalog's countries of origin, duration, age ratings, release years, directors, and type of work primarily.   

```sql
SELECT *
FROM netflix_works AS nw
JOIN netflix_country AS nc ON nw.title = nc.title
JOIN netflix_cast AS ncast ON nw.title = ncast.title;


```

Follow this up by conducting classic "data cleanliness" checks against all datasets being used

```sql
-- Checking for NULL values in each column
SELECT 'netflix_works' AS dataset, COUNT(*) AS null_count
FROM netflix_works
WHERE title IS NULL OR <other_column> IS NULL;

SELECT 'netflix_country' AS dataset, COUNT(*) AS null_count
FROM netflix_country
WHERE title IS NULL OR <other_column> IS NULL;

SELECT 'netflix_cast' AS dataset, COUNT(*) AS null_count
FROM netflix_cast
WHERE title IS NULL OR <other_column> IS NULL;

-- Check for inconsistent data types (example for the 'year' column)
SELECT 'netflix_works' AS dataset, COUNT(*) AS inconsistent_type_count
FROM netflix_works
WHERE TRY_CAST(year AS INT) IS NULL;

-- Add similar checks for other columns as needed

```

Using Tableau's innate functionality, UNION combine all datasets to then shape into graphics for end users.


### Using Tableau, create graphics to clearly communicate information to potential end users.

(Example screenshots pulled from dashboard)

When the Country Map is used as a filter within the dashboard, selecting the United States for example can show you breakdowns on information like # of Works created by year or by director. (Notice some popular names for the Directors from the US!)

![USANetflix](https://github.com/jordanrrice/jordanrrice.github.io/assets/26234385/487484cf-1ce7-48a7-b341-612c7980a670)

![DirectorsUSA](https://github.com/jordanrrice/jordanrrice.github.io/assets/26234385/7883470a-0316-4f82-9647-ed7bf33cc2f8)

Once the graphics planned to be used are all completed (Bubble Chart, Country Map filter, Shows Added by Year, etc.) combine them together into a final dashboard. Include Netflix's logo and match the color scheme to that of the company for additional visual appeal.



### Highlighted Insights

**Production Trends by Country:**

The countries with highest production rates are the US, UK & Australia.

Production trends over time for different countries are relatively similar, with massive increases in # of shows/movies created over the past decade or so, which aligns with Netflix's growth as whole.

Regional preference in content production appears to focus on the Anglosphere.

**Genre Popularity:**

Genre preferences across different regions or countries appears to be stable, with Documentaries, Comedies, and Dramas consistently appearing most often.

Emerging niche markets in Southeast Asia and sub-Saharan Africa.


Hosting the finalized project is easily done on one's Tableau Profile, using Tableau Public's freely offered services. See link below:

https://public.tableau.com/views/NetflixStats_17168516079510/DashboardMain?:language=en-US&publish=yes&:sid=&:display_count=n&:origin=viz_share_link


