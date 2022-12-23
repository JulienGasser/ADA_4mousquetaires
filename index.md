---
layout: page
title: The guy that became a brewer
subtitle: An original ADA story about beer !
gh-repo: juliengasser/ADA4mousquetaires
tags: [brewery, beer, flavour, taste, export, plotly]
---


## Once upon a time...
 
$$\quad$$ There was a little and gentle brewer who dreamed of spreading happiness in the world. As everyone knows, beer makes people happy, so he decided to reach his dream by creating a beer and to spread it around the world. The problem is that he sucked at market study and didn't know how to begin with his business... If he first aimed to reach as many countries as possible and secondly the most people as possible with his beer, he had to make the good choices ! Which type of beers to choose ? Where to open his brewery ? ... That's a complicated problem, isn't it ? Fortunately, *Les4Mousquetaires* were here to help this litte and gentle brewer by creating a tool that would help him a lot. This tool is a brewery success simulation that will predict the spread of his beer according to the choice of his beer and brewery. Will this gentle and little brewer reach is dream ?

## Brewery success simulation tool

{: .box-note}
**Note:** The temporality of the story is given in the assupmtion 1

$$\quad$$ Here is the brewery success simulation tool created by *Les4Mousquetaires* for the little and gentle brewer. As the latter is generous, he leaves this precious tool in open source to the internet. 

$$\quad$$ This simulation was created to guide the little and gentle brewer when establishing its brewery in 2004. This tool takes as inputs a country where to set up a brewery and a style of beer to brew. Then, it outputs a world map with the prediction of the distribution of the beers produced by the brewery across countries and years, until 2016, for an initial expected production of 1'000 beers. In addition, given the little and gentle brewer's goals of first reaching as many countries as possible and then as many people as possible, a second graph shows the cumulative number of countries reached by its beer and the cumulative number of beers distributed across years. The happiness gauge on the right of the world map shows how happy are the countries on the map. This happiness score is based on taking the $$log_{10}$$ of the distributed beers in each country.

{: .box-note}
**Note:** Advice of *Les4Mousquetaires* for the little and gentle brewer : Open a brewery that produces Ale style beers in the United States. You, user of this website, feel free to brew your preferred beer style in different countries to try to make people happier than the little and gentle brewer.

<p align="center">
<img align="center" width="350" src="https://user-images.githubusercontent.com/77831063/209349672-40304fa3-03a8-483f-8c60-3e424b4d8c83.jpg">
</p>

A little trouble to find it or by curiosity to better understand the simulation, the following story of the little and gentle brewer and *Les4Mousquetaires* is waiting for you…


### Let's play with the simulation

{% include beermap.html %}

<br>
<br>
<div id="plotly-exportfig"></div>

## Story

### *1) Birth of the algorithm*

$$\quad$$Created by *Les4Mousquetaires*, the above simulation is a practical tool to help the little and gentle brewer to spread happiness 🍻 around the world. The conception of this tool was a long and perilous adventure ! Here is the story...


<img align="right" width="180" height="220" src="https://user-images.githubusercontent.com/77831063/209109848-ab9ce2c6-ba5e-4256-877d-c3f20a159ed0.png">

$$\quad$$ The first ordeal to overcome was to find datas. After many reflections, *Les4Mousquetaires* decided to ask the *great druid* for help because he was known to be a real beer lover. The *great druid* was also known for hanging out in bars all day long. So *Les4Mousquetaires* went to the most famous bar in town and, as expected, they found the *great druid* in a sorry state. After explaining their project, the *great druid* took out an old crystal ball from his bag and consulted the oracles to find out how the beer market would evolve in the next few years. After consultation, the *great druid* took a USB stick, plugged it into his crystal ball and saved two datasets [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/). These datasets were beer rating predictions for the next years. Each rating contains many features such as the posting date, a possible review, the beer name, the brewery location, the user location, ratings on appearance, aroma...  While giving the USB stick to *Les4Mousquetaires*, as the *great druid* was a little bit wasted, he dropped it in his beer... They jumped on the beer and saved the USB stick from drowning. However, both datasets were partially corrupted. Panic-stricken by the poor state of the two datasets, Aramis decided to isolate himself to start a big cleaning process of the two datasets.

$$\quad$$On their side, D'Artagnan, Athos and Porthos sat down around a table and started to elaborate the tool to help the little and gentle brewer. Based on the two datasets being cleaned by Aramis, they decided to create an interative algorithm divided into 3 steps. This algorithm is explained below and illustrated on a parchment: 

