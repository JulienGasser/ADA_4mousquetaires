---
layout: page
title: Assumptions and material
subtitle: This markedown describes the material and main assumptions of this story
---

### Data
$$\quad$$ Two datasets *RateBeer* and *BeerAdvocate* respectively from the websites [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/) are used to provide this data story. Both datasets contain user ratings about beers. Each rating contains many features such as the posting date, a possible review, the beer name, the brewery, ratings on appearance, aroma... Datasets on beers and breweries have been merged to the ratings to get further information about the beers and breweries such as the brewery and user location, the beer style.

### Assumption 1
$$\quad$$ Regarding the expension of the websites, the first years regarding the union of both datasets are not very well supplied with data. It has been decided to keep the data only from 2004. For the story, it is chosen that the little and gentle brewer wanted to create its brewery in 2004 and then the prediction data given by the *great druid* to *Les4Mousquetaires* were from 2004 to 2017.

{% include rating_year.html %}


### Assumption 2
$$\quad$$ For the sake of creating the proposed story, the datasets *RateBeer* and *BeerAdvocate* are considered as data given by the *great druid* that took out an old crystal ball from his bag and consulted the oracles to get them. They represent rating predictions given by the oracles for the beginning of the year 2004 until the year 2017. In this project, the data are no more viewed as data from the websites [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/) but as prediction data from the *great druid*.


### Assumption 3
$$\quad$$ This story studies the distribution of beers across time and space. However, regarding space, a biais can be detected by observing the following heavy-tailed distributions of ratings across user locations and brewery locations. Indeed, it seems that the presence of user locations and brewery locations depends on social factors. For example, due to the fact that the website is from Northern America, the countries such as USA, Canada and English speaking countries or with access to the English language have more ratings. Other causes may be also investigated such as access to internet. However in this story, these ratings are taken as predictions given by the *great druid* from the oracles (assumption 2), so these biases are not treated as such. Indeed, these effects are just the outcome of the prediction of the *great druid* and do not represent a biais. More generally, it assumed that the oracles predict people beer consumption and rating without biais, i.e. without for instance social or geographical biais. The small quantity of beers brewed in the artisanal brewery of the little and gentle brewer is assumed to not impact their prediction.

$$\quad$$ The graphs below present 65 user locations out of 185 and 57 brewery locations out of 203.

{% include rating_user.html %}

{% include rating_brew.html %}

### Assumption 4
$$\quad$$ During the analysis of the different beer styles, the dataset that was cleaned up contained a lot of different styles. The choice was therefore made to group these different styles into 23 distinct categories. The list of categories is as follows:

| 🍺 Categories |
| :-----|
| Ale |
| Amber Ale |
| Amber Lager |
| Belgian Ale |
| Bitter Ale |
| Bock |
| Brown Ale|
| Cider |
| Dark Ale |
| Dark Lager |
| IIPA |
| IPA |
| Lager |
| Mead |
| Pale Ale |
| Pilsner |
| Porter |
| Saké |
| Sour |
| Speciality Beer |
| Stout |
| Strong Ale |
| Wheat Beer |

$$\quad$$ It remains to be noted that the clustering was done on the basis of the style categories that are defined on the websites [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/)


