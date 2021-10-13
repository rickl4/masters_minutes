# 2021-10-13

## Connectivity

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-10-13/img/2021-10-13.png)


* Connectivity measures the redundancy of service and benefits zones with large connecting hubs
    * Connecting hubs are stops with many routes and frequencies connected to it

### Changes Since June

* Networkx had issues with multiple parallel edges in a directed graph (MultiDiGraph). Not all algorithms were available

* Network was changed to a directed graph/Route Map Graph, where each edge has a frequency weight
    * There can only be 1 edge from a stop to another stop, but that edge contains information on the frequency of the edge.

* Random removal will randomly remove links from the graph model, then recalculate travel times
    * Prone to less bias than targeted removal
    * Batch size is 50 links per removal (some link removals will have little to no effect on travel times)
    * Random removal doesn't take into account probability of failure by route/mode

## General Findings

* Carless households and low income (to some extent) are not as impacted by disruptions, and those populations are less vulnerable than the general population

* Other equity groups do not perform that much differently than the general population

* Order of equity groups change depending on the period

* Carless households/Low Income are more likely to live in areas with more redundant transit networks and travel to destinations where walking is a viable mode

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-10-13/img/connectivity_od_weighted.png)


