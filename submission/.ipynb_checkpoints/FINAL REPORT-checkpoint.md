<div align="center">
    <img src="https://images.unsplash.com/photo-1552288084-454d4fa5caa1?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1954&q=80"  width="80%" />
    <h1>BATTLE OF THE NEIGHBORHOOD</h1>
    <h3>by Kurt Irvin M. Rojas</h3>
</div>

## A. Introduction

### Objective
Japanese cuisine is undoubtly one of most famous cuisine. However, from the perspective of an investor or a chef dreaming of opening his/her own japanese restaurant, it is a remarkable challenge in getting into the market due to the highly saturated supply of japanese food. 

The objective of this project is to find the best neighborhood in Toronto to open a Japanese restaurant. In this project, we'll be trying to create a projection on which place is best to start a japanese restaurant using Foursquare location data and clustering analysis. 

### Target Audience
* Japanese chef's trying to open their own restaurant.
* Investors looking to establish a business related to japanese food. 
* Tourists who are interested in Japanese cuisine. 

### Data Description 

1. **Basic Toronto City data**
- **Source**: https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M
- **Description**: The wikipedia page containts the basic city data of Canada. From here, we can get the specific boroughs and neighborhoods, as well as its corresponding postal codes. 

2. **Geolocation data**
- **Source**: https://cocl.us/Geospatial_data
- **Description**: As the nominatim service is quite slow to use, a dataset is provided which contains the latitude and longitude of Postal codes. In the event that a latitude and longitude entry is not in the dataset, I used **google maps API** to check for the details. 

3. **Venue data**
- **Source**: https://foursquare.com/developers/apps
- **Description**: To explore each vicinity, we need some data about the various businesses local to the place. In this case, we query the foursquare API to see the local businesses. It returns the name, category and geolocation data of the establishments. This data is key in the analysis section where this data is used to create the clusters. 

## B. Methodology





