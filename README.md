# netflix movies and tv show data analysis using sql
![netflix logo](https://github.com/binduta/netflix_sql_prj/blob/main/netflix.jpg)

Overview

This project involves a comprehensive analysis of Netflix's movies and TV shows data using SQL. The goal is to extract valuable insights and answer various business questions based on the dataset. The following README provides a detailed account of the project's objectives, business problems, solutions, findings, and conclusions.

Objectives

    Analyze the distribution of content types (movies vs TV shows).
    Identify the most common ratings for movies and TV shows.
    List and analyze content based on release years, countries, and durations.
    Explore and categorize content based on specific criteria and keywords.

Dataset

The data for this project is sourced from the Kaggle dataset:

    Dataset Link: Movies Dataset

Schema
``` sql

DROP TABLE IF EXISTS netflix;
CREATE TABLE netflix
(
    show_id      VARCHAR(5),
    type         VARCHAR(10),
    title        VARCHAR(250),
    director     VARCHAR(550),
    casts        VARCHAR(1050),
    country      VARCHAR(550),
    date_added   VARCHAR(55),
    release_year INT,
    rating       VARCHAR(15),
    duration     VARCHAR(15),
    listed_in    VARCHAR(250),
    description  VARCHAR(550)
);

```

create database netflix_prj;

show databases;

create table netflix(
	 show_id varchar(6),	
	  show_type varchar(10),
		title   varchar(200),
		director varchar(250),
		casts varchar(1000),
		country varchar (150),
		date_added varchar (50),
		release_year int,
		rating varchar (10),
		duration  varchar (15),
		listed_in varchar (25),
		descriptions varchar (250));


select * from netflix;

select count(*) as total_content
from netflix;

select distinct show_type
from netflix;

-- 1 count the no of movies and tv shows
select show_type,count(*) as total_count
from netflix
group by show_type;

-- 2. List all movies released in a specific year (e.g., 2020)
SELECT * 
FROM netflix
WHERE release_year = 2020


-- 3.Count how many titles were released each year
SELECT release_year, COUNT(*) AS total_titles
FROM netflix
GROUP BY release_year
ORDER BY release_year DESC;

-- 4.Find all movies directed by “Rajiv Chilaka”
SELECT title, release_year
FROM netflix
WHERE director = 'Rajiv Chilaka';

-- 5.Find the top 5 countries with the most content on Netflix.
SELECT country, COUNT(*) AS total_content
FROM netflix
GROUP BY country
ORDER BY total_content DESC
LIMIT 5;

-- 6. List all Movies released after 2020 that are rated “PG-13”.
SELECT title, release_year, rating
FROM netflix
WHERE show_type = 'Movie'
  AND release_year > 2020
  AND rating = 'PG-13';
  
  -- 7.Find how many titles each director has directed (Top 10).
  SELECT director, COUNT(*) AS total_titles
FROM netflix
WHERE director IS NOT NULL
GROUP BY director
ORDER BY total_titles DESC
LIMIT 10;

-- 8.Find the oldest movie on Netflix.
SELECT title, release_year
FROM netflix
WHERE show_type = 'Movie'
ORDER BY release_year ASC
LIMIT 1;


 -- 9.Titles Released in the Same Year 
  SELECT 
    a.title AS title1,
    b.title AS title2,
    a.release_year
FROM netflix AS a
JOIN netflix AS b
ON a.release_year = b.release_year
AND a.show_id <> b.show_id
WHERE a.release_year = 2020;


-- 10.Create All Movie & TV Show Pairs.
SELECT 
    m.title AS movie_title,
    s.title AS show_title
FROM netflix m
CROSS JOIN netflix s
WHERE m.show_type = 'Movie' AND s.show_type = 'TV Show'
LIMIT 10;
