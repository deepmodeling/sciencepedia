## Introduction
In the intricate world of integrated circuit (IC) design, [floorplanning](@entry_id:1125091) stands as a pivotal early stage that dictates the ultimate performance, area, and power of a chip. At its heart, floorplanning is a complex packing puzzle: arranging dozens or hundreds of functional blocks onto a silicon die. The key to solving this puzzle lies not just in the [optimization algorithm](@entry_id:142787), but in the very language used to describe a layout—the **floorplan representation**. How can we encode the topological arrangement of modules in a way that is both expressive enough to capture high-quality layouts and structured enough for efficient algorithmic manipulation?

This article addresses this fundamental question by providing a deep dive into the two dominant families of floorplan representations. You will learn the core principles that distinguish these approaches and the trade-offs that guide their use in modern Electronic Design Automation (EDA).

First, in **Principles and Mechanisms**, we will dissect the theoretical foundations, exploring slicing representations like Polish expressions and non-slicing methods like Sequence Pairs and B*-Trees. We will uncover how these abstract data structures are decoded into valid, non-overlapping physical layouts. Next, **Applications and Interdisciplinary Connections** will bridge theory and practice, demonstrating how these representations are employed within multi-objective optimization frameworks to balance competing goals like chip area, wirelength, and timing performance. Finally, **Hands-On Practices** will offer a chance to solidify your understanding by working through concrete examples of encoding and decoding floorplans.

We begin our exploration by establishing the formal problem of floorplanning and delving into the principles of the first major class of representations: the slicing floorplan.

## Principles and Mechanisms

In the [physical design](@entry_id:1129644) of [integrated circuits](@entry_id:265543), floorplanning is a critical early stage where the relative positions and shapes of major functional blocks, or modules, are determined. The quality of a floorplan profoundly impacts the final chip's area, performance, and power consumption. A floorplan representation is a data structure that encodes the topological arrangement of these modules. The choice of representation is fundamental, as it defines the search space for [optimization algorithms](@entry_id:147840) and dictates the feasibility and efficiency of constructing a valid, non-overlapping physical layout. This chapter delves into the principles and mechanisms of the two primary families of floorplan representations: slicing and non-slicing.

### The Formal Problem of Floorplanning

Before examining specific representations, we must first formally define what constitutes a valid floorplan. At its core, a floorplan is a packing problem. We are given a set of $n$ rectangular modules, and the goal is to place them within a bounding rectangle such that no two modules overlap. In the ideal case, known as a **mosaic floorplan**, the modules perfectly tile the bounding rectangle with no wasted space.

Let us formalize this. Consider $n$ rectangular modules, where for each module $i \in \{1, \dots, n\}$, we define its width $w_i > 0$, height $h_i > 0$, and the coordinates of its lower-left corner $(x_i, y_i)$. The module $i$ occupies the closed rectangular region $R_i = [x_i, x_i+w_i] \times [y_i, y_i+h_i]$. The overall layout is contained within a bounding rectangle $B = [0, W] \times [0, H]$. A valid mosaic floorplan must satisfy two fundamental conditions:

1.  **Non-Overlap**: The interiors of any two distinct modules must be disjoint. For any pair of modules $i \neq j$, their interiors $R_i^\circ = (x_i, x_i+w_i) \times (y_i, y_i+h_i)$ and $R_j^\circ = (x_j, x_j+w_j) \times (y_j, y_j+h_j)$ must satisfy $R_i^\circ \cap R_j^\circ = \emptyset$. This condition is equivalent to a disjunction of four linear inequalities: module $i$ is entirely to the left of module $j$, or to the right, or below, or above. Mathematically, for every pair $i \neq j$, at least one of the following must hold:
    $$ (x_i + w_i \le x_j) \lor (x_j + w_j \le x_i) \lor (y_i + h_i \le y_j) \lor (y_j + h_j \le y_i) $$
    This set of disjunctive constraints captures the essence of non-overlapping placement for any type of floorplan, be it slicing or non-slicing.

