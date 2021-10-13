# data-512-a2

The goal of this project


source data and description

table with column and what it is 
all csv outputs and 6 tables

List any known issues or special considerations with the data that would be useful for another researcher to know. For example, you should describe that data from the Pageview API excludes spiders/crawlers, while data from the Pagecounts API does not.

## 1. What biases did you expect to find in the data (before you started working with it), and why?
I expected to find that countries with a higher population would have both a higher article count and a higher quality article count. I expected that as Wikipedia is crowdsourced that the countries with higher populations would have more people countributing to the articles in the country they are from leading to more articles and thus more quality articles. I also expected the United States and other English speaking European countries to have a high quality article percentage as the data is coming from English Wikipedia. 
## 2. What (potential) sources of bias did you discover in the course of your data processing and analysis?
One potential source of bias I discovered in my analysis was that there were quite a few countries that had 0 quality articles and so just showing the bottom 10 wasn't necessarily reflective of all the countries that were in this bucket. Also since these countries tended to have lower article counts in general showing a 0% for the article quality percentage didn't fully highlight what was going on. Another bias I found was that as the quality ratings are coming from English wikipedia the fact that Northern America is first is probably biased by the fact that Northern America has a high percentage of people that speak English. 
## 7. How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?
A researcher could potentially supplement this data by expanding the source data beyond just English Wikipedia. This would reduce the bias of lower article counts observed in countries who's primary language isn't English as there would probably be more articles written in that countries native language and could also reduce the quality article percentage as well. If the data was available the researcher could even get the article count and quality article count for a specific country using that country's wikipedia. So far instance, the article count for France could come from fr.wikipedia instead of en.wikipedia. Additionally, a researcher could make adjustments to the data in an attempt to normalize population size so that you could get a better understanding of if there's a defecit of quality articles in a certain country.
