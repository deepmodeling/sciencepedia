## Introduction
Many of the most important problems in science and engineering, from designing efficient networks to analyzing complex data, fall under the umbrella of [combinatorial optimization](@entry_id:264983). While some of these problems can be solved efficiently, a vast and significant class, known as NP-hard problems, defy all known algorithms for finding exact solutions in a reasonable timeframe. The Maximum Cut (Max-Cut) problem is a classic example: despite its simple description, finding the optimal partition of a graph is notoriously difficult. This intractability creates a critical knowledge gap, demanding powerful techniques that can provide high-quality, provably good approximate solutions.

This article introduces [semidefinite relaxation](@entry_id:635087), a profound and elegant framework that has revolutionized the field of [approximation algorithms](@entry_id:139835). By bridging discrete [combinatorics](@entry_id:144343) with continuous [convex optimization](@entry_id:137441), this method offers a principled way to tackle otherwise intractable problems. Over the next three chapters, you will gain a deep understanding of this powerful tool.
- **Principles and Mechanisms** will demystify the core strategy of "lifting and relaxing," explain its beautiful geometric interpretation, and detail the celebrated Goemans-Williamson rounding algorithm that turns a relaxed solution back into a concrete answer.
- **Applications and Interdisciplinary Connections** will showcase the remarkable versatility of semidefinite relaxations, exploring their use in machine learning, computer vision, robotics, and [computational logic](@entry_id:136251).
- **Hands-On Practices** will provide an opportunity to apply these concepts, guiding you through the process of formulating, solving, and analyzing SDP relaxations for concrete optimization tasks.

We begin by delving into the fundamental principles that make [semidefinite relaxation](@entry_id:635087) one of the most powerful techniques in modern optimization.

## Principles and Mechanisms

Many of the most challenging and consequential problems in computer science, [operations research](@entry_id:145535), and engineering can be framed as [combinatorial optimization](@entry_id:264983) problems. These problems involve finding an optimal object from a finite, but often exponentially large, set of possible objects. A canonical example is the **Maximum Cut (Max-Cut)** problem on a weighted [undirected graph](@entry_id:263035) $G = (V,E)$. The goal is to partition the set of vertices $V$ into two disjoint subsets, say $S_1$ and $S_2$, such that the sum of the weights of the edges crossing between $S_1$ and $S_2$ is maximized.

To formalize this, we can assign a variable $x_i \in \{-1, 1\}$ to each vertex $i \in V$, where the value indicates which side of the partition the vertex belongs to. An edge $(i,j)$ with weight $w_{ij} \ge 0$ is "cut" if and only if vertices $i$ and $j$ are on opposite sides, which corresponds to the condition $x_i x_j = -1$. The term $\frac{1}{2}(1 - x_i x_j)$ is equal to $1$ if the edge is cut and $0$ otherwise. The Max-Cut problem is thus equivalent to the following [quadratically constrained quadratic program](@entry_id:636709) (QP):

$$
\max_{x \in \mathbb{R}^n} \quad \sum_{(i,j) \in E} w_{ij} \frac{1 - x_i x_j}{2} \quad \text{subject to} \quad x_i^2 = 1 \text{ for all } i \in V.
$$

This problem is known to be **NP-hard**, meaning there is no known algorithm that can solve it to optimality for all graphs in polynomial time. This difficulty contrasts sharply with the related **Minimum Cut (Min-Cut)** problem, which asks for a partition that minimizes the weight of the cut. Min-Cut is polynomially solvable. This tractability stems from the fact that the cut function is **submodular**, a property that lends itself to exact solutions via convex [optimization methods](@entry_id:164468), such as linear programming (LP). The famous [max-flow min-cut theorem](@entry_id:150459), for instance, is a manifestation of strong LP duality, where the LP relaxation of the [min-cut problem](@entry_id:275654) has integer solutions . Maximizing a submodular function, as Max-Cut effectively does, is generally hard. This dichotomy between minimization and maximization of the same underlying structure motivates the need for different algorithmic tools for NP-hard problems like Max-Cut. The primary tool we will explore is that of [semidefinite relaxation](@entry_id:635087).

### The Lifting and Relaxation Strategy

