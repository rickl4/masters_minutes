# 2021-09-29 Minutes

## Global Efficiency with Random Removal

* Targeted removal based off _General Population Weighted Betweenness Centrality_ will always show the General Population as the group thats most impacted

* Global Efficiency does not model bus diversions; diversions can't be modeled by graph networks
    * Link removals analagous to subway disruption where service cannot be diverted, and the line is split into multiple independent segments

* Random removal will randomly remove links from the graph model, then recalculate travel times
    * Prone to less bias than targeted removal
    * Batch size is 50 links per removal (some link removals will have little to no effect on travel times)
    * Random removal doesn't take into account probability of failure by route/mode

## General Findings

* Carless households and low income (to some extent) are not as impacted by disruptions, and those populations are less vulnerable than the general population

* Other equity groups do not perform that much differently than the general population

* Order of equity groups change depending on the period

* Carless households/Low Income are more likely to live in areas with more redundant transit networks and travel to destinations where walking is a viable mode

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-09-29/img/GE-Random_Graph.png)

![All Modes](https://github.com/rickl4/masters_minutes/blob/main/2021-09-29/img/GE-Random_Heatmap.png)

