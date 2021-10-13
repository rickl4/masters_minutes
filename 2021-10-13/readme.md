# 2021-10-13

## Connectivity

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-10-13/img/2021-10-13.png)


* Connectivity measures the redundancy of service and benefits zones with large connecting hubs
    * Connecting hubs are stops with many routes and frequencies connected to it

### Graph Changes Since June

* Networkx had issues with multiple parallel edges in a directed graph (MultiDiGraph). Not all algorithms were available

* Network was changed to a directed graph/Route Map Graph, where each edge has a frequency weight
    * There can only be 1 edge from a stop to another stop, but that edge contains information on the frequency of the edge.
    * Graph itself does not have route information, but it was added in the connectivity calculations

### OD Weighting

* Once connectivity was found for the 25 wards, the scores for each group was found
* Steps:
    1. Find OD trips by ward and group
    2. For each trip, find connectivity score by averaging origin ward and destination ward scores
    3. Average the results for each equity group

* **Next steps**: find out the relationships between equity group population in ward, and connectivity score.

#### Ward OD Trips
* Found by summing the TTS Zones OD Trips
* If more than 7.5% of zone lie in another ward, the trips were proportionally allocated by area
    * 7.5% found by visual inspection

#### Table Format

| Period | Black | Low Income | LEP  | General Population | Carless Households | Racialized | Recent Immigrants |
|--------|-------|------------|------|--------------------|--------------------|------------|-------------------|
| EM     | 7.1   | 8.0        | 7.8  | 7.7                | 7.6                | 7.5        | 7.8               |
| AM     | 79.8  | 82.7       | 83.2 | 84.6               | 85.4               | 85.7       | 87.2              |
| MD     | 53.0  | 54.8       | 53.5 | 54.8               | 55.7               | 55.2       | 56.3              |
| PM     | 78.1  | 79.6       | 79.8 | 81.9               | 83.0               | 82.7       | 83.7              |
| EV     | 48.0  | 50.6       | 49.2 | 50.2               | 51.2               | 50.7       | 51.4              |

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-10-13/img/connectivity_od_weighted.png)