The difficulty in the Max-Cut QP formulation arises from the combination of a quadratic objective and the discrete constraints $x_i \in \{-1, 1\}$. The core idea of [semidefinite relaxation](@entry_id:635087) is to transform this non-convex problem into a convex one that we can solve efficiently. This is achieved through a two-step process: **lifting** and **relaxation**.

First, we "lift" the problem from the vector space $\mathbb{R}^n$ of the variables $x$ to the matrix space $\mathbb{S}^n$ of $n \times n$ [symmetric matrices](@entry_id:156259). We define a matrix $X$ whose entries are the products of the components of $x$, i.e., $X_{ij} = x_i x_j$. In vector notation, this is $X = xx^\top$. The objective function, which is quadratic in $x$, becomes linear in $X$. Let $L$ be the **graph Laplacian**, defined as $L = D - W$, where $W$ is the weighted [adjacency matrix](@entry_id:151010) and $D$ is the diagonal matrix of weighted degrees ($D_{ii} = \sum_j w_{ij}$). The Max-Cut objective can be expressed as $\frac{1}{4} x^\top L x$ . Using the [trace operator](@entry_id:183665) property $\text{Tr}(A B) = \text{Tr}(B A)$, we can write:

$$
\frac{1}{4} x^\top L x = \frac{1}{4} \text{Tr}(x^\top L x) = \frac{1}{4} \text{Tr}(L xx^\top) = \frac{1}{4} \text{Tr}(LX).
$$

The constraints on $x$ translate to constraints on $X$. The condition $x_i^2 = 1$ implies that the diagonal entries of $X$ must be one: $X_{ii} = x_i^2 = 1$. The definition $X = xx^\top$ implies that $X$ must be a symmetric, [positive semidefinite matrix](@entry_id:155134) of rank one. The original Max-Cut problem is therefore equivalent to:

$$
\max_{X \in \mathbb{S}^n} \quad \frac{1}{4} \text{Tr}(LX) \quad \text{subject to} \quad \text{diag}(X) = \mathbf{1}, \quad X \succeq 0, \quad \text{rank}(X) = 1.
$$

The constraint $\text{rank}(X)=1$ is non-convex and encapsulates the entire difficulty of the problem. Re-imposing this constraint on a [convex relaxation](@entry_id:168116) immediately returns the problem to its original NP-hard state .

The second step, **relaxation**, is to drop this difficult non-convex rank constraint. This yields the celebrated **Goemans-Williamson [semidefinite programming](@entry_id:166778) (SDP) relaxation**:

$$
\max_{X \in \mathbb{S}^n} \quad \frac{1}{4} \text{Tr}(LX) \quad \text{subject to} \quad \text{diag}(X) = \mathbf{1}, \quad X \succeq 0.
$$

This is a semidefinite program because it involves optimizing a linear function over the intersection of an affine subspace and the convex cone of [positive semidefinite matrices](@entry_id:202354). Such problems can be solved to arbitrary precision in [polynomial time](@entry_id:137670). The optimal value of this SDP, let's call it $s^\star_{\text{SDP}}$, provides an upper bound on the true optimal value of the Max-Cut, $z^\star$, because we are optimizing over a larger feasible set.

### The Geometry of Relaxation

To gain deeper insight into why this relaxation is powerful, we must understand its geometry. A fundamental result in linear algebra states that a [symmetric matrix](@entry_id:143130) $X$ is positive semidefinite if and only if it is a **Gram matrix**. That is, there exist vectors $v_1, \dots, v_n$ in some Euclidean space $\mathbb{R}^k$ (with $k \le n$) such that $X_{ij} = v_i^\top v_j$ for all $i,j$.

Under this interpretation, the SDP relaxation takes on a beautiful geometric form  . The constraint $\text{diag}(X) = \mathbf{1}$ means $X_{ii} = v_i^\top v_i = \|v_i\|^2 = 1$, so each $v_i$ must be a [unit vector](@entry_id:150575). The [objective function](@entry_id:267263) becomes:

$$
\max \quad \sum_{(i,j) \in E} w_{ij} \frac{1 - v_i^\top v_j}{2} \quad \text{subject to} \quad \|v_i\|=1 \text{ for all } i \in V.
$$

