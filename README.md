# The Torchbearer

**Student Name:** Sushil Rawtani
**Student ID:** 827320709
**Course:** CS 460 – Algorithms | Spring 2026

---

## Part 1: Problem Analysis

- **Why a single shortest-path run from S is not enough:**
  We cannot use a shortest-path from just S because a single shortest path does not give the order in which to visit relics

- **What decision remains after all inter-location costs are known:**
  The order to visit the relics

- **Why this requires a search over orders (one sentence):**
  This requires a search over orders because the total cost depends on the order relics are visited

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

| Source Node Type | Why it is a source |
|---|---|
| Spawn Node | Its a source node because you want to compute shortest distance froom the spawn to everry other node and the exit|
| Other Relic Nodes | Its a source because at each relic, you want the shortest distance between that relic and other relics and the exit|

### Part 2b: Distance Storage


| Property | Your answer |
|---|---|
| Data structure name | Dictionary / Hashmap|
| What the keys represent | Source nodes |
| What the values represent | Shortest Distance |
| Lookup time complexity | O(1)|
| Why O(1) lookup is possible | Hashmaps have O(1) lookup |

### Part 2c: Precomputation Complexity


- **Number of Dijkstra runs:** Run Dijkstra for every relic + the spawn
- **Cost per run:** O((n+m)logn)
- **Total complexity:** O(k*(n+m)logn)
- **Justification (one line):** You Run Dijkstra's for each relic and the spawn

---

## Part 3: Algorithm Correctness


### Part 3a: What the Invariant Means


- **For nodes already finalized (in S):**
  Their distance is the guaranteed shortest path from the source node

- **For nodes not yet finalized (not in S):**
  Their distance is the current shortest path so far, but not guaranteed. 

### Part 3b: Why Each Phase Holds


- **Initialization : why the invariant holds before iteration 1:**
  The initialization holds because the distance from the source to the source is zero. We have not discovered any other nodes, therefore the distance to them is infinity. 

- **Maintenance : why finalizing the min-dist node is always correct:**
  Because the edge weights are nonnegative, it's safe to finalize because there cannot be another path found later that sums up to less than what's been finalized. 

- **Termination : what the invariant guarantees when the algorithm ends:**
 When the algorithm ends, the invariant gaurentees the shortest path from the source node to all other nodes.  

### Part 3c: Why This Matters for the Route Planner


This matters for the route planner becuase if you don't have correct distances, then you will not be able to have an optimal route. 

---

## Part 4: Search Design

### Why Greedy Fails


- **The failure mode:** Greedy choosing the next closet node can lead to a globally suboptimal solution despite making the local best choice.
- **Counter-example setup:** Using the illustration, only changing D to C to be 4 instead of 1.
- **What greedy picks:** reedy starts by choosing B (1), from B goes to D (1), from D to C since B had already been visisted, from C to T. Total Cost = 7
- **What optimal picks:** Optimal could start by choosing S to D (2), D to C (1), C to B (1), B to T(1), total cost = 5
- **Why greedy loses:** Greedy lost because although it chose the locally optimal choice, it did not consider future choices.

### What the Algorithm Must Explore

- The algorithm must explore the most optimal order to visit relics which produces the lowest cost. 

---

## Part 5: State and Search Space

### Part 5a: State Representation


| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | current_loc | node | The current node of the search |
| Relics already collected | relics_remaining | set[node] | unvisited relics |
| Fuel cost so far | cost_so_far | float | The total cost so far |

### Part 5b: Data Structure for Visited Relics


| Property | Your answer |
|---|---|
| Data structure chosen | set |
| Operation: check if relic already collected | Time complexity: O(1)|
| Operation: mark a relic as collected | Time complexity: O(1) |
| Operation: unmark a relic (backtrack) | Time complexity: O(1)|
| Why this structure fits |A set fits because sets can do all these operations O(1) time, much faster than other data structures like a list|

### Part 5c: Worst-Case Search Space

- **Worst-case number of orders considered:** O(k!)
- **Why:** For each relic, you can consider all possible orders. As you go forward, there's less to consider, so that's why it's O(k!)

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

- **What is tracked:** The best route so far
- **When it is used:** It it used before the loop to check if the current path is equal or worse than the best known path
- **What it allows the algorithm to skip:** Allows the algorithm to skip paths that are already equal or worse than the best known path 

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** You know the cost so far, the current location, and the relics that need to be visited. 
- **What the lower bound accounts for:** The lower bound accounts for the current cost so far
- **Why it never overestimates:** It doesn't over estimate because the only thing being considered is the current cost so far. 

### Part 6c: Pruning Correctness

- The reason why pruning is safe is because if the current path cost is equal or worse than the best known path,  then there is no resune to continute explorating that path. 

---

## References

- https://www.geeksforgeeks.org/dsa/dijkstras-shortest-path-algorithm-greedy-algo-7/
- https://www.geeksforgeeks.org/dsa/time-and-space-complexity-of-dijkstras-algorithm/
- Lecture notes
