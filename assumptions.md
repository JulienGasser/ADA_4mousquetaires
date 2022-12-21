---
layout: page
title: Assumptions and material
subtitle: This markedown describes the main assumptions that have been performed for the story
---

The material as well as the general assumptions regarding this project are stated on this page.

### Data
Two datasets *RateBeer* and *BeerAdvocate* respectively from the websites [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/) are used to provide this data story. Both datasets contain user ratings about beers. Each rating contains many features such as the posting date, a possible review, the beer name, the brewery, ratings on appearance, aroma... Datasets on beers and breweries has been merged to the ratings to get further information about the beers and breweries such as the brewery and user location, the beer style.

### Assumption 1
Regarding the expension of the websites, the first year of the union of both datasets are not very well supplied with data. It has been decided to keep the data only from 2004 to 2017.

{% include consumingPerProducing.html %}


### Assumption 2
For the sake of creating the proposed story, the datasets *RateBeer* and *BeerAdvocate* are considered as data given by the *great druid* that took out an old crystal ball from his bag and consulted the oracles to get them. They represent rating predictions given by the oracles for the beginning of the year 2004 until the year 2017. In this project, the data are no more viewed as data from the websites [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/) but as prediction data from the *great druid*.


### Assumption 3
This story studies the distribution of beers across time and space. However, regarding space, a biais can be detected by observing the following heavy-tailed distributions of ratings across user locations and brewery locations.   
{% include rating_user.html %}
{% include rating_brew.html %}







### Assumption 1
* When Athos studies the affinity of a country to a beer style, there might be missing data. In this case, the draw is made on a uniform score distribution. This means that the probability of obtaining the score $$[i]$$ is the same for all scores.

* $$\quad$$Because of the lack of datas, Les4Mousquetaires considered that this simulation follows a pattern according the datas between 2004 and 2017. For step 2, they decided to weight the consumption variation rate with a random coefficient drawn from the beers ratings distribution to better simulate the unpredicability of the beer's world market.
