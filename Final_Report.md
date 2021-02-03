# Introduction/Business Problem

![Montreal Downtown](http://images.dailyhive.com/20180821110913/Montreal-Skyline.jpg)
*Downtown Montreal. Image obtained from [this link](http://images.dailyhive.com/20180821110913/Montreal-Skyline.jpg)*

### Background


> As the largest city in Quebec Canada, Montreal offers great opportunities for students planning to study in an university.  
Montreal has more than five universities, so every year, there are a large number of students looking for an apartment to rent. 
However, it is always a struggle for students to select the most suitable neighborhood to rent an apartment, especially for the newcomers to the city. 
When looking for an apartment, there are numerous factors to consider, such as availability of rental properties, neighbourhood quality, and distance to grocery stores, restaurants and metro stations.

### Problem Definition
> The objective of this project is to help university students who are looking for an apartment to rent in Montreal find a neighbourhood that fits their academic and social life.

# Data

### 1. Census Profile of Montreal City, 2016
> Obtained from Statistics Canada [here](https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/details/page.cfm?Lang=E&Geo1=CSD&Code1=2466023&Geo2=PR&Code2=24&SearchText=Montreal&SearchType=Begins&SearchPR=01&B1=All&GeoLevel=PR&GeoCode=2466023&TABID=1&type=0). It is a collection of .xls files, with a huge variety of census data for each neighbourhood of Montreal.
> We can obtain information on number of rental properties available, as well as the qualities of neighbourhoods (based on average income and population density).
> After data cleaning on this set of files, we will extract the following columns for each neighbourhood: 
* Number of Rental Properties as column "Rental"
* Population Density as column "Density"
* Average Income as column "Income"

> Here is a sample of the dataframe table.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/1.jpg)

### 2. Coordinates Data from GeoPy 
> For each neighbourhood of Montreal, we gather the geographical coordinates using the Nominatim API from *geopy.geoencoders*.
> Here is a sample of the dataframe table.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/2.jpg)

### 3. GeoJSON File for Montreal Boroughs
> A GeoJSON file for the neighbourhoods in Montreal, obtained from the city of Montreal government database: [Limite administrative de l'agglomération de Montréal (Arrondissements et Villes liées)](https://donnees.montreal.ca/ville-de-montreal/polygones-arrondissements)
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/5.jpg)


### 4. Venue Data from Foursquare API
> From their collection of venue data, we will gather information on grocery stores, metro stations, restaurants and parks in Montreal. The following are the IDs retrieved from Foursquare API [Documentation](https://developer.foursquare.com/docs/build-with-foursquare/categories/), for the venue categories we are interested in.
* Metro station ID: 4bf58dd8d48988d1fd931735
* Grocery store ID: 4bf58dd8d48988d118951735
* Park ID: 4bf58dd8d48988d163941735
* Restaurant(Food) ID: 4d4b7105d754a06374d81259
> We can visualize the map of Montreal with each neighbourhood marked out using Folium.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/3.jpg)



# Methodology

### Visualization of the geographical distributions

> We can generate a map of Montreal with partitions of neighbourhoods, using the GeoJSON file that we obtained from the city of Montreal website. Then, we will first focus on visualizing the four important categories of venues on the map. Using the Folium library, we can add the four types of markers to the map, as shown below.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/4.jpg)
* Orange: Parks
* Dark green: Restaurants
* Purple: Grocery stores
* Yellow: Metro stations