<p align="center">
<img align="center" height="400" src="https://user-images.githubusercontent.com/77831063/208921468-755e4e4a-eddd-4035-a6fb-8e9f15db28c8.png">
</p>

$$\quad$$The algorithm works as follow. First, the little and gentle brewer has to choose, as input, the type of beers that he wants to produce and the country where he wants to open his brewery. Then, the next three steps are iterated across the years :

* **Step 1**:$$\quad$$At the start of the year, the number of beers expected to be distributed during this year is divided in shares of beers that are allocated to different beer consuming countries. This is the exportation rate step determined with the **beer exportation profile**.


* **Step 2**:$$\quad$$ Estimate how beer exports will vary during the year, based on the **popularity of beer** and the **affinity that the country has for a style of beer**. This results in the number of beers that will be effectively consummed this current year.

* **Step 3**:$$\quad$$ The number of beers expected to be distributed during the next year (step 1, next iteration) is taken as the effectively consummed number of beers this current year. The number of beers expected to be distributed during the first year is initialized with 1'000 beers.

$$\quad$$ The output of this algorithm is the brewery success simulation tool. 

To easy the elaboration of this algorithm, the work was separated into three tasks:

| Who $$\quad\quad\quad $$ | Task |
| :--       | :--   |
| D'Artagnan       | Study of the beer export profile       |
| Athos   | Study of the beer ratings distributions        |
| Porthos   | Study of the popularity of beer        |
| Aramis | Already fighting against cleaning datasets        |


## *2) Beer export profile*

$$\quad$$ At the beginning of the year $$i$$, a certain number of beers is expected to be distributed during the year: $$expected.number[i]$$. 

$$\quad$$  The objective of D'Artagnan was first to determine the expected beer export profile. He took the data from the *great druid* cleaned by Aramis. As the dataset contained beer ratings with the user countries, the brewery countries and the posting dates, he calculated for each year, for each beer producing country the proportion of beers expected to be distributed in each beer consuming country. He collected all these data in a table named $$proportion.export$$ to build later the simulation algorithm.

$$\quad$$ The table $$expected.export$$ is ordered as follows: $$proportion.export_{c_0,c}[i]$$ is the proportion of beers expected to be distributed from the beer producing country $$c_0$$ that is exported to the beer consuming country $$c$$ during the year $$i$$.

$$\quad$$ The following **hypothesis** concerning the $$proportion.export$$ table were made : 
* each rating is considered as a beer consummed. A beer rating for a certain user country is considered as a beer drunk in this beer consuming country. A beer rating for a certain brewery country is taken as a beer produced in this beer producing country. The posting date year is assumed to be the year when the beer was consumed.
* thus, the proportion of beers exported from a certain beer producing country to a beer consuming country during a year is calculated as the proportion of ratings for beers with a brewery in the considered beer producing country and rated by users in a consuming country during a year. 
* the calculated proportion of beers exported from a country to another during a year is assumed to represent the proportion of beers that would be exported from a brewery implanted in this country by the little and gentle brewer to another country.
* this calculation assumes that the proportion of beer exportation is independant of the beer style. Nevertheless, in the meantime, Athos and Porthos were developing an analysis to take this effect into account.

$$\quad$$ At this step, D'Artagnan had a big table including 14 years (i.e. 2004 to 2017), 203 beer production countries and 186 beer consuming countries. His next task was to filter these data to help the little and gentle brewer to decide in which country to establish its brewery. Remembering the first will of the little and gentle brewer to spread its beer and thus happiness in as many countries as possible, he plotted the number of beer consuming countries to which a beer producing country exports during the whole time story. From this heavy-tailed distribution, he could advice the little and gentle brewer to choose one beer producing country that reach a high number of beer consuming countries to settle down.

{% include consumingPerProducing.html %}

$$\quad$$ Finally, D'Artagnan plotted the detailled yearly repartition of beers expected to be distributed from some beer producing countries. For display purpose, he opted to show the following subset from the $$proportion.export$$ table. He selected the top ten of advised beer producing countries (on the above plot, this corresponds to countries with a number of consuming countries above the red line) and five other random countries (France, Thailand, Switzerland, Peru, Colombia). Then, he kept the beer consuming countries that contributed at least a proportion of 0.008 of the beers exported from the selected beer producing countries. The objective of this plot is to represent the annual evolution of the exports of the top-ten beer producing countries that D'Artagan advised to the little and gentle brewer and to compare them to less-optimal ones. He also wanted to illustrate the table $$proportion.export$$ with this subset of data through this figure.

