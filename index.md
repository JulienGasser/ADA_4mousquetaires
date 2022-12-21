---
layout: page
title: What if I set up a brewery?
subtitle: An original ADA story about beer !
gh-repo: juliengasser/ADA4mousquetaires
tags: [brewery, beer, flavour, taste, export, plotly]
---

 ## Once upon a time...
 
There was a little and gentle brewer who dreamed of spreading happiness in the world. As everyone knows, beer makes people happy, so he decided to reach his dream by creating a beer and to spread it around the world. The problem is that he sucked at market study and didn't know how to begin with his business... If he aimed to reach the most people with his beer, he had to make the good choices ! Which type of beers to choose ? Where to open his brewery ? ... That's a complicated problem, isn't it ? Fortunately, Les4Mousquetaires were here to help this litte and gentle brewer by creating a tool that would help him a lot. This tool is a market simulator that will predict the spread of his beer according to the choice of his beer and brewery. Will this gentle and little brewer reach is dream ?

## Brewery success simulation tool

Il faut: 1) voici le tool, 2) comment utiliser le tool (user guide), 3) dire de lire la datastory qui va amener à ce tool

### Let's play with the simulation

{% include beermap.html %}

### Introduire la cummulative et afficher la nouvelle version de la figure
Il faut: 1) Dans un premier temps, il veut exporter dans un max de pays 2) dans un 2ème temps, exporter un max de bières.

<br>
<br>
<div id="plotly-countryfig"></div>

### Could you do better than the gentle and little brewer?

Il faudra donner lequel il a choisi grâce à l'outil que lui ont fourni les 4 mousquetaires.
Dire: Lisez déjà son histoire. Une fois que ce sera fait, pourriez vous faire mieux que lui?


### *1) Birth of the algorithm*

$$\quad$$Created by Les4Mousquetaires, the above simulation is a practical tool to help the little and gentle brewer to spread happiness 🍻 around the world. The conception of this tool was a long and perilous adventure ! Here is the story...


<img align="right" width="120" height="120" src="https://user-images.githubusercontent.com/77831063/208921476-d9d9df57-807e-4d7d-be22-125298e39ff0.png">

