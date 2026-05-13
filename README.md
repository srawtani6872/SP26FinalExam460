# The Torchbearer

**Student Name:** Sushil Rawtani
**Student ID:** 827320709
**Course:** CS 460 – Algorithms | Spring 2026

> This README is your project documentation. Write it the way a developer would document
> their design decisions , bullet points, brief justifications, and concrete examples where
> required. You are not writing an essay. You are explaining what you built and why you built
> it that way. Delete all blockquotes like this one before submitting.

---

## Part 1: Problem Analysis

> Document why this problem is not just a shortest-path problem. Three bullet points, one
> per question. Each bullet should be 1-2 sentences max.

- **Why a single shortest-path run from S is not enough:**
  We cannot use a shortest-path from just S because a single shortest path does not give the order in which to visit relics

- **What decision remains after all inter-location costs are known:**
  The order to visit the relics

- **Why this requires a search over orders (one sentence):**
  This requires a search over orders because the total cost depends on the order relics are visited

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

> List the source node types as a bullet list. For each, one-line reason.

| Source Node Type | Why it is a source |
|---|---|
| Spawn Node | Its a source node because you want to compute shortest distance froom the spawn to everry other node and the exit|
| Other Relic Nodes | Its a source because at each relic, you want the shortest distance between that relic and other relics and the exit|

### Part 2b: Distance Storage

> Fill in the table. No prose required.

| Property | Your answer |
|---|---|
| Data structure name | Dictionary / Hashmap|
| What the keys represent | Source nodes |
| What the values represent | Shortest Distance |
| Lookup time complexity | O(1)|
| Why O(1) lookup is possible | Hashmaps have O(1) lookup |

### Part 2c: Precomputation Complexity

> State the total complexity and show the arithmetic. Two to three lines max.

- **Number of Dijkstra runs:** Run Dijkstra for every relic + the spawn
- **Cost per run:** O((n+m)logn)
- **Total complexity:** O(k*(n+m)logn)
- **Justification (one line):** You Run Dijkstra's for each relic and the spawn

---

## Part 3: Algorithm Correctness

> Document your understanding of why Dijkstra produces correct distances.
> Bullet points and short sentences throughout. No paragraphs.

### Part 3a: What the Invariant Means

> Two bullets: one for finalized nodes, one for non-finalized nodes.
> Do not copy the invariant text from the spec.

- **For nodes already finalized (in S):**
  Their distance is the guaranteed shortest path from the source node

- **For nodes not yet finalized (not in S):**
  Their distance is the current shortest path so far, but not guaranteed. 

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
  The initialization holds because the distance from the source to the source is zero. We have not discovered any other nodes, therefore the distance to them is infinity. 

- **Maintenance : why finalizing the min-dist node is always correct:**
  Because the edge weights are nonnegative, it's safe to finalize because there cannot be another path found later that sums up to less than what's been finalized. 

- **Termination : what the invariant guarantees when the algorithm ends:**
 When the algorithm ends, the invariant gaurentees the shortest path from the source node to all other nodes.  

### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

This matters for the route planner becuase if you don't have correct distances, then you will not be able to have an optimal route. 

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** Greedy choosing the next closet node can lead to a globally suboptimal solution despite making the local best choice.
- **Counter-example setup:** Using the illustration, only changing D to C to be 4 instead of 1.
- **What greedy picks:** reedy starts by choosing B (1), from B goes to D (1), from D to C since B had already been visisted, from C to T. Total Cost = 7
- **What optimal picks:** Optimal could start by choosing S to D (2), D to C (1), C to B (1), B to T(1), total cost = 5
- **Why greedy loses:** Greedy lost because although it chose the locally optimal choice, it did not consider future choices.

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- The algorithm must explore the most optimal order to visit relics which produces the lowest cost. 

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | | | |
| Relics already collected | | | |
| Fuel cost so far | | | |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | |
| Operation: check if relic already collected | Time complexity: |
| Operation: mark a relic as collected | Time complexity: |
| Operation: unmark a relic (backtrack) | Time complexity: |
| Why this structure fits | |

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** _Your answer (in terms of k)._
- **Why:** _One-line justification._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** _Your answer here._
- **When it is used:** _Your answer here._
- **What it allows the algorithm to skip:** _Your answer here._

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** _Your answer here._
- **What the lower bound accounts for:** _Your answer here._
- **Why it never overestimates:** _Your answer here._

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Your answer here._

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Your references here._
