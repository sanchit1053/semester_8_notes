# lecture 15 <div style="text-align:right"> 13/03/2024 </div>

## Resource management mechanisms + policies / orchestration

Papers to talk about
- memmgmt
- sandpiper
- live migration
- remus
- snowflock

### Sandpiper
Manage cluster resources to meet SLAs with dynamic workloads (dynamic resource requirements)  

for every load level we will have a inverse proportional curve between resource and performance/latency

- Vertical Scaling:
    * Increasing resources on the same physical system
- Horizontal Scaling:
    * Using resources on another machine

**sandpiper only relates to purple part in sir's notes** 

1. measurements and profiling (black box vs gray box)
2. hotspot detection
3. resolution via ballooning and migration

How Much resources to add/change
- Feed back control loop
- lookup performance to resource profile (measurements)
- performance model

$$
\begin{align*}
    p = f(\mathbb{R}, \mathbb C)
\end{align*}
$$



## gray box

$$
\begin{align*}
    \lambda_{cap} &\propto \frac 1\mu \\
    \lambda_{peak} &\approx 2\lambda_{cap}
\end{align*}
$$


## Which VM to migrate (and where)
The Placement problem
- Knapsack / bin-packing (multidimensional)

$$
\begin{align*}
    \mathbb{V} &= \{v_i\} && v_i \sim v_m \\
    v_i &= \{v_{ij}\} && v_{ij} \sim \text{resource req of VM\_i on res j} \\
    \mathbb{C} &= \{c_i\} && \text{capacity of ith Physical machine}
\end{align*}
$$

place $\mathbb V$ on $\mathbb C$ such that some obective function is met

- least physical machines used
- highest slack
- balanced load/allocation
- NP hard (exponential search space)

#### heuristic
- Heuristic that they are trying to use 
 
$$
\begin{align*}
    vol = \frac{1}{1 - cpu} * \frac{1}{1 - mem} * \frac{1}{1 - h/w\,util}
\end{align*}
$$

move vm with highest vsr to least loaded physical machine

## Remus
- High Availablity via Asynchronous VM replication
