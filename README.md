# data-512-a2

The goal of this project was to perform an analysis to see which countries and geographic regions had the highest and lowest percentages of articles per population and percentages of quality articles per article count. A quality article was defined as an article with a rating of either "Featured Article (FA)" or "Good Article (GA)". 

The data was sourced from the following locations:
1. Wikipedia's politician by country dataset: https://figshare.com/articles/dataset/Untitled_Item/5513449
This dataset contained the following columns:
  a. page - a string containing the name of the politician's article 
  b. country - a string with the country name
  c. rev_id - a numeric unique identifier for the specific page
Note that the pages that started with "Template:" were filtered out as they weren't Wikipedia articles. 
2. Population Reference Bureau's population data: https://docs.google.com/spreadsheets/d/1CFJO2zna2No5KqNm9rPK5PCACoXKzb-nycJFhV689Iw/edit?usp=sharing (for more information see: https://www.prb.org/international/indicator/population/table/)
This dataset contained the following columns:
  a. FIPS - the country or region unique code
  b. Name - a string containing the region or country name
  c. Type - a string that indicated if the row was a country or region
  d. TimeFrame - a year
  e. Data (M) - the population represented in millions
  f. Population - the population
  
Additionally the ORES REST API was used to determine the rating, or content assessment, of an article. The documentation can be found here: https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model
The potential outcomes were Featured Article, Good Article, B, C, Start, and Stub. The value returned from the API for "prediction" was the value used in this analysis as the article quality rating. Note that some articles did not get a quality rating returned from this API and these were saved in a seperate file location discussed below. It should also be noted that this API has a max batch GET of 50 articles at a time which can lead to a slow processing time if lots of articles were used as the input.

Output tables:
Found in clean-data folder:
1. page_data.csv
This has Template: filtered out of page data so only Wikipedia articles are included
Columns:
  a. page - a string containing the name of the politician's article 
  b. country - a string with the country name
  c. rev_id - a numeric unique identifier for the specific page
2. population_country_lvl.csv
This has only countries and no regions
Columns:
  a. FIPS - the country or region unique code
  b. Name - a string containing the region or country name
  c. Type - a string that indicated if the row was a country or region
  d. TimeFrame - a year
  e. Data (M) - the population represented in millions
  f. Population - the population
3. country_region_map.csv
This has a mapping of countries to their region
Columns:
  a: Region - A string with region for that country
  b: Country - A string with country name
4. ores_data.csv
This contains the revision id for the article reference and a quality estimate for articles that have a quality estimate.
Columns:
  a: revision_id - a numeric unique identifier for the specific page
  b: article_quality_est. - A string rating from ORES for the quality prediction of that article
5. no_quality_score.csv
This contains the information for the rev_ids that do not have a quality rating from ORES
Columns: 
  a: Error Message - a message containing the error and the rev id
6. wp_wpds_countries-no_match.csv
This contains the rows that don't match from population and page data
Columns:
  a: page - a string containing the name of the politician's article 
  b: country - a string with the country name
  c: rev_id - a numeric unique identifier for the specific page
  d: FIPS - the country or region unique code
  e. Name - a string containing the region or country name
  f. Type - a string that indicated if the row was a country or region
  g. TimeFrame - a year
  h. Data (M) - the population represented in millions
  i. Population - the population_
  j. merge - a string field that tells you if the row is contained in the left (page_data) or right (population_data) table

Found in results folder:
1. wp_wpds_politicians_by_country.csv
This is the merged data file with population data, page data, and the OREs data.
The columns are:
  a: country - a string field with the country name
  b: article_name - a string containing the name of the politician's article 
  c: revision_id - a numeric unique identifier for the specific page
  d: article_quality_est. - A string rating from ORES for the quality prediction of that article
  e: population - a numeric field with the population count

Additionally the following 6 tables were embedded in the Jupyter notebook and were not output to csv files:

1. Top 10 countries by coverage
This was the top 10 highest-ranked countries in terms of number of politician articles as a proportion of country population. 
The columns were:
  a: country - a string field with the country name
  b: Population - a numeric field with the population count
  c: country_article_count - a numeric field with the total number of articles for the country
  d: articles-per-pop - a numeric field with the percentage of articles per population (country_article_pop / Population) * 100.0
