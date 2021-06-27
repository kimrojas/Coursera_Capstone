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

### Source Code

The source code is presetend in notebook form as hosted in github [link](https://github.com/kimrojas/Coursera_Capstone/blob/main/week_4_capstone.ipynb)

---

## B. Methodology

In this section, we prepare the dataframe to be use for the modelling. The summary of the flow is:

1. Webscrape the data from city info webpage
2. Get and connect the Postal Codes to the neighborhoods
3. Check the business venues in the vicinity of the neighborhood using Foursquare 
4. Use K-means clustering to group the neighborhoods
5. Create an analysis of the data


### Python libraries

```python
# For webscraping 
from bs4 import BeautifulSoup as bs
import requests
import json # library to handle JSON files
from pandas.io.json import json_normalize # tranform JSON file into a pandas dataframe

# For Data manipulation
import pandas as pd
import numpy as np

import folium # For map
import keys # For identity keys, separate for security reasons
import googlemaps # For lon lat request inplace of nominatim
from sklearn.cluster import KMeans # For clustering

# For graph and folium colors
import matplotlib.pyplot  as plt
import matplotlib.cm as cm
import matplotlib.colors as colors

from tqdm import tqdm
import seaborn as sns
```




---

## C. Results

### Webscraping

In this section we used the Beautifulsoup package to parse the webpage. 
We can do that using the following code:
```python
# Get the neighborhood data using beautiful soup 
url='https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M'
result = requests.get(url)
data_html = bs(result.content)
soup = bs(str(data_html)) # read the data into a Pandas Dataframe
```

After some corrections and basic cleanup on some data entries, the city dataset should look like this. 

<div align="center">
<img src="images/webscape.JPG" align="center">
</div>

### Geolocation of Postal codes

Next we take the postal codes of each borough and neighborhood using the dataset given. 

```python
# get the latitude and the longitude coordinates of each Postal code
geo_url = "https://cocl.us/Geospatial_data" # rather than nominatim (which is so slow), we use this data set of postal codes instead.

geo_df = pd.read_csv(geo_url)
geo_df.rename(columns={'Postal Code': 'PostalCode'}, inplace=True) # shorten name
geo_df.head()
```
<div align="center">
<img src="images/postalcode.JPG" align="center">
</div>

### City data
Finally, combine both city and geolocation data and apply a filter to only include the Toronto area
```Python
df = pd.merge(df, geo_df, on='PostalCode')
toronto_data = df[df['Borough'].str.contains("Toronto")].reset_index()
```

<div align="center">
<img src="images/citydata.PNG" align="center">
</div>

### Mapping out the city

<div align="center">
<img src="images/initialcity.PNG" align="center">
</div>

### Venue exploration

Using the Foursquare API, we can query the 100 nearby location per venue. With this API, we can get what businesses are in the locality. 

On our queary, we actually get at least 1505 businesses with at least 216 unique categories.  

Here is an example of the data we've retrieved. 

<div align="center">
<img src="images/foursquare.PNG" align="center">
</div>

Of course, we also implemented a onehot encoding transformation for the venue data such that we get the frequency as the data itself. However, for the sake of clarity in this report, it will not be shown as it is not that crucial for the analysis.

---

## D. Analysis

### Defining the feature

We are most interested in the frequency of Japanese restaurants, hence, this will be our main feature for the clustering. 

```python
jap = toronto_grouped[["Neighborhood","Japanese Restaurant"]]
jap.head()
```

<div align="center">
<img src="images/limitjap.PNG" align="center">
</div>

### Optimal K value

Since a K-means clustering method is highly reliant on the number of clusters, it is important to examine how many clusters are needed for our study. We can do this using the **Elbow method**. This is basically testing out various K values and seeing where the inflection point is. 


<div align="center">
<img src="images/elbow.PNG" align="center">
</div>

Our results show that the optimal K value is 4. Hence, K=4 will be used to divide our dataset. 

### Applying the K-mean clustering

With K=4, we applied the K-means clustering method to divide and label the locations. 

The raw data looks like this: 

<div align="center">
<img src="images/label.PNG" align="center">
</div>

Additionally, we can visualize the neighborhoods' location with respect to its cluster division. Note that the same colors signifies the same division. 

<div align="center">
<img src="images/clustermap.PNG" align="center">
</div>

### Data analysis

By summarizing the data, we can get the following graphs

<div align="center">
<img src="images/plot.PNG" align="center">
</div>

It apears that Cluster 1 actually has a most number of neighborhood, however, it also has the lowest average number of japanese restaurants. 

Alternatively, an opposite remark may be said to the Cluster 4 where it has the lowest number of neighborhood while having the highest average number of japanese restaurants. 

---

## E. Conclusion

From the perspective of a tourist, it may be best to go to the neighborhoods in cluster 4. There are a lot of Japanese restaurants that will cater to the adventurous pallete. 

From the perspective of a businessman, the optimal location is in cluster 1, where there are a lot of potential demands for a japanese restaurant while having the least competition around the vicinity. Of course it might be possible that these neighborhoods are less commercialize as compared to cluster 4. 