2.  **Complete Coverage**: The union of all module rectangles must be identical to the bounding rectangle, i.e., $\bigcup_{i=1}^n R_i = B$. This condition can be decomposed into two parts. First, all modules must be contained within the [bounding box](@entry_id:635282), which is expressed by the inequalities $0 \le x_i$, $x_i+w_i \le W$, $0 \le y_i$, and $y_i+h_i \le H$ for all $i$. Second, there must be no empty space, or "voids," within the bounding box. Given the non-overlap and containment constraints, a necessary and [sufficient condition](@entry_id:276242) to guarantee complete coverage is that the sum of the areas of the individual modules equals the area of the bounding rectangle :
    $$ \sum_{i=1}^n w_i h_i = W H $$

These conditions form a precise mathematical programming model of the floorplanning problem. Any representation must provide a mechanism to generate placements that satisfy these constraints.

### Slicing Floorplan Representations

The conceptually simplest class of floorplans is the slicing floorplan. These structures are defined by their method of construction.

#### Guillotine Cuts and Slicing Trees

A **slicing floorplan** is a rectangular dissection that can be obtained by recursively partitioning a rectangle with a sequence of **guillotine cuts**. A guillotine cut is a single straight line, either horizontal or vertical, that extends from one side of the current rectangle to the opposite side, dividing it into two smaller sub-rectangles . This [recursive partitioning](@entry_id:271173) process naturally lends itself to a tree-based representation.

A slicing floorplan is canonically represented by a **rooted ordered [binary tree](@entry_id:263879)**, known as a **slicing tree**. In this structure :
-   Each **leaf node** corresponds to an individual circuit module (an indivisible rectangle).
-   Each **internal node** represents a cut. It is labeled either $H$ for a horizontal cut or $V$ for a vertical cut. The two children of the node represent the two sub-floorplans created by the cut.

For an internal node labeled $H$, the region is split into a top and a bottom sub-rectangle. For a node labeled $V$, the region is split into a left and a right sub-rectangle. The overall dimensions (width and height) of a composite floorplan represented by a subtree can be calculated recursively from the dimensions of its children. Let a subtree rooted at an internal node have children corresponding to sub-floorplans with dimensions $(W_L, H_L)$ and $(W_R, H_R)$. The composite dimensions $(W_C, H_C)$ are determined as follows:

-   If the node is a **V-cut**, the sub-floorplans are placed side-by-side. The composite width is the sum of the child widths, and the composite height is the maximum of the child heights:
    $W_C = W_L + W_R$ and $H_C = \max(H_L, H_R)$.

-   If the node is an **H-cut**, the sub-floorplans are stacked vertically. The composite height is the sum of the child heights, and the composite width is the maximum of the child widths:
    $H_C = H_L + H_R$ and $W_C = \max(W_L, W_R)$.

For example, consider a floorplan with three modules: $B_1$ with $(w_1, h_1)=(2,3)$, $B_2$ with $(w_2, h_2)=(4,1)$, and $B_3$ with $(w_3, h_3)=(3,2)$. Let the slicing tree have a root node $H$, whose left child is a $V$ node and right child is the leaf $B_3$. The $V$ node has leaves $B_1$ and $B_2$ as its children. To find the [bounding box](@entry_id:635282) of the entire floorplan, we first compute the dimensions of the subtree rooted at $V$. Its width is $w_V = w_1 + w_2 = 2+4=6$, and its height is $h_V = \max(h_1, h_2) = \max(3,1)=3$. This composite block $(6,3)$ is then combined with block $B_3(3,2)$ at the root node $H$. The final width is $W = \max(w_V, w_3) = \max(6,3)=6$, and the final height is $H = h_V + h_3 = 3+2=5$. The resulting floorplan has a [bounding box](@entry_id:635282) of $(6,5)$ .

