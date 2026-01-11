# movies analyses 
Hollywood most profitable movies 
## Project objective
Analyse Hollywood most profitable movies in MySQL WOrkbench.
## Dataset 
HollywoodsMostProfitableStories (1).csv file
Provides information about different genre movies released between 2007 and 2011 by different studios, public and professional film critics’ scores, and the movies profitability rates. 
## Data cleaning process
HollywoodsMostProfitableStories (1).csv dataset was imported into excel for cleaning.
Checked the errors, duplicated and the missing values using Conditional formatting tool. Filled missing cells with respective value after researching them.
Checked the data type of the columns to be accurate and changed it where it was necessary.
## Data analyses: Questions and process

- Datadet was imported into MySQL Workbench as CSV file for data analyses.
- What movies got less scored (Rotten tomatoe) from film critics ?

 select film,Studio,Film_critics_score
from hollywood_movies AS hm
where Film_critics_score <60
order by Film_critics_score ASC;

- what movies have scored as good(Fresh tomatoes) by film critics?
  
select film,Studio,Film_critics_score
from hollywood_movies AS hm
where Film_critics_score >60
order by Film_critics_score desc;

- Which are the top 10 movies, considered good by audience?

select film,Studio,Public_score, movie_year
from hollywood_movies 
order by Public_score desc
limit 10;

- Which are the less liked movies by audience?

select film,Studio,Public_score, movie_year
from hollywood_movies 
order by Public_score asc
limit 10;

- Which movies were profitable each year, which were broken even and which made loss?

select movie_year, Studio,Film, Profitability
from hollywood_movies
where profitability >1
order by movie_year,Studio,Film,Profitability;

select movie_year, Studio,Film, Profitability
from hollywood_movies
where profitability <1
order by movie_year,Studio,Film,Profitability;

select movie_year, Studio,Film, Profitability
from hollywood_movies
where profitability =1
order by movie_year,Studio,Film,Profitability;

- how many profitable movies had each studio in each year?

select movie_year, Studio,Count(Film) as Film_count
from hollywood_movies
where profitability >1
group by movie_year, Studio;

- which movies brought the top 10 highest gross income worldwide?
  
select Film,Genre, Worldwide_grossincome
from hollywood_movies
order by worldwide_grossincome Desc
limit 10;

- how many movies in each category were released by each studio?
  
select Studio, Genre,Count(Film) as Genre_film
from hollywood_movies
group by Studio,Genre
order by Studio;

- Which categories had the most profitable movies?
  
select Genre,Count(Film) as Film_count
from hollywood_movies
where profitability>1
group by Genre
order by Film_count desc;

- number of movies released by each studio which were profitable and got positive score by film critics
  
select movie_year,Studio,Count(Film) as Film_count
from hollywood_movies
where profitability>1 and Film_critics_score >60
group by movie_year,Studio
order by movie_year desc;







