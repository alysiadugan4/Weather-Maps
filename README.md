# What's the Weather Like?

## Background

"What's the weather like as we approach the equator?"

Now, we know what you may be thinking: *"Duh. It gets hotter..."*

But, if pressed, how would you **prove** it?



### Part I - WeatherPy

Create a Python script to visualize the weather of 500+ cities across the world of varying distance from the equator. To accomplish this, you'll be utilizing a [simple Python library](https://pypi.python.org/pypi/citipy), the [OpenWeatherMap API](https://openweathermap.org/api), and a little common sense to create a representative model of weather across world cities.

Your first requirement is to create a series of scatter plots to showcase the following relationships:

- Temperature (F) vs. Latitude
- Humidity (%) vs. Latitude
- Cloudiness (%) vs. Latitude
- Wind Speed (mph) vs. Latitude

Your second requirement is to run linear regression on each relationship, only this time separating them into Northern Hemisphere (greater than or equal to 0 degrees latitude) and Southern Hemisphere (less than 0 degrees latitude):

- Northern Hemisphere - Temperature (F) vs. Latitude
- Southern Hemisphere - Temperature (F) vs. Latitude
- Northern Hemisphere - Humidity (%) vs. Latitude
- Southern Hemisphere - Humidity (%) vs. Latitude
- Northern Hemisphere - Cloudiness (%) vs. Latitude
- Southern Hemisphere - Cloudiness (%) vs. Latitude
- Northern Hemisphere - Wind Speed (mph) vs. Latitude
- Southern Hemisphere - Wind Speed (mph) vs. Latitude

### Part II - VacationPy

Now let's use this weather data to plan future vacations. 

- Create a heat map that displays the humidity for every city from WeatherPy.
- Narrow down the DataFrame to find your ideal weather condition. 
- Use Google Places API to find the first hotel for each city located within 5000 meters of your coordinates.
- Plot the hotels on top of the humidity heatmap with each pin containing the **Hotel Name**, **City**, and **Country**.

## Summary

This project was all about use APIs to access useful information and apply various analytical techniques to gain insight into weather conditions around the world. 

I began by creating lists for the coordinates and cities, then created a set of random latitudes and longitudes. Using the citypy library, I linked these random coordinates to the closest city. Once that was set, it was time to link in the weather API. I used a for loop to perform an API call for each of the randomly selected cities in my list, with an exception for any fields that  were missing data.


The raw data was converted into a data frame and the rows missing data were removed. I exported this cleaned up data to a CSV and was ready to perform my analysis. I started by checking for any cities that reported having a humidity greater than 100%, as those would be inaccurate and skew my results. Luckily, this search returned zero results. 

The first plot was comparing city latitude vs temperature.


As you would expect, the cities closer to the equator have higher temperatures. It is interesting that those closer to the North Pole have lower temperatures than those closer to the South Pole. That could be due to fewer cities selected in the Southern Hemisphere, though.

Next was city latitude vs humidity.


There doesn't seem to be much correlation between humidity and latitude. This isn't too surprising as there are rain-heavy/very-humid regions all over the globe, just like there are deserts scattered around. 

Then I looked at city latitude vs cloudiness.


Much like humidity, there isn't much correlation between cloudiness and latitude. I am curious about the straight lines of points that appeared. My guess would be something in how the cloudiness is calculated that results in the multiple cities having the same exact measurement.

Finally, I plotted city latitude vs wind speed.


Not much correlation between the two factors here, either, though it does show that most of the cities selected tend to not have very high wind-speeds.

The next step of the process was to apply linear regression to the data. This was split between the northern and southern hemispheres so that like was with like.

First, I looked at the maximum temperature vs latitude.


The regression here is showing a high correlation between latitude and temperature, namely that the closer to the equator that you get, the higher the temperature. The correlation is, oddly, stronger in the northern hemisphere than the southern (0.73 vs 0.6 r-value).

Then I checked the regression for humidity vs latitude.


The regression model for humidity shows that there is essentially no correlation between humidity and latitude. 

Cloudiness vs latitude was next.


There is minimal correlation between latitude and cloudiness. 

And finally, I looked at wind speed vs latitude.


The correlation between wind speed and latitude is very similar for both the northern and southern hemispheres. Unfortunately, there is still no strong correlation between these two factors.


For the next step, I saved my results from part one into a csv and used the resulting data frame as the basis for my analysis. 

To create my humidity heatmap, I configured my gmaps and set the latitude/longitude as the location and the humidity as the weight. 


Next, I decided to narrow down the cities in my list based on my ideal weather conditions. I decided to filter for cities with temperatures between 70 and 80 degrees Farenheit and humidity below 30%. With this refined list, I created a for loop to call the Google Places API for hotels within 5000 meters of the coordinates. Unfortunately, there did not appear to be any hotels in the API for the cities on my list. Had there been, though, I set up a layer on the heatmap to plot their locations. It is likely that, with a different random selection of cities, I would have had results.




