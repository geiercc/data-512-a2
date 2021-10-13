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


source data and description

table with column and what it is 
all csv outputs and 6 tables



## 1. What biases did you expect to find in the data (before you started working with it), and why?
I expected to find that countries with a higher population would have both a higher article count and a higher quality article count. I expected that as Wikipedia is crowdsourced that the countries with higher populations would have more people countributing to the articles in the country they are from leading to more articles and thus more quality articles. I also expected the United States and other English speaking European countries to have a high quality article percentage as the data is coming from English Wikipedia. 
## 2. What (potential) sources of bias did you discover in the course of your data processing and analysis?
One potential source of bias I discovered in my analysis was that there were quite a few countries that had 0 quality articles and so just showing the bottom 10 wasn't necessarily reflective of all the countries that were in this bucket. Also since these countries tended to have lower article counts in general showing a 0% for the article quality percentage didn't fully highlight what was going on. Another bias I found was that as the quality ratings are coming from English wikipedia the fact that Northern America is first is probably biased by the fact that Northern America has a high percentage of people that speak English. 
## 7. How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?
A researcher could potentially supplement this data by expanding the source data beyond just English Wikipedia. This would reduce the bias of lower article counts observed in countries who's primary language isn't English as there would probably be more articles written in that countries native language and could also reduce the quality article percentage as well. If the data was available the researcher could even get the article count and quality article count for a specific country using that country's wikipedia. So far instance, the article count for France could come from fr.wikipedia instead of en.wikipedia. Additionally, a researcher could make adjustments to the data in an attempt to normalize population size so that you could get a better understanding of if there's a defecit of quality articles in a certain country.