2. Bottom 10 countries by coverage
This was the 10 lowest-ranked countries in terms of number of politician articles as a proportion of country population
The columns were:
  a: country - a string field with the country name
  b: Population - a numeric field with the population count
  c: country_article_count - a numeric field with the total number of articles for the country
  d: articles-per-pop - a numeric field with the percentage of articles per population (country_article_pop / Population) * 100.0
3. Top 10 countries by relative quality
This was the 10 highest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality
The columns were:
  a: country - a string field with the country name
  b: Population - a numeric field with the population count
  c: country_article_count - a numeric field with the total number of articles for the country
  d: quality_count - a numeric field with the total number of quality articles for the country (articles in either FA or GA quality)
  e: quality_articles_pct - a numeric field with the percentage of quality articles per article count (quality_count/ country_article_count) * 100.0
4. Bottom 10 countries by relative quality
This was the 10 lowest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality
The columns were:
  a: country - a string field with the country name
  b: Population - a numeric field with the population count
  c: country_article_count - a numeric field with the total number of articles for the country
  d: quality_count - a numeric field with the total number of quality articles for the country (articles in either FA or GA quality)
  e: quality_articles_pct - a numeric field with the percentage of quality articles per article count (quality_count/ country_article_count) * 100.0
5. Geographic regions by coverage
This was a ranking of geographic regions (in descending order) in terms of the total count of politician articles from countries in each region as a proportion of total regional population
The columns were:
  a: Population - a numeric field with the population count
  b: regional_article_count - a numeric field with the total number of articles for the region
  c: quality_count - a numeric field with the total number of quality articles for the region (articles in either FA or GA quality)
  d: regional_article_pct	-  a numeric field with the percentage of articles per population in the region
  e: regional_quality_pct - a numeric field with the percentage of quality articles per article count in the region
6. Geographic regions by high quality article coverage
This was a ranking of geographic regions (in descending order) in terms of the relative proportion of politician articles from countries in each region that are of GA and FA-quality
The columns were:
  a: Population - a numeric field with the population count
  b: regional_article_count - a numeric field with the total number of articles for the region
  c: quality_count - a numeric field with the total number of quality articles for the region (articles in either FA or GA quality)
  d: regional_article_pct	-  a numeric field with the percentage of articles per population in the region
  e: regional_quality_pct - a numeric field with the percentage of quality articles per article count in the region

Reflection:
I learned that you often need to take a look at the data before working with it and truly understand what all the data attributes mean, and also that it is important to fully understand how an API works before working with it. As an example I didn't know that the API could only return 50 article ratings at a time which caused some confusion as I tried to understand the erros I wsa getting. I was suprised that Northern America wasn't higher on the list of regions by article coverage as I would have expected it to be higher given the data was coming from English Wikipedia and Northern America is heavily English speaking. This assignment raised the question of what kind of biases the Wikipedia content assessment criteria contains for each country? I think this would be something interesting to look into and also to see if the criteria is much different across different languages of Wikipedia.

1. What biases did you expect to find in the data (before you started working with it), and why?
I expected to find that countries with a higher population would have both a higher article count and a higher quality article count. I expected that as Wikipedia is crowdsourced that the countries with higher populations would have more people countributing to the articles in the country they are from leading to more articles and thus more quality articles. I also expected the United States and other English speaking European countries to have a high quality article percentage as the data is coming from English Wikipedia. 

2. What (potential) sources of bias did you discover in the course of your data processing and analysis?
One potential source of bias I discovered in my analysis was that there were quite a few countries that had 0 quality articles and so just showing the bottom 10 wasn't necessarily reflective of all the countries that were in this bucket. Also since these countries tended to have lower article counts in general showing a 0% for the article quality percentage didn't fully highlight what was going on. Another bias I found was that as the quality ratings are coming from English wikipedia the fact that Northern America is first is probably biased by the fact that Northern America has a high percentage of people that speak English. 

7. How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?
A researcher could potentially supplement this data by expanding the source data beyond just English Wikipedia. This would reduce the bias of lower article counts observed in countries who's primary language isn't English as there would probably be more articles written in that countries native language and could also reduce the quality article percentage as well. If the data was available the researcher could even get the article count and quality article count for a specific country using that country's wikipedia. So far instance, the article count for France could come from fr.wikipedia instead of en.wikipedia. Additionally, a researcher could make adjustments to the data in an attempt to normalize population size so that you could get a better understanding of if there's a defecit of quality articles in a certain country.
