# Coursera Capstone
Toronto neighborhood classification

The basic idea that when you have success story for your business or your direct competitor in one of the Toronto neighborhoods you want to replicate in another neighborhood with the same attributes or clause enough. First of all we need to have neighborhood geographical  boundaries so we can analyze defined unique neighborhood and to find the data we used Toronto  open data portal and I came across shape file that have the boundaries in polygon with the neighborhood name and neighborhood ID.
To get an idea of the Data this is geo dataframe header ![]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Toronto%20boundries.png "GeoDataFrame")
Also, we can visualize it 
![as]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Screenshot_2018-10-19%20Cognitive%20Class%20-%20Labs%20JupyterLab.png "Folium Map")

To get the venues data with venue category and point of interest we used two sources. The first one we used Foursquare API explore function and to get understanding of the Data collected this is the header
![as]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/venue%20list.png "venue list header")
    
The second source of data was the open Data portal for the city of Toronto This dataset contains information about points of interest for residents and visitors to enjoy including public art, murals, buildings with historic or architectural significance, green spaces, restaurants and more .as example see the header
![as]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/pont%20of%20interest.png "point of interest header")

One of the main Issues for the retail industry is accessibility in term of pedestrians traffic and vehicles traffic in  that area, and the source for that was open Data portal for the city of Toronto This dataset contains the most recent 8 peak hour vehicle and pedestrian volume counts collected at intersections where there are traffic signals.  The data is typically collected between the hours of 7:30 a.m. and 6:00 p.m. as example for the Dataframe header 
![as]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/traffic%20data.png "traffic")
Also, we can visualize it, the orange circles is vehicle traffic and the blue circles is pedestrian traffic
![as]( https://github.com/kamilamin123/Coursera_Capstone/blob/master/images/Traffic%20map.png "traffic map using Folium")
