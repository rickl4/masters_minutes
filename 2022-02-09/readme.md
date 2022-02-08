# 2022-02-09

## Line 3 Scarborough Update

* We're finding gaps longer than 7.5 minutes at Kennedy Station (PM, EV), and Lawrence East (EM, AM, MD)
  * Headway ranges from 5 minutes to 6.5 minutes, depending on time of day
* We're removing GTFS trips that arrive at Kennedy/Lawrence East during the gap. This includes all other stops for that trip
* In the real time graph, we're inserting the remaining GTFS trips

## Transsee Data Update (AVL/NextBus API)

* Consolidated the stops to intersection, we now have a "GTFS" feed made up of intersections
* Haven't QC'd the dataset. The data on Transsee seems to be already cleaned. Will only investigate the data quality if there's an issue with the graph results
* Transsee data contains some trips that don't have a GTFS trip associated with it (the field is blank). These trips are being used in the graph

## Next Train Arrival Data Update

* Continued to work on making train trajectories
* Methodology is to take the latest available API request before the train enters the station as the arrival. Earlier API requests may suggest an earlier/later time
  * For departures, its either the same as the arrival time, or the latest API request where the train is still sitting at the station

### Issues

* Previous station departures are before next station arrivals
* The travel time on some links is too small to be feasible
* Large gaps in the data for the same train
* Some travel times were above 60 minutes
* Some arrival times do not follow the proper order
* Inconsistencies with how trains are taken to the yard, causing uncertainty for the TYSSE stations

### Mitigation Solutions
* Remove all links that aren't between directly adjacent stations. Ignore "bypassing"
* Remove all links where the travel time is above a travel time threshold 
* Only determine the arrival time. Do not make an attempt to estimate the departure time or dwell time

### Next Steps

* What level of accuracy should we aim for? Is it acceptable to underestimate the number of trips/links? 
* Should we wait for the wifi data trajectories instead?

#### Hold off on further work with Next Train Arrival Data
* Build a graph for 2019 GTFS and compute GE
* Build multiple graphs using Transsee data, and GTFS subway schedule, and compute GE as a test
