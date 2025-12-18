## Introduction
The Unbounded Knapsack Problem and the Coin Change Problem are foundational topics in computer science, serving as classic illustrations of the power and elegance of [dynamic programming](@entry_id:141107). As core problems in [combinatorial optimization](@entry_id:264983), they model countless scenarios involving resource allocation and combination counting. However, students and practitioners often face a knowledge gap: while the basic concept may be familiar, the subtle but critical differences between variants—such as minimizing coins, counting unique combinations, or counting ordered [permutations](@entry_id:147130)—can be confusing, as each requires a distinct algorithmic approach.

This article bridges that gap by providing a systematic exploration of these problems and their solutions. In the first chapter, **"Principles and Mechanisms,"** we will build the [dynamic programming](@entry_id:141107) solutions from the ground up, deriving the [recurrence relations](@entry_id:276612) for the Unbounded Knapsack problem and its various Coin Change specializations. Next, **"Applications and Interdisciplinary Connections"** will reveal how these abstract models are used to solve tangible problems in fields ranging from [computational biology](@entry_id:146988) to finance. Finally, **"Hands-On Practices"** will challenge you to apply and extend your knowledge with a curated set of exercises that push the boundaries of the basic models. By the end, you will have a deep, versatile understanding of how to recognize and solve this important class of problems.

## Principles and Mechanisms

The Unbounded Knapsack Problem (UKP) and its close relative, the Coin Change Problem, are cornerstones of [combinatorial optimization](@entry_id:264983) and serve as exemplary models for the application of **[dynamic programming](@entry_id:141107)**. This powerful algorithmic technique solves complex problems by breaking them down into simpler, [overlapping subproblems](@entry_id:637085), solving each subproblem just once, and storing their solutions in a memory-based data structure (a "table") to avoid redundant computation. The validity of this approach rests on the **Principle of Optimality**, which asserts that an optimal solution to a problem can be constructed from optimal solutions to its subproblems.

In this chapter, we will derive the fundamental [dynamic programming](@entry_id:141107) solutions for these problems from first principles. We will begin with the general form of the Unbounded Knapsack Problem, then specialize it to the various forms of the Coin Change Problem, and finally, explore advanced extensions and a comparison with alternative algorithmic strategies.

### The Unbounded Knapsack Problem: Maximizing Value

The Unbounded Knapsack Problem provides a general framework for resource allocation under constraints. Imagine a scenario where a gambler has a variety of games to play. Each game requires a specific wager and offers a specific payout. The gambler has a total bankroll and can play any game as many times as they wish. The goal is to choose a combination of plays that maximizes the total payout without exceeding the bankroll .

Formally, we have a set of $n$ items. Each item $i$ has a **weight** $w_i$ (the wager) and a **value** $v_i$ (the payout). Given a knapsack with a maximum capacity $W$ (the bankroll), we want to select a quantity $x_i \ge 0$ of each item to maximize the total value, subject to the total weight not exceeding the capacity. The term "unbounded" signifies that the quantities $x_i$ are not limited to 0 or 1; we can take any number of copies of each item.

The optimization problem is:
$$
\text{Maximize } \sum_{i=1}^{n} v_i x_i \quad \text{subject to} \quad \sum_{i=1}^{n} w_i x_i \le W, \quad x_i \in \mathbb{Z}_{\ge 0}
$$

To solve this using dynamic programming, we must define a state that captures the structure of the subproblems. A natural choice is to define a function, let's call it $dp[c]$, that represents the maximum achievable value for a knapsack of capacity exactly $c$. Our ultimate goal is to find $dp[W]$.

The **base case** is self-evident: with a capacity of $0$, no items can be placed in the knapsack, so the maximum value is $0$.
$$
dp[0] = 0
$$

For any capacity $c > 0$, an optimal solution can be constructed by making a final, optimal choice. Suppose in an optimal packing for capacity $c$, one of the items included is item $j$. If we remove that single item $j$, the remaining items must constitute an optimal packing for the remaining capacity, which is $c - w_j$. The value contributed by this configuration is thus $v_j + dp[c - w_j]$. Since we do not know which item $j$ is the best final choice, we must consider all possibilities. We can try adding each possible item $i$ (where $w_i \le c$) to an optimal solution for capacity $c - w_i$ and take the best outcome. This leads to the **[recurrence relation](@entry_id:141039)**:

$$
dp[c] = \max_{i \,:\, w_i \le c} \{ v_i + dp[c - w_i] \}
$$

This relation can be implemented using a **bottom-up approach**. We construct a one-dimensional array (our DP table) of size $W+1$ and compute the values of $dp[c]$ for $c = 1, 2, \dots, W$. For each capacity $c$, we iterate through all available items to find the maximum possible value.

