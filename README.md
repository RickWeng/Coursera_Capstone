# Optimal Chinese Restaurant Location  
[Jupyter notebook]()
## Abstract
* Investors have a promising future in investment of Chinese restaurant at the City of Vancouver
* Location, census data, Foursquare API and machine learning were used to assess the optimal restaurant location
* Victoria-Fraserview can be the optimal location because of its low competition level
* Future study could incorporate more factors such as transportation into the analysis
## Introduction
Vancouver has one of the highest concentrations of Chinese people outside the continent of Asia. Chinese account for nearly 28% of the population (Statistics Canada, 2011), which leads to emerging Chinese restaurants over the past decade. The number of Chinese population in Vancouver is likely to continue to grow at a faster rate than the non-Chinese population (Statistics Canada, 2016). An accelerating rise of Chinese restaurants can be expected. Now is a good time for investors to open a Chinese restaurant, the real problem is what is the optimal location?  
Location is important for the success of restaurant because it affects the cost and competition. Locations with high density of population but low density of restaurants in the vicinity are likely to attract more customers. Most restaurant location selection analyses in Vancouver cover rent cost, yet very few address or seriously recognize competition. To address these knowledge gaps, I conducted an assessment of Chinese population and restaurant distribution across the City of Vancouver. Local areas were then segmented and clustered accordingly. I assumed major customers of Chinese restaurants were Chinese. I posed three questions:  
* How was Chinese population distributed in the City of Vancouver?
* How were Chinese restaurants distributed in the City of Vancouver?
* Which local area in the City of Vancouver should the investor open a Chinese restaurant?  

