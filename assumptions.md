---
layout: page
title: Assumptions and material
subtitle: This markedown describes the material and main assumptions of this story
---

The material as well as the general assumptions regarding this project are stated on this page.

### Data
Two datasets *RateBeer* and *BeerAdvocate* respectively from the websites [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/) are used to provide this data story. Both datasets contain user ratings about beers. Each rating contains many features such as the posting date, a possible review, the beer name, the brewery, ratings on appearance, aroma... Datasets on beers and breweries has been merged to the ratings to get further information about the beers and breweries such as the brewery and user location, the beer style.

### Assumption 1
Regarding the expension of the websites, the first year of the union of both datasets are not very well supplied with data. It has been decided to keep the data only from 2004 to 2017 and therefore to begin the story in 2004.

{% include rating_year.html %}


### Assumption 2
For the sake of creating the proposed story, the datasets *RateBeer* and *BeerAdvocate* are considered as data given by the *great druid* that took out an old crystal ball from his bag and consulted the oracles to get them. They represent rating predictions given by the oracles for the beginning of the year 2004 until the year 2017. In this project, the data are no more viewed as data from the websites [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/) but as prediction data from the *great druid*.


### Assumption 3
This story studies the distribution of beers across time and space. However, regarding space, a biais can be detected by observing the following heavy-tailed distributions of ratings across user locations and brewery locations. Indeed, it seems that the representation of user locations and brewery locations depends on social factors. For example, as the website is from Northern America, USA, Canada and English speaking countries or with access to the English language has more ratings. Other causes may be also investigated such as access to internet. However in this story, these ratings are taken as predictions given by the *great druid* from the oracles (assumption 2), so these biases are not treated as such. Indeed, these effects are just the outcome of the prediction of the *great druid* and do not represent a bias. The same goes for other effects that are specific to this data from website ratings like herding effects.

{% include rating_user.html %}

{% include rating_brew.html %}