The algorithm is as follows:
1.  Create an array `dp` of size $W+1$ and initialize all its entries to $0$.
2.  Iterate for each capacity $c$ from $1$ to $W$.
3.  For each capacity $c$, iterate through each item $i$ from $1$ to $n$.
4.  If the item's weight $w_i$ is less than or equal to the current capacity $c$, consider the possibility of including it. Update the value for capacity $c$:
    $$ dp[c] = \max(dp[c], v_i + dp[c - w_i]) $$

After the loops complete, $dp[W]$ will hold the maximum value for a capacity of $W$. Note that this formulation inherently handles the $\le W$ constraint, as the value for a capacity $c$ can be carried over from $c-1$ if no item is added (which is implicitly handled by the max operation against the existing $dp[c]$ value if it were propagated from $dp[c-1]$). The standard implementation above is sufficient. The [time complexity](@entry_id:145062) is $O(n \cdot W)$ and the [space complexity](@entry_id:136795) is $O(W)$.

### The Coin Change Problem: Key Variants

The Coin Change Problem can be viewed as a family of special cases of the Unbounded Knapsack Problem. Here, the "weights" are the coin denominations, and the "capacity" is the target amount $N$ we wish to form. However, the objective can vary, leading to different problems that require subtle but crucial modifications to the DP formulation .

#### Minimizing the Number of Coins

The most common variant is to find the minimum number of coins that sum to a target amount $N$. This is an optimization problem directly analogous to the UKP.

- **Objective**: Minimize $\sum_{i=1}^{n} x_i$
- **Constraint**: $\sum_{i=1}^{n} c_i x_i = N$

Here, $c_i$ is the denomination of coin type $i$, and $x_i$ is the number of coins of that type used. This problem is equivalent to an Unbounded Knapsack problem where every item has a value of $1$, and we seek to fill the knapsack *exactly* to capacity $N$ while minimizing the total value (which is the count of items).

We define our DP state $dp[a]$ as the minimum number of coins required to make change for amount $a$.
- **Base Case**: To form an amount of $0$, we need $0$ coins. So, $dp[0] = 0$.
- **Initialization**: For all other amounts $a > 0$, we initialize $dp[a] = \infty$ to signify that we have not yet found a way to form them. This large value will be replaced as soon as a valid coin combination is found.
- **Recurrence Relation**: Similar to the UKP, any optimal solution for amount $a$ must have a last coin, say $c_i$. Removing it leaves an [optimal solution](@entry_id:171456) for amount $a - c_i$. The total number of coins is $1 + dp[a - c_i]$. We minimize over all possible last coins:
$$
dp[a] = \min_{i \,:\, c_i \le a} \{ 1 + dp[a - c_i] \}
$$

The bottom-up implementation is straightforward and follows the UKP structure. If, after completing the process, $dp[N]$ remains $\infty$, it means the amount $N$ is impossible to form with the given denominations.

#### Counting Combinations (Order Doesn't Matter)

A fundamentally different objective is to count the number of distinct ways to make change for amount $N$. Here, "distinct ways" refers to combinations of coins, meaning the order in which coins are selected does not matter. For example, the multiset of coins $\{2, 3, 5\}$ is one way to make change for 10, and it is considered the same as $\{5, 3, 2\}$.

This can be stated formally as finding the number of distinct sequences of coins $\langle c_1, \dots, c_k \rangle$ that sum to $N$ and are sorted in non-decreasing order . This sorted sequence is a [canonical representation](@entry_id:146693) for the multiset.

To solve this, we must design our DP update step carefully to avoid counting [permutations](@entry_id:147130). Let $dp[a]$ be the number of ways to make change for amount $a$.
- **Base Case**: There is exactly one way to form the amount $0$: by choosing no coins. So, $dp[0] = 1$.
- **Recurrence and Implementation**: The key insight is to build the solution by considering one coin denomination at a time. We iterate through each coin $c_i$ in our set of denominations. For each coin, we update the `dp` table for all amounts that this coin can contribute to.

The algorithm is:
1.  Create an array `dp` of size $N+1$. Initialize $dp[0] = 1$ and $dp[a] = 0$ for $a > 0$.
2.  For each coin denomination $c_i$ in the set:
3.  For each amount $a$ from $c_i$ to $N$:
    $$ dp[a] = dp[a] + dp[a - c_i] $$

