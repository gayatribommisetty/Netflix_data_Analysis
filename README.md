# Netflix Content Analysis Project
![netflix](https://github.com/user-attachments/assets/75a1ae59-ede7-42a4-a2eb-c281d63f530e)


## Overview
The **Netflix Content Analysis Project** provides insights into Netflix's content catalog by utilizing SQL queries. The project demonstrates how to create a structured database, analyze the dataset, and address various business problems related to Netflix content. This repository includes the SQL scripts used to create, manage, and query the `netflix` table.

## Features
This project focuses on analyzing Netflix's content data to extract actionable insights, including:
- Count of total content.
- Classification of content into Movies and TV Shows.
- Identification of the most common content ratings.
- Analysis of content by country, genre, and release year.
- Exploration of specific content attributes, such as duration and director involvement.

## Table Structure
The `netflix` table includes the following columns:

| Column Name     | Data Type    | Description                                      |
|-----------------|--------------|--------------------------------------------------|
| `show_id`       | `VARCHAR(10)` | Unique identifier for each content.             |
| `type`          | `VARCHAR(10)` | Type of content: `Movie` or `TV Show`.          |
| `title`         | `VARCHAR(150)`| Title of the content.                           |
| `director`      | `VARCHAR(210)`| Director(s) of the content.                     |
| `casts`         | `VARCHAR(775)`| Cast members of the content.                    |
| `country`       | `VARCHAR(150)`| Country where the content was produced.         |
| `date_added`    | `VARCHAR(50)` | Date the content was added to Netflix.          |
| `release_year`  | `VARCHAR(10)` | Year the content was released.                  |
| `rating`        | `VARCHAR(10)` | Content rating (e.g., PG, R).                   |
| `duration`      | `VARCHAR(15)` | Duration of the content (e.g., `90 min`, `2 Seasons`). |
| `listed_in`     | `VARCHAR(150)`| Categories/Genres of the content.               |
| `description`   | `VARCHAR(250)`| Brief description of the content.               |

## SQL Queries
The project addresses various business questions through SQL queries:

### General Queries
1. **Drop and Recreate the Netflix Table**
   ```sql
   DROP TABLE IF EXISTS netflix;
   CREATE TABLE netflix (
	   show_id VARCHAR(10),
	   type VARCHAR(10),
	   title VARCHAR(150),
	   director VARCHAR(210),
	   casts VARCHAR(775),
	   country VARCHAR(150),
	   date_added VARCHAR(50),
	   release_year VARCHAR(10),
	   rating VARCHAR(10),
	   duration VARCHAR(15),
	   listed_in VARCHAR(150),
	   description VARCHAR(250)
   );
   ```

2. **Fetch All Records**
   ```sql
   SELECT * FROM netflix;
   ```

3. **Total Content Count**
   ```sql
   SELECT COUNT(*) AS total_content FROM netflix;
   ```

4. **Distinct Types of Content**
   ```sql
   SELECT DISTINCT type FROM netflix;
   ```

### Business Problems
1. **Count of Movies vs TV Shows**
   ```sql
   SELECT DISTINCT type, COUNT(*) AS total_count
   FROM netflix
   GROUP BY type;
   ```

2. **Most Common Rating for Movies and TV Shows**
   ```sql
   SELECT type, rating
   FROM (
	   SELECT type, rating, COUNT(*) AS count, 
	          RANK() OVER (PARTITION BY type ORDER BY COUNT(*) DESC) AS ranking
	   FROM netflix 
	   GROUP BY type, rating
   ) AS t1
   WHERE ranking = 1;
   ```

3. **Movies Released in 2020**
   ```sql
   SELECT title 
   FROM netflix
   WHERE type = 'Movie' AND release_year = '2020';
   ```

4. **Top 5 Countries with Most Content on Netflix**
   ```sql
   WITH CTE_countries AS (
	   SELECT country, COUNT(*) AS total, 
	          DENSE_RANK() OVER (ORDER BY COUNT(*) DESC) AS rank
	   FROM netflix
	   WHERE country IS NOT NULL
	   GROUP BY country
   ) 
   SELECT country 
   FROM CTE_countries
   WHERE rank <= 5;
   ```

5. **Longest Movie**
   ```sql
   SELECT title
   FROM netflix
   WHERE type = 'Movie'
   AND duration = (SELECT MAX(duration) FROM netflix);
   ```

6. **Content Added in Last 5 Years**
   ```sql
   SELECT *
   FROM netflix
   WHERE TO_DATE(date_added, 'Month DD, YYYY') >= (CURRENT_DATE - INTERVAL '5 years');
   ```

7. **Movies/TV Shows by Director 'Rajiv Chilaka'**
   ```sql
   SELECT title
   FROM netflix
   WHERE director LIKE '%Rajiv Chilaka%';
   ```

8. **TV Shows with More Than 5 Seasons**
   ```sql
   SELECT *
   FROM netflix
   WHERE type = 'TV Show' 
   AND SPLIT_PART(duration, ' ', 1)::NUMERIC > 5;
   ```

9. **Content Count by Genre**
   ```sql
   SELECT UNNEST(STRING_TO_ARRAY(listed_in, ',')) AS genre, COUNT(*)
   FROM netflix
   GROUP BY genre
   ORDER BY COUNT(*) DESC;
   ```

10. **Top 5 Years with Highest Average Content Released in India**
    ```sql
    SELECT release_year, COUNT(*) AS avg_num
    FROM netflix
    WHERE country = 'India'
    GROUP BY release_year 
    ORDER BY avg_num DESC
    LIMIT 5;
    ```

11. **Movies That Are Documentaries**
    ```sql
    SELECT DISTINCT title, genre
    FROM (
	    SELECT *, UNNEST(STRING_TO_ARRAY(listed_in, ',')) AS genre 
	    FROM netflix
    ) AS genres
    WHERE genre = 'Documentaries';
    ```

12. **Content Without a Director**
    ```sql
    SELECT *
    FROM netflix
    WHERE director IS NULL;
    ```

13. **Movies with Salman Khan in the Last 10 Years**
    ```sql
    SELECT *
    FROM netflix
    WHERE casts ILIKE '%Salman Khan%'
    AND CAST(release_year AS INTEGER) > EXTRACT(YEAR FROM CURRENT_DATE) - 10;
    ```

14. **Top 10 Actors in Indian Movies**
    ```sql
    SELECT UNNEST(STRING_TO_ARRAY(casts, ',')) AS actors, COUNT(*) AS total_content
    FROM netflix
    WHERE country = 'India'
    GROUP BY actors
    ORDER BY total_content DESC
    LIMIT 10;
    ```

15. **Categorize Content by Keywords**
    ```sql
    WITH cte_content AS (
	    SELECT *,
	           CASE 
	               WHEN description ILIKE '%kill%' OR description ILIKE '%violence%' THEN 'Bad_content'
	               ELSE 'Good_content' 
	           END AS category
	    FROM netflix
    ) 
    SELECT category, COUNT(*) AS total_items
    FROM cte_content
    GROUP BY category;
    ```

## Learning Outcomes
By completing this project, the following skills and insights were developed:
- **SQL Proficiency**: Gained advanced SQL skills, including the use of `WITH`, `CASE`, `RANK()`, and `DENSE_RANK()`.
- **Data Analysis**: Learned how to analyze and extract meaningful insights from structured data.
- **Problem-Solving**: Solved real-world business problems by applying logical thinking to structured queries.
- **Data Cleaning**: Understood the importance of handling missing or inconsistent data (e.g., content without directors).

## Conclusion
This project demonstrates how SQL can be effectively used to analyze a dataset, uncover insights, and address business challenges. By exploring Netflix's content data, we highlighted trends in content type, genre, ratings, and more. This approach can be extended to other datasets to make informed, data-driven decisions in various industries.







