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

I began by creating lists for the coordinates and cities, then created a set of random latitudes and longitudes. Using the citypy library, I linked these random coordinates to the closest city. This produced a list of 606 cities. Once that was set, it was time to link in the weather API. I used a for loop to perform an API call for each of the randomly selected cities in my list, with an exception for any fields that  were missing data.

The raw data was converted into a data frame and the rows missing data were removed. I exported this cleaned up data to a CSV and was ready to perform my analysis. I started by checking for any cities that reported having a humidity greater than 100%, as those would be inaccurate and skew my results. Luckily, this search returned zero results. 

![image](https://user-images.githubusercontent.com/81889411/155856539-0d593ce9-307d-440c-ae42-a906f64e5d16.png)

The first plot was comparing city latitude vs temperature.

![image](https://user-images.githubusercontent.com/81889411/155856554-70242951-8b84-4db5-beed-dc58592b95ce.png)

As you would expect, the cities closer to the equator have higher temperatures. It is interesting that those closer to the North Pole have lower temperatures than those closer to the South Pole. That could be due to fewer cities selected in the Southern Hemisphere, though.

Next was city latitude vs humidity.

![image](https://user-images.githubusercontent.com/81889411/155856562-e3abf117-3a6d-466a-9fce-b283ad3172d3.png)

There doesn't seem to be much correlation between humidity and latitude. This isn't too surprising as there are rain-heavy/very-humid regions all over the globe, just like there are deserts scattered around. 

Then I looked at city latitude vs cloudiness.

![image](https://user-images.githubusercontent.com/81889411/155856569-f96ead23-b2c3-49c0-9951-c291ac9cc250.png)

Much like humidity, there isn't much correlation between cloudiness and latitude. I am curious about the straight lines of points that appeared. My guess would be something in how the cloudiness is calculated that results in the multiple cities having the same exact measurement.

Finally, I plotted city latitude vs wind speed.

![image](https://user-images.githubusercontent.com/81889411/155856577-e356a048-53fe-4878-a6d8-ea4f0d00ea0f.png)

Not much correlation between the two factors here, either, though it does show that most of the cities selected tend to not have very high wind-speeds.

The next step of the process was to apply linear regression to the data. This was split between the northern and southern hemispheres so that like was with like.

First, I looked at the maximum temperature vs latitude.

![image](https://user-images.githubusercontent.com/81889411/155857252-1943fe0a-5aeb-4ca1-91f8-9bc010fce3de.png)
![image](https://user-images.githubusercontent.com/81889411/155857262-2efd220e-6d57-41cc-9328-5b86f8065bd8.png)

The regression here is showing a high correlation between latitude and temperature, namely that the closer to the equator that you get, the higher the temperature. The correlation is, oddly, stronger in the northern hemisphere than the southern (0.73 vs 0.6 r-value).

Then I checked the regression for humidity vs latitude.

![image](https://user-images.githubusercontent.com/81889411/155857272-c4191413-953f-4506-8e4a-e96d212bb1b8.png)
![image](https://user-images.githubusercontent.com/81889411/155857276-84b465ec-88e2-474f-a7da-df1a0f86d5ee.png)

The regression model for humidity shows that there is essentially no correlation between humidity and latitude. 

Cloudiness vs latitude was next.

![image](https://user-images.githubusercontent.com/81889411/155857385-039d78a8-0056-44f7-9a31-a87f400f07d9.png)
![image](https://user-images.githubusercontent.com/81889411/155857388-d6d28e90-ac8c-4f6b-bb99-af7dcf30ccea.png)

There is minimal correlation between latitude and cloudiness. 

And finally, I looked at wind speed vs latitude.

![image](https://user-images.githubusercontent.com/81889411/155857397-b8727211-bbd2-4f92-9f04-9f11ed6793f7.png)
![image](https://user-images.githubusercontent.com/81889411/155857401-ee97494a-59f0-4c2b-bf47-ed355842f398.png)

The correlation between wind speed and latitude is very similar for both the northern and southern hemispheres. Unfortunately, there is still no strong correlation between these two factors.
