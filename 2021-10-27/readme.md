# 2021-10-27

## Clustering

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/cluster_explain.png)


* Cluster Coefficient measures redundancy by analyzing the frequency of service among neighbouring nodes
* Disadvantage is that there are a significant number of nodes without links connecting the neighbours
    * Neighbouring node degree is a simpler, but more intuitive measure that fulfils the same purpose, TODO for next meeting

![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/cluster.png)

|Group|Black|Low Income|LEP  |General Population|Carless Households|Racialized|Recent Immigrants|
|-----|-----|----------|-----|------------------|------------------|----------|-----------------|
|EM   |0.025|0.026     |0.026|0.027             |0.026             |0.027     |0.026            |
|AM   |0.241|0.251     |0.249|0.247             |0.245             |0.252     |0.254            |
|MD   |0.142|0.145     |0.145|0.143             |0.144             |0.147     |0.149            |
|PM   |0.218|0.223     |0.221|0.221             |0.222             |0.225     |0.226            |
|EV   |0.130|0.135     |0.132|0.131             |0.132             |0.134     |0.134            |

## OD Trips by Group, Period and Zone

* Looked into Census options from UofT library, the data was on the same detail as the data I used in June

* Mapped out where trips are originating and ending by group

![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/trip_distribution.png)
![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/trip_distribution2.png)
![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/trip_distribution3.png)
![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/trip_distribution4.png)
![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/trip_distribution5.png)


## Connectivity Regression Exploration

* With the connectivity scores, I graphed the scores by ward as the dependent variable, and equity group population as the independent variable as a first step for a linear regression model.

![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/connectivity-reg_EM.png)
![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/connectivity-reg_AM.png)
![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/connectivity-reg_MD.png)
![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/connectivity-reg_PM.png)
![img](https://github.com/rickl4/masters_minutes/blob/main/2021-10-27/img/connectivity-reg_EV.png)

* Questions/Concerns

    1. There are only 25 data points (representing 25 wards), would it be appropriate to construct a model?
    2. Some variables are related to other variables. A person can be considered to have a low-income, without a car, and a person of colour.
    3. When graphed individually, many of these variables have no effect on the connectivity scores (used `scipy.stats.pearsonr`, for R and P)

## Real World Data

* If we want to use real world data/incidents, the GE, and NX (connectivity, clustering, cycles) measures should be the focus since they are quick to calculate
* To continue the theme of the project, we need delay data for buses, in addition to buses and streetcars
* We can analyze delays for buses and streetcars separately, but we should devise a separate analysis that involves buses if no bus delay data exists (since we know that certain groups, such as Black residents, rely on Streetcars far less than the general population)

    * If we use delay data from 2017/2018, would we need to create a new graph that uses a 2017/2018 GTFS?


### Real World Data Incorporating Buses

* If cleaned historical AVL data exists (from a previous study), we can pick multiple days, create a graph based on real world data, run the analysis for those days, and compare to our baseline 2016 graph
* If only unclean data exists, we need to spend additional effort determining the time a bus arrives at each stop

## Planned Work for Nov 17

* Cycle analysis
* Reconstruct the Route map graph to account for low fequencies in the early morning period (by using a 2 hour representative period instead of 1 hour)
* Neighbouring Node analysis
* Complexity Analysis
* If possible, finish the regression analysis