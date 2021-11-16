# 2021-10-27

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
* <img src="https://render.githubusercontent.com/render/math?math=n_a^{rs}"> 