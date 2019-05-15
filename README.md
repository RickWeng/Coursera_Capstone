# Optimal Chinese Restaurant Location
## Requirements
A description of the problem and a discussion of the background.    
A description of the data and how it will be used to solve the problem.    

A link to your Notebook on your Github repository, showing your code.   
A full report consisting of all of the following components:    
Introduction where you discuss the business problem and who would be interested in this project.    
Data where you describe the data that will be used to solve the problem and the source of the data.   
Methodology section which represents the main component of the report where you discuss and describe any exploratory data analysis that you did, any inferential statistical testing that you performed, and what machine learnings were used and why.    
Results section where you discuss the results.    
Discussion section where you discuss any observations you noted and any recommendations you can make based on the results.    
Conclusion section where you conclude the report.   
## Abstract

## Introduction
Vancouver has one of the highest concentrations of Chinese people outside the continent of Asia. Chinese account for nearly 28% of the population (Statistics Canada, 2011), which leads to emerging Chinese restaurants over the past decade. The number of Chinese population in Vancouver is likely to continue to grow at a faster rate than the non-Chinese population (Statistics Canada, 2016). An accelerating rise of Chinese restaurants can be expected. Now is a good time for investors to open a Chinese restaurant, the real problem is what is the optimal location?  
Location is important for the success of restaurant because it affects the cost and competition. Locations with high density of population but low density of restaurants in the vicinity are likely to attract more customers. Most restaurant location selection analyses in Vancouver cover rent cost, yet very few address or seriously recognize competition. To address these knowledge gaps, I conduct an assessment of Chinese population and restaurant distribution across the City of Vancouver. Local areas are then segmented and clustered accordingly. I assume major customers of Chinese restaurants are Chinese. I pose three questions:
1. How is Chinese population distributed in the City of Vancouver?
2. How are Chinese restaurants distributed in the City of Vancouver?
3. Which local area in the City of Vancouver should the investor open a Chinese restaurant? 
This study is aimed at providing location insights for investors interested in opening a Chinese restaurant in the City of Vancouver.   
 
## Data
**Local Area Boundary**  
Local Area Boundary (City of Vancouver, 2019) contains the polygons for the city’s 22 local areas (also known as local planning areas). These boundaries generally follow street centerlines.   
**2016 Census of Population**  
The 2016 Census (Statistics Canada, 2016) provides statistical information about the population. Visible minority for the population in private households was used to assess the number of Chinese population in each of the city's 22 Local Areas. Visible minorities refer to persons, other than Aboriginal peoples, who are non-Caucasian in race or non-white in color. The visible minority population consists many groups such as Chinese, Black, Latin American and Arab.  
**Foursquare API**  
Foursquare builds a massive dataset of location data. Using Foursquare API and centroid coordinates, I can acquire spatial and detailed information (e.g. venue category) of venues in each local area (Foursquare, 2019). Chinese restaurants including dim sum restaurants, Shanghai restaurants, Taiwan restaurants, etc. can be extracted. Foursquare API also allows me to get rating (0-10) for each restaurant, which is helpful to evaulate quality of restaurants in each local area.    
## Methodology
### Exploratory Data Analysis
Centroid as the arithmetic mean position of the polygon were derived from Local Area Boundary data for searching nearby Chinese restaurants. To get the density of Chinese population, shape area of each local area was calculated. The density of Chinese population in each local area were calculated. Radius was set to 1500 m to cover most area of each local area. To get the number of Chinese restaurants in each local area, I searched Chinese restaurants (id: 4bf58dd8d48988d145941735) specifically. The density of Chinese restaurants in each local area can then be calculated using the equation denisty = number / (pai * radius^2).
Chinese restaurants map (neighborhood change to local area in legend)  
Histogram of rating (add density curve and border)  

There are There is no Chinese restaurants can be found within 1500 m distance from the centroid of West Point Grey . Missing rating in West Point Grey is thus bec restaurants while 
3... of 7... restaurants do not have a rating so ratings were not included in the cluster analysis. Ratings were only used to help me understand each local area. 
### Cluster Analysis
DBSCAN is a popular unsupervised clustering algorithm that is commonly used in machine learning (Ester et al., 1996). DBSCAN groups similar points that are close to each other based on a radius and a minimum number of points. Unlike K-means, DBSCAN can identify clusters of arbitrary shape and find outliers without specifying the number of clusters before the clustering process. In the study, Min-Max Normalization which gives the same importance to all variables was applied to data. DBSCAN was then used to segment and cluster local areas. To group local areas precisely and have an appropriate number of clusters, 0.2 radius was used and the minimum number of points was set to 2.

## Results
### Distribution of Chinese Population

### Distribution of Chinese Restaurants

### Optimal Chinese Restaurant Location
Other than Victoria-Fraserview, ... are also good choices
## Discussion
focus on competition, rent cost, pedestrian volume, distance, Richmond
## Conclusion


