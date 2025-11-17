## Introduction
When designing a network, whether it's a social platform, a communication system, or a chemical molecule, a fundamental question arises: can a given set of connection requirements be physically realized? In graph theory, this translates to asking whether a sequence of integers can represent the degrees of vertices in a [simple graph](@entry_id:275276)—a property known as being "graphic." Answering this question by trial and error is inefficient and often impossible. This article addresses this knowledge gap by providing a definitive framework for verifying degree sequences, centered around the powerful Erdős-Gallai theorem.

This article will guide you through the [complete theory](@entry_id:155100) and application of [graphic sequences](@entry_id:274087). In the "Principles and Mechanisms" chapter, you will learn the fundamental necessary conditions and delve into the Erdős-Gallai theorem, understanding its elegant inequality that balances degree demand with connection supply. The "Applications and Interdisciplinary Connections" chapter will demonstrate how this theorem is used to validate network designs, infer structural properties of graphs, and connect to other areas of mathematics. Finally, the "Hands-On Practices" section will allow you to apply these concepts to solve practical problems, solidifying your understanding. By the end, you will have mastered the primary tool for determining the [realizability](@entry_id:193701) of any network from its degree specifications.

## Principles and Mechanisms

In the study of graphs, a fundamental question arises: given a sequence of non-negative integers, can it represent the degrees of the vertices in a simple graph? Such a sequence is termed **graphic**. Formally, a sequence $D = (d_1, d_2, \dots, d_n)$ is a **[graphic sequence](@entry_id:274330)** if there exists a [simple graph](@entry_id:275276) $G$ with $n$ vertices whose degrees are precisely the integers in $D$. While one could attempt to construct a graph for any given sequence, this is often impractical. We require a more systematic method to determine if a sequence is graphic without resorting to trial and error. This chapter establishes the principles and mechanisms that provide a complete answer to this question.

### Fundamental Necessary Conditions

Before presenting the definitive test, we can often disqualify a sequence by checking two simple but powerful necessary conditions. A failure to meet either of these instantly proves a sequence is not graphic.

#### The Parity Condition

The first condition stems from one of the most elementary results in graph theory, the **Handshaking Lemma**. It states that the sum of the degrees of all vertices in a graph is equal to twice the number of edges, $|E|$.

$$ \sum_{i=1}^{n} d_i = 2|E| $$

Since the number of edges must be an integer, the sum of all degrees must be an even number. This provides our first test: for a sequence to be graphic, its sum must be even.

Consider, for example, the task of designing a symmetric communication network where every one of $n$ nodes must connect to exactly $k$ other nodes—a structure known as a $k$-[regular graph](@entry_id:265877). The [degree sequence](@entry_id:267850) would be $(k, k, \dots, k)$, repeated $n$ times. The sum of degrees is $n \times k$. For this to be graphic, the product $nk$ must be even. Consequently, it is impossible to construct a [3-regular graph](@entry_id:261395) on 7 vertices (since $3 \times 7 = 21$ is odd) or a 5-[regular graph](@entry_id:265877) on 9 vertices (since $5 \times 9 = 45$ is odd) [@problem_id:1501526]. Similarly, a proposed [degree sequence](@entry_id:267850) such as $(5, 4, 3, 2, 1, 0)$ can be immediately identified as non-graphic because its sum is 15, an odd number [@problem_id:1501548]. This [parity check](@entry_id:753172) is a simple yet effective preliminary filter.

#### The Degree Bound

The second necessary condition arises from the definition of a [simple graph](@entry_id:275276), which forbids loops (edges from a vertex to itself) and multiple edges between the same two vertices. In a graph with $n$ vertices, any single vertex can be connected to at most the other $n-1$ vertices. Therefore, the maximum possible degree for any vertex, often denoted $\Delta$, is $n-1$.

This implies that for a sequence $D = (d_1, d_2, \dots, d_n)$ to be graphic, every degree $d_i$ must satisfy the inequality $0 \le d_i \le n-1$. If any proposed degree exceeds this bound, no [simple graph](@entry_id:275276) can realize the sequence. For instance, a sequence $(6, 5, 4, 1, 1, 1)$ for a graph on $n=6$ vertices is impossible, because the leading term $d_1 = 6$ violates the condition $d_1 \le n-1 = 5$ [@problem_id:1501548].

While these two conditions are necessary, they are not sufficient. Many sequences that satisfy both conditions are still not graphic. For a complete answer, we must turn to a more powerful result.

### The Erdős-Gallai Theorem: A Complete Characterization

The definitive test for determining if a sequence is graphic was provided by Paul Erdős and Tibor Gallai. The **Erdős-Gallai theorem** gives a set of inequalities that are both necessary and sufficient. It provides a complete characterization of [graphic sequences](@entry_id:274087).

**Theorem (Erdős-Gallai):** A sequence of non-negative integers $D = (d_1, d_2, \dots, d_n)$ sorted in non-increasing order, $d_1 \ge d_2 \ge \dots \ge d_n \ge 0$, is graphic if and only if the sum of the degrees is even and for every integer $k$ from $1$ to $n$, the following inequality holds:

$$ \sum_{i=1}^{k} d_i \le k(k-1) + \sum_{i=k+1}^{n} \min(k, d_i) $$

If the parity condition holds and this inequality is satisfied for all $n$ values of $k$, the sequence is guaranteed to be graphic. Conversely, if the inequality fails for even a single value of $k$, the sequence is not graphic [@problem_id:1509399].

#### Deconstructing the Inequality: A Balance of Demand and Supply

The Erdős-Gallai inequality may appear opaque, but it has a clear, intuitive interpretation based on partitioning the vertices and balancing the "demand" for connections against the available "supply".

For any given integer $k$ ($1 \le k \le n$), let's divide the vertices of our hypothetical graph into two sets: a **core set** $V_k = \{v_1, v_2, \dots, v_k\}$ corresponding to the $k$ vertices with the highest degrees, and a **peripheral set** $V_{>k} = \{v_{k+1}, \dots, v_n\}$ containing the remaining $n-k$ vertices.

The **left-hand side (LHS)** of the inequality, $\sum_{i=1}^{k} d_i$, represents the total number of connections demanded by the vertices in the core set. Each edge connected to a vertex in $V_k$ uses up one "degree unit" from that vertex. The sum is the total number of such units that must be satisfied.

The **right-hand side (RHS)** represents the maximum possible number of connections that can be made to the vertices in the core set, from any source. This supply of connections comes from two places:

1.  **Internal Connections:** Edges connecting two vertices *within* the core set $V_k$. The maximum number of edges possible in a [simple graph](@entry_id:275276) on $k$ vertices is $\binom{k}{2}$. Since each edge contributes 2 to the total degree sum within the set, the maximum degree sum that can be accounted for by internal connections is $2 \binom{k}{2} = k(k-1)$. This term represents the maximum capacity for connections entirely among the core servers [@problem_id:1501527] [@problem_id:1501502].

2.  **External Connections:** Edges connecting a vertex in the core set $V_k$ to a vertex in the peripheral set $V_{>k}$. Consider a peripheral vertex $v_j$ (where $j > k$). It can connect to at most $k$ vertices (all of the vertices in $V_k$). Furthermore, its total number of connections is limited by its degree, $d_j$. Therefore, the maximum number of connections that vertex $v_j$ can provide to the core set is $\min(k, d_j)$. Summing this over all vertices in the periphery gives the term $\sum_{i=k+1}^{n} \min(k, d_i)$, which represents the total connection capacity offered by the peripheral set [@problem_id:1501502].

The Erdős-Gallai inequality, therefore, makes a simple, powerful statement: for any $k$, the total connection demand from the $k$ highest-degree vertices cannot exceed the maximum possible supply of connections, which is the sum of the maximum internal capacity and the maximum external capacity.

### Applying the Theorem: Verification and Analysis

To test if a sequence is graphic, one must first check the parity and degree bounds, and then systematically verify the Erdős-Gallai inequality for every $k=1, \dots, n$.

#### Example of a Non-Graphic Sequence

Let's examine the sequence $D = (6, 6, 5, 4, 3, 3, 1)$ with $n=7$ [@problem_id:1501522].
The sum of degrees is $28$, which is even. The max degree is $6$, which satisfies $d_1 \le n-1=6$. The simple checks pass. We now proceed with the Erdős-Gallai inequalities. Let's calculate the "excess" $E(k) = \max(0, \text{LHS} - \text{RHS})$ for each $k$.

For $k=1$: $\sum d_i = 6$. RHS is $1(0) + \sum_{i=2}^7 \min(1, d_i) = 0 + (1+1+1+1+1+1) = 6$. LHS $\le$ RHS. $E(1)=0$.

For $k=2$: $\sum d_i = 6+6=12$. RHS is $2(1) + \sum_{i=3}^7 \min(2, d_i) = 2 + (2+2+2+2+1) = 11$. Here, $12 \not\le 11$. The inequality fails. $E(2)=1$.

For $k=3$: $\sum d_i = 12+5=17$. RHS is $3(2) + \sum_{i=4}^7 \min(3, d_i) = 6 + (3+3+3+1) = 16$. Here, $17 \not\le 16$. The inequality fails. $E(3)=1$.

For $k=4$: $\sum d_i = 17+4=21$. RHS is $4(3) + \sum_{i=5}^7 \min(4, d_i) = 12 + (3+3+1) = 19$. Here, $21 \not\le 19$. The inequality fails. $E(4)=2$.

Since the inequality fails for $k=2, 3, 4$, the sequence is not graphic. The failure at $k=4$ is the most severe, with an excess of 2.

