# Netflix Content Analysis Project

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
1. **Drop and Recreate the Netflix Table**: Ensures a clean start by dropping and recreating the `netflix` table.
2. **Fetch All Records**: Displays all the records in the table.
3. **Total Content Count**: Retrieves the total number of records in the `netflix` table.
4. **Distinct Types of Content**: Identifies unique content types.

### Business Problems
1. **Count of Movies vs TV Shows**: Calculates the count of Movies and TV Shows.
2. **Most Common Rating for Movies and TV Shows**: Determines the most frequent rating for each type of content.
3. **Movies Released in 2020**: Lists movies released in the year 2020.
4. **Top 5 Countries with Most Content**: Identifies the top five countries producing the most content.
5. **Longest Movie**: Finds the longest movie based on duration.
6. **Content Added in Last 5 Years**: Displays content added to Netflix within the last 5 years.
7. **Movies/TV Shows by Rajiv Chilaka**: Fetches content directed by Rajiv Chilaka.
8. **TV Shows with More Than 5 Seasons**: Lists TV Shows with more than five seasons.
9. **Content Count by Genre**: Counts the content categorized by genre.
10. **Top 5 Years with Highest Average Content Released in India**: Identifies years with the highest average content release in India.
11. **Movies That Are Documentaries**: Extracts movies categorized as documentaries.
12. **Content Without a Director**: Displays content where no director is listed.
13. **Movies with Salman Khan in the Last 10 Years**: Lists movies featuring Salman Khan released in the last 10 years.
14. **Top 10 Actors in Indian Movies**: Identifies the top 10 actors featured in Indian movies.
15. **Categorize Content by Keywords**: Categorizes content based on specific keywords in descriptions (e.g., `kill`, `violence`).

## Usage
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/netflix-content-analysis.git
   ```
2. Set up a database environment (e.g., PostgreSQL).
3. Execute the SQL scripts in order.
4. Analyze the outputs to answer the business questions.

## Prerequisites
- Database Management System (PostgreSQL preferred)
- Basic knowledge of SQL

## Project Objectives
This project aims to:
1. Demonstrate proficiency in SQL for data analysis.
2. Address real-world business problems using structured data.
3. Provide insights into Netflix's content catalog.

## Contributions
Contributions are welcome! Feel free to fork this repository and submit a pull request with enhancements or additional queries.

## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Contact
For questions or feedback, please contact:
- **Your Name**: [your-email@example.com](mailto:your-email@example.com)
- **GitHub**: [https://github.com/your-username](https://github.com/your-username)

---
Thank you for exploring the Netflix Content Analysis Project!