Let's analyze why this loop structure works. When we process coin $c_i$, we are adding new combinations that include at least one $c_i$. These are formed by taking existing combinations for a smaller amount, $a - c_i$, and adding a coin $c_i$. The crucial detail is that the combinations for $a - c_i$ could *only* have been formed by coins processed *before* $c_i$ (or other coins of type $c_i$ due to the single DP array). By enforcing this order of processing denominations (the outer loop), we ensure that each multiset of coins is generated in exactly one canonical order (e.g., sorted by denomination), thus preventing overcounting.

#### Counting Permutations (Order Matters)

What if the order of coins *does* matter? For instance, in a game where scores are accumulated, the sequence of scores $(2, 3)$ might be different from $(3, 2)$ . We are now counting ordered sequences, not multisets.

The DP state definition remains the same: $dp[a]$ is the number of ordered sequences that sum to $a$. The [base case](@entry_id:146682) is also the same: $dp[0] = 1$ (for the empty sequence). However, the [recurrence relation](@entry_id:141039) changes its interpretation, leading to a different loop structure.

- **Recurrence Relation**: An ordered sequence summing to $a$ must have a last element. This last element could be any coin $c_i$ (where $c_i \le a$). If the last coin is $c_i$, the preceding part of the sequence must sum to $a - c_i$. The number of ways to form such a preceding sequence is $dp[a-c_i]$. By the rule of addition, we can sum over all possibilities for the last coin:
$$
dp[a] = \sum_{i \,:\, c_i \le a} dp[a - c_i]
$$
- **Implementation**: To implement this, we must swap the order of the loops compared to the combination counting problem.

The algorithm is:
1.  Create an array `dp` of size $N+1$. Initialize $dp[0] = 1$ and all other entries to $0$.
2.  For each amount $a$ from $1$ to $N$:
3.  For each coin denomination $c_i$ in the set:
4.  If $a \ge c_i$:
    $$ dp[a] = dp[a] + dp[a - c_i] $$

By making the outer loop iterate over amounts $a$, we ensure that when we compute $dp[a]$, all values $dp[j]$ for $j  a$ are final. The inner loop then correctly sums up the contributions from all possible preceding sequences, regardless of which coin was used last in those sub-solutions. This correctly counts all [permutations](@entry_id:147130).

### Extending the Dynamic Programming Models

The true power of dynamic programming lies in its adaptability. The fundamental models we have discussed can be extended to handle a wide array of additional constraints by augmenting the DP state or combining DP with other techniques.

#### Augmenting the DP State

Consider a problem where we must count the ways to make change for $N$, but only those combinations that use an **even number of coins** are valid . A simple `dp[a]` state is no longer sufficient, as we cannot determine if adding a coin will lead to a valid (even) or invalid (odd) total count without knowing the parity of the coin count for the subproblem.

The solution is to **augment the state** to track this extra piece of information. We define a 2D DP table:
- $dp[a][0]$: the number of ways to make amount $a$ using an even number of coins.
- $dp[a][1]$: the number of ways to make amount $a$ using an odd number of coins.

The base case is $dp[0][0] = 1$ (zero coins is an even count) and $dp[0][1] = 0$. The recurrence relations are updated accordingly. When we add a coin to a sub-solution for amount $a-c_i$, the parity flips:
- An even-count solution for $a-c_i$ becomes an odd-count solution for $a$.
- An odd-count solution for $a-c_i$ becomes an even-count solution for $a$.

This leads to the following update rules within the standard combination-counting loop structure (outer loop over coins):
$$
dp[a][0] \leftarrow dp[a][0] + dp[a-c_i][1] \\
dp[a][1] \leftarrow dp[a][1] + dp[a-c_i][0]
$$
The final answer is simply $dp[N][0]$. This principle of [state augmentation](@entry_id:140869) is broadly applicable to many problems with side constraints.

#### Hybrid Approaches: DP with Enumeration

Sometimes, a problem contains a mix of unbounded and bounded constraints. For instance, what if we need to find the minimum number of coins to make change for $N$, but one specific denomination $d_k$ can be used at most $L$ times, while all others remain unlimited? 

A direct DP formulation becomes complicated. A more elegant solution is a **hybrid approach**. We can isolate the constrained element and enumerate its possibilities. Here, the special coin $d_k$ can be used $j$ times, where $j \in \{0, 1, \dots, L\}$. For each fixed choice of $j$, the problem reduces to a standard one:
1.  Assume we use coin $d_k$ exactly $j$ times.
2.  These $j$ coins contribute a value of $j \cdot d_k$ and a count of $j$.
3.  The remaining amount to form is $N' = N - j \cdot d_k$.
4.  This amount $N'$ must be formed using the *other*, unconstrained coins, minimizing their count. This is the standard coin change minimization problem.

