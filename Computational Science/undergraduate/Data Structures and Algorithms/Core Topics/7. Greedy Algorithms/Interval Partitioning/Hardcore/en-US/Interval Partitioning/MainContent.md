## Introduction
How do we efficiently allocate a limited number of resources—be it classrooms, CPU cores, or operating rooms—to a series of time-sensitive requests? This fundamental challenge is at the heart of the Interval Partitioning problem, a cornerstone of scheduling theory with vast practical implications. The problem addresses the critical knowledge gap of how to satisfy all requests using the absolute minimum number of resources, avoiding both conflicts and waste. This article provides a comprehensive guide to mastering this powerful algorithmic concept.

You will begin your journey in "Principles and Mechanisms," where we will formalize the problem, establish a theoretical lower bound for any solution using the concept of "depth," and present the elegant [greedy algorithm](@entry_id:263215) that provably achieves this optimal result. Next, in "Applications and Interdisciplinary Connections," we will explore the remarkable versatility of this algorithm, showcasing its use in real-world scenarios ranging from [compiler design](@entry_id:271989) and logistics to [bioinformatics](@entry_id:146759) and telecommunications. Finally, "Hands-On Practices" will challenge you to apply your knowledge to practical problems, incorporating realistic complexities like setup times and task dependencies to solidify your understanding.

## Principles and Mechanisms

The Interval Partitioning problem is a fundamental challenge in resource allocation and scheduling. It arises in numerous contexts, from assigning university lectures to a limited number of classrooms to scheduling jobs on processors or allocating tables in a restaurant . This chapter will dissect the core principles that govern this problem and the elegant, efficient mechanisms developed to solve it. We will establish a theoretical lower bound for any solution, present a constructive algorithm that achieves this bound, and explore the theoretical underpinnings that guarantee its optimality.

### The Problem Formalized: Conflicts and Partitions

The problem is defined over a set of $n$ requests, each represented by an **interval** on the real line. We will consistently use the **half-[open interval](@entry_id:144029)** convention, denoted $[s_i, f_i)$, which includes the start time $s_i$ but excludes the finish time $f_i$. This means the interval corresponds to the set of all time points $t$ such that $s_i \le t \lt f_i$.

Two intervals, $I_i = [s_i, f_i)$ and $I_j = [s_j, f_j)$, are said to be in **conflict** if they overlap, meaning their intersection is non-empty. This occurs if and only if one interval starts before the other one finishes, i.e., $s_i \lt f_j$ and $s_j \lt f_i$. The half-open interval definition carries a crucial implication: if one interval ends at the exact moment another begins (e.g., $f_i = s_j$), they do not conflict. This allows a resource to be used sequentially without any idle time.

An **interval partition** is an assignment of each interval to a resource (e.g., a classroom, a processor, a table) such that all intervals assigned to the same resource are mutually non-conflicting. The objective is to find a partition that uses the minimum possible number of resources.

### A Fundamental Lower Bound: The Concept of Depth

Before attempting to solve the problem, we must first ask: what is the absolute minimum number of resources we could possibly need? A simple but powerful argument provides a lower bound. If, at some specific point in time $t$, there are $d$ intervals that are all simultaneously active (i.e., all of them contain the point $t$), then each of these $d$ intervals must be assigned to a different resource, as they all conflict with one another. Therefore, any valid partition must use at least $d$ resources.

This leads to a crucial concept. We define the **depth** of a set of intervals as the maximum number of intervals that are mutually overlapping at any single point in time. Let $c(t)$ be the **active-count function**, representing the number of intervals that contain time $t$. The depth, which we will denote by $D$, is the [global maximum](@entry_id:174153) of this function:

$$
D = \max_{t \in \mathbb{R}} c(t) = \max_{t \in \mathbb{R}} |\{i \mid s_i \le t \lt f_i\}|
$$

The reasoning above establishes that the minimum number of resources required for any valid partition, $k_{opt}$, must be at least the depth: $k_{opt} \ge D$. The point in time where the depth is first achieved is sometimes called the **critical time** . Finding this depth is therefore a key subproblem.

