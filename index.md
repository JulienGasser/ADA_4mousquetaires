---
layout: page
title: What if I set up a brewery?
subtitle: An original ADA story about beer !
gh-repo: juliengasser/ADA4mousquetaires
tags: [brewery, beer, flavour, taste, export, plotly]
---


 ## Once upon a time
 
There was a little and gentle brewer who dreamed of spreading happiness in the world. As everyone knows, beer makes people happy, so he decided to reach his dream by creating a beer and to spread it around the world. The problem is that he sucked at market study and didn't know how to begin with his business... If he first aimed to reach as many countries as possible and secondly the most people as possible with his beer, he had to make the good choices ! Which type of beers to choose ? Where to open his brewery ? ... That's a complicated problem, isn't it ? Fortunately, Les4Mousquetaires were here to help this litte and gentle brewer by creating a tool that would help him a lot. This tool is a market simulator that will predict the spread of his beer according to the choice of his beer and brewery. Will this gentle and little brewer reach is dream ?

## Brewery success simulation tool

Here is the brewery success simulation tool created by *Les4Mousquetaires* for the little and gentle brewer. As the latter is generous, he leaves this precious tool in open source to the internet. 

This simulation was created to guide the little and gentle brewer when establishing its brewery in 2004. This tool takes as inputs a country where to set up a brewery and a style of beer to brew. Then, it outputs a world map with the prediction of the distribution of the beers produced by the brewery across countries and years, until 2017, for an initial expected production of 10'000 beers. In addition, given the little and gentle brewer's goals of first reaching as many countries as possible and then as many people as possible, a second graph shows the cumulative number of countries reached by its beer and the cumulative number of beers distributed across years. The happiness gauge on the right of the world map shows how happy are the country on the map. This happiness score is based on taking the $$log_{10}$$ of the distributed beers in each country.

The little and gentle brewer decided (TODO). Do you feel the soul of the brewer in you to find a better prediction than the little and gentle brewer ?

A little trouble to find it or by curiosity to better understand the simulation, the following story of the little and gentle brewer and *Les4Mousquetaires* is waiting for you …

### Let's play with the simulation

{% include beermap.html %}

<br>
<br>
<div id="plotly-countryfig"></div>

## Story of the little and gentle brewer and Les4Mousquetaires

### *1) Birth of the algorithm*

$$\quad$$Created by Les4Mousquetaires, the above simulation is a practical tool to help the little and gentle brewer to spread happiness 🍻 around the world. The conception of this tool was a long and perilous adventure ! Here is the story...


<img align="right" width="180" height="220" src="https://user-images.githubusercontent.com/77831063/209109848-ab9ce2c6-ba5e-4256-877d-c3f20a159ed0.png">

$$\quad$$ The first ordeal to overcome was to find datas. After many reflections, *Les4Mousquetaires* decided to ask the *great druid* for help because he was known to be a real beer lover. The *great druid* was also known for hanging out in bars all day long. So Les4Mousquetaires went to the most famous bar in town and, as expected, they found the *great druid* in a sorry state. After explaining their project, the *great druid* took out an old crystal ball from his bag and consulted the oracles to find out how the beer market would evolve in the next few years. After consultation, the *great druid* took a USB stick, plugged it into his crystal ball and saved two datasets [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/). These datasets were beer rating predictions for the next years. Each rating contains many features such as the posting date, a possible review, the beer name, the brewery location, the user location, ratings on appearance, aroma...  While giving the USB stick to *Les4Mousquetaires*, as the *great druid* was a little bit wasted, he dropped it in his beer... They jumped on the beer and saved the USB stick from drowning. However, both datasets were partially corrupted. Panic-stricken by the poor state of the two datasets, Aramis decided to isolate himself to start a big cleaning process of the two datasets.

$$\quad$$On their side, D'Artagnan, Athos and Porthos sat down around a table and started to elaborate the tool to help the little and gentle brewer. Based on the two datasets being cleaned by Aramis, they decided to create an interative algorithm divided into 3 steps. This algorithm is explained below and illustrated on a parchment: 

<p align="center">
<img align="center" width="480" height="480" src="https://user-images.githubusercontent.com/77831063/208921468-755e4e4a-eddd-4035-a6fb-8e9f15db28c8.png">
</p>

$$\quad$$The algorithm works as follow. First, the little and gentle brewer has to choose, as input, the type of beers that he wants to produce and the country where he wants to open his brewery. Then, the next three steps are iterated across the years :

* **Step 1**:$$\quad$$At the start of the year, the number of beers expected to be distributed during this year is divided in shares of beers that are allocated to different beer consumming countries. This is the **exportation rate** step.


