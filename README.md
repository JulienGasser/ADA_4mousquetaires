# Website

Website url : https://juliengasser.github.io/ADA4mousquetaires/
Template : https://beautifuljekyll.com/

# Embeded figure

We use plotly library to plot our figure. See our [repo](https://github.com/epfl-ada/ada-2022-project-les4mousquetaires) to find how we generate the figures.
To avoid using dash, we generate the plotly code description of all figures and add a HTML dropdown menu with a bit of javascript to update the figure. Look at footer-script.html to see how it works. Note that this solution slow down the the loading of the page because of all the data to download.