This study was aimed at providing location insights for investors interested in opening a Chinese restaurant in the City of Vancouver. 
## Data
### Local Area Boundary 
Local Area Boundary (City of Vancouver, 2019) contains the polygons for the city’s 22 local areas (also known as local planning areas). These boundaries generally follow street centerlines.  
### 2016 Census of Population
The 2016 Census (Statistics Canada, 2016) provides statistical information about the population. Visible minority for the population in private households was used to assess the number of Chinese population in each of the city's 22 Local Areas. Visible minorities refer to persons, other than Aboriginal peoples, who are non-Caucasian in race or non-white in color. The visible minority population consists many groups such as Chinese, Black, Latin American and Arab.
### Foursquare API  
Foursquare builds a massive dataset of location data. Using Foursquare API and centroid coordinates, I can acquire spatial and detailed information (e.g. venue category) of venues in each local area (Foursquare, 2019). Chinese restaurants including dim sum restaurants, Shanghai restaurants, Taiwan restaurants, etc. can be extracted. Foursquare API also allows me to get rating (0-10) for each restaurant, which is helpful to evaluate quality of restaurants in each local area.
## Methodology
### Exploratory Data Analysis
Centroid as the arithmetic mean position of the polygon was derived from Local Area Boundary data for searching nearby Chinese restaurants (Fig. 1). To get the density of Chinese population, shape area of each local area was calculated. The density of Chinese population in each local area were calculated using the equation: density = number / shape area. To get the number of Chinese restaurants in each local area, I searched Chinese restaurants (id: 4bf58dd8d48988d145941735) specifically. Radius was set to 1500 m to cover most area of each local area. The density of Chinese restaurants in each local area can then be calculated using the equation: density = number / (pi * radius^2).  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/local-area-boundary.png)
Figure 1. Centroids and boundary of each local area.  
After checking venue's unique category, I found one venue called "Bamboo Village" misclassified into the Chinese restaurant category. I deleted it from our analysis because it is an arts and crafts store. In total, 531 Chinese restaurants were found within 1500 m distance from the centroid of each local area (Fig. 2). Ratings were missing in West Point Grey due to lack of Chinese restaurants. Nearly 64% of Chinese restaurants do not have a rating (Fig. 3). Ratings are unavailable for all Chinese restaurants in Grandview-Woodland and Dunbar-Southlands local area. The distribution of available ratings varies across each local area (Fig. 4). Considering that missing values accounted for a large portion of data, ratings were not included in the cluster analysis and were only used to help me understand each local area in the study.  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/cr-dist.png)
Figure 2. Chinese restaurants within 1500 m from the centroid of each local area.  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/cr-na-dist.png)
Figure 3. Ratings of Chinese restaurants.  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/rating-hist.png)
Figure 4. Distribution of available ratings for each local area.
### Cluster Analysis
DBSCAN is a popular unsupervised clustering algorithm that is commonly used in machine learning (Ester et al., 1996). DBSCAN groups similar points that are close to each other based on a radius and a minimum number of points. Unlike K-means, DBSCAN can identify clusters of arbitrary shape and find outliers without specifying the number of clusters before the clustering process. In the study, Min-Max Normalization which gives the same importance to all variables was applied to data. DBSCAN was then used to segment and cluster local areas. To group local areas precisely and have an appropriate number of clusters, 0.2 radius was used and the minimum number of points was set to 2.  
Local area in a cluster with high density of Chinese population and low density of Chinese restaurants, indicating a lower level of competition, was considered as an optimal location to open a Chinese restaurant.  
## Results
### Distribution of Chinese Population
Chinese population was concentrated near the East side of the City of Vancouver (Fig. 5). Victoria-Fraserview was the local area with the highest density of Chinese population (2856 per km^2), followed by Renfrew-Collingwood (2638 per km^2) and Kensington-Cedar Cottage (2145 per km^2) (Fig. 6).  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/cp-dist.png)
Figure 5. Distribution of Chinese population.  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/density-cp.png)
Figure 6. Density of Chinese population (#/km^2) in each local area.  
### Distribution of Chinese Restaurants
North-central part of the City of Vancouver was the hotspot of Chinese restaurants (Fig. 7). West End (7.1 per km^2), Downtown (7.1 per km^2), and Fairview (6.9 per km^2) were the top 3 local areas with the highest density of Chinese restaurants (Fig. 8).  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/cr-heatmap.png)
Figure 7. Distribution of Chinese restaurants.
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/density-cr.png)
Figure 8. Density of Chinese restaurants (#/km^2) in each local area.
### Optimal Chinese Restaurant Location
DBSCAN clustering identified 4 clusters and 2 outliers (Renfrew-Collingwood and Victoria-Fraserview) (Fig. 9). The two outliers were assigned to cluster -1. Renfrew-Collingwood had both very high density of Chinese population and restaurants. Very high density of Chinese population and low density of Chinese restaurant in Victoria-Fraserview made it a distinct local area from other clusters.  
By contrast, Fairview and West End grouped together because of their very high density of Chinese restaurants and low density of Chinese population. Marpole, Arbutus-Ridge, Hastings-Sunrise, Killarney, and Oakridge formed a cluster with relatively high density of Chinese restaurants but relatively low density of Chinese restaurants.  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/dbscan-scatter.png)
Figure 9. Clusters of normalized Chinese population and restaurants.  
In terms of available ratings, Victoria-Fraserview ranked first in the median value and second in the mean value (Fig. 10).  
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/cluster-boxplot.png)
Figure 10. Ratings of Chinese restaurants in each local area. Plus signs represent mean values; center lines represent median values.  
## Discussion
![](https://github.com/RickWeng/optimal-restaurant-location/blob/master/figures/optimal-location.png)
Figure 11. Optimal Chinese restaurant location.  
Based on the density of Chinese population and restaurants, I recommended Victoria-Fraserview to be an optimal location for investors to open a Chinese Restaurant in the City of Vancouver (Fig. 11). However, the high quality of food and service is needed for the restaurant to stand out from all the rest since nearby Chinese restaurants generally have a high rating. Other than Victoria-Fraserview, Oakridge might be another good choice.  
It should be noted that the study focused on density of population and restaurants, ignoring the rent cost. This focus gave me more space to evaluate the competition in each local area. The approach and analysis was conducted for the City of Vancouver case but can have broader applicability. Although it was beyond the scope of this study, many other factors including transportation (cost and convenience), rent cost and size of parking space can affect the location selection (Tzeng et al., 2002). Residential census data used in the study was criticized for imposing a bias upon the estimation of pedestrian volume. Future study should incorporate these factors into the analysis.  
## Conclusion
Vancouver is one of the best places in North America to open a Chinese restaurant. Using location, census data, Foursquare API and DBSCAN clustering algorithm, I assessed the competition level of each local area. High density of Chinese population and low density of Chinese restaurants makes Victoria-Fraserview an optimal location to start the business. I recommended investors to select Victoria-Fraserview local area as their restaurant location because of the low competition level. Future study should incorporate other factors such as rent cost, transportation, size of parking space and pedestrian volume into the location selection analysis.  
## References
City of Vancouver. (2019). *Local area boundary*. Retrieved from https://data.vancouver.ca/datacatalogue/localareaboundary.htm  
Ester, M., Kriegel, H. P., Sander, J., & Xu, X. (1996, August). A density-based algorithm for discovering clusters in large spatial databases with noise. In *Kdd* (Vol. 96, No. 34, pp. 226-231).  
Foursquare. (2019). *Places API*. Retrieved from https://developer.foursquare.com/places-api  
Statistics Canada. (2011). *2011 Census*. Retrieved from https://www12.statcan.gc.ca/census-recensement/2011/dp-pd/prof/index.cfm?Lang=E  
Statistics Canada. (2016). *2016 Census*. Retrieved from https://www12.statcan.gc.ca/census-recensement/2016/dp-pd/prof/index.cfm?Lang=E  
Tzeng, G. H., Teng, M. H., Chen, J. J., & Opricovic, S. (2002). Multicriteria selection for a restaurant location in Taipei. *International journal of hospitality management*, 21(2), 171-187.  