The physical meaning of such a failure is profound. Consider the sequence $D = (7, 7, 7, 7, 1, 1, 1, 1)$ for $n=8$ [@problem_id:1501527]. For $k=4$, the four highest-degree vertices have a total degree demand of $7 \times 4 = 28$. The four [peripheral vertices](@entry_id:264062) have a total degree sum of $1 \times 4 = 4$. They can at most contribute 4 edges to the core set. This means $28-4 = 24$ degree units must be satisfied by edges *within* the core set. Since each internal edge accounts for 2 degree units, this requires $24/2 = 12$ edges among the four core vertices. However, a simple graph on 4 vertices can have at most $\binom{4}{2} = 6$ edges. The requirement of 12 edges exceeds the absolute maximum of 6, demonstrating the impossibility. This is precisely what the Erdős-Gallai inequality detects.

#### Example of a Graphic Sequence

Now let's find the largest integer $x$ such that the sequence $D = (10, 8, 7, 6, 5, 5, 4, 3, 2, 2, x)$ is graphic, for $n=11$ and $0 \le x \le 2$ [@problem_id:1501532].
The sum of the first 10 terms is 52. For the total sum $52+x$ to be even, $x$ must be even. So, $x$ can be 0 or 2. We test the larger candidate, $x=2$.
The sequence is $(10, 8, 7, 6, 5, 5, 4, 3, 2, 2, 2)$. The sum is 54 (even). We must check the inequality for $k=1, \dots, 11$.

For $k=1$: $10 \le 1(0) + (1+1+1+1+1+1+1+1+1+1) = 10$. (Holds)
For $k=2$: $18 \le 2(1) + (2+2+2+2+2+2+2+2+2) = 2+18=20$. (Holds)
For $k=3$: $25 \le 3(2) + (3+3+3+3+2+2+2+2) = 6+20=26$. (Holds)
...and so on. A full verification (as performed in [@problem_id:1501532]) shows that the inequality holds for all $k \le 11$. Therefore, the sequence with $x=2$ is graphic, and the largest such value for $x$ is 2. The verification process, while tedious, is computationally straightforward.

#### Special Insights from the Theorem

The Erdős-Gallai framework also encapsulates more basic graph properties. Consider the case $k=1$. The inequality becomes:
$$ d_1 \le 1(0) + \sum_{i=2}^{n} \min(1, d_i) $$
The term $\min(1, d_i)$ is 1 if $d_i \ge 1$ and 0 if $d_i = 0$. So, the sum on the right simply counts the number of vertices (other than $v_1$) that have a degree of at least 1. At most, there can be $n-1$ such vertices. This leads directly to the conclusion:
$$ d_1 \le n-1 $$
This shows that the fundamental degree bound is a direct consequence of the Erdős-Gallai condition for $k=1$ [@problem_id:1501551].

This theorem can be used alongside other tools. In some cases, determining an unknown degree in a sequence can be solved by checking the necessary conditions and then using a constructive method like the **Havel-Hakimi algorithm**, which recursively simplifies the sequence. If the process completes without generating negative degrees, the sequence is graphic [@problem_id:1501540] [@problem_id:1501548]. While Erdős-Gallai provides an existence criterion, Havel-Hakimi offers a method of construction.

### The Structural Meaning of the Equality Condition

The true power of the Erdős-Gallai theorem is revealed when we consider the case where the inequality holds with equality for some $k  n$.
$$ \sum_{i=1}^k d_i = k(k-1) + \sum_{i=k+1}^n \min(k, d_i) $$
This equality is not just a numerical curiosity; it imposes rigid structural constraints on any graph that realizes the [degree sequence](@entry_id:267850) [@problem_id:1501563].

Recall our interpretation of the RHS as the sum of two maximum capacities. For the overall equality to hold, both capacities must be met exactly.
1.  The total degree contribution from edges *within* the core set $V_k$, which is $2e(V_k)$, must equal its maximum possible value, $k(k-1)$. This implies $e(V_k) = \binom{k}{2}$.
2.  The total number of edges between the core set $V_k$ and the peripheral set $V_{k}$, which is $e(V_k, V_{k})$, must equal its maximum possible value, $\sum_{i=k+1}^n \min(k, d_i)$.

These two conditions force the following structure on any [graph realization](@entry_id:270634) $G$:
- **The [subgraph](@entry_id:273342) induced by the core vertices $V_k$ must be a complete graph ($K_k$).** Every vertex in the core must be connected to every other vertex in the core.
- **Each peripheral vertex $v_j \in V_{k}$ must connect to exactly $\min(k, d_j)$ vertices in the core.** The connections from the periphery to the core are completely saturated.
- Consequently, all remaining edges for vertices in $V_{k}$ must be among themselves. The degree of vertex $v_j$ within the [subgraph](@entry_id:273342) induced by $V_{k}$ is exactly $d_j - \min(k, d_j) = \max(0, d_j-k)$.

This remarkable result shows that the Erdős-Gallai inequality is deeply tied to the decomposability of a graph. An equality at index $k$ signifies that the graph must split cleanly into a core [clique](@entry_id:275990) and a periphery, with a maximally dense set of connections between them. This elevates the theorem from a mere numerical check to a profound statement about graphical structure.