{% include export_beer.html %}

**Parchment of use of the figure**
* each line represents one of the selected beer producing countries $$c_0$$. From bottom to top, the beer producing countries are displayed from more advised to less advised countries to install a brewery according to the ranking from the figure about the 'number of beer consumming countries reached by a beer producing country'.
* each column represents one of the selected beer consuming countries $$c$$.
* the value of a cell is $$proportion.export_{c_0,c}[i]$$, the proportion of beers expected to be distributed from a beer producing country $$c_0$$ to a beer consuming country $$c$$ during the considered year $$i$$. 
* a producing country with a higher number of non-zero values on a line (i.e. not white cell) exports beers to a higher number of consuming countries.


## *3) Study of the beers ratings distributions*

$$\quad$$ Since the step of creating the beer export table $$proportion.export$$ did not take into account the style of the beer, the task of Athos and Porthos was to adjust the expected production $$expected.number[i]$$ defined at the beginning of the year $$i$$ by taking into account the impact of a certain chosen type of beer. In this chapter, Athos' tasks is developped.

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


$$\quad$$ This table means that, if its beer in a beer consumming country received a rating between 1.5 and 2 in year $$[i]$$, then the corresponding adaptation weight was (1-10\%) = 0.9.


$$\quad$$ The task was thus to predict what the rating would have been in each beer consuming country, for each possible chosen beer style, for each year. Fortunately, thanks to the data provided by the *great druid*, it was possible to determine the distribution of ratings that a beer style will have had in each country for each year, as shown in the following graph.

{% include rating_fig.html %}

{: .box-note}
**Note:** The distribution of the ratings in your country is plotted given the beer style that has been chosen to brew in the above Brewery success simulation tool to assess the affinity that a country has towards the chosen beer style.


$$\quad$$ A random draw has also been performed according to the multinomial distribution of ratings to determine the rating of the chosen beer style in each beer consuming country for each year. This method had been chosen in order to take into account the distribution of rating and the factor of randomness in rating assignments. Indeed, a user's evaluation depends on many different factors. Since all these factors could not be accurately assessed, Athos assumed that the value of a rating was based on the multinomial distribution abovely described and that the uncertainty induced by the more complex factors could be translated by a random draw on this probability density.

$$\quad$$ When Athos studied the affinity of a country to a beer style, there may have been missing values. For example, if in 2015 in Spain there were no ratings for Ale style. In these cases, he made the following **hypothesis**: the draw was made on a uniform rating distribution.

$$\quad$$ The above described random draw was thus performed and the results were stored for each beer consumming country, for each year and for each possible chosen beer style. A sample of the obtained Dataframe that contains the adaptation weigths. Below a sample of this Dataframe is presented.

### Adaptation weight on the beer exports of a country towards a certain style of beer during a chosen year

<table border="1" class="dataframe">   <thead>     <tr style="text-align: right;">       <th></th>       <th></th>       <th>Ale</th>       <th>Belgian Ale</th>       <th>Bock</th>       <th>IPA</th>       <th>Pilsener</th>       <th>Wheat Beer</th>       <th>IIPA</th>     </tr>     <tr>       <th>period</th>       <th>user_location</th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>     </tr>   </thead>   <tbody>     <tr>       <th rowspan="5" valign="top">2015.0</th>       <th>United States</th>       <td>0.6</td>       <td>1.2</td>       <td>1.2</td>       <td>1.0</td>       <td>1.0</td>       <td>0.9</td>       <td>1.3</td>     </tr>     <tr>       <th>United Kingdom</th>       <td>0.6</td>       <td>0.9</td>       <td>0.7</td>       <td>1.0</td>       <td>1.0</td>       <td>1.2</td>       <td>0.8</td>     </tr>     <tr>       <th>Brazil</th>       <td>1.0</td>       <td>1.4</td>       <td>0.8</td>       <td>0.7</td>       <td>1.2</td>       <td>0.6</td>       <td>0.6</td>     </tr>     <tr>       <th>Canada</th>       <td>1.3</td>       <td>0.7</td>       <td>0.7</td>       <td>0.6</td>       <td>0.7</td>       <td>0.8</td>       <td>0.6</td>     </tr>     <tr>       <th>Germany</th>       <td>1.1</td>       <td>1.3</td>       <td>1.1</td>       <td>1.2</td>       <td>0.7</td>       <td>1.2</td>       <td>0.7</td>     </tr>   </tbody> </table>