$$\quad$$ The first ordeal to overcome was to find datas. After many reflections, *Les4Mousquetaires* decided to ask the *great druid* for help because he was known to be a real beer lover. The *great druid* was also known for hanging out in bars all day long. So Les4Mousquetaires went to the most famous bar in town and, as expected, they found the *great druid* in a sorry state. After explaining their project, the *great druid* took out an old crystal ball from his bag and consulted the oracles to find out how the beer market would evolve in the next few years. After consultation, the *great druid* took a USB stick, plugged it into his crystal ball and saved two datasets [**RateBeer**](https://www.ratebeer.com/) and [**BeerAdvocate**](https://www.beeradvocate.com/). While giving the USB stick to *Les4Mousquetaires*, as the *great druid* was a little bit wasted, he dropped it in his beer... They jumped on the beer and saved the USB stick from drowning. However, both datasets were partially corrupted. Panic-stricken by the poor state of the two datasets, Aramis decided to isolate himself to start a big cleaning process of the two datasets.

$$\quad$$On their side, D'Artagnan, Athos and Porthos sat down around a table and started to elaborate the tool to help the little and gentle brewer. Based on the two datasets being cleaned by Aramis, they decided to create an interative algorithm divided into 3 steps. This algorithm is explained below and illustrated on a parchment: 

<img align="right" width="120" height="120" src="https://user-images.githubusercontent.com/77831063/208921468-755e4e4a-eddd-4035-a6fb-8e9f15db28c8.png">

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


## Beer export rate

D'Artagnan went in search of data to determine the **beer export rate**. He took the data from the *great druid* cleaned by Aramis and for each year, he calculated **for each beer producing country the yearly proportion of beers expected to be distributed in each beer consumming country**. He collected all these data in a **table named $$exported$$ and transmitted it to Athos and Porthos**, in order to go on with the building of the simulation algorithm.

The table $$exported$$ is ordered as follows: $$exported_{c_0,c}[i]$$ is the proportion of beers expected to be distributed from the beer producing country $$c_0$$ that is exported to the beer consumming country $$c$$ during the year $$i$$.

The following **hypothesis** concerning the $$exported$$ table were made : 
* each ratings is considered as a beer consummed. Thus the proportion of beers exported from a certain beer producing country to a beer consumming country during a year is calculated as the proportion of ratings for beers with a brewery in the considered beer producing country and rated by users in a consumming country during a year. 
* the calculated proportion of beers exported from a country to another during a year represents the proportion that would be exported from a brewery implanted in this country by the little and gentle brewer to another country.
* this calculation assumes that the proportion of beer exportation is independant of the beer style. Nevertheless, in the meantime, Athos and Porthos were developing an analysis to take this effect into account.

At this step, D'Artagnan had a big table including 14 years (i.e. 2004 to 2017), 203 beer production countries and 186 beer consuming countries. His next task was to **filter these data to help the little and gentle brewer** to decide in which country to establish its brewery. Remembering the first will of the little and gentle brewer to spread its beer and thus happiness in as many countries as possible, he generated the graph (fig.'Number of beer consumming countries per beer producing country'). He **plotted the number of beer consumming countries to which a beer producing country exports** during the whole time story. From this heavy-tailed distribution, he could **advice the little and gentle brewer to choose one beer producing country** that reach a high number of beer consumming countries to settle down.

**renommer le titre et enlever les html**

{% include consumingPerProducing.html %}

Finally, D'Artagnan **plotted the detailled yearly repartition of beers expected to be distributed from some beer producing countries**. For display purpose, he opted to show the following subset from the $$exported$$ table. He selected the top ten of advised beer producing countries (on the plot (fig.'Number of beer consumming countries per beer producing country'), this corresponds to countries with a number of consumming country above the red line) and five other random countries. Then, he kept the beer consumming countries that contributed at least a proportion of 0.008 of the beers exported from the selected beer producing countries. The objective of this plot is to represent the annual evolution of the exports of the top-ten beer producing countries that D'Artagan advised to the little and gentle brewer and to compare them to less-optimal ones. He also wanted to illustrate the table $$exported$$ with this subset of data through this figure (fig.'Proportion of beer exported from the selected beer producing countries').

{% include export_beer.html %}

**Parchment of use of the graph (fig.'Proportion of beer exported from the selected beer producing countries')** :
* each line represents one of the selected beer producing countries $$c_0$$. From bottom to top, the beer producing countries are displayed from more advised to less advised countries to install a brewery according the ranking on the figure (fig.'Proportion of beer exported from the selected beer producing countries').
* each column represents one of the selected beer consumming countries $$c$$.
* the value of a cell is $$exported_{c_0,c}[i]$$, the proportion of beers expected to be distributed from a beer producing country $$c_0$$ to a beer consumming country $$c$$ during the considered year $$i$$. 
* a producing country with a higher number of non-zero values on a line (i.e. not white cell) exports beers to a higher number of consumming countries.



## Story de jerem
In the course of these various investigations, Athos decided to look more closely at the influence of the small brewer's choice of beer style.
Noting that each style is not appreciated in the same way in all countries, he realized that exports varied significantly when the ratings were very good or very bad. However, this was not an immutable and universal rule. Chance played a significant role in the equation. He knew that.
He had his back to the wall and had to find a way to model a country's affinity for a style of beer when an idea came to him. He constructed the following algorithm.

Thanks to the data provided by the druid, it is possible to determine the distribution of ratings that a style of beer has had in each country, as shown in the following graph.

{% include rating_fig.html %}

              
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

### ___3) Study of the popularity of beer___

$$\quad$$Once produced, the beers are exported around the world with rates studied by D'Artagnan. On its side, Athos calculated the ratings distribution depending on the year, the beer type and the country. To predict how many beers our little and gentle brewer have to produce for the following year to fit the worldwide demand for its beer, Porthos came up with an idea... 

$$\quad$$As the dataset contained ratings with the rated **beers type**, the **publication dates** and **the locations** of the users, he defines the notion of *beer's popularity*. The latter calculated the proportion of one type of beer among all the beers considered in one year and for one country. Porthos made the assumption that a decreasing *beer's popularity* means that people drink less of this beer and vice versa. 

$$\quad$$Porthos found a formula to calculate how many beers the little and gentle brewer have to produce the year $$i + 1$$ to satisfy the demand of a specific country $$c$$  : 

\\[production_{c}[i+1] = exported_{c_0,c}[i] \times (1 +  w_{c}[i] \times \Delta popularity_{c}[i])\\]

\\[
\begin{aligned}
&\begin{array}{ll}
production_{c}[i+1] : & \text{number of beers to produce for the year i+1 to statisfy the demand of the country $$c$$ }\\
exported_{c_0,c}[i] : & \text{number of beers exported for the year i in the country $c$ from the country $$c_0$$ where the brewery is located (given by D'Artagnan)}\\
\Delta popularity_{c}[i] : & \text{difference in beer's popularity between years i+1 and i in the country $$c$$}\\
w_{c}[i] : & \text{coefficient for year i to weight the popularity variation in the country $$c$$ (given by Athos)}\\
\end{array}
\end{aligned}
\\]

{: .box-note} 
**Note** : $$production_{c}$$, $$exported_{c}$$, $$\Delta popularity_{c}$$ and $$w_{c}$$ are calculated for the fixed beer's type chosen by the little and gentle brewer.

$$\quad$$To calculate the $$\Delta popularity$$'s, Porthos first plotted the popularity of beers for all countries and for all types of beers during time. As the obtained curves were not smooth and regular, that isn't expected from a beer popularity evolution during time, he decided to smooth these curves out by applying a k-nearest neighbors algorithm with $$k = 5$$. His calculations are shown on the figure below.

{% include porthos.html %}

$$\quad$$To calculate the total production for the year i+1 :

$$
production[i+1] = \sum_{c \in Country} production_c[i]
$$