* **Step 2**:$$\quad$$ Estimate how beer exports will vary during the year, based on the **popularity of beer** and the **affinity that the country has for a style of beer**. This resulting number of beers that will be effectively consummed this current year.

* **Step 3**:$$\quad$$ The number of beers expected to be distributed during the next year (step 1, next iteration) is taken as the effectively consummed number of beers this current year.

$$\quad$$ The output of this algorithm is the brewery success simulation tool. **Il faut dire encore des trucs sur les courbes obtenues, mais ça va dépendre de ce qu'on a mis dans le paragraphe introductif.**

To easy the elaboration of this algorithm, the work was separated into three tasks:

| Who $$\quad\quad\quad $$ | Task |
| :--       | :--   |
| D'Artagnan       | Study of the beers exportation rates       |
| Athos   | Study of the beers ratings distributions        |
| Porthos   | Study of the popularity of beer        |
| Aramis | Already fighting against cleaning datasets        |


## *2) Beer export rate*

D'Artagnan went in search of data to determine the **beer export rate**. He took the data from the *great druid* cleaned by Aramis. As the dataset contained **beer ratings with the user countries, the brewery countries and the posting dates**, he calculated **for each year, for each beer producing country the proportion of beers expected to be distributed in each beer consumming country**. He collected all these data in a **table named $$expected.export$$ and transmitted it to Athos and Porthos**, in order to go on with the building of the simulation algorithm.

The table $$expected.export$$ is ordered as follows: $$expected.export_{c_0,c}[i]$$ is the proportion of beers expected to be distributed from the beer producing country $$c_0$$ that is exported to the beer consumming country $$c$$ during the year $$i$$.

The following **hypothesis** concerning the $$expected.export$$ table were made : 
* each ratings is considered as a beer consummed. A beer rating for a certain user country is considered as a beer drunk in this beer consuming country. A beer rating for a certain brewery country is taken as a beer produced in this beer producing country. The posting date year is assumed to be the year when the beer was consumed.
* thus, the proportion of beers exported from a certain beer producing country to a beer consumming country during a year is calculated as the proportion of ratings for beers with a brewery in the considered beer producing country and rated by users in a consumming country during a year. 
* the calculated proportion of beers exported from a country to another during a year represents the proportion that would be exported from a brewery implanted in this country by the little and gentle brewer to another country.
* this calculation assumes that the proportion of beer exportation is independant of the beer style. Nevertheless, in the meantime, Athos and Porthos were developing an analysis to take this effect into account.

At this step, D'Artagnan had a big table including 14 years (i.e. 2004 to 2017), 203 beer production countries and 186 beer consuming countries. His next task was to **filter these data to help the little and gentle brewer** to decide in which country to establish its brewery. Remembering the first will of the little and gentle brewer to spread its beer and thus happiness in as many countries as possible, he generated the graph (fig.'Number of beer consumming countries per beer producing country'). He **plotted the number of beer consumming countries to which a beer producing country exports** during the whole time story. From this heavy-tailed distribution, he could **advice the little and gentle brewer to choose one beer producing country** that reach a high number of beer consumming countries to settle down.

{% include consumingPerProducing.html %}

Finally, D'Artagnan **plotted the detailled yearly repartition of beers expected to be distributed from some beer producing countries**. For display purpose, he opted to show the following subset from the $$expected.export$$ table. He selected the top ten of advised beer producing countries (on the plot (fig.'Number of beer consumming countries per beer producing country'), this corresponds to countries with a number of consumming country above the red line) and five other random countries. Then, he kept the beer consumming countries that contributed at least a proportion of 0.008 of the beers exported from the selected beer producing countries. The objective of this plot is to represent the annual evolution of the exports of the top-ten beer producing countries that D'Artagan advised to the little and gentle brewer and to compare them to less-optimal ones. He also wanted to illustrate the table $$expected.export$$ with this subset of data through this figure (fig.'Proportion of beer exported from the selected beer producing countries').

{% include export_beer.html %}

**Parchment of use of the graph (fig.'Proportion of beer exported from the selected beer producing countries')**
* each line represents one of the selected beer producing countries $$c_0$$. From bottom to top, the beer producing countries are displayed from more advised to less advised countries to install a brewery according the ranking on the figure (fig.'Proportion of beer exported from the selected beer producing countries').
* each column represents one of the selected beer consumming countries $$c$$.
* the value of a cell is $$expected.export_{c_0,c}[i]$$, the proportion of beers expected to be distributed from a beer producing country $$c_0$$ to a beer consumming country $$c$$ during the considered year $$i$$. 
* a producing country with a higher number of non-zero values on a line (i.e. not white cell) exports beers to a higher number of consumming countries.


## *3) Study of the beers ratings distributions*

$$\quad$$ Since the step of creating the beer export table $$expected.export$$ did not take into account the style of the beer, the task of Athos and Porthos was to adjust the expected exports by taking into account the impact of a certain type of beer. In this chapter, Athos' tasks is developped.

$$\quad$$ The old musketeer, thanks to his long experience and his hard-earned data science skills, had succeeded to identify the little and gentle brewer. He had managed to estimate the brewer behavior by imagining the reaction he might have had when analyzing the ratings his beer would have received. He made the following assumptions:

* If the ratings that his beer received in a country [c1] were very good, he would have adapted his production and would have sent more beers than initially expected to that country [c1].

* Conversely, if the ratings his beer received in a country [c2] were not good, he would have adapted his production and  would have sent fewer beers than initially planned to this country [c2].

Athos therefore tried to model his behavior in the following correspondence table:

| Rating of his beer <br> in a country| Adaptation of the <br> beer exportations | Corresponding adaptation<br>weight on the beer exports |
| :------ |:--- | :--- |
| 0 - 0.5 | -40% | 0.6 |
| 0.5 - 1 | -30% | 0.7 |
| 1 - 1.5 | -20% | 0.8 |
| 1.5 - 2 | -10% | 0.9 |
| 2 - 2.5 | / | 1 |
| 2.5 - 3 | / | 1|
| 3 - 3.5 | +10% | 1.1 |
| 3.5 - 4 | +20% | 1.2 |
| 4 - 4.5 | +30% | 1.3 |
| 4.5 - 5 | +40% | 1.4 |


This table means that, if its beer in a beer consumming country received a rating between 1.5 and 2 in year $$[i]$$, then the corresponding adaptation weight was (1-10\%) = 0.9.


$$\quad$$ The next task was then to predict what the rating would have been in each beer consuming country, for each possible chosen beer style, for each year. Fortunately, thanks to the data provided by the *great druid*, it was possible to determine the distribution of ratings that a beer style will have had in each country for each year, as shown in the following graph.

{% include rating_fig.html %}

{: .box-note}
**Note:** It's up to you, user of this sublime website, to play with the button to display these ratings densities in the countries of your choice.

{: .box-note}
**Note:** The distribution of the ratings in your country is plotted given the beer style that has been chosen to brew in the above Brewery success simulation tool to assess the affinity that your country has towards the chosen beer style.


$$\quad$$ A random draw has also been performed according to the multinomial distribution of ratings to determine the rating of the chosen beer style in each beer consumming country for each year. This method had been chosen in order to take into account the distribution of rating and the factor of randomness in rating assignments. Indeed, a user's evaluation depends on many different factors. Since all these factors could not be taken into account, Athos assumed that the value of a rating was based on the multinomial distribution abovely described and that the uncertainty induced by the more complex factors could be translated by a random draw on this probability density.

{: .box-warning}
**Hypothesis:** When Athos studied the affinity of a country to a beer style, there may have been missing values. For example, if in 2015 in Spain there were no ratings for Ale style. In these cases, the draw was made on a uniform rating distribution.

$$\quad$$ The above described random draw was thus performed and the results were stored for each beer consumming country, for each year and for each possible chosen beer style. A sample of the obtained Dataframe that contains the adaptation weigths.

### Adaptation weight on the beer exports of a country towards a certain style of beer during a chosen year

<table border="1" class="dataframe">   <thead>     <tr style="text-align: right;">       <th></th>       <th></th>       <th>Ale</th>       <th>Belgian Ale</th>       <th>Bock</th>       <th>IPA</th>       <th>Pilsener</th>       <th>Wheat Beer</th>       <th>IIPA</th>     </tr>     <tr>       <th>period</th>       <th>user_location</th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>     </tr>   </thead>   <tbody>     <tr>       <th rowspan="5" valign="top">2015.0</th>       <th>United States</th>       <td>0.6</td>       <td>1.2</td>       <td>1.2</td>       <td>1.0</td>       <td>1.0</td>       <td>0.9</td>       <td>1.3</td>     </tr>     <tr>       <th>United Kingdom</th>       <td>0.6</td>       <td>0.9</td>       <td>0.7</td>       <td>1.0</td>       <td>1.0</td>       <td>1.2</td>       <td>0.8</td>     </tr>     <tr>       <th>Brazil</th>       <td>1.0</td>       <td>1.4</td>       <td>0.8</td>       <td>0.7</td>       <td>1.2</td>       <td>0.6</td>       <td>0.6</td>     </tr>     <tr>       <th>Canada</th>       <td>1.3</td>       <td>0.7</td>       <td>0.7</td>       <td>0.6</td>       <td>0.7</td>       <td>0.8</td>       <td>0.6</td>     </tr>     <tr>       <th>Germany</th>       <td>1.1</td>       <td>1.3</td>       <td>1.1</td>       <td>1.2</td>       <td>0.7</td>       <td>1.2</td>       <td>0.7</td>     </tr>   </tbody> </table>

