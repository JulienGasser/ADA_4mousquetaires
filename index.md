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

D'Artagnan went in search of data to determine the **beer export rate**. He took the data from the druid cleaned by Aramis and for each year, he calculated **for each beer producing country the yearly proportion of beer distributed in each beer consumming country**. He collected all these data in a **table named $$exported$$ and transmitted it to Athos**, in order to go on with the building of the simulation algorithm.

The table $$exported$$ is ordered as follows: $$exported_{c_0,c}[i]$$ is the proportion of beers of the beer producing country $$c_0$$ that is exported to the beer consumming country $$c$$ during the year $$i$$.

The following **hypothesis** concerning the $$exported$$ were made : 
* each ratings is considered as a beer consummed. Thus the proportion of beers exported from a certain beer producing country to a beer consumming country during a year is calculated as the proportion of ratings for beers with a brewery in the considered beer producing country and rated by users in a consumming country during a year. 
* the calculated proportion of beers exported from a country to another during a year represents the average proportion that would be exported from a brewery implemented in this country by the little and gentle brewer to another country.
* this calculation assumes that the proportion of beer exportation is independant of the style of beer. Nevertheless, in the meantime, Athos was developing an analysis to take this effect into account.

At this step, D'Artagnan had a big table including 14 years, 203 beer production countries and 186 beer consuming countries. His next task was to **filter these data to help the little and gentle brewer** to decide in which country to establish its brewery. Remembering the will of the little and gentle brewer to spread its beer and thus happiness in as many countries as possible, he generated the graph (fig.'Number of beer consumming countries per beer producing country'). He **plotted the number of beer consumming countries to which the beer producing countries export** during the whole time story (i.e. 2004 to 2017). From this heavy-tailed distribution, he could **advice the little and gentle brewer to choose one beer producing country** with a high number of beer consumming countries to settle down.

[figure1]: {% include consumingPerProducing.html %} "Figure 1"

Finally, D'Artagnan **plotted a detailled yearly exportation of beers for some beer producing countries**. For displaying purpose, he opted to show the following subset of the $exported$ table. He selected the the top ten of advised beer producing countries (on the plot (fig.'Number of beer consumming countries per beer producing country'), this corresponds to countries with a number of consumming country above the red line) and five other random countries. Then, he kept the beer consumming countries that contributed at least a proportion of 0.008 of the beers exported from the selected beer producing countries. The objective of this plot is to represent the annual evolution of the exports of the top-ten beer producing countries that D'Artagan advises to the little and gentle brewer and to compare them to less-optimal ones. He also wanted to illustrate the table $$exported$$ with this subset of data with this figure (fig.'Proportion of beer exported from the selected beer producing countries').

{% include export_beer.html %}

**Parchment of use of the graph (fig.'Proportion of beer exported from the selected beer producing countries')** :
* each line represents one of the selected beer producing countries $$c_0$$. From bottom to top, the beer producing countries are displayed from more advised to less advised countries to install a brewery according the ranking on the figure (fig.'Proportion of beer exported from the selected beer producing countries'). [ce lien][figure1]
* each column represents one of the selected beer consumming countries $$c$$.
* the value of a cell $$exported_{c_0,c}[i]$$ is the proportion exported from a beer producing country $$c_0$$ to a beer consumming country $$c$$ during the considered year $$i$$. 
* a producing country exports beers to a higher number of consumming countries when the higher number of non-zero values on a line (i.e. not white cell).



## Story de jerem
In the course of these various investigations, Athos decided to look more closely at the influence of the small brewer's choice of beer style.
Noting that each style is not appreciated in the same way in all countries, he realized that exports varied significantly when the ratings were very good or very bad. However, this was not an immutable and universal rule. Chance played a significant role in the equation. He knew that.
He had his back to the wall and had to find a way to model a country's affinity for a style of beer when an idea came to him. He constructed the following algorithm.

Thanks to the data provided by the druid, it is possible to determine the distribution of ratings that a style of beer has had in each country, as shown in the following graph.

              **introduire le graph htlm fait par Julien**
              
On the latter, the distribution of the score that the young brewer can obtain depends on the style of beer he has chosen to brew, but also on the country in which D'Artagnan advises him to export these beers.

{: .box-note}
**Note:** It's up to you, user of this sublime website, to play with the button to display these scores in the countries of your choice.

Then, a random draw is performed according to the multinomial distribution of scores to take into account the factor of chance in assigning a score.

Also taking into account the smart mind of the little and gentle brewer, who will adapt his beer production according to the feedback he recieves form his exports, the effect of the score on beer production is quantified arbitrarily by Athos is the followng correspondence table. Notice that the minimum score is 0 and the maximum score is 5.

| Randomly drawn <br> score | Effect on the variation of <br> the beer exportations |
| :------ |:--- |
| 0 - 0.5 | -40% |
| 0.5 - 1 | -30% |
| 1 - 1.5 | -20% |
| 1.5 - 2 | -10% |
| 2 - 2.5 | / |
| 2.5 - 3 | / |
| 3 - 3.5 | +10%
| 3.5 - 4 | +20% |
| 4 - 4.5 | +30% |
| 4.5 - 5 | +40% |

