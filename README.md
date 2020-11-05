# 0. Usage:
Code to extract GHCN Daily Weather data using geographical co-ordinates. This code was used to generate a dataset with weather data of 10000+ cities across the world. The dataset is available at: https://www.kaggle.com/abhijitk/ghcn-daily-weather-data-by-city-20152020

**World Cities Nearest Stations.csv**: This file contains City names, geographical coordinates, Population, **ID of closest weather station and distance to closest weather station**. First, retrieve the city's 'Closest Station ID' from this file. Then use this ID to retrieve weather data from the Weather files in the dataset.
```python
import pandas as pd

world_cities = pd.read_csv("World Cities Nearest Stations.csv")
w_2018 = pd.read_csv("Weather all cities 2018.csv")
w_2016 = pd.read_csv("Weather all cities 2016.csv")

paris_station = list(world_cities["Closest Station ID"][(world_cities["city"]=="Paris")&(world_cities["country"]=="France")])

w_par2018 = w_2018[w_2018["ID"]==paris_station[0]] 
w_par2018[["Date","TAVG"]].head() #Daily average temperature in Paris during 2018
```
          Date	 TAVG
808 	20180101	80.0
6156	20180102	84.0
11547	20180103	101.0
16981	20180104	116.0
22419	20180105	88.0

```
w_par2016 = w_2016[w_2016["ID"]==paris_station[0]]
w_par2016[["Date","PRCP"]].head() #Daily Precipitaion in paris during 2016
```
          Date	PRCP
846	20160101	0.0
6163	20160102	15.0
11491	20160103	15.0
16852	20160104	84.0
22302	20160105	0.0

# 1. Introduction
Code to extract GHCN Daily Weather data using geographical co-ordinates. This code was used to generate a dataset with weather data of 10000+ cities across the world. The dataset is available at: https://www.kaggle.com/abhijitk/ghcn-daily-weather-data-by-city-20152020

In a nutshell, it uses a city's coordinates to identify the nearest weather station and then extracts the historical daily weather data of this station. A dataset on weather patterns is generated by using the following open/public datasets:

i)**Global Historical Climatology Network (GHCN) (https://www.ncdc.noaa.gov/ghcn-daily-description):**
"GHCN (Global Historical Climatology Network)-Daily is an integrated database of daily climate summaries from land surface stations across the globe. Like its monthly counterpart (GHCN-Monthly) , GHCN-Daily is comprised of daily climate records from numerous sources that have been integrated and subjected to a common suite of quality assurance reviews.GHCN-Daily contains records from over 100,000 stations in 180 countries and territories. NCEI provides numerous daily variables, including maximum and minimum temperature, total daily precipitation, snowfall, and snow depth; however, about one half of the stations report precipitation only. Both the record length and period of record vary by station and cover intervals ranging from less than a year to more than 175 years.

ii) **World Cities Database (https://simplemaps.com/data/world-cities):** A database of 26000 cities containing city names, geographical co-ordinates, population, density and country names. The database is available under Creative Commons Attribution 4.0 license.

# 2. Method

I) Obtain files from NOAA and Simplemaps

II) Use the co-ordinates of each City and weather station to find the weather station closest to each city

III) Extract the data for these weather stations and shape it in a human readable format.

IV) Kaggle notebook: https://www.kaggle.com/abhijitk/extracting-weather-data-from-city-coordinates

# 3. Advantages:
The dataset generated and the code in this notebook has applications beyond the current competition.

i) Ease of Access: The dataset makes climate data on thousands of cities instantly accessible through year-wise CSV files. Additionally , a 'key file' which links each city to the nearest weather station makes it easy to retrieve weather data with only the city and country name. It is presented in a human readable format. It can be easily manipulated using Python, R or even Microsoft Excel/ Google Sheets.

ii) Scope and Usage The dataset covers thousands of cities. Hence, its potential uses extend to individuals and organizations engaged in sustainability, climate change, metereology etc. Although the notebook generates data for only the last 5 years, the code can be easily modified further to obtain data for any other years from the NOAA database or to obtain data for any other cities.

iii) Size NOAA GHCN annual files sizes range from 1-2 GB. The extracted dataset files sizes are in the range of 150-200 MB i.e. almost 10-20% of the original files

# 4. Limitations:
Weather data on certain cities is missing or inaccurate because of the following reasons:

i) Some of the weather stations identified in the notebook are not polled by the NOAA in recent years. Hence, weather data on certain cities is missing.

ii) In a few cases, the identified weather stations are very far from the respective cities.