The overall algorithm is:
1.  First, solve the standard unbounded coin change minimization problem for all amounts up to $N$ using only the *unconstrained* coins. Store these results in a DP table, say `dp_unconstrained`.
2.  Initialize the minimum total coins found so far to $\infty$.
3.  Iterate $j$ from $0$ to $L$:
    a. Calculate the remaining amount $N' = N - j \cdot d_k$.
    b. If $N' \ge 0$ and `dp_unconstrained[N']` is not $\infty$, a solution is possible.
    c. The total coins for this case is $j + \text{dp\_unconstrained}[N']$.
    d. Update the overall minimum with this value.
4.  The final result is the overall minimum found.

This decomposition strategy is extremely effective when a constraint applies to a small, enumerable part of the problem.

#### Advanced State Transitions for Complex Costs

Consider a variant where using any coin of type $i$ (denomination $d_i$) incurs a one-time "production cost" $p_i$. The goal is to minimize the sum of the coin count and the total production costs incurred .

This fixed cost component complicates the standard recurrence because the cost of adding a coin depends on whether a coin of its type has already been used. We can handle this by processing coin types one by one and maintaining two DP tables during each step. Let `dp[a]` be the minimum cost to make amount `a` using the coin types processed so far. When we introduce a new coin type $(d, p)$:

1.  We compute a temporary table, `temp_dp[a]`, representing the minimum cost to make amount `a` *given that at least one coin of type $(d,p)$ is used*.
2.  To compute `temp_dp[a]`, we consider two possibilities for forming `a` with the new coin:
    - **First use**: We take a solution for $a-d$ from the main `dp` table (which used only prior coins), and add the first coin $(d,p)$. Cost: `dp[a-d] + p + 1`.
    - **Subsequent use**: We take a solution for $a-d$ from the `temp_dp` table (which by definition already used coin $(d,p)$), and add another. Cost: `temp_dp[a-d] + 1`.
    The value `temp_dp[a]` is the minimum of these two.
3.  After computing the `temp_dp` table, we update our main `dp` table. The new optimal cost for amount `a`, `dp_new[a]`, is the minimum of the old cost (not using coin $(d,p)$ at all) and the cost from the temporary table (using coin $(d,p)$).
    $$
    dp_{new}[a] = \min(dp_{old}[a], temp\_dp[a])
    $$
This [iterative refinement](@entry_id:167032) correctly captures the state-dependent fixed costs and demonstrates a sophisticated DP technique.

### Dynamic Programming vs. Greedy Algorithms

Given the computational cost of dynamic programming, typically $O(n \cdot W)$, it is natural to ask if a simpler, faster approach might suffice. A **greedy algorithm** is one such alternative. It builds a solution by repeatedly making a locally optimal choice—for example, always taking the largest denomination coin that is less than or equal to the remaining amount.

While appealing, [greedy algorithms](@entry_id:260925) do not guarantee a globally optimal solution for all problems. Their correctness depends on the problem possessing the **[greedy-choice property](@entry_id:634218)**.

Consider the Unbounded Knapsack Problem with weights that are powers of two (e.g., $1, 2, 4, 8, \dots$) . A greedy strategy might be to select items corresponding to the binary representation of the capacity $W$. If item values are arbitrary, this can fail spectacularly. For a capacity $W=4$, with items of weights $\{1, 2, 4\}$ and values $\{3, 5, 8\}$, the greedy choice is one item of weight 4, for a value of 8. The optimal solution, however, is two items of weight 2, for a value of $5+5=10$. In fact, one can construct examples where the ratio of the greedy solution's value to the optimal value is arbitrarily close to zero. However, if the values are proportional to the weights (e.g., $v_i = \alpha \cdot w_i$), the greedy strategy of maximizing the total weight used *is* optimal.

For the coin change minimization problem, the standard greedy approach is only optimal for certain "canonical" coin systems. Most real-world currency systems (like USD or Euro) are canonical. Another interesting example is a system composed of Fibonacci numbers . For denominations $\{1, 2, 3, 5, 8, \dots\}$, the [greedy algorithm](@entry_id:263215) of always taking the largest possible Fibonacci coin is guaranteed to produce a solution with the minimum number of coins. This algorithm runs in $O(\log N)$ time, far outperforming the $O(N \cdot |D|)$ DP solution.

In conclusion, dynamic programming is the more general and robust tool. It guarantees optimality for this entire class of problems. A greedy algorithm should only be employed when the problem is known to have the specific structure required for it to work. When in doubt, the systematic exploration offered by dynamic programming is the correct and reliable path to a solution.