In the original problem, the "vectors" $x_i$ were constrained to be in $\{-1, 1\}$, which are unit vectors in a one-dimensional space. The SDP relaxation allows these vectors to "live" in a higher-dimensional space, relaxing the constraints on their relative orientations. Instead of being restricted to be collinear (either identical or antipodal), they can now "fan out" on the surface of a unit hypersphere. This enlargement of the search space is what makes the problem tractable.

The relationship between the exact problem and its relaxation can be characterized by their feasible sets. Let $C = \{xx^\top : x \in \{-1,1\}^n\}$ be the set of matrices corresponding to actual cuts. The feasible set of the SDP is the **elliptope**, $\mathcal{E} = \{X \in \mathbb{S}^n : X \succeq 0, \text{diag}(X) = \mathbf{1}\}$. Since each matrix in $C$ is positive semidefinite and has ones on the diagonal, we have $C \subseteq \mathcal{E}$. Because $\mathcal{E}$ is a [convex set](@entry_id:268368), it must also contain the convex hull of $C$, denoted $\text{conv}(C)$. Therefore, $\text{conv}(C) \subseteq \mathcal{E}$ .

This inclusion is often strict. Optimizing a linear function over $\text{conv}(C)$ would solve Max-Cut exactly, but obtaining a simple description of $\text{conv}(C)$ (known as the **cut polytope**) is itself an NP-hard problem. The SDP relaxation provides a tractable outer approximation. The difference between optimizing over $\mathcal{E}$ versus $\text{conv}(C)$ gives rise to an **[integrality gap](@entry_id:635752)**.

A classic example arises with [odd cycles](@entry_id:271287). Consider an unweighted [path graph](@entry_id:274599) on 4 vertices, $P_4$. This graph is bipartite, and its [max-cut](@entry_id:271899) is 3 (all its edges can be cut). An optimal SDP solution can be constructed by assigning antipodal vectors to vertices in opposite partitions (e.g., $v_1=v_3$ and $v_2=v_4=-v_1$), yielding an SDP value of 3. The relaxation is exact. Now, add an edge $(1,3)$ to form a graph $H$ containing a 3-cycle. The [max-cut](@entry_id:271899) is still 3 (at most 2 edges of a triangle can be cut). However, the SDP can achieve a higher value. A feasible SDP solution places vectors $v_1, v_2, v_3$ in a plane at $120^\circ$ angles to each other ($v_i^\top v_j = \cos(2\pi/3) = -1/2$). The contribution to the SDP objective from each edge in the triangle is $\frac{1 - (-1/2)}{2} = 3/4$. For a 3-cycle, the SDP value is $3 \times (3/4) = 9/4 = 2.25$, while the true [max-cut](@entry_id:271899) is 2. This gap of $0.25$ is a direct consequence of the geometric freedom afforded by the relaxation .

### From Relaxation to Solution: The Rounding Step

Solving the SDP yields an optimal matrix $X^\star$ (or, equivalently, a set of [unit vectors](@entry_id:165907) $\{v_i\}$), but this is a solution to the *relaxed* problem. We still need to produce a discrete partition, i.e., a vector $x \in \{-1, 1\}^n$. This process is known as **rounding**.

The celebrated rounding technique proposed by Goemans and Williamson is **randomized [hyperplane](@entry_id:636937) rounding**. The procedure is simple and elegant:
1. Solve the SDP to obtain the optimal vectors $\{v_i\}_{i=1}^n$ lying on a unit sphere in $\mathbb{R}^k$.
2. Choose a random hyperplane through the origin. This is done by drawing a [normal vector](@entry_id:264185) $r$ uniformly from the surface of the unit sphere.
3. Partition the vertices based on which side of the [hyperplane](@entry_id:636937) their corresponding vector lies: assign $x_i = \text{sign}(r^\top v_i)$.

The power of this method lies in its provable performance guarantee. The probability that two vertices $i$ and $j$ are separated by the random cut depends only on the angle between their vectors $v_i$ and $v_j$. Geometrically, the random [hyperplane](@entry_id:636937) separates $v_i$ and $v_j$ if and only if its [normal vector](@entry_id:264185) $r$ falls within the two sectors defined by the planes orthogonal to $v_i$ and $v_j$. The total angle of these sectors is $2\theta_{ij}$, where $\theta_{ij} = \arccos(v_i^\top v_j)$ is the angle between the vectors. As the random normal is uniformly distributed over the sphere, the probability of separation is the ratio of this angle to the full angle of a [great circle](@entry_id:268970) containing the projection, which is $\pi$ radians in each direction. Thus, the probability of separation is :

