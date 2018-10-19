# Coursera Capstone
# Toronto neighborhood classification
## Introduction
This project intended to use geo-spatial analysis in the city of Toronto to cluster neighborhoods to take decision where to open new branch for retail based on previous success in one of Toronto neighborhood. The main problem for retail is accessibility. Some retails thrive by locating near others and some retails prefer areas where there is high pedestrian footage or high vehicle traffic density. 
Throughout this project we tried to cluster Toronto neighborhood by the category of retails and entertainment facility in that neighborhood combined with the vehicles and pedestrians’ traffic using ten different clusters. So, the business owners from the area where direct competitors located successfully or in neighborhood where they achieved success before so they can choose new places to expand in the city have almost similar attributes in the same cluster.

### Data

First of all we need to have neighborhood geographical boundaries so we can analyze defined unique neighborhoods and to find the data we used Toronto [open data portal]( https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#a45bd45a-ede8-730e-1abc-93105b2c439f) and I came across the shape file that have the boundaries in polygon with the neighborhood name and neighborhood ID. To get an idea of the Data this is Geodataframe header
### Figure1
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Toronto%20boundries.png "GeoDataFrame") 
Also, we can visualize it
### Figure2
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Screenshot_2018-10-19%20Cognitive%20Class%20-%20Labs%20JupyterLab.png "Folium Map")
also, to get the venues data with venue category and point of interest we used two sources. The first one we used was the [Foursquare API explore](https://developer.foursquare.com/) function and to get understanding of the Data collected take this example for the header
### Figure3
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/venue%20list.png "venue list header")
The second source of data was the open Data portal for [the city of Toronto](https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#7b9deecd-a51a-3485-5e3d-94f27cc8b7d4) , this data-set contains information about points of interest for residents and visitors to enjoy including public art, murals, buildings with historic or architectural significance, green spaces, restaurants and more, we added to enrich the venues data, as example see the header
### Figure4
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/pont%20of%20interest.png "point of interest header")
One of the main Issues for the retail industry is accessibility in terms of pedestrians and vehicles traffic in that area, to get those dimensions the source for was open Data portal for [the city of
Toronto](https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#7c8e7c62-7630-8b0f-43ed-a2dfe24aadc9). This data-set contains the most recent 8 peak hour vehicle and pedestrian volume counts collected at intersections where there are traffic signals. The data was typically collected between the hours of 7:30 a.m. and 6:00 p.m. as example for the Dataframe header:
### Figure5
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/traffic%20data.png "traffic")
Also, we can visualize it, the orange circles is vehicle traffic and the blue circles is pedestrian traffic
### Figure6
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Traffic%20map.png "traffic map using Folium")

### Methodology

The basic idea that when you have success story for your business or your direct competitor in one of the Toronto neighborhoods you want to replicate in another neighborhood with the same attributes or close enough. Using four different data sources came with it is own challenge of cleaning the data and integrating it then normalizing it. I started with the boundaries of Toronto because it gives us the definition of the neighborhood from Toronto open data [the link](https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#a45bd45a-ede8-730e-1abc-93105b2c439f) and put it in Geodataframe using [geopandas Library](http://geopandas.org/), that allowed to get polygon boundaries of each neighborhood [figure1](#figure1), [figure2](#figure2) To use the explore function foursquare, we need a point inside each neighborhood polygon and to get this point we used [Shapley](https://pypi.org/project/Shapely/) and [jeojason](http://geojson.io/#map=2/20.0/0.0).
### Figure7
![](https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Neigh%20data.png "points assigned to neighborhood ")
### Figure8
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/neigh%20points.png " points using Folium ")
After we assigned the point we are ready to get the data from the foursquare API, the problem we faced was a little bit different because explore function takes longitude, latitude and radius to draw circle and provide all the venues inside that circle, but the neighborhood boundaries takes the shape of the polygon , so the output of venues could provide mixed venues assigned to wrong neighborhood [figure3](#figure3), to solve this problem we filtered and reassigned venues to neighborhood using shapley, and data cleaning so we solve our problem. To add more data we used points of interest data from the open Data portal for [the city of Toronto](https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#7b9deecd-a51a-3485-5e3d-94f27cc8b7d4) as DBf file and we read it using [simpledbf library](https://pypi.org/project/simpledbf) then appended with the venues  DataFrame [figure4](#figure4).
After compiling the venues data from Foursquare and the points of interest from Toronto open data platform to enrich the data, we started processing the data by using one hot encoding to find category existed. also, we grouped the data-set by neighborhood and the mean of the one hot encoding results for each venue category so we can create the new DataFrame and display the top 10 venues types for each neighborhood .
### Figure9
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/processed%20Data.png "processed Data ")
To add the traffic dimension to solve the problem of finding customers we added the traffic data from [the city of Toronto](https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#7c8e7c62-7630-8b0f-43ed-a2dfe24aadc9), the data provided for the number of the people crossing intersections and cars for the 8 peak hours [figure6](#figure6), [figure5](#figure5). 
To render this data on the neighborhood level we assigned each intersection to neighborhood and we summed the traffic for pedestrians and also for vehicle inside each neighborhood, then we normalized the result using [scikit-learn](http://scikit-learn.org/stable/) per-processing attributes so This can guarantee stable convergence of weight and biases. Then we came to the last point by clustering using k-mean so we can find similar neighborhood using the dimensions above .

### Results
After data wrangling and clustering we reconstructed the data to provide us with final Dataframe, so we can visualize it and provide it to the target retails owners to take informed based decision on those neighborhood clusters. the results we can sum it in
### Figure10
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/clustering%20table.png "processed Data ")
### Figure11
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/clustering.png "processed Data ")

### Discussion
As the clusters merged for business owners the neighborhood as unit is a big area so they want to locate new branch arbitrary, they just can’t locate it inside any location in the neighborhood and expect that will achieve the targeted goals their targets. As example to put the retail in a secondary small road this will not achieve the target from using the model . as business owner, they must use their business sense and their industry norms associated with the preferable location inside each neighborhood in high potential cluster results.
As example for quick service restaurant that have drive-thru. they need to have retail location that allow cars to access from different road directions. Another example for a big supermarket where the business norms that the people needs parking space for their cars because they will stay for long to collect their groceries, so the place needed to have parking spots for customer.

### Conclusion
This model provides a tool that will help retail business owners to decide where their next retail expansion neighborhood, without understanding the model and the dimensions used for clustering and without associate he industry practice this could lead to total failure.

 [githup code link]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/Toronto%20clustering%20pedistranian%20clustering.ipynb) 
 kamilAmin

* [Open Data](https://medium.com/tag/open-data?source=post)
* [Clustering](https://medium.com/tag/clustering?source=post)
* [Geospatial](https://medium.com/tag/geospatial?source=post)
* [Python3](https://medium.com/tag/python3?source=post)

### [Kamil Amin](https://medium.com/@kamilamin123)