This basically means: if the randomly drawn score is between 1 and 1.5 for one country, the variation of beer consummed (still for a given beer style) that is predicted by Porthos will be multiplied by 0.8 for the next year. The principle remains the same for the whole correspondence table above.

Finally, the obtained weights are sent to the Porthos algorithm as $$w_c[i]$$:
$$\Delta Var_{beer} \leftarrow \Delta Var_{beer} \cdot w_c[i]$$

The above described algorithm is run for each year, for each country where users (beer drinkers) can be found and for each beer style. A sample of the obtained Dataframe is display in the following figure:

### Affinity of a country towards a certain style of beer during a chosen year

<table border="1" class="dataframe" style="overflow-x: auto;">  <thead>    <tr style="text-align: center;">      <th></th>      <th></th>      <th>Ale</th>      <th>Amber Ale</th>      <th>Amber Lager</th>      <th>Belgian Ale</th>      <th>Bitter Ale</th>      <th>Bock</th>      <th>Brown Ale</th>      <th>Cider</th>      <th>Dark Ale</th>      <th>Dark Lager</th>      <th>IIPA</th>      <th>IPA</th>      <th>Lager</th>      <th>Mead</th>      <th>Pale Ale</th>      <th>Pilsener</th>      <th>Porter</th>      <th>Saké</th>      <th>Sour</th>      <th>Specialty Beer</th>      <th>Stout</th>      <th>Strong Ale</th>      <th>Wheat Beer</th>    </tr>    <tr>      <th>period</th>      <th>user_location</th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>      <th></th>    </tr>  </thead>  <tbody>    <tr>      <th rowspan="5" valign="top">2015.0</th>      <th>Antarctica</th>      <td>1.2</td>      <td>0.8</td>      <td>1.2</td>      <td>1.3</td>      <td>1.3</td>      <td>0.6</td>      <td>1.3</td>      <td>1.4</td>      <td>1.0</td>      <td>0.7</td>      <td>1.0</td>      <td>0.7</td>      <td>1.0</td>      <td>1.0</td>      <td>0.7</td>      <td>1.0</td>      <td>1.4</td>      <td>1.1</td>      <td>0.9</td>      <td>1.2</td>      <td>1.2</td>      <td>1.0</td>      <td>1.2</td>    </tr>    <tr>      <th>Egypt</th>      <td>1.0</td>      <td>0.9</td>      <td>0.6</td>      <td>0.7</td>      <td>0.7</td>      <td>1.0</td>      <td>1.2</td>      <td>1.1</td>      <td>1.0</td>      <td>1.0</td>      <td>1.1</td>      <td>0.9</td>      <td>0.9</td>      <td>0.8</td>      <td>1.0</td>      <td>0.7</td>      <td>1.1</td>      <td>1.1</td>      <td>0.7</td>      <td>1.3</td>      <td>1.0</td>      <td>0.9</td>      <td>0.9</td>   </tr>    <tr>      <th>Vatican City</th>      <td>1.3</td>      <td>1.1</td>      <td>0.6</td>      <td>1.4</td>      <td>1.0</td>      <td>1.4</td>      <td>0.8</td>      <td>1.3</td>      <td>1.0</td>      <td>1.1</td>      <td>1.1</td>      <td>1.0</td>      <td>0.7</td>      <td>0.9</td>      <td>0.8</td>      <td>1.0</td>      <td>1.2</td>      <td>1.4</td>      <td>0.6</td>      <td>0.9</td>      <td>1.0</td>      <td>1.0</td>      <td>1.0</td>    </tr>    <tr>      <th>Micronesia</th>      <td>0.7</td>      <td>1.0</td>      <td>1.1</td>      <td>0.7</td>      <td>0.9</td>      <td>0.8</td>      <td>1.2</td>      <td>1.0</td>      <td>1.0</td>      <td>0.6</td>      <td>0.8</td>      <td>1.4</td>      <td>0.8</td>      <td>0.7</td>     <td>1.1</td>      <td>1.0</td>      <td>1.0</td>      <td>1.4</td>      <td>1.1</td>      <td>0.7</td>      <td>0.8</td>      <td>0.6</td>      <td>0.6</td>    </tr>    <tr>      <th>Palestine</th>      <td>0.6</td>      <td>1.4</td>      <td>1.2</td>      <td>1.4</td>      <td>1.4</td>     <td>0.6</td>      <td>1.1</td>      <td>1.2</td>      <td>0.8</td>      <td>1.2</td>      <td>0.7</td>      <td>1.2</td>      <td>1.4</td>      <td>1.4</td>      <td>1.2</td>      <td>1.3</td>      <td>0.8</td>      <td>1.0</td>      <td>1.2</td>      <td>1.4</td>      <td>1.3</td>      <td>1.1</td>      <td>1.3</td>    </tr>  </tbody></table>

