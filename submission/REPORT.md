<div align="center">
    <img src="https://images.unsplash.com/photo-1552288084-454d4fa5caa1?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1954&q=80"  width="80%" />
    <h1>BATTLE OF THE NEIGHBORHOOD</h1>
    <h3>by Kurt Irvin M. Rojas</h3>
</div>

### **Objective**
Japanese cuisine is undoubtly one of most famous cuisine. However, from the perspective of an investor or a chef dreaming of opening his/her own japanese restaurant, it is a remarkable challenge in getting into the market due to the highly saturated supply of japanese food. 

The objective of this project is to find the best neighborhood in Toronto to open a Japanese restaurant. In this project, we'll be trying to create a projection on which place is best to start a japanese restaurant using Foursquare location data and clustering analysis. 

### **Target Audiance**
* Japanese chef's trying to open their own restaurant.
* Investors looking to establish a business related to japanese food. 
* Tourists who are interested in Japanese cuisine. 

### **Data Description**
For this project we need these following data:



- **Basic Toronto City data** [link](https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M) - Contains the data basic city data such as the boroughs and neighborhoods.

- **Geolocation data** 
    - Postal Address [link](https://cocl.us/Geospatial_data) - Postal address of each Borough in the Toronto City data.
    - Geographical location via Google maps API - Postal code for Toronto thats not in the City data.   

- **Venue data** via [Foursquare](https://foursquare.com/developers/apps) - Venue data to be used in exploring each region/place.

### **Methodology**
In this section, we prepare the dataframe to be use for the modelling. The summary of the flow is:

1. Webscrape the data from city info webpage
2. Get and connect the Postal Codes to the neighborhoods
3. Check the business venues in the vicinity of the neighborhood using Foursquare 
4. Use K-means clustering to group the neighborhoods
5. Create an analysis of the data


