---
layout: page
title: What if I set up a brewery?
subtitle: An original ADA story about beer !
gh-repo: juliengasser/ADA4mousquetaires
tags: [brewery, beer, flavour, taste, export, plotly]
---

## Let's write something for our datastory !

Her you can add some text with the markdown syntax and enjoy it online as soon as you push it on github !
Isn'it wonderful ?

{: .box-note}
**Note:** How ! Did I tell you I don't give you the authorization to modify my git ? Sorry...

### A first fig integration

{% include beermap.html %}


plein de commentaire sur cette première figure...

<div id="plotly-exportfig"></div>

Voici l'emplacement de la figure suivante.

<br>
<br>
<div id="plotly-countryfig"></div>

On devrait pas mélanger les balises et le markdown mais on va voir ce que ça donne....

### Our main simulation

{: .box-warning}
**Warning:** We don't now how to upload it in this website !

{% include athos.html %}

{% include porthos.html %}


## Beer export rate

D'Artagnan went in search of data to determine the **beer export rate**. He took the data from the druid cleaned by Aramis and for each year, he calculated **for each beer producing country the yearly proportion of beer distributed in each beer consumming country**. He collected all these data in a **table named $exported$ and transmitted it to Athos**, in order to go on with the building of the simulation algorithm.

The table $exported$ is ordered as follows: $$exported_{c_0,c}[i]$$ is the proportion of beers of the beer producing country $$c_0$$ that is exported to the beer consumming country $$c$$ during the year $$i$$.

The following **hypothesis** were done to build the table $exported$ : 
* each ratings is considered as a beer consummed. Thus the proportion of beers exported from a certain beer producing country to a beer consumming country during a year is calculated as the proportion of ratings for beers with a brewery in the considered beer producing country and rated by users in a consumming country during a year. 
* the calculated proportion of beers exported from a country to another during a year represents the average proportion that would be exported from a brewery implemented in this country by the little and gentle brewer to another country.
* this calculation assumes that the proportion of beer exportation is independant of the style of beer. Nevertheless, in the meantime, Athos was developing an analysis to take this effect into account.

At this step, D'Artagnan had a big table including 14 years, 203 beer production countries and 186 beer consuming countries. His next task was to **filter these data to help the little and gentle brewer** to decide in which country to establish its brewery. Remembering the will of the little and gentle brewer to spread its beer and thus happiness in as many countries as possible, he generated the graph (fig.'Number of beer consumming countries per beer producing country'). He **plotted the number of beer consumming countries to which the beer producing countries export** during the whole time story (i.e. 2004 to 2017). From this heavy-tailed distribution, he could **advice the little and gentle brewer to choose one beer producing country** with a high number og beer consumming countries to settle down.

{% include consumingPerProducing.html %}

Finally, D'Artagnan **plotted a detailled yearly exportation of beers for some beer producing countries**. For displaying purpose, he opted to show the following subset of the $exported$ table. He selected the about top-ten percent of advised beer producing countries (on the plot (fig.'Number of beer consumming countries per beer producing country'), this corresponds to countries with a number of consumming country above the red line) and the beer consumming countries that contributed at least a share of 0.001 of the beers exported from the selected beer producing countries. The objective of this plot is to represent the annual evolution of the exports of the beer producing countries that D'Artagan advises to the little and gentle brewer and also to illustrate the table $exported$ with this subset of data (fig.'Proportion of beer exported from the selected beer producing countries')
{% include export_beer.html %}

**Parchment of use of the graph (fig.'Proportion of beer exported from the selected beer producing countries')** :
* each line represents one of the selected beer producing countries $$c_0$$.
* each column represents one of the selected beer consumming countries $$c$$.
* the value of a cell $$exported_{c_0,c}[i]$$ is the proportion exported from a beer producing country $$c_0$$ to a beer consumming country $$c$$ during the considered year $$i$$. 
* a producing country exports beers to a higher number of consumming countries when the higher number of non-zero values on a line (i.e. not white cell).




