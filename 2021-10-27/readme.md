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

