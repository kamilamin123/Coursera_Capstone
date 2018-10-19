# Coursera Capstone
# Toronto neighborhood classification
## Introduction
this project intended to use geospatial analysis in Toronto city to cluster the neighborhood of Toronto to take decision where to open new branch for retail based on previous success in one of Toronto neighborhood. The main problem for retail is accessibility. Some retails thrive by locating near each other and some retails prefer areas where there is high pedestrian footage or high vehicle traffic density.
Throughout this project we tried to cluster Toronto neighborhood by the category of retails and entrainment facility in the neighborhood combined with the vehicles and pedestrians’ traffic in that neighborhood using ten different clusters. So, the business owners from the area where direct competitors achieve success or in neighborhood where they achieved success before they can choose new places to expand in the city from the same cluster. 
## Data
 First of all we need to have neighborhood geographical boundaries so we can analyze defined unique neighborhood and to find the data we used Toronto[open data portal]( https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#a45bd45a-ede8-730e-1abc-93105b2c439f)and I came across shape file that have the boundaries in polygon with the neighborhood name and neighborhood ID.
To get an idea of the Data this is geo dataframe header
### Figure1
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Toronto%20boundries.png "GeoDataFrame") 
Also, we can visualize it 
### Figure2
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Screenshot_2018-10-19%20Cognitive%20Class%20-%20Labs%20JupyterLab.png "Folium Map")
To get the venues data with venue category and point of interest we used two sources. The first one we used [Foursquare API explore]( https://developer.foursquare.com/) function and to get understanding of the Data collected this is the header
### Figure3
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/venue%20list.png "venue list header")
The second source of data was the open Data portal for[the city of Toronto]( https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#7b9deecd-a51a-3485-5e3d-94f27cc8b7d4) This dataset contains information about points of interest for residents and visitors to enjoy including public art, murals, buildings with historic or architectural significance, green spaces, restaurants and more .as example see the header
### Figure4
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/pont%20of%20interest.png "point of interest header")
One of the main Issues for the retail industry is accessibility in term of pedestrians traffic and vehicles traffic in that area, and the source for that was open Data portal for [the city of Toronto]( https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#7c8e7c62-7630-8b0f-43ed-a2dfe24aadc9) This dataset contains the most recent 8 peak hour vehicle and pedestrian volume counts collected at intersections where there are traffic signals.  The data is typically collected between the hours of 7:30 a.m. and 6:00 p.m. as example for the Dataframe header 
### Figure5
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/traffic%20data.png "traffic")
Also, we can visualize it, the orange circles is vehicle traffic and the blue circles is pedestrian traffic
### Figure6
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Traffic%20map.png "traffic map using Folium")
## Methodology
The basic idea that when you have success story for your business or your direct competitor in one of the Toronto neighborhoods you want to replicate in another neighborhood with the same attributes or close enough. Using four different data sources came with it is own challenge of cleaning the data and integrating it then normalizing it.
I started with the boundaries of Toronto because it gives us the definition of the neighborhood  from Toronto open data [the link]( https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#a45bd45a-ede8-730e-1abc-93105b2c439f) and put it in Geodataframe using [geopandas Library]( http://geopandas.org/)  that allowed to get polygon boundaries of each neighborhood [figure1](#figure1), [figure2](#figure2). To use the explore function foursquare, we need a point inside the neighborhood polygon and to get that points we used [Shapley](https://pypi.org/project/Shapely/)   and [jeojason](http://geojson.io/#map=2/20.0/0.0).
### Figure7
![](https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Neigh%20data.png
"points assigned to neighborhood ")
### Figure8
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/neigh%20points.png
" points using Folium ")
After we assigned the point we are ready to get the data from the foursquare API, the problem we are facing is a little bit different  because explore function takes longitude, latitude and radius to draw circle and provide  all the venues inside that circle but the neighborhood s polygon , so the output of venues  could provide mixed venues assigned to wrong neighborhood[figure3](#figure3), to solve this problem we filtered and reassigned venues to neighborhood using shapley. And sed data cleaning so we solve our problem.
To add more data we used point of interest data from the open Data portal for[the city of Toronto]( https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#7b9deecd-a51a-3485-5e3d-94f27cc8b7d4) as DBf file and we read it using [simpledbf library](https://pypi.org/project/simpledbf) and we appended with the venues DataFrame [figure4](#figure4).
 After compiling the venues data from Foursquare and the point of interest from Toronto open data platform to enrich the data. We started processing the data by using one hot encoding to find  category existed and we grouped by  neighborhood and the mean of the one hot encoding result for the category so we can create  the new DataFrame and display the top 10 venues types  for each neighborhood .
### Figure10
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/processed%20Data.png
"processed Data ")
To add the traffic dimension to the data solve the problem of finding customers we added the traffic data from [the city of Toronto]( https://www.toronto.ca/city-government/data-research-maps/open-data/open-data-catalogue/#7c8e7c62-7630-8b0f-43ed-a2dfe24aadc9) the data provided for the number of the people crossing intersections and cars for the on peak  8 hour [figure6](#figure6), [figure5](#figure5). To render this data on he neighborhood level we assigned each intersection to neighborhood and we summed the traffic for pedestrians and also for vehicle then we normalized the result using [scikit-learn]( http://scikit-learn.org/stable/) preprocessing attributes so This can guarantee stable convergence of weight and biases.
Then we will come to the last point clustering using k-mean clustering so we can find similar neighborhood using the dimensions above . 
## Results
 After data wrangling and clustering we reconstructed the data to provide us with final Data frame, so we can visualize it and provide it to the targeted retails owners to take informed decision based on those neighborhood clusters. the results we can sum it in 
### Figure11
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/clustering%20table.png "processed Data ")
### Figure12
![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/clustering.png
"processed Data ")

## Discussion 
As the clusters merged for business owner the neighborhood is big area when they want to locate new branch for their business they just can’t locate it inside any location in the neighborhood and expect that will achieve their targets. As example to but the retail in secondary small road. They must use their business sense and industry norms with the clustering results. 
As example for quick service restaurant that have drive-thru. they need to have retail location that allow cars access from different roads. Another example for big supermarkets where the business norms that the people needs space to park their cars because they will stay for long to collect their groceries. 
## Conclusion
This model provides a tool that will help retail business owners to decide where their next retail expansion neighborhood, without understanding the model and the dimensions used for clustering and without associate he industry practice this could lead to total failure. 


 [githup code ink]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/Toronto%20clustering%20pedistranian%20clustering.ipynb) 
kamilAmin 