#### Polish Expressions

While slicing trees are intuitive, they are not ideal for algorithmic manipulation, particularly in optimization contexts like simulated annealing. A more compact, linear encoding is the **Polish postfix expression**. This expression is obtained by performing a [post-order traversal](@entry_id:273478) of the slicing tree. The resulting string is a sequence of operands (module identifiers) and operators ($\{H, V\}$).

For a slicing floorplan with $n$ modules, a valid Polish expression is not just any string of symbols. It must conform to specific structural properties that guarantee it corresponds to a valid full [binary tree](@entry_id:263879). A full [binary tree](@entry_id:263879) with $n$ leaves has exactly $n-1$ internal nodes. Consequently, a valid Polish expression must have a length of $2n-1$ and contain exactly $n$ operands and $n-1$ operators.

The most critical property is the **balloting condition**, which ensures that the expression is syntactically well-formed and can be evaluated on a stack without [underflow](@entry_id:635171). When scanning the expression from left to right, an operand is pushed onto the stack, and a binary operator pops two items and pushes one result. To avoid an operator encountering an insufficiently full stack, the number of operands must always maintain a lead over the number of operators. Formally, a string is a valid Polish postfix encoding if and only if :

1.  It has length $2n-1$, with $n$ operands and $n-1$ operators.
2.  For every proper prefix (from length $1$ to $2n-2$), the number of operands strictly exceeds the number of operators.

For the full expression of length $2n-1$, the number of operands is exactly one more than the number of operators, leaving a single element on the stack, which represents the final floorplan.

#### Redundancy and Normalization in Polish Expressions

A significant issue with both slicing trees and Polish expressions is **redundancy**: many distinct encodings can represent the same topological floorplan. This redundancy arises from two properties of the cut operations :

-   **Associativity**: A chain of identical cuts can be parenthesized in multiple ways without changing the [final topology](@entry_id:150988). For example, partitioning three blocks vertically can be done as $V(V(a,b), c)$ or $V(a, V(b,c))$. These correspond to different tree structures (left-skewed vs. right-skewed) and different Polish expressions (`abVcV` vs. `abcVV`), but the same set of adjacencies. For a chain of $k$ operands under a single operator, there are $C_{k-1}$ such associative variants, where $C_m$ is the $m$-th Catalan number.
-   **Commutativity**: Since we often consider floorplans that are mirror images of each other to be topologically equivalent, the order of children at a node does not matter. $H(a,b)$ is equivalent to $H(b,a)$. This allows swapping subtrees, leading to different Polish expressions (e.g., `abH` vs. `baH`).

This redundancy bloats the search space for optimization algorithms. To address this, **normalized Polish expressions** are used. A common normalization scheme enforces a canonical form :
1.  **Associative Normalization**: Forbid consecutive identical operators in the Polish expression (i.e., no `"HH"` or `"VV"` substrings). This rule forces any chain of identical operators into a unique, left-skewed tree structure.
2.  **Commutative Normalization**: For each maximal block of operands governed by a chain of identical operators, sort the operands according to a predefined [total order](@entry_id:146781). This selects a single canonical permutation from all possible mirror-image variants.

Together, these two rules ensure that each distinct slicing topology corresponds to exactly one normalized Polish expression, drastically reducing the search space.

### Non-Slicing Floorplan Representations

The primary limitation of slicing representations is their incomplete **expressiveness**. Not all mosaic floorplans are slicing. A classic [counterexample](@entry_id:148660) is the "pinwheel" floorplan, where five modules are arranged in a cyclic structure. Any attempt to apply a guillotine cut to the [bounding box](@entry_id:635282) of a pinwheel floorplan will inevitably slice through the interior of at least one module. Such "interlocking" arrangements are non-guillotinable and thus non-slicing . To handle these general mosaic floorplans, more powerful non-slicing representations are required.