$$\quad$$ At the end, the output of this work consisted in all the corresponding adaptation weights on the beer exports based on the ratings distribution. This output is organized in a table $$weightings$$. The table is ordered as follows: $$weightings_{c,s}[i]$$ is the weight that reflects the affinity that a beer consumming country $$c$$ has with a beer style $$s$$ during the year $$i$$.

## *4) Study of the popularity of beer*

$$\quad$$ As explained in the previous chapters, Porthos' work was complementary to that done by Athos regarding the objective to assess the beer style dependence on the expected production $$expected.number[i]$$ defined at the beginning of the year.

$$\quad$$As the dataset contained ratings with the rated beer style, the publication dates and the locations of the users, Porthos first defined the notion of *beer's popularity*. The latter is calculated as the proportion of one type of beer among all the rated beers considered in one year and for one user country i.e. beer consuming country. Porthos made the assumption that a decreasing *beer's popularity* means that people drink a lower proportion of this beer style compared to other in the same beer consuming country and vice versa.

$$\quad$$ To evaluate this data, he plotted the *beer's popularity* for all countries and for all types of beers across years. Porthos had the feeling that the latter did not represent well a plausible evolution of *beer's popularity* within a year, as too abrupt. He thus decided to smooth these curves out by applying a k-nearest neighbors algorithm with $$k = 5$$. His calculations are illustrated on the figure below.

{% include porthos.html %}

$$\quad$$ He then created a table $$popularity.variations$$, in which the coefficient $$popularity.variations_{c,s}[i]$$ represents the variation rate of the proportion of the number of ratings of a beer style $$s$$ in a beer consuming country $$c$$ during the year $$i$$. In other words, $$popularity.variations_{c,s}[i]$$ corresponds to the difference between the *beer's popularity* for the beer consuming country $$c$$ and beer style $$s$$ of the year $$i+1$$ and the one of the year $$i$$. To obtain a multiplicative factor from this rate, one should add the scalar $$1$$ to it. 

{: .box-note}
**Note:** It should be noticed here that as the data of 2018 are not available, then *popularity.variations* cannot be computed for 2017, thus the brewery success simulation run from 2004 to 2016.

$$\quad$$ At that time, all tools were ready to build the algorithm.


## *5) Gathering of all tasks*

$$\quad$$ As a final step, *Les4mousquetaires* gathered their work to calculate how many beers the little and gentle brewer will have produced the year $$i$$ considering his **brewery location** and **beer style** choices. Following the steps described in chapter 1 :**Step 1**, they first picked the export proportion profiles computed by D'Artagnan from the table $$proportion.export$$ and multiplied it with the expected number of beer to be exported before the adjustments, $$expected.number$$. **Step 2**, they multiplied the expected exports by the weights that are given by Athos in $$weightings$$ that expressed the affinity that a country had towards a beer style during a specific year. They then multiplied this result by the muliplicative factor $$(1 + popularity.variations_{c}[i])$$ in order to take into account the variation in *beer's popularity* of a beer style during the considered year. The above paragraph can be summarized with the following formula:

$$exportation_{c_0,c}[i] =$$

$$expected.number[i] \times proportion.export_{c_0,c}[i] \times weightings_{c,s}[i] \times (1 + popularity.variations_{c,s}[i])$$

In the above equation, the variables are explained below:

* $$exportation_{c_0,c}[i]$$ : adjusted number of beers that is effectively exported for the year i from the beer producing country $$c_0$$ to the beer consuming country $$c$$

* $$expected.number[i]$$ : expected number of beers to be exported, estimated at the beginning of the year i before the musketeers adjustments

* $$proportion.export_{c_0,c}[i]$$ : proportion of beers expected to be distributed for the year i in the beer consummer country $$c$$ from the country $$c_0$$ where the brewery is located

* $$popularity.variations_{c,s}[i]$$ : difference between the *beer’s popularity* for the beer consuming country *c* and beer style *s* of the year *i+1* and the one of the year *i*

* $$weightings_{c,s}[i]$$ : coefficient for year *i* to weight the exports estimating the affinity of a beer consuming country *c* towards a beer style $$s$$

After these adjustments, for the year $$i$$ the total number of beers distributed by the little and gentle brewer corresponds to the sum of all exports over all beer consuming countries:

$$
Total.exports[i] = \sum_{c \in Country} exportation_{c_0,c}[i]
$$

$$\quad$$ **Step 3**. The expected production $$expected.number[i]$$ for the year $$i$$ defined at the beginning of the year, is taken as the total exports of the year $$i-1$$. Id est:


$$
expected.number[i] = Total.exports[i-1]
$$

