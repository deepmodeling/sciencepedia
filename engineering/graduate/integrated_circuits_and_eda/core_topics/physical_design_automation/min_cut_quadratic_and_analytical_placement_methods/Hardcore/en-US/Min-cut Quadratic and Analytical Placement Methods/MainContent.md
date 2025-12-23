## Introduction
In the intricate world of Very Large-Scale Integration (VLSI) design, placement is a critical and computationally intensive step that determines the ultimate performance, power, and area of an integrated circuit. The fundamental challenge lies in arranging millions, or even billions, of circuit components onto a silicon chip to optimize connectivity while adhering to a complex web of physical and electrical rules. A poor placement can lead to [routing congestion](@entry_id:1131128), timing violations, and a non-functional chip, making the development of robust and efficient placement algorithms a cornerstone of Electronic Design Automation (EDA). This article addresses the knowledge gap between abstract [optimization theory](@entry_id:144639) and its concrete application in modern placement tools.

Across three comprehensive chapters, we will navigate the evolution and synthesis of the primary placement paradigms. The journey begins in **Principles and Mechanisms**, where we will establish the fundamental mathematical models—from netlist hypergraphs to quadratic and non-linear wirelength objectives—that define the placement problem. We will dissect the core mechanics of [min-cut](@entry_id:1127910) partitioning, [quadratic placement](@entry_id:1130359), and advanced analytical methods. Next, **Applications and Interdisciplinary Connections** will demonstrate how these foundational algorithms are extended to tackle real-world multiobjective problems, integrating constraints like timing, power, and placement density through sophisticated techniques drawn from numerical analysis and control theory. Finally, the **Hands-On Practices** chapter provides practical exercises, allowing you to apply these concepts and solve placement problems using the very methods discussed, solidifying your understanding of this essential engineering discipline.

## Principles and Mechanisms

This chapter delves into the foundational principles and core mechanisms that underpin modern placement algorithms. We will transition from abstract mathematical representations of the placement problem to the concrete formulations used in [min-cut](@entry_id:1127910), quadratic, and advanced [analytical placement](@entry_id:1121000) methods. Our exploration will systematically build upon fundamental concepts, illustrating how progressively more sophisticated models address the multifaceted challenges of minimizing wirelength while managing circuit density and respecting physical constraints.

### Fundamental Models for Placement

At its core, a placement algorithm seeks to assign geometric coordinates to a collection of circuit modules. To achieve this in a computationally tractable manner, we must first establish a formal mathematical framework for both the circuit's connectivity and its geometry.

#### The Netlist Hypergraph

An integrated circuit's netlist, which specifies modules and the electrical nets connecting their pins, can be naturally modeled as a **hypergraph**. A hypergraph $\mathcal{H} = (V, E)$ consists of a set of vertices $V$ and a set of hyperedges $E$, where each hyperedge is a subset of the vertices.

For the purpose of module placement, the most canonical construction is a module-level hypergraph. In this model:
-   The set of **vertices** $V = \{v_1, v_2, \dots, v_n\}$ represents the set of $n$ movable modules in the netlist.
-   The set of **hyperedges** $E = \{e_1, e_2, \dots, e_m\}$ represents the set of $m$ nets. Each hyperedge $e \in E$ is defined as the set of module-vertices connected by that net.

Formally, if a net connects to one or more pins on a module $i$, then the vertex $v_i$ is included in the corresponding hyperedge. Even if a net connects to multiple pins on the same module, the module appears only once in the hyperedge set, as the hyperedge simply records which modules are involved in the connection. Each hyperedge $e$ is often assigned a non-negative weight $w_e$, reflecting its importance for timing or other performance metrics . This hypergraph structure forms the combinatorial basis for most placement algorithms, capturing the essential connectivity information that drives the optimization.

#### Geometric Representation and Coordinate Transformation

