# NYC2015SEP_Taxi
analyze September 2015 green taxi data and come up with recommendations for the taxi companies 


Task 1:

The file contains 21 columns and 1,494,926 rows. The 21 different attributes are VendorID, lpep_pickup_datetime, Lpep_dropoff_datetime, Store_and_fwd_flag, RateCodeID, Pickup_longitude, Pickup_latitude, Dropoff_longitude, Dropoff_latitude, Passenger_count, Trip_distance, Fare_amount, Extra, MTA_tax, Tip_amount, Tolls_amount, Ehail_fee, improvement_surcharge, Total_amount, Payment_type, and Trip_type.

Task 2:

The distances of the trips were recorded by mile. A histogram was plotted to illustrate the most popular distance amongst the trips. Below is the histogram produced:

We can see the most common distances are from 0-2 miles. This means that the majority of trips are shorter trips rather than longer trips. The graph excludes distances greater than 25 miles for clarity; there are considered outliers.
Task 3: 
The mean distances grouped by hour are shown in the histogram below. 
It is obvious that the longest trips occur between 5:00 and 7:00 am. Longer trips also occur later during the day as well, 10:00 pm - 12:00 am.
Below is the list of hours in 24 hour time with their respective average distances:





Task 4:

During this task, we studied the trips that terminate at an airport. For this task, we specifically looked at Laguardia and JFK. To determine what constitutes a trip that terminates at an airport, Google maps was utilized to determine an approximate range for latitude and longitude for each respective airport. Laguardia is located at  40.7769° N, 73.8740° W. An appropriate range was determined to be 40.769° N  - 40.78° N, 73.856° W - 73.88° W. JFK is located at 40.6413° N, 73.7781° W. An appropriate range was determined to be 40.63° N - 40.66° N, 73.75° W - 73.82° W.

The trips were filtered to leave only the trips that terminate within one of these ranges. It was determined that there are 31117  trips to an airport (Laguardia or JFK). The average fare to either Laguardia or JFK is $29.55. Another interesting fact (which makes sense given the fact that an airport is the end destination) is that the average distance for these trips is 9.39709419288 miles.
This is compared to the average distance for all trips of 2.96814085112 miles. In regards to the number of passengers, 91.66% of to the airport trips have 1  or 2 passengers. Therefore, we see that these trips tend to have fewer passengers. The average tips for trips to the airport is 2.77664500907  more than the tips for non-airport trips.
Task 5:   

In this task, we created clusters on pickup and dropoff locations respectively. We first cleaned the locations’ latitude and longitude since there are some invalid data such as 0. Then we created a list of numbers of k from 2 to 21 and tried the KMeans.train function for each k. To find the optimal k, we graphed the WSSEE for pickups: 

The key is to choose a number so that adding another cluster does not give much better modeling of the data, so in this case we chose k = 11. In order to get the centers of all clusters, we ran KMeans.train with k = 11 and macIterarions = 10. Below shows the pickup clusters’ centers: 

We then repeated the same procedure for dropoffs. As shown below, the optimal k is 10. 
 
To have a better visualization for all the clusters, we used gmplot module to display the centroid information on a map. We can see that the pickup and dropoff centroids are very closely related. 
*Dark purple - pickups, pink - dropoffs


Task 6: 

We repeated the procedure (clean the data and then plot the error on a group for k from 2 to 21)in task 5 to create clusters for both pickup and dropoff locations together. We chose 12 for optimal trade-off between complexity and error as shown below: 


Here are the visualization on a map and the cluster centers: 
             

To further analyze the data, we ignored the 0.136% of the invalid latitude and longitude, and found that cluster 5 covers almost 50% of all the pickups and dropoffs in these 12 clusters. The complete data is shown below: 
		

Also, the percentage of trips where pickups and dropoffs are in the same clusters is 53.67%, meaning that it would be profitable for taxis to concentrate themselves in the clusters shown on previous map. 


Task 7: 

In this task, we used the given line equation y = 1.323942*x + 138.669195 as the boundary of NJ and NYC, with NJ having latitudes greater than 1.323942*x + 138.669195, and NYC having the opposite. After grouping all trips into four categories (NJ -> NJ, NJ -> NYC, NYC -> NJ, NYC -> NYC), we found association rules on intra and inter borough traffic: 

The results show that over 75% of the revenue comes from intrastate rides. 