A robust method for calculating the depth is the **[sweep-line algorithm](@entry_id:637790)** . The logic is that the active-count function $c(t)$ is a step function that can only change its value at the start or end points of the intervals. We can find its maximum value by "sweeping" a vertical line across the time axis, stopping at each interval endpoint to update the count. The algorithm proceeds as follows:

1.  **Create Events:** For each interval $[s_i, f_i)$, generate two events: a "start" event at time $s_i$ and a "finish" event at time $f_i$. We can represent these as tuples $(t, \text{type})$, where a start event has type $+1$ and a finish event has type $-1$.

2.  **Sort Events:** Collect all $2n$ events into a single list and sort them chronologically by time. A critical detail is the tie-breaking rule for events occurring at the same time. Because an interval ending at time $t$ frees up its resource for an interval starting at time $t$, we must process finish events *before* start events. Sorting by event type in ascending order (since $-1 \lt +1$) naturally enforces this rule.

3.  **Sweep and Count:** Initialize a counter for the current depth, `current_depth = 0`, and a variable to track the maximum depth, `max_depth = 0`. Iterate through the sorted event list. For each event, update `current_depth = current_depth + type`. After each update, set `max_depth = max(max_depth, current_depth)`.

After processing all events, `max_depth` will hold the value of $D$. The dominant step in this algorithm is sorting the $2n$ events, giving it an efficient worst-case [time complexity](@entry_id:145062) of $O(n \log n)$ .

For instance, consider the set of reservations $[0, 60), [15, 120), [30, 90), \dots$. At time $t=0$, the count becomes 1. At $t=15$, it becomes 2. At $t=30$, it becomes 3. At $t=60$, an interval ends, and the count drops to 2. By systematically processing all start and end points in this manner, we can determine the peak resource demand . In one detailed example, a maximum depth of 7 was found to first occur at the critical time $t^\star=7$, within the interval $[7, 7.5)$ .

### The Optimal Greedy Algorithm: Achieving the Lower Bound

We have established that we need at least $D$ resources. The pivotal question is whether $D$ resources are also *sufficient*. A constructive [greedy algorithm](@entry_id:263215) proves that they are. This algorithm not only confirms that the optimal number of resources is exactly $D$, but it also provides an actual assignment of intervals to resources.

The algorithm is remarkably simple and elegant :

1.  Sort the intervals in order of non-decreasing **start times**, $s_i$.
2.  Process the intervals one by one in this sorted order.
3.  For each interval $I_i = [s_i, f_i)$, try to place it in an existing resource. A resource is available if the last interval assigned to it, say $I_j$, finishes at or before $I_i$ starts (i.e., $f_j \le s_i$).
4.  If one or more resources are available, assign $I_i$ to any one of them.
5.  If no resource is available, create a new resource and assign $I_i$ to it.

To prove this algorithm is optimal, we demonstrate that it never uses more than $D$ resources. Suppose the algorithm is processing interval $I_j$ and is forced to create the $k$-th resource. This can only happen because all $k-1$ previously used resources are busy. A resource is "busy" if the interval most recently assigned to it, say $I_{p_m}$, has a finish time $f_{p_m} > s_j$. Since we are processing intervals sorted by start time, we also know that the start time of each of these intervals satisfies $s_{p_m} \le s_j$.

Therefore, for each of the $k-1$ busy resources, there is an interval $I_{p_m}$ for which $s_{p_m} \le s_j \lt f_{p_m}$. This means that at the specific point in time $s_j$, all of these $k-1$ intervals are active. In addition, the current interval $I_j$ is also active at time $s_j$. This gives us a total of $k$ intervals that are all simultaneously active at time $s_j$. By the definition of depth, the maximum number of overlapping intervals $D$ must be at least $k$. Thus, $k \le D$.

This proves that the algorithm never uses more than $D$ resources. Since we already know we need at least $D$ resources, the algorithm must be optimal, using exactly $D$ resources. This proof holds true regardless of which available resource is chosen, a subtle but powerful feature of the algorithm's design . For an efficient implementation, the available resources can be managed using a [min-priority queue](@entry_id:636722) keyed by their finish times, allowing for an overall $O(n \log n)$ [time complexity](@entry_id:145062) .

