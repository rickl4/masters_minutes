# 2022-02-16

## Next Train Arrival Data

### New Methodology

* Take most recent request per train and direction in each API request
* Reset the `trip_id` for a change in direction, or if theres a gap larger than 30 minutes 
  * Previous methodology: `trip_id` only resets after a change in direction.
  * This change also removes very long links. 
* Take most recent record for each station
  * Previous methodology: We attempted to find both arrival and departure time by finding the most recent record the train was not in the station, and the most recent record the train was in the station
* Remove any `timint` (Estimated time before arrival) longer than 2 minutes, since those predictions are not reliable. If the train is more than 2 minutes away, its likely there is a more accurate and recent prediction
* Implement a link cost limit of 60 minutes (travel time between a link cannot be more than 60 minutes)
  * This only applied for 1 link out of 12203 in November 28

### Links between Non-Adjacent Stations (ex a link from St. George to Eglinton West)
* Twitter Data suggests there was only one instance of trains bypassing (Line 1 Dec 19, at 9:13 PM at York Mills)
  * Trains still arrive at the station when its bypassing the station of interest, the record exists in the Next Train Arrival Data
* Some of the error is due to missing data

#### Questions
 * Should I remove these links? This represents 122 out of 12203 links for Nov 28 Morning Rush Hour. 
  * If these links are removed, path itineraries will alight at the station, and wait for the next train that traveses the section with missing data
  * If these links are not removed, for an example where the link is from St. George to Eglinton West, and no record for a train exists at Spadina, Dupont, St. Clair stations...
    * Path itineraries where the final destination is Eglinton West or North will stay on the same train
    * Path itineraries where the final destination is one of the 3 stations with no data will have to alight at St. George and wait for the next train

### Error Rates

#### Nov 28 AM Peak
* 12203 Inital Links
* 1 link longer than 60 minutes
* 204 Links travelling between the same station (mostly at terminals, these links will be removed).
  * Caused by the allocation of platforms to trains at terminals changing mid-trip 
  * For example, from Kipling platform 1 to Kipling platform 2.
* 122 Links not between adjacent stations
* 0 Links where the train arrived at the successive station before the preceeding station

#### Dec 2 AM Peak (There was a delay on Line 2)
* 10259 Inital Links
* 3 links longer than 60 minutes
* 175 Links travelling between the same station (mostly at terminals, these links will be removed).
* 60 Links not between adjacent stations
* 0 Links where the train arrived at the successive station before the preceeding station
