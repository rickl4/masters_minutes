# 2022-01-26

## AVL Data

* New stops present in 2019 GTFS that wasn't in 2016. The new stops have been assigned to intersections

## Wifi Data Background

* What has already been done for the wifi data? How long has the data been analyzed?
* What is the aim of the wifi data? 

## Wifi Data Exploration

* Using the `od_segment` table to find the estimated train arrival/departure times
    * 5 stations do not have origin data for the analysis period (December 2019)
        * Warden, Eglinton West, Rosedale, Ellesmere, Yorkdale
* For the 5 stations without data in `od_sgement`, it appears in the `raw` table here are 1 or 2 wifi antennas for each of those stations, and none of the antennas are located on the platform (the association and dissociation time are for the concourses)
* Challenging to truly estimate the number of trips and arrival/departure times
    * Using the `od_segment` table, I reset the `train_id` if there is a gap longer than 45 seconds, and removed instances where the departure time was before the next row's departure time, but the arrival time was after the next row's arrival time by more than 30 seconds
    * Used median departure as the departure and arrival for the train, for all rows sharing same `train_id`
    * For Ossington to Dufferin, counted 115 trips, but scheduled (assuming no drawdown) of 106 in same 5 hour period
    * Process would be easier with longer headways (ex Line 3, 4)
* Wouldn't association/disassociation heavily depend on the wifi antenna of the phone?

## Train Arrival Data Exploration

* Missing Line 3 Scarborough
* Data is returned every minute
* Data records when a train is delayed, or is sitting at the station
* Data has a `train_id`, no issues about undercounting/overcounting train trips
* Process to determine arrival/departures
    * Arrivals is determined by the last location of the train before it's reported that the train entered the station (or departed)
    * Departure is determined by the last record of the train waiting in the station. If there is no record of the train sitting at the station, it's the same as the arrival time

## Future Steps

* Since graph is limited to a minute resolution, the need for precise times is small
* Use train arrival data for Line 1,2,4
* Use Wifi data for Line 3