### The Criticality of the Greedy Choice and Related Problems

The success of the greedy partitioning algorithm hinges on sorting by **start times**. It is instructive to see why other seemingly intuitive strategies fail. Consider sorting by non-decreasing **end times** or by non-decreasing **duration**. Both of these [heuristics](@entry_id:261307) can lead to suboptimal solutions. A carefully constructed set of intervals can force these variants to open more rooms than necessary, demonstrating that the order in which intervals are considered is paramount .

The strategy of sorting by end times is particularly important because it is the optimal greedy choice for a related but fundamentally different problem: the **Activity Selection Problem** . This problem asks for the largest possible subset of intervals that can be scheduled on a *single* resource. To solve it, one should sort all intervals by non-decreasing **finish times** and greedily select intervals that are compatible with the previously chosen one.

The contrast is stark and essential to grasp:
-   **Interval Partitioning:** To minimize resources for *all* intervals, sort by **start time**.
-   **Activity Selection:** To select the maximum number of compatible intervals for *one* resource, sort by **finish time**.

Confusing these two algorithms is a common pitfall. The former seeks to accommodate every request with minimal [parallelization](@entry_id:753104), while the latter seeks to maximize throughput on a single resource, discarding requests that do not fit.

### Variations and Deeper Perspectives

The principles we have discussed are robust and apply even when the problem is presented differently, for instance, with intervals defined by a center and radius rather than start and end points . Once converted to the standard $[s, f)$ format, the same optimal algorithms apply.

#### Discretization and Complexity

The general $O(n \log n)$ complexity of our algorithms arises from the need for comparison-based sorting. However, if the interval endpoints are restricted to be integers within a known, relatively small range $[0, U]$, an alternative approach becomes viable. By using a **[difference array](@entry_id:636191)** of size $U+1$, we can compute the depth in $O(n + U)$ time. For each interval $[s_i, f_i)$, we increment the array at index $s_i$ and decrement it at index $f_i$. A single pass to compute the prefix sums of this array will then reveal the active-count function $c(t)$ at all integer points, and its maximum is the depth. This method is faster than sorting when $U$ is not significantly larger than $n$, but the sorting-based approach remains superior for intervals with large or real-valued coordinates .

#### An Advanced View: Linear Programming and Duality

A more profound understanding of why the depth $D$ is the precise answer can be found through the lens of linear programming. The interval partitioning problem can be formulated as an **Integer Linear Program (ILP)**. This involves defining a variable for every possible non-conflicting subset of intervals (an **independent set**) and seeking the smallest collection of such sets that covers all intervals.

When this ILP is relaxed into a **Linear Program (LP)**, we can analyze its **dual LP**. The [dual problem](@entry_id:177454) assigns a weight $y_i$ to each interval and seeks to maximize the sum of these weights, subject to the constraint that the total weight of any independent set cannot exceed 1.

It can be shown that the optimal value of this dual LP is precisely the size of the largest set of mutually conflicting intervals (a **maximum [clique](@entry_id:275990)**). For [interval graphs](@entry_id:136437), a powerful result from [perfect graph](@entry_id:274339) theory states that the size of the maximum clique is equal to the depth $D$. By the [strong duality theorem](@entry_id:156692) of linear programming, the optimal value of the primal LP (our relaxed partitioning problem) is equal to the optimal value of the dual LP. For [interval graphs](@entry_id:136437), this value is an integer and equals $D$. This provides a deep mathematical justification for the equivalence between the minimum number of resources and the maximum depth of the intervals .

Finally, it is worth noting that many variations of these problems exist. For example, one might ask for the maximum number of activities that can be scheduled given a fixed number of rooms, $k$. This more complex problem requires a different greedy strategy, one that also sorts by finish time but employs a more sophisticated rule for assigning intervals to rooms . These variations highlight the richness of the field and the importance of correctly identifying the problem structure before selecting an algorithmic tool.