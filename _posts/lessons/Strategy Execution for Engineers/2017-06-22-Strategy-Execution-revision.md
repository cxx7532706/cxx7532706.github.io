---
layout: post
category : Strategy Execution
tagline: "Supporting tagline"
tags : [ENGM90013]
---
{% include JB/setup %}

### Little's Law

* Flow Rate: Average time between the output of successive units(e.g. 5min/unit).
* Flow Time: The average amount of time it takes a unit to get through the process.
* Inventory or Work in process(WIP): Average number of units in the process at any point in time(includes the units waiting to be processed).

#### Little's law: Inventory(I) = flow rate(R) * flow time(T). All in <strong>average</strong>!!!

* Utilization = (demand capacity) / (resource capacity).

* PERT Chart: Bootleneck && Critical Path.

### Adding Resource Set-up Time

* Flow rate = (Batch size) / (Setup time + Time per unit * Batch Size)

* Recommended Batch Size = (flow rate * setup time) / (1 - flow rate * time per unit)

### Inventory Management(optimal order quantity to minimise inventory and ordering costs)

* K: Order cost(fixed per order)(e.g. shipment).
* Q: Order quantity
* R: flow rate(output units/unit of time)
* h: Inventory cost($/per unit of time and unit of output) (e.g storage cost)
* Q: optimal order quantity

* Setup costs per unit of time(average) = K/(Q/R) = K*R/Q
* Average inventory: Half of the order quantity = Q/2
* Inventory Costs = h * Q/2
* Total costs C(Q) = K*R/Q + h*Q/2
* Q = sqrt(2KR/h)

### Adding Waiting time

Customer comes for service, if all resources(e.g tables for restaurants) are occupied, they need to wait in queue.

How to calculate average customer waiting time?

* a: average inter-arrival time(customer walk in).
* std(a): standard deviation of the inter-arrival time.
* p: average processing time(e.g time between getting seat until leave).
* std(p): standard deviation of processing time.
* CVa: coeeficient of variation: std(a)/a
* CVp: std(p)/p
* m: number of resources (e.g number of tables)
* Utilization = p/(a * m)
* Avg Time in Queue = (p/m)*((utilization^(sqrt(2m+2)-1))/(1-utilization))*((CVa^2 + CVp^2)/2)

### Throughput losses

Customer may choose to leave if they need to wait for being serviced.

How to calculate the average probability of customers leave?

* Define r = p / a
* m: number of resources
Use Erlang Loss Function Table

<img src="/assets/photos/Erlang Table.jpg" alt="Erlang Table" style="width: 630px; margin: 0 auto; display:block;"/>

The number is the probability of customer leaving.