The geometric aspect of placement involves assigning a position and an orientation to each module in the Euclidean plane. We establish a global coordinate frame and define the placement of each module $i$ by a pair $(\mathbf{r}_i, o_i)$, where:
-   $\mathbf{r}_i = (x_i, y_i) \in \mathbb{R}^2$ is the **placement vector**, representing the global coordinates of a distinguished anchor point (or local origin) within the module.
-   $o_i$ is the **orientation** of the module, typically chosen from a finite set of isometries such as rotations by $0^\circ, 90^\circ, 180^\circ, 270^\circ$ and possible reflections.

The locations of a module's pins are specified by local offset vectors relative to its anchor point. Let $\mathbf{p}_{i\alpha}$ be the local offset of pin $\alpha$ on module $i$ in its canonical orientation. To determine the absolute global coordinate of this pin, $\mathbf{x}_{i\alpha}$, we must apply a [rigid-body transformation](@entry_id:150396). This transformation consists of first applying the module's orientation and then its translation.

The orientation $o_i$ can be represented by a $2 \times 2$ [orthogonal matrix](@entry_id:137889) $Q(o_i)$. For example, a counter-clockwise rotation by an angle $\theta_i$ corresponds to the rotation matrix:
$$
R(\theta_i) = \begin{pmatrix} \cos(\theta_i) & -\sin(\theta_i) \\ \sin(\theta_i) & \cos(\theta_i) \end{pmatrix}
$$
Applying this orientation to the local pin offset $\mathbf{p}_{i\alpha}$ yields the reoriented offset vector $Q(o_i)\mathbf{p}_{i\alpha}$. The final absolute coordinate is obtained by translating this vector by the module's anchor position $\mathbf{r}_i$. Thus, the complete transformation is:
$$
\mathbf{x}_{i\alpha} = \mathbf{r}_i + Q(o_i)\mathbf{p}_{i\alpha}
$$
Writing this out in component form for a pin with local offset $(\delta x_{i\alpha}, \delta y_{i\alpha})$ and a module orientation of pure rotation by $\theta_i$, its global coordinate $(x_{i\alpha}, y_{i\alpha})$ becomes :
$$
x_{i\alpha} = x_i + \delta x_{i\alpha} \cos(\theta_i) - \delta y_{i\alpha} \sin(\theta_i)
$$
$$
y_{i\alpha} = y_i + \delta x_{i\alpha} \sin(\theta_i) + \delta y_{i\alpha} \cos(\theta_i)
$$
This fundamental geometric relationship is central to all placement methods. However, the presence of [trigonometric functions](@entry_id:178918) of the orientation angles $\theta_i$ makes the absolute pin coordinates highly non-linear functions of the orientation variables. This non-linearity poses a significant challenge for optimization, and different placement paradigms handle it in distinct ways.

### Min-Cut Placement: A Partitioning-Based Approach

Min-cut placement is a top-down, hierarchical method that relies on the principle of **recursive bisection**. The core idea is to repeatedly partition the set of modules into two balanced subsets while minimizing the number of nets cut by the partition. These two subsets are then assigned to two distinct geometric subregions, and the process is recursively applied to each subregion until each module is assigned to a small enough area.

#### Hypergraph Cut Metrics

The quality of a partition $(S, \bar{S})$ of the module set $V$ is measured by a **cut metric**. The most fundamental metric is the **cut-net size**, which simply counts the number of hyperedges that have at least one vertex in $S$ and at least one vertex in $\bar{S}$. Formally, for a net $e$, its contribution is 1 if it is cut and 0 otherwise. The total cutsize is:
$$
C_{\text{cut}}(S) = \sum_{e \in E} \mathbf{1}\big(|e \cap S| \ge 1 \text{ and } |e \cap \bar{S}| \ge 1\big)
$$
where $\mathbf{1}(\cdot)$ is the [indicator function](@entry_id:154167). This metric directly corresponds to the **connectivity metric**, where the cost for a net is $\lambda(e) - 1$, and $\lambda(e)$ is the number of partitions the net touches .

While intuitive, the cut-net metric treats all cut nets equally. More sophisticated metrics have been developed to better estimate wirelength. Two prominent examples are:

1.  **Sum-of-Pins Metric:** This metric considers how the pins of a cut net are distributed. For a bipartition, a common form is $\sum_{e \in E} \min(|e \cap S|, |e \cap \bar{S}|)$. This metric can be interpreted as counting the minimum number of connections that must cross the partition boundary.

2.  **Clique Expansion Metric:** In this model, each hyperedge $e$ is approximated by a clique of $\binom{|e|}{2}$ two-pin nets. The cut cost is the number of these two-pin nets that cross the partition boundary, which for a net $e$ is given by $|e \cap S| \cdot |e \cap \bar{S}|$.

These metrics are related. For any cut net, $\min(|e \cap S|, |e \cap \bar{S}|) \ge 1$ and $|e \cap S| \cdot |e \cap \bar{S}| \ge \min(|e \cap S|, |e \cap \bar{S}|)$. Therefore, the [clique](@entry_id:275990) metric generally provides a higher penalty for unbalanced cuts than the sum-of-pins metric, which in turn is a more nuanced measure than the simple cut-net metric .

#### Geometric Mapping and Area Constraints

After partitioning the netlist, the algorithm must divide the physical placement area. Consider a parent rectangular region of width $W$ and height $H$. A partition yields two sets of modules with total cell areas $s_1$ and $s_2$. To manage routability, each partition is assigned a **utilization target** $u_k \in (0, 1]$, which specifies the desired ratio of cell area to placement area. The required area for each subregion is therefore $A_k = s_k / u_k$.

The parent region is split by either a vertical or a horizontal cutline.
-   A **vertical split** creates two subregions of height $H$ and widths $w_1 = A_1 / H$ and $w_2 = A_2 / H$.
-   A **horizontal split** creates two subregions of width $W$ and heights $h_1 = A_1 / W$ and $h_2 = A_2 / W$.

A crucial physical constraint is the **aspect ratio** $\rho = \text{height}/\text{width}$ of the resulting subregions, which must typically lie within a specified range $[\rho_{\min}, \rho_{\max}]$ to ensure they are not too long and thin. The algorithm must choose the split orientation (vertical or horizontal) that satisfies these aspect ratio bounds for both children. If both orientations are valid, a heuristic (e.g., creating squarer partitions) can be used. If neither is valid, the algorithm may choose the orientation that minimizes the violation of the bounds . This geometric mapping step translates the abstract netlist partition into a concrete physical division of space.

### Quadratic Placement: An Analytical Approach

Quadratic placement reformulates the problem as a [continuous optimization](@entry_id:166666). Instead of partitioning, it seeks to find cell coordinates that minimize a smooth, analytical objective function representing total wirelength.

#### The Quadratic Wirelength Objective

The most common quadratic objective models nets as springs. For a two-pin net connecting cells at coordinates $\mathbf{x}_i$ and $\mathbf{x}_j$, the squared Euclidean distance, weighted by $w_{ij}$, is used as an energy term: $w_{ij} \|\mathbf{x}_i - \mathbf{x}_j\|^2$. The total wirelength objective is the sum over all such connections:
$$
\Phi(\mathbf{x}, \mathbf{y}) = \frac{1}{2} \sum_{i,j} w_{ij} \left( (x_i-x_j)^2 + (y_i-y_j)^2 \right)
$$
This objective has the convenient property of being a quadratic function of the cell coordinates. Minimizing it is equivalent to finding the equilibrium positions of a physical [mass-spring system](@entry_id:267496).

#### Modeling Multi-Pin Nets

For nets with more than two pins, the simple pairwise model is insufficient. Two common extensions are the **star model** and the **clique model**.

The star model introduces a virtual "star node" at the center of gravity of the net's pins and sums the squared distances from each pin to this center. The energy for a net $e$ with weight $w_e$ and $m$ pins is $E_e = w_e \sum_{i \in e} \|\mathbf{x}_i - \bar{\mathbf{x}}_e\|^2$, where $\bar{\mathbf{x}}_e$ is the net's [center of gravity](@entry_id:273519).