$$\quad$$ At the end, the output of this work consisted in all the corresponding adaptation weights on the beer exports based on the ratings distribution. This output was sent further to Porthos in a table $$weightings$$. The table is ordered as follows: $$weightings_{c,s}[i]$$ is the weight that reflects the affinity that a beer consumming country $$c$$ has with a beer style $$s$$ during the year $$i$$.

## *4) Study of the popularity of beer*

$$\quad$$ As explained in the previous chapters, Porthos' work was complementary to that done by Athos regarding the objective to assess the beer style dependence on the number of beers exported.

$$\quad$$As the dataset contained ratings with the rated **beer style**, the **publication dates** and **the locations** of the users, Porthos first defined the notion of *beer's popularity*. The latter is calculated as the proportion of one type of beer among all the rated beers considered in one year and for one country. Porthos made the assumption that a decreasing *beer's popularity* means that people drink a lower proportion of this beer style compared to other in the same beer consuming country and vice versa.

$$\quad$$ Porthos defined the variation of popularity: $$\Delta popularity$$. It represents the variation of the proportion of the number of ratings of a given beer style in a given beer consuming country between two years.

$$\quad$$ To evaluate this, he plotted the *beer's popularity* for all countries and for all types of beers across years. Porthos had the feeling that the latter did not represent well a plausible evolution of *beer's popularity* within a year, as too abrupt. He thus decided to smooth these curves out by applying a k-nearest neighbors algorithm with $$k = 5$$. His calculations are shown on the figure below.

{% include porthos.html %}

$$\quad$$ He then created a table $$popularity.variations$$, in which the coefficient $$popularity.variations_{c,s}[i]$$ represents the variation rate of the proportion of the number of ratings of a beer style $$s$$ in a beer consummer country $$c$$ during the year $$i$$. To obtain a multiplicative factor from this rate, one should add the scalar $$1$$ to it.

$$\quad$$ At that time, all tools were ready to build the algorithm.


## *5) Gathering of all tasks*

$$\quad$$ As a final step, *Les4mousquetaires* gathered their work to calculate how many beers the little and gentle brewer will have produced the year $$i$$ considering his **brewery location** and **beer style** choices. They first picked the expected proportions computed by D'Artagnan from the table $$proportion.export$$ and multiplied it with the expected number of beer to be exported before the adjustments. Then, they multiplied the expected exports by the weights that are given by Athos in $$weightings$$ that expressed the affinity that a country had towards a *beer style* during a specific year. Finally, he multiplied this result by the muliplicative factor $$(1 + popularity.variations_{c}[i])$$ in order to take into account the variation in *beer's popularity* of a *beer style* during the considered year. The above paragraph can be summarized with the following formula:

\\[exportation_{c}[i] = expected.number[i] \times expected.export_{c_0,c}[i] \times weightings_{c,s}[i] \times (1 + popularity.variations_{c}[i])\\]



**copy-paste pour la partie Gomez**

$$exportation_{c}[i]$$ : adjusted number of beers that is effectively exported for the year i

$$expected.number[i]$$ : expected number of beers to be exported, estimated at the beginning of the year i before the musketeers adjustments

$$expected.export_{c_0,c}[i]$$ : number of beers expected to be distributed for the year i in the beer consummer country $c$ from the country $$c_0$$ where the brewery is located

$$popularity.variations_{c}[i]$$ : variation rate of the beer style popularity between years i+1 and i in the beer consuming country $$c$$

$$weightings_{c,s}[i]$$ : coefficient for year i to weight the exports estimating the affinity of a beer consuming country towards a beer style $$s$$

At that time, the total exports of the little and gentle brewer corresponds to the sum of all exports over all beer consuming countries:

$$
Total\_exports = \sum_{c \in Country} exportation_{c}[i]
$$

$$\quad$$ At the end, to calculate the total production for the year i+1, the following sum is computed:
