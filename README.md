# Analysis for NYC taxi data 
Analyze September 2015 green taxi data and come up with recommendations for the taxi companies 
data source: http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml

Credit to: Zhenyu Li, Katie Wu, Franco Lombardi

Task 1:

The file contains 21 columns and 1,494,926 rows. The 21 different attributes are:
VendorID, lpep_pickup_datetime, Lpep_dropoff_datetime, Store_and_fwd_flag, RateCodeID, Pickup_longitude, Pickup_latitude, Dropoff_longitude, Dropoff_latitude, Passenger_count, Trip_distance, Fare_amount, Extra, MTA_tax, Tip_amount, Tolls_amount, Ehail_fee, improvement_surcharge, Total_amount, Payment_type, and Trip_type.

Task 2:

The distances of the trips were recorded by mile. A histogram was plotted to illustrate the most popular distance amongst the trips. Below is the histogram produced:

![screen shot 2017-10-10 at 11 16 20 pm](https://user-images.githubusercontent.com/31937095/31420788-a3b255ce-ae11-11e7-9402-d7b25ade33c6.png)

We can see the most common distances are from 0-2 miles. This means that the majority of trips are shorter trips rather than longer trips. The graph excludes distances greater than 25 miles for clarity; they are considered outliers.

Task 3: 
The mean distances grouped by hour are shown in the histogram below. 
It is obvious that the longest trips occur between 5:00 am - 7:00 am. Longer trips also occur later during the day as well, 10:00 pm - 12:00 am.
Below is the list of hours in 24 hour time with their respective average distances:

![2](https://user-images.githubusercontent.com/31937095/31420846-f4eac4f8-ae11-11e7-96cb-8e1420ac98a4.png)


Task 4:

During this task, we studied the trips that terminate at an airport. For this task, we specifically looked at Laguardia and JFK. To determine what constitutes a trip that terminates at an airport, Google maps was utilized to determine an approximate range for latitude and longitude for each respective airport. Laguardia is located at  40.7769° N, 73.8740° W. An appropriate range was determined to be 40.769° N  - 40.78° N, 73.856° W - 73.88° W. JFK is located at 40.6413° N, 73.7781° W. An appropriate range was determined to be 40.63° N - 40.66° N, 73.75° W - 73.82° W.

The trips were filtered to leave only the trips that terminate within one of these ranges. It was determined that there are 31,117  trips to an airport (Laguardia or JFK). The average fare to either Laguardia or JFK is $29.55. Another interesting fact (which makes sense given the fact that an airport is the end destination) is that the average distance for these trips is 9.397 miles.
This is compared to the average distance for all trips of 2.968 miles. In regards to the number of passengers, 91.66% of to the airport trips have 1  or 2 passengers. Therefore, we see that these trips tend to have fewer passengers. The average tips for trips to the airport is 70%  more than the tips for non-airport trips.

Task 5:   

In this task, we created clusters on pickup and dropoff locations respectively. We first cleaned the locations’ latitude and longitude since there are some invalid data such as 0. Then we created a list of numbers of k from 2 to 20 and tried the KMeans.train function for each k. To find the optimal k, we graphed the WSSEE for pickups: 

![51](https://user-images.githubusercontent.com/31937095/31420893-39d5db7a-ae12-11e7-88a0-9f6f2fcf8d93.png)

The key is to choose a number so that adding another cluster does not give much better modeling of the data, so in this case we chose k = 11. In order to get the centers of all clusters, we ran KMeans.train with k = 11 and maxIterations = 10. Below shows the pickup clusters’ centers: 

![52](https://user-images.githubusercontent.com/31937095/31420909-4ab41f38-ae12-11e7-82fe-d0df19aeca01.png)


We then repeated the same procedure for dropoffs. As shown below, the optimal k is 10. 
 
To have a better visualization for all the clusters, we used gmplot module to display the centroid information on a map. We can see that the pickup and dropoff centroids are very closely related. 
*Dark purple - pickups, pink - dropoffs

![53](https://user-images.githubusercontent.com/31937095/31420916-53677aee-ae12-11e7-98d6-aadf0e980b15.png)


Task 6: 

We repeated the procedure (clean the data and then plot the error on a group for k from 2 to 21)in task 5 to create clusters for both pickup and dropoff locations together. We chose 12 for optimal trade-off between complexity and error as shown below:

![61](https://user-images.githubusercontent.com/31937095/31420942-7c5f0afc-ae12-11e7-9e45-3ccb04b019d3.png)

Here are the visualization on a map and the cluster centers: 

![62](https://user-images.githubusercontent.com/31937095/31420950-851ecfe2-ae12-11e7-9fa0-c7402d2cd291.png)
             

To further analyze the data, we ignored the 0.136% of the invalid latitude and longitude, and found that cluster 5 covers almost 50% of all the pickups and dropoffs in these 12 clusters. The complete data is shown below: 
** Note that we combine all the pickups and dropoffs, so the total percentage adds up to 200%

![63](https://user-images.githubusercontent.com/31937095/31420963-9cec5108-ae12-11e7-9dd3-2743ff857ca0.png)

		

Also, the percentage of trips where pickups and dropoffs are in the same clusters is 53.67%, meaning that it would be profitable for taxis to concentrate themselves in the clusters shown on previous map. 


Task 7: 

In this task, we used the given line equation y = 1.323942*x + 138.669195 as the boundary of NJ and NYC, with NJ having latitudes greater than 1.323942*x + 138.669195, and NYC having the opposite. After grouping all trips into four categories (NJ -> NJ, NJ -> NYC, NYC -> NJ, NYC -> NYC), we found association rules on intra and inter borough traffic: 
Intra-State Fares
NY -> NY
Average taxi fare cost: $11.48
Contributes 52.9% of revenue
NJ -> NJ
Average taxi fare cost: $10.57
Contributes 25% of revenue
Inter-State Fares
NY -> NJ
Average taxi fare cost: $21.94
Contributes 16.9% of revenue
NJ -> NY
Average taxi fare cost: $25.01
Contributes 4.9% of revenue
The results show that over 75% of the revenue comes from intra-state rides.

Further, if we look at the trips taken to and from the different boroughs by hour, we find the following results:

![72](https://user-images.githubusercontent.com/31937095/31421035-10c287c8-ae13-11e7-948e-a0cbc112a7f1.png)

 
We can see that there is much more intra-borough traffic in this graph (NY-NY and NJ-NJ) than inter-borough traffic. There are peaks in the NY-NY traffic late at night -- this is probably due to people going out to bars and the active nightlife in the city. There are peaks in NJ-NJ traffic during the morning and evening rush hours, probably due to people catching rides to work. There are slight peaks in NY-NJ traffic during the morning rush hour and at night, but these peaks are not very significant -- and overall compared to the intra-borough traffic, the number of these trips is small. There is a very low amount of NJ-NY traffic as well, meaning that most people probably take trains or drive. Further, we find that 35% of the trips occur during rush hours (7:00 - 9:00 am, 4:00 - 7:00 pm).

Further, we can analyze the number of street-hail versus dispatch acquirements of the taxis.

![73](https://user-images.githubusercontent.com/31937095/31421074-5358f40a-ae13-11e7-9aef-d998ee438209.png)


During certain hours of the ddat there are higher proportions of one type of taxi call over the other.  We took a look at each hour and calculated the contribution of trips made from dispatch and street hail.  If the number of trips called were over 52% of one type call, we deemed it significant as a preference to that type.  During the hours of 10AM-5PM, 56% of all trips were made from dispatch calls.  This suggests that less than half of all operable taxis should be roaming for a customer and instead, remain stationed awaiting a call.  Also in NY there is a slight increase in street hail taxi calls from the hours of 8AM-10AM.  About 56% percent of trips during those hours are made via street hail.  Likewise, this suggests that more taxis should await a call from people on the street rather than via dispatch.

![74](https://user-images.githubusercontent.com/31937095/31421087-63f4dc7a-ae13-11e7-81bf-a118f6395447.png)




We further analyzed the differences between the weekdays and the weekend (specifically Saturday). We found that the number of trips on a weekend or holiday (Labor Day) is 25% more than an average weekday. Consequently, profit is higher on the weekends. Below, the yellow graph shows the number of trips per day in September 2015. The peaks that are shown are on the Saturdays of the month. The red graph below shows the profit throughout the month. The peaks in profit also occur on the Saturdays due to the higher number of trips on these days.

We further broke down the number of trips per hour and compared the distribution of the data for a Saturday compared to a typical weekday. The blue graph below represents the number of trips throughout the day on a Saturday while the red graph represents the number of trips throughout the day on a weekday.

![75](https://user-images.githubusercontent.com/31937095/31421098-743d6b4c-ae13-11e7-91e4-9c121193b9fc.png)








We can see that on Saturdays, the popular hours occur late at night or very early in the morning due to an active nightlife in NYC. However, during weekdays, we see that the most popular times are in the late morning and early evening.

Task 8: 
Based on all analysis above, here are our recommendations: 
1. Concentrate drivers in below locations since most trips are short and over half of the trips start and end with one of  these locations: 

![81](https://user-images.githubusercontent.com/31937095/31421131-a8b80616-ae13-11e7-92d3-6cbd81315259.png)

	
2. ecause the average tips to airports are 70% more than normal, individual drivers might want to strategize a way to take advantage of these tip

3. In order to be in the locations where most trips will occur, for every hour, we created 5 pickup clusters for the drivers, so they will not have to drive around randomly and look for passengers. Below shows clusters on a typical day at 10am: 

![82](https://user-images.githubusercontent.com/31937095/31421135-b0fc4f76-ae13-11e7-98b1-5c7d7dbee295.png)
	
If we do this for each hour, the drivers will better know which locations to go to during which hours in order to maximize business.

4. Since greater than 75% of fare revenue comes from intrastate trips, it is a good idea to allocate taxis to only go intrastate, perhaps from street hail. 

5. Take advantage of the number of street-hails and dispatch calls. 
	From 8am to 10am in NYC, 56% of trips are made via street-hail 
		Over half the taxis should be await calls while roaming popular street areas
	From 10am to 5pm in both NJ and NYC, 57% of trips are made via dispatch  
		Over half the taxis remained stationed and await dispatch calls.
		
6. More taxi drivers should be prepared to drive passengers within NYC in the very early hours (1am) and very late hours (after 10pm) on Saturdays. 

7. Driving force should be largest on Saturdays. 

8. During weekdays, drivers should be ready to drive workers within NYC and within NJ in their morning commutes. 

9. Since 35% of trips occur during the rush hours of 7:00 - 9:00 am, the companies should make sure that there are ample drivers on the roads to satisfy this demand.

10. We found that there are 4418 no charge cases with a total distance of 10,436.88 miles. Based on Sept. 2015 taxi rate ($2 initial + 0.30 per ⅕ miles), there is a $24,491.32 profit loss due to “No Charge”, which means that there is a roughly $200,000 profit loss a year. Therefore, an investigation on these no charge cases is needed. 