The **[clique](@entry_id:275990) model** is a widely used approximation that replaces a hyperedge with a complete graph (a [clique](@entry_id:275990)) of two-pin nets connecting every pair of pins in the original net. A crucial question is how to set the weights of these new two-pin nets. To preserve the mathematical properties of the star model, the weight $\alpha$ for each edge in the [clique](@entry_id:275990) expansion of a net with original weight $w_e$ and $m$ pins must be set to $\alpha = w_e / m$. This choice ensures that the quadratic energy of the clique model is identically equal to the energy of the star model, providing a rigorous basis for this common heuristic .

#### Formulating and Solving the Linear System

Since the total quadratic wirelength objective $\Phi$ is a quadratic function of the cell coordinates, its minimum can be found by setting its gradient to zero. This results in a large, sparse system of linear equations. The problem conveniently decouples into independent systems for the $x$ and $y$ coordinates:
$$
L \mathbf{x} = \mathbf{b}_x \quad \text{and} \quad L \mathbf{y} = \mathbf{b}_y
$$
The matrix $L$ is the **graph Laplacian** of the connectivity graph, defined as $L = D - W$, where $W$ is the symmetric weight matrix of pairwise connections and $D$ is the diagonal degree matrix with $D_{ii} = \sum_j W_{ij}$.

In a realistic setting, the placement area contains fixed objects like I/O pads or pre-placed macros. When a net connects a movable cell to a fixed one, the corresponding energy term contains known coordinate values. By partitioning the coordinates into movable (free) and fixed sets, $\mathbf{x} = (\mathbf{x}_f, \mathbf{x}_p)$, the optimization is performed only over $\mathbf{x}_f$. This leads to a reduced linear system for the [free variables](@entry_id:151663):
$$
L_{ff} \mathbf{x}_f = \mathbf{b}_f
$$
Here, $L_{ff}$ is the submatrix of the Laplacian corresponding to connections between free cells. The right-hand side vector $\mathbf{b}_f$ represents the "pull" exerted by the fixed pins. It can be derived that $\mathbf{b}_f = W_{fp} \mathbf{x}_p$, where $W_{fp}$ is the submatrix of weights connecting free cells to fixed pins, and $\mathbf{x}_p$ is the vector of fixed pin coordinates .

The Laplacian matrix $L$ has a [nullspace](@entry_id:171336) corresponding to uniform translation (i.e., $L\mathbf{1} = \mathbf{0}$). To obtain a unique solution, the system must be constrained. This can be done by fixing the position of at least one cell. A more robust technique is to introduce **soft anchors**: weak springs connecting each movable cell to a target grid location. This adds small positive values to the diagonal entries of the Laplacian, making it [positive definite](@entry_id:149459) and guaranteeing a unique solution that is "pulled" towards a reasonable initial configuration .

### Modern Analytical Placement: Non-linear Optimization

While [quadratic placement](@entry_id:1130359) is computationally efficient, its wirelength model is a rough approximation. Modern [analytical placement](@entry_id:1121000) methods employ more accurate but non-linear [objective functions](@entry_id:1129021), which they solve using iterative numerical techniques.

#### The HPWL Objective and its Smooth Approximation

A more accurate wirelength proxy is the **Half-Perimeter Wirelength (HPWL)**, defined for a net as the half-perimeter of its axis-aligned bounding box. For a net with pin coordinates $\{(x_i, y_i)\}$, the HPWL is:
$$
\text{HPWL} = (\max_i x_i - \min_i x_i) + (\max_i y_i - \min_i y_i)
$$
The HPWL is a better correlator to final routed wirelength than the quadratic model. However, the $\max$ and $\min$ functions are non-differentiable, making them unsuitable for standard [gradient-based optimization](@entry_id:169228).

This difficulty is overcome by using a smooth approximation. A powerful technique is the **[log-sum-exp](@entry_id:1127427) (LSE)** function, which provides a differentiable surrogate for the maximum operator:
$$
\text{smax}(\{x_i\}, \tau) = \tau \ln\left(\sum_i \exp(x_i / \tau)\right) \approx \max_i x_i
$$
The parameter $\tau > 0$ is a "temperature" that controls the smoothness; as $\tau \to 0$, the approximation becomes exact. Using the identity $\min_i x_i = -\max_i(-x_i)$, a smooth minimum function can be similarly constructed. Combining these yields a fully differentiable surrogate for HPWL :
$$
\text{HPWL}_s = \text{smax}(\{x_i\}) - \text{smin}(\{x_i\}) + \text{smax}(\{y_i\}) - \text{smin}(\{y_i\})
$$
This smoothed objective function forms the wirelength component of many modern analytical placers. It is worth noting that the quadratic objective can be seen as a different kind of smoothing of HPWL. Under small displacement assumptions, their expected values can be matched, but the quadratic model's gradient is systematically steeper, indicating it penalizes large displacements more aggressively than HPWL .

#### Handling Cell Overlap with Repulsive Forces

Minimizing any wirelength objective alone would cause all cells to collapse to a single point. A crucial component of [analytical placement](@entry_id:1121000) is a mechanism to manage cell density and reduce overlaps. This is typically achieved by adding a penalty term to the objective function.

A common approach models cells as electrically charged particles that repel each other. A **smooth [repulsive potential](@entry_id:185622)** is introduced between every pair of cells. For two cells with centers separated by a distance $d$, a [potential function](@entry_id:268662) like $g(d) = \beta (d^2 + \epsilon)^{-1}$ can be used, where $\beta$ is a repulsion strength and $\epsilon$ is a small softening parameter to prevent division by zero . The total objective function becomes:
$$
E_{\text{total}} = E_{\text{wirelength}} + \lambda E_{\text{density}}
$$
The addition of these repulsive terms makes the problem non-linear. The Hessian of the density term can be interpreted as a position-dependent modification to the system's effective Laplacian matrix. Each pairwise repulsion adds a term to the Hessian that acts like a spring with a variable, distance-dependent stiffness. This "stiffness" is typically negative when cells are far apart (encouraging them to move closer to reduce wirelength) and becomes strongly positive when they get too close (repelling them to resolve overlap). The balance between the wirelength and density terms, controlled by the weight $\lambda$, is adjusted iteratively during the placement process.

### Numerical Solvers for Placement Systems

The [optimization problems](@entry_id:142739) formulated above, whether linear or non-linear, must be solved numerically.

For [quadratic placement](@entry_id:1130359), this involves solving the large, sparse, [symmetric positive-definite](@entry_id:145886) (SPD) linear system $Lx=b$. The **Conjugate Gradient (CG)** method is the [iterative solver](@entry_id:140727) of choice for such systems. The convergence rate of CG depends on the **condition number** $\kappa(L) = \lambda_{\max}(L) / \lambda_{\min}(L)$ of the Laplacian matrix. For netlists resembling regular grids, which are common in structured designs, the condition number grows as $\Theta(n^2)$, where $n$ is the side length of the grid. This poor conditioning leads to a large number of CG iterations, scaling as $O(n)$.

To accelerate convergence, **preconditioning** is essential. A simple and effective technique is **diagonal (or Jacobi) preconditioning**, where the system is effectively multiplied by the inverse of the diagonal of $L$. While this improves the constant factors and balances the scales of the problem, for grid-like graphs, it does not change the asymptotic scaling of the condition number. More advanced preconditioners, such as those based on [algebraic multigrid](@entry_id:140593) (AMG), are often required to achieve [scalability](@entry_id:636611) for very large problems .

For non-linear [analytical placement](@entry_id:1121000), the problem is typically solved with [iterative methods](@entry_id:139472) like non-linear [conjugate gradient](@entry_id:145712) or quasi-Newton methods, where at each step a search direction is computed based on the gradient of the total energy function (wirelength plus density). This complex, [non-convex optimization](@entry_id:634987) landscape is navigated iteratively, gradually reducing both wirelength and overlap to produce a high-quality, legal placement.