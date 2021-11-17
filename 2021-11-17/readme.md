# 2021-11-17

## Clustering

* Average neighbour degree takes the average degree of nodes surrounding the node
* Similar in purpose to the cluster coefficient, but more intuitive to understand and better suited for Toronto's bus network

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-11-17/img/nearest_neighbour.png)

| Period | Black | Low Income | LEP   | General Population | Carless Households | Racialized | Recent Immigrants |
|--------|-------|------------|-------|--------------------|--------------------|------------|-------------------|
| EM     | 0.145 | 0.161      | 0.161 | 0.157              | 0.157              | 0.154      | 0.157             |
| AM     | 0.754 | 0.738      | 0.771 | 0.780              | 0.790              | 0.772      | 0.774             |
| MD     | 0.523 | 0.520      | 0.530 | 0.543              | 0.544              | 0.526      | 0.530             |
| PM     | 0.704 | 0.688      | 0.712 | 0.728              | 0.736              | 0.717      | 0.719             |
| EV     | 0.474 | 0.471      | 0.483 | 0.491              | 0.494              | 0.481      | 0.483             |

## Cycle Density

* Based on cycle availability metric

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-11-17/img/2021-11-17.png)

* Cycle basis was used instead of number of cycles in a ward.
    * Some wards had an excess number of cycles. Ward 3 Etobicoke Lakeshore had ~1 million cycles compared to an average of ~250
* Cycles were weighted by frequency of the least frequent link in the cycle
* Area was used instead of size of graph as the denominator. This is more appropriate for a public transit/access context.

| Period | Black | Low Income | LEP   | General Population | Carless Households | Racialized | Recent Immigrants |
|--------|-------|------------|-------|--------------------|--------------------|------------|-------------------|
| EM     | 0.011 | 0.012      | 0.013 | 0.011              | 0.012              | 0.011      | 0.011             |
| AM     | 0.038 | 0.037      | 0.042 | 0.040              | 0.040              | 0.039      | 0.039             |
| MD     | 0.040 | 0.039      | 0.043 | 0.044              | 0.043              | 0.041      | 0.040             |
| PM     | 0.035 | 0.034      | 0.038 | 0.037              | 0.037              | 0.036      | 0.035             |
| EV     | 0.038 | 0.036      | 0.041 | 0.041              | 0.041              | 0.039      | 0.039             |

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-11-17/img/cycles.png)

## Distinct Paths

* Based on measure from Jing et Al. 2020

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-11-17/img/path_gamma.png)
![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-11-17/img/distinct_path_eqn.png)

* l is length/cost of segment
* <img src="https://render.githubusercontent.com/render/math?math=n_a^{rs}"> is number of route segments passing through segment a
* The measure intends to measure the number of effective routes
* If multipe routes share the same route segments, the original

### Graph Changes

* The original graph structure had a time dependent origin, and variable destination. This has been changed to have both the orign and destination be time dependent.
* Goal is to extract all available paths that fall under the threshold. The threshold is 15 minutes + Shortest Path Travel Time.
    * Find paths that may not be the most attractive option, and determine which OD pairs have the most redundant options incase the primary/most attractive option (the shortest path) is not available

### Issues

* Using a number larger than 15 minutes will lead to excess memory being used due to number of shortest path (Humber College to Scarborough had ~9 million paths and required 75GB of RAM using 20 minutes + shortest path travel time. Using 1.2x shortest path travel time crashed the computer)
* Extracting Route-Edge paths will cause storage issue (Some OD pairs result in a 500MB file), and use up too much computation time
* Some paths may be due to "looping", or adding unnecessary route segments to reach the destination constraint. This is already deterred by the fact transfer's are a minimum of 4 minutes. 
    * This may be furthered reduced by lowering the buffer time from 15 minutes, or completing the analysis on shortest paths only
* Cost for some segments varies. Roughly 85% of segments have no variation in costs.


### Steps to Extract Paths
1. Determine shortest path travel time for OD pair and departure time
2. Determine the new cutoff time by adding 15 minutes
3. Load the OD constrained graph
4. Find the number of paths using the departure and arrival constraints.

### Questions

* How should walking paths be treated?
* Normalizing by distance. Longer OD Pairs may result in more distinct paths. 
    * Shortest Path Travel time?
    * Euclidean Distance?
    * No Normalization?