At the beginning of the simulation, for the year 2004, the expected production $$expected.number[2004]$$ is set to 1'000 beers.

## 6) 🎊🎉 Final advice 🎊🎉

Although D'Artagnan's advice was explicit and easy to interpret, Athos' and Porthos' advices were more complex and therefore less obvious to the little and gentle brewer. It is for this reason that *Les4Mousquetaires* chose to explore all the different possibilities of brewery locations and beer syles.

As the little and gentle brewer based his choice firstly on the number of countries reached by his beer and secondly on the number of beers produced, *Les4Mousquetaires* chose to represent their results in two distinct tables.


The first was the top 10 pairs `(brewery location, beer style)` in terms of number of beers produced.

<table border="1" class="dataframe">   <thead>     <tr> </tr>     <tr>       <th>Rank</th>       <th>country</th>       <th>beer</th>       <th>cumulated countries</th>       <th>cumulated beers</th>     </tr>   </thead> 
    
<tbody>     <tr>       <th>🥇</th>       <td>North Korea</td>       <td>Specialty Beer</td>       <td>14</td>       <td>34589.0</td>     </tr>     <tr>       <th>🥈</th>       <td>Canada</td>       <td>IIPA</td>       <td>102</td>       <td>33356.0</td>     </tr>     <tr>       <th>🥉</th>       <td>United States</td>       <td>Strong Ale</td>       <td>141</td>       <td>33144.0</td>     </tr>     <tr>       <th>4</th>       <td>United States</td>       <td>IIPA</td>       <td>141</td>       <td>31565.0</td>     </tr>     <tr>       <th>5</th>       <td>Moldova</td>       <td>Dark Lager</td>       <td>33</td>       <td>30722.0</td>     </tr>     <tr>       <th>6</th>       <td>United States</td>       <td>Ale</td>       <td>141</td>       <td>30533.0</td>     </tr>     <tr>       <th>7</th>       <td>Belarus</td>       <td>Sour</td>       <td>42</td>       <td>30388.0</td>     </tr>     <tr>       <th>8</th>       <td>Antigua &amp; Barbuda</td>       <td>Strong Ale</td>       <td>15</td>       <td>29395.0</td>     </tr>     <tr>       <th>9</th>       <td>Tunisia</td>       <td>Ale</td>       <td>32</td>       <td>29249.0</td>     </tr>     <tr>       <th>10</th>       <td>Madagascar</td>       <td>Dark Lager</td>       <td>19</td>       <td>29060.0</td>     </tr>   </tbody> </table>

The second one was the top 10 pairs in terms of number of countries in which the beer was spread.

<table border="1" class="dataframe">   <thead>   <tr>       <th>Rank</th>       <th>country</th>       <th>beer</th>       <th>cumulated countries</th>       <th>cumulated beers</th>     </tr>   </thead>   <tbody>     <tr>       <th>🥇</th>       <td>United States</td>       <td>Ale</td>       <td>141</td>       <td>30533.0</td>     </tr>     <tr>       <th>🥈</th>       <td>United States</td>       <td>Lager</td>       <td>141</td>       <td>18852.0</td>     </tr>     <tr>       <th>🥉</th>       <td>United States</td>       <td>Belgian Ale</td>       <td>141</td>       <td>15480.0</td>     </tr>     <tr>       <th>4</th>       <td>United States</td>       <td>Bitter Ale</td>       <td>141</td>       <td>16030.0</td>     </tr>     <tr>       <th>5</th>       <td>United States</td>       <td>Bock</td>       <td>141</td>       <td>9436.0</td>     </tr>     <tr>       <th>6</th>       <td>United States</td>       <td>Brown Ale</td>       <td>141</td>       <td>16459.0</td>     </tr>     <tr>       <th>7</th>       <td>United States</td>       <td>Cider</td>       <td>141</td>       <td>16736.0</td>     </tr>     <tr>       <th>8</th>       <td>United States</td>       <td>Dark Ale</td>       <td>141</td>       <td>14363.0</td>     </tr>     <tr>       <th>9</th>       <td>United States</td>       <td>Dark Lager</td>       <td>141</td>       <td>22483.0</td>     </tr>     <tr>       <th>10</th>       <td>United States</td>       <td>IIPA</td>       <td>141</td>       <td>31565.0</td>     </tr>   </tbody> </table>

According to the wishes of the little and gentle brewer, *Les4Mousquetaires* suggested the following combinations:

    🥇 United States : Ale 
    🥈 United States : IIPA
    🥉 United States : Strong Ale
