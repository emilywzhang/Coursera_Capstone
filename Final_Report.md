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
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/1.jpg)*Fig. 1*

### 2. Coordinates Data from GeoPy 
> For each neighbourhood of Montreal, we gather the geographical coordinates using the Nominatim API from *geopy.geoencoders*.
> Here is a sample of the dataframe table.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/2.jpg)*Fig. 2*

### 3. GeoJSON File for Montreal Boroughs
> A GeoJSON file for the neighbourhoods in Montreal, obtained from the city of Montreal government database: [Limite administrative de l'agglomération de Montréal (Arrondissements et Villes liées)](https://donnees.montreal.ca/ville-de-montreal/polygones-arrondissements)
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/5.jpg)*Fig. 3*


### 4. Venue Data from Foursquare API
> From their collection of venue data, we will gather information on grocery stores, metro stations, restaurants and parks in Montreal. The following are the IDs retrieved from Foursquare API [Documentation](https://developer.foursquare.com/docs/build-with-foursquare/categories/), for the venue categories we are interested in.
* Metro station ID: 4bf58dd8d48988d1fd931735
* Grocery store ID: 4bf58dd8d48988d118951735
* Park ID: 4bf58dd8d48988d163941735
* Restaurant(Food) ID: 4d4b7105d754a06374d81259


***


# Methodology

* First, we performed data cleaning on the aforementioned datasets in step 1 and 2. The resulting dataframe contains: Neighbourhood, Latitude, Longitude, Population Density, Number of Rental Properties, Average Income. Then, we will utilize the FourSquare API to obtain information on the venues. In particular, we are interested in Restaurants, Grocery Stores, Parks and Metro Stations, because first of all, university students usually don't own cars, so they need to live close enough to public transit stations and grocery stores; second, many of them get busy during exam seasons and don't have time to cook, so delivery and take-out from restaurants are usually very helpful; third, everyone loves nature, and university students need to find ways to relax and forget about the stress from their assignments, exams, presentations, quizzes, group projects etc..... So having parks nearby is definitely a plus! With these ideas in mind, we can perform exploratory data analysis to visualize the locations of those important venues on the map of Montreal.
* Second, we will perform k-means clustering to devide the neighbourhoods into clusters based on the columns that we have identified.
* From the clustering result, we can visualize patterns in each cluster in terms of average population density, average income and average number of rental properties. This will also help us compare the clustered neighbourhoods.


# Results

We can generate a map of Montreal with partitions of neighbourhoods, using the GeoJSON file that we obtained from the city of Montreal website. Then, we will first focus on visualizing the four important categories of venues on the map. Using the Folium library, we can add the four types of markers to the map, as shown below.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/4.jpg)*Fig. 4*
* Orange: Parks
* Dark green: Restaurants
* Purple: Grocery stores
* Yellow: Metro stations

Now, we perform k-means clustering and divide the neighbourhoods into 5 clusters. The resulting dataframe is shown below.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/8.jpg)*Fig. 5*

Now, we plot the neighbourhoods on the map, with different colors indicating different clusters.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/7.jpg)*Fig. 6*

Finally, we will visualize the average population density, average income and average number of rental properties for each cluster. The three plots generated are shown below.
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/9.jpg)*Fig. 7*
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/10.jpg)*Fig. 8*
![image](https://github.com/emilywzhang/Coursera_Capstone/blob/main/11.jpg)*Fig. 9*


# Discussion

By examining the dataframe produced from FourSquare, we notice that the avialable data on locations are not as abundant and accurate as other metropolitan cities we have studied like Toronto and San Francisco. For example, the total number of metro stations returned by the FourSquare API is only 13, while in reality Montreal has 4 lines of metro with 68 stations. It is possible that some location names are in French and are not included in the FourSquare database. Apart from that, the overall result is consistent with the geographical distributions in Montreal.

# Conclusion

From the above Fig. 4, we can conclude that neither the north nor the west part are good places for students to live, mainly due to the lack of metro stations to commute to the universities downtown, and the locations for grocery stores and restaurants are also too sparse. But again, it might be because of the incomplete dataset from FourSquare. Upon examining Fig. 7,8,9, we can conclude that neighbourhoods in Cluster 4 might be more suitable in terms of the availability of rental properties. It also has the highest average population density, which means it is possibly closer to downtown and has easier access to various venues. Overall, it is more likely that neighbourhoods in Cluster 4 (light orange circles in Fig. 6) are suitable for university students. 