$$
P(\text{sign}(r^\top v_i) \neq \text{sign}(r^\top v_j)) = \frac{\arccos(v_i^\top v_j)}{\pi} = \frac{\arccos(X^\star_{ij})}{\pi}.
$$

For example, if two vectors $v_i$ and $v_j$ are nearly antipodal, so $v_i^\top v_j \approx -1$, the angle between them is close to $\pi$. The probability of separation is $\approx \pi/\pi = 1$. They are almost certain to be cut, which is desired. Conversely, if they are nearly identical, $v_i^\top v_j \approx 1$, the angle is close to 0, and the probability of being cut is almost 0 . If they are orthogonal, the probability is $\arccos(0)/\pi = 1/2$. This elegant formula allows for an analysis of the expected value of the rounded cut, leading to the famous Goemans-Williamson [approximation ratio](@entry_id:265492) of $\approx 0.878$.

Alternative rounding schemes exist, such as one based on the signs of the components of the leading eigenvector of $X^\star$. However, such deterministic methods can be brittle; for instance, if the largest eigenvalue has multiplicity greater than one, the choice of eigenvector is not unique, making the rounding procedure ill-defined. The randomized hyperplane scheme is robust to such issues and its distribution is uniquely defined by the matrix $X^\star$ .

### Duality, Certificates, and Tightening Relaxations

The theory of convex optimization provides powerful tools for analyzing SDP relaxations, including duality. The Max-Cut SDP has a corresponding [dual problem](@entry_id:177454). For optimal primal and dual solutions, a condition known as **[complementary slackness](@entry_id:141017)** must hold. This condition can be used to certify optimality. If one can construct a [feasible solution](@entry_id:634783) to the primal SDP that is rank-one (i.e., it corresponds to an actual cut) and also construct a [feasible solution](@entry_id:634783) to the dual SDP such that the pair satisfies [complementary slackness](@entry_id:141017), then one has proven that the SDP relaxation is exact for that problem instance. The dual solution acts as a **[certificate of optimality](@entry_id:178805)** .

When the relaxation is not exact, as in the case of the 3-cycle, one might wonder if it can be improved. The [integrality gap](@entry_id:635752) exists because the feasible set of the SDP, the elliptope $\mathcal{E}$, is larger than the convex hull of integer solutions, $\text{conv}(C)$. We can "tighten" the relaxation by adding more linear constraints, known as **[cutting planes](@entry_id:177960)**, that are valid for all integer solutions but are violated by the fractional solution of the current relaxation.

A powerful class of such constraints are the **triangle inequalities**. For any three vertices $i,j,k$, the inequality $X_{ij} + X_{jk} + X_{ki} \ge -1$ (and its three variants) must hold for any matrix $X \in C$. However, the optimal solution to the vanilla SDP for a 3-cycle, where $X_{ij} = -1/2$ for all pairs, violates this: $-1/2 - 1/2 - 1/2 = -3/2  -1$. Adding this inequality to the SDP formulation cuts off this fractional solution and forces the new optimum to be exactly 2, closing the [integrality gap](@entry_id:635752) for this graph .

This idea of systematically adding [valid inequalities](@entry_id:636383) to strengthen a relaxation is the foundation of hierarchies of relaxations, such as the **Sherali-Adams** and **Lasserre (or Sum-of-Squares)** hierarchies. These methods construct increasingly tighter relaxations by considering moment matrices of higher-degree monomials and enforcing [positive semidefiniteness](@entry_id:147720). For instance, for the 5-cycle, the standard Goemans-Williamson SDP yields an upper bound of $\frac{5(5+\sqrt{5})}{8} \approx 4.52$, while the true [max-cut](@entry_id:271899) is 4. By adding a single [valid inequality](@entry_id:170492) derived from the fact that at most 4 edges can be cut in a 5-cycle, the SDP relaxation can be tightened to yield the exact bound of 4 . These hierarchical methods provide a principled way to trade computational effort for solution quality, bridging the gap between fast, approximate relaxations and the original hard combinatorial problem.