#### Sequence Pairs

The **Sequence Pair (SP)** representation is a powerful and elegant method for encoding general non-slicing floorplans. Introduced by Murata et al., it encodes a floorplan using an [ordered pair](@entry_id:148349) of permutations, $(\pi_x, \pi_y)$, of the $n$ module identifiers. These two [permutations](@entry_id:147130) are sufficient to determine the relative placement of every pair of modules without ambiguity.

The geometric constraints are derived from the following rules. For any two modules $i$ and $j$:
-   If $i$ appears before $j$ in **both** $\pi_x$ and $\pi_y$, then module $i$ is placed to the **left** of module $j$.
-   If $i$ appears before $j$ in $\pi_x$ but **after** $j$ in $\pi_y$, then module $i$ is placed **below** module $j$.

These pairwise "left-of" and "below" relations define a set of precedence constraints. These constraints can be modeled using two [directed acyclic graphs](@entry_id:164045) (DAGs): a **Horizontal Constraint Graph ($G_H$)** and a **Vertical Constraint Graph ($G_V$)**.

-   In $G_H$, the vertices are the modules. A directed edge is drawn from module $i$ to $j$ if "$i$ is left of $j$".
-   In $G_V$, the vertices are also the modules. A directed edge is drawn from module $i$ to $j$ if "$i$ is below $j$".

The minimum coordinates for each module, and thus the minimum dimensions of the overall floorplan, can be found by computing the **longest path** in each graph  . For a module $i$, its x-coordinate $x_i$ is the length of the longest path from a source node to vertex $i$ in $G_H$, where the length of a path is the sum of the widths of the modules on it. Similarly, its y-coordinate $y_i$ is the length of the longest path to vertex $i$ in $G_V$, where path length is determined by module heights. The total width $W$ of the floorplan is the length of the longest path in $G_H$ from source to sink, and the total height $H$ is the length of the longest path in $G_V$.

For instance, consider four modules A, B, C, D with dimensions $w_A=3, h_A=2; w_B=2, h_B=3; w_C=4, h_C=1; w_D=1, h_D=2$. Given the [sequence pair](@entry_id:1131501) $(\pi_x, \pi_y) = ((A,C,B,D), (C,A,D,B))$, we can derive the constraints. The "left-of" relations are that $A$ is left of $D$, $C$ is left of $B$, and $C$ is left of $D$. The "below-of" relations are that $A$ is below $B$, $A$ is below $C$, and $B$ is below $D$. Computing the longest paths in the corresponding [constraint graphs](@entry_id:267131) yields a total width $W=6$ and total height $H=7$. Thus, the minimal bounding box is $(W,H)=(6,7)$ .

#### B*-Trees and Skyline Packing

Another influential non-slicing representation is the **B*-tree**. Like the slicing tree, it is a rooted ordered [binary tree](@entry_id:263879) where each node represents a module. However, its geometric interpretation is entirely different and does not rely on recursive cuts. Instead, the tree structure encodes direct adjacency hints :

-   The **left child** of a node (parent) is placed to the immediate **right** of the parent.
-   The **right child** of a node (parent) is placed **above** the parent.

To convert a B*-tree into a compacted physical layout, a deterministic packing algorithm is used, typically based on a **skyline** or **contour**. The skyline is a piecewise-[constant function](@entry_id:152060), $Y(x)$, that tracks the upper envelope of all modules placed so far. The packing process, often a [pre-order traversal](@entry_id:263452) of the B*-tree, works as follows:

1.  The root is placed at $(0,0)$. The skyline is initialized.
2.  For each subsequent node (module) to be placed, its tentative $x$-coordinate is determined by its parent in the B*-tree. If it's a left child of parent $p$, its $x_{tent} = x_p + w_p$. If it's a right child, $x_{tent} = x_p$.
3.  To find the module's $y$-coordinate, the algorithm queries the skyline. For a module of width $w$ at tentative $x_{tent}$, its minimal non-overlapping $y$-coordinate is the maximum value of the skyline over the interval $[x_{tent}, x_{tent} + w)$. That is, $y_{place} = \max_{x_{tent} \le \xi \le x_{tent}+w} Y(\xi)$.
4.  The module is placed at $(x_{tent}, y_{place})$.
5.  The skyline is updated. The function $Y(x)$ over the interval $[x_{tent}, x_{tent} + w)$ is set to the new height, $y_{place} + h$.

This incremental process guarantees a valid, non-overlapping, and compact placement. When the skyline is maintained in an efficient [data structure](@entry_id:634264) like an augmented [balanced binary search tree](@entry_id:636550) or a segment tree, each placement step (query and update) takes $O(\log n)$ time, leading to an overall packing time of $O(n \log n)$ for $n$ modules .

### Comparative Analysis of Representations

Understanding the trade-offs between different floorplan representations is crucial for selecting the right tool for an optimization task. The key metrics for comparison are expressiveness and redundancy.

#### Expressiveness and Completeness

The **expressiveness** of a representation is the set of all floorplans it can encode. A representation is considered **complete** if it can express all possible mosaic floorplans.

-   **Slicing Tree (ST)**: By definition, slicing trees can only represent slicing floorplans. As we've established, the set of slicing floorplans is a [proper subset](@entry_id:152276) of the set of all mosaic floorplans. Therefore, the slicing tree representation is **incomplete**.

-   **Sequence Pair (SP)**: The [sequence pair](@entry_id:1131501) representation was specifically designed to overcome the limitation of slicing structures. It has been proven that for any mosaic floorplan (slicing or non-slicing), there exists at least one [sequence pair](@entry_id:1131501) that can encode it. Therefore, the [sequence pair](@entry_id:1131501) representation is **complete**.

This leads to the strict inclusion relationship $\mathcal{E}(\text{ST}) \subsetneq \mathcal{E}(\text{SP})$, where $\mathcal{E}$ denotes the set of expressible floorplans. Any floorplan that can be encoded by a slicing tree can also be encoded by a [sequence pair](@entry_id:1131501), but the reverse is not true .

#### Redundancy and Symmetry

While completeness is desirable, it often comes with increased **redundancy**, where multiple distinct encodings map to the same topological structure. This can hinder optimization algorithms by creating a larger, more complex search space with many equivalent solutions.

-   **Slicing Representations**: As discussed, Polish expressions suffer from redundancy due to [associativity](@entry_id:147258) and [commutativity](@entry_id:140240). However, this redundancy can be completely eliminated through normalization schemes, leading to a unique [canonical representation](@entry_id:146693) for each slicing topology .

-   **Non-Slicing Representations**: Sequence pairs are highly redundant. A single floorplan topology can correspond to many different sequence pairs. A major source of this redundancy comes from geometric symmetries. The set of axis-preserving isometries of a plane (rotations by $0^\circ, 90^\circ, 180^\circ, 270^\circ$, and reflections) forms a group of 8 transformations. Each of these 8 [geometric transformations](@entry_id:150649) on a floorplan corresponds to a specific algebraic transformation on its [sequence pair](@entry_id:1131501) encoding $(\pi, \sigma)$. For example, a $180^\circ$ rotation corresponds to $(\pi^R, \sigma^R)$, where $\pi^R$ is the reverse of $\pi$. For a generic floorplan, these 8 transformations result in 8 distinct but topologically equivalent sequence pairs .

This inherent redundancy in non-slicing representations like sequence pairs presents both a challenge and an opportunity. While it complicates the search for a unique optimum, the different encodings for the same topology can provide diverse starting points for local search algorithms. The choice of representation thus involves a fundamental trade-off between the ability to represent all possible solutions (completeness) and the efficiency of navigating the [solution space](@entry_id:200470) (compactness and low redundancy).