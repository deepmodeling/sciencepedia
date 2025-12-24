## Introduction
In the complex process of integrated circuit (IC) physical design, placement is a critical stage where the locations of millions of cells are determined. This geometric arrangement fundamentally dictates the final performance, power consumption, and manufacturability of the chip. A primary goal is to minimize the total length of interconnecting wires, as shorter wires translate to faster signals and lower power usage. However, a significant challenge arises because the exact wire paths are only determined in the subsequent routing stage. Placement algorithms must therefore operate with incomplete information, relying on efficient and accurate mathematical models—or surrogate objectives—to estimate the final wirelength.

This article provides a comprehensive exploration of these fundamental placement objectives and [wirelength metrics](@entry_id:1134103). The first chapter, **"Principles and Mechanisms,"** delves into the mathematical foundations of common models like the Half-Perimeter Wirelength (HPWL) and quadratic wirelength (QWL), examining their properties and trade-offs. The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates how these core metrics are applied in modern multi-objective optimization to address real-world challenges like [timing closure](@entry_id:167567), power reduction, and routability. Finally, the **"Hands-On Practices"** section offers practical exercises for calculating these metrics and understanding their role in [analytical placement](@entry_id:1121000), bridging theory with application. This structure will guide you from the core theory of wirelength estimation to its practical implementation in solving complex engineering problems at the heart of [electronic design automation](@entry_id:1124326) (EDA).

## Principles and Mechanisms

In the [physical design](@entry_id:1129644) of [integrated circuits](@entry_id:265543), the placement stage determines the spatial location of each circuit element. A primary objective of this process is to arrange the cells in a way that minimizes the total length of the interconnecting wires. Shorter wires lead to reduced signal delay, lower power consumption, and improved routing feasibility. However, the exact wire paths are not known until the subsequent routing stage. Therefore, placement algorithms rely on surrogate objectives—mathematical models that estimate the final wirelength based on the positions of the pins that each net connects. This chapter explores the principles and mechanisms of the most fundamental wirelength objectives used in modern [electronic design automation](@entry_id:1124326) (EDA).

### The Hierarchy of Wirelength Metrics

The most accurate representation of the shortest possible rectilinear interconnect for a given net is the **Rectilinear Steiner Minimal Tree (RSMT)**. An RSMT is a network of horizontal and vertical line segments that connects all pins of a net, possibly by introducing new junction points, known as Steiner points, to achieve the minimum possible total length. While the RSMT provides an ideal target, its computation is an NP-hard problem, making it computationally infeasible to use directly as an objective function for large-scale optimization.

This computational challenge necessitates the use of more tractable proxies. One such proxy is the **Rectilinear Minimum Spanning Tree (RMST)**, which finds the shortest tree connecting all pins of a net using only the pin locations themselves as vertices. By disallowing Steiner points, the RMST is simpler to compute but provides a length that is always greater than or equal to the RSMT length, $L(\text{RSMT}) \le L(\text{RMST})$. An even simpler and more widely used proxy is the Half-Perimeter Wirelength.

### The Half-Perimeter Wirelength (HPWL) Model

The **Half-Perimeter Wirelength (HPWL)** is the most common combinatorial metric for wirelength estimation. For a given net, the HPWL is defined as the half-perimeter of the smallest axis-aligned [bounding box](@entry_id:635282) that encloses all of its pins. If a net has a set of pins located at coordinates $\{(x_i, y_i)\}$, its HPWL is given by:

$$
\mathrm{HPWL} = \left( \max_{i} x_i - \min_{i} x_i \right) + \left( \max_{i} y_i - \min_{i} y_i \right)
$$

The term $\max_{i} x_i - \min_{i} x_i$ represents the width of the bounding box (the horizontal span), and $\max_{i} y_i - \min_{i} y_i$ represents its height (the vertical span). For a simple two-pin net, the HPWL is precisely equal to the **Manhattan distance** (or $L_1$ distance) between the pins, which is also the length of the two-pin RSMT. For any multi-pin net, the HPWL serves as a lower bound on the RSMT length, because any rectilinear tree connecting the pins must span at least the full width and height of the bounding box.

A crucial property of the HPWL objective is its **separability**. The total wirelength is the sum of a component depending only on the $x$-coordinates and a component depending only on the $y$-coordinates. This allows placement optimizers to handle the horizontal and vertical dimensions of the problem independently, significantly simplifying the optimization process.

For example, consider a net with pins at $(3,5)$, $(10,14)$, and $(7,9)$. The x-coordinates are $\{3, 7, 10\}$ and the y-coordinates are $\{5, 9, 14\}$. The horizontal span is $10 - 3 = 7$, and the vertical span is $14 - 5 = 9$. The HPWL for this net is $7 + 9 = 16$. The total HPWL for a design is simply the sum of the HPWLs of all its nets.

#### Mathematical Properties of HPWL

From an optimization perspective, the HPWL function has several important characteristics. The total HPWL, being a sum of individual net HPWLs, is a **convex function** of the pin coordinates. This is a desirable property, as it implies that any local minimum is also a [global minimum](@entry_id:165977). The convexity arises because the `max` and `-min` operators are themselves convex.

However, the HPWL function is **not differentiable** everywhere. Differentiability fails at configurations where two or more pins tie for an extremal coordinate (maximum or minimum) along an axis. At these "kinks," the gradient is not uniquely defined. This property makes HPWL challenging for optimizers that rely on smooth gradients.

To handle this non-[differentiability](@entry_id:140863), we employ the concept of a **[subgradient](@entry_id:142710)**. For a [convex function](@entry_id:143191), a [subgradient](@entry_id:142710) at a point is a vector that defines a [tangent plane](@entry_id:136914) which lies entirely on or below the function. At points where the function is differentiable, the [subgradient](@entry_id:142710) is unique and equals the gradient. At points of non-[differentiability](@entry_id:140863), there is a set of valid subgradients, called the [subdifferential](@entry_id:175641).

For the HPWL model, the [subgradient](@entry_id:142710) provides a clear physical intuition. Consider the sensitivity of a net's HPWL to the movement of a single pin $(x_k, y_k)$.
- If the pin is strictly in the interior of the [bounding box](@entry_id:635282) (i.e., not at $x_{\min}, x_{\max}, y_{\min},$ or $y_{\max}$), small movements of the pin do not change the bounding box dimensions. In this case, the partial derivatives of the HPWL with respect to $x_k$ and $y_k$ are zero.
- If the pin is uniquely at an extremum (e.g., it is the sole rightmost pin), the gradient is well-defined. For instance, if pin $k$ is the unique rightmost pin and pin $j$ is the unique leftmost pin, the gradient of the x-span with respect to the vector of x-coordinates is a vector with $+1$ at position $k$, $-1$ at position $j$, and $0$ elsewhere.
- If multiple pins tie for an extremum, any convex combination of their indicator vectors forms a valid [subgradient](@entry_id:142710). For example, if two pins tie for the maximum y-coordinate, a valid [subgradient](@entry_id:142710) component for the $\max_i y_i$ term would be any vector $(\dots, c, \dots, 1-c, \dots)$ where $c \in [0,1]$ is placed at the tying pin indices.

### The Quadratic Wirelength Model

While HPWL is geometrically intuitive, its non-[differentiability](@entry_id:140863) led to the development of smooth, **analytical** wirelength models suitable for gradient-based optimization. The most prevalent of these is the **quadratic wirelength (QWL)** model.

#### The Spring Analogy

The QWL model is often explained through a physical analogy: each two-pin connection in the netlist is modeled as an ideal linear spring. The energy stored in the spring system is proportional to the sum of the squared lengths of all connections. For a connection between pin $i$ at $\mathbf{r}_i=(x_i, y_i)$ and pin $j$ at $\mathbf{r}_j=(x_j, y_j)$ with a [spring constant](@entry_id:167197) (weight) $w_{ij}$, the energy is $w_{ij} \|\mathbf{r}_i - \mathbf{r}_j\|_2^2$. The total wirelength objective is the sum of these energies over all connections:

$$
E_{QWL} = \sum_{\{i,j\} \in \text{connections}} w_{ij} \left( (x_i - x_j)^2 + (y_i - y_j)^2 \right)
$$

This objective is a smooth, strictly convex quadratic function of the pin coordinates (assuming a [connected graph](@entry_id:261731) of pins), which makes it exceptionally easy to optimize. Its minimization leads to a [system of linear equations](@entry_id:140416).

#### Modeling Multi-Pin Nets

A key challenge is how to apply this pairwise model to nets connecting more than two pins (hyperedges). Two main strategies exist:

1.  **Clique Model:** The simplest approach is to expand a hyperedge of $k$ pins into a **[clique](@entry_id:275990)** of $\binom{k}{2}$ pairwise connections. Each pair of pins in the net is connected by a spring. While simple to implement, a naive clique model where each spring has the same weight introduces **degree bias**: the effective stiffness pulling on a pin in a high-degree net becomes excessively large, scaling with the net's degree $(k-1)$. This can cause high-degree nets to dominate the optimization, unnaturally collapsing their pins together.

2.  **Star Model:** A more sophisticated approach is the **star model**. For each net, a virtual "net-center" variable $\mathbf{z}_e$ is introduced. Each pin $\mathbf{r}_i$ in the net is then connected only to this center with a spring. The energy for a net $e$ is:
    $$
    E_e^\star(\{\mathbf{r}_v\}, \mathbf{z}_e) = w_e \sum_{v \in e} \|\mathbf{r}_v - \mathbf{z}_e\|_2^2
    $$
    The net-center $\mathbf{z}_e$ is a variable in the optimization. By minimizing the energy with respect to $\mathbf{z}_e$, we find that its optimal position is the [centroid](@entry_id:265015) ([center of gravity](@entry_id:273519)) of the pins in the net: $\mathbf{z}_e^* = \frac{1}{k_e} \sum_{v \in e} \mathbf{r}_v$, where $k_e$ is the number of pins in net $e$.

A remarkable result is that substituting this optimal $\mathbf{z}_e^*$ back into the star model energy function yields a [quadratic form](@entry_id:153497) that is mathematically equivalent to a [clique](@entry_id:275990) model. However, the equivalent clique has a specific, non-uniform pairwise weight: each pair $\{i,j\}$ in the net is assigned an effective weight of $w_e' = w_e / k_e$. This weighting scheme automatically corrects the degree bias. The total stiffness on a pin now scales as $(k_e-1) \times (w_e/k_e)$, which approaches a constant for large $k_e$. This makes the star model the preferred method for [quadratic placement](@entry_id:1130359).

#### The Matrix Formulation

The total quadratic energy for an entire design can be expressed compactly using matrix notation. For the x-coordinates, the total energy is a [quadratic form](@entry_id:153497) $E_x = \frac{1}{2} \mathbf{x}^T Q \mathbf{x} + \mathbf{b}^T \mathbf{x}$, where $\mathbf{x}$ is the vector of all cell x-coordinates and $Q$ is the **graph Laplacian** matrix. The entries of $Q$ are determined by the spring constants: $Q_{ii}$ is the sum of weights of all connections attached to pin $i$, and for $i \neq j$, $Q_{ij}$ is the negative of the weight of the connection between $i$ and $j$. The total system matrix $Q$ is the sum of elemental Laplacian contributions from each connection.

The matrix $Q$ is symmetric and positive semi-definite. If no pins are fixed, the quadratic objective is invariant to a global translation of all cells, which corresponds to a [nullspace](@entry_id:171336) of $Q$ spanned by the all-ones vector. To obtain a unique solution, we must anchor the placement by fixing the positions of some cells (e.g., I/O pads). If at least one pin in each connected component of the netlist graph is fixed, the [system matrix](@entry_id:172230) for the remaining [free variables](@entry_id:151663) becomes positive definite, guaranteeing a unique solution that can be found by solving the linear system $\nabla E = Q\mathbf{x} + \mathbf{b} = 0$. The physical interpretation of this solution is that each free cell is placed at the center of gravity of its neighbors.

### Smooth Approximations of HPWL: The Log-Sum-Exp Method

The quadratic model, while analytically convenient, is a relatively loose approximation of the rectilinear HPWL metric. An alternative approach aims to create a smooth, [differentiable function](@entry_id:144590) that more closely mimics the HPWL objective itself. This can be achieved using the **Log-Sum-Exp (LSE)** function, a well-known smooth approximation of the `max` operator.

The LSE function is defined with a positive [smoothing parameter](@entry_id:897002) $\beta$:
$$
f_\beta(\mathbf{x}) = \frac{1}{\beta} \log \left( \sum_{i=1}^n e^{\beta x_i} \right)
$$
This function is convex and provides an upper bound on the true maximum: $\max_i x_i \le f_\beta(\mathbf{x}) \le \max_i x_i + \frac{1}{\beta} \log n$. Using the identity $\min_i x_i = - \max_i (-x_i)$, we can construct a smooth approximation for the minimum operator as $g_\beta(\mathbf{x}) = -f_\beta(-\mathbf{x})$.

A smooth, convex surrogate for the HPWL span can then be constructed as $H_\beta(\mathbf{x}) = f_\beta(\mathbf{x}) - g_\beta(\mathbf{x})$. This function is a differentiable upper bound on the true HPWL span, and as the [smoothing parameter](@entry_id:897002) $\beta \to \infty$, it converges uniformly to the exact HPWL function.

The gradient of this LSE-based surrogate distributes the sensitivity across all pins according to a **[softmax](@entry_id:636766)** weighting. For the `max` approximation, the partial derivative with respect to $x_k$ is $\frac{\partial f_\beta}{\partial x_k} = \frac{e^{\beta x_k}}{\sum_j e^{\beta x_j}}$. This means that pins with larger coordinates have a greater influence on the "maximum". As $\beta \to \infty$, the [softmax function](@entry_id:143376) approaches a one-hot vector that selects the unique maximizing pin, and the gradient of the LSE surrogate converges to a valid [subgradient](@entry_id:142710) of the exact HPWL function. This allows for the power of [gradient-based optimization](@entry_id:169228) while more faithfully representing the geometric intent of the HPWL metric.

In summary, placement algorithms have a rich set of wirelength objectives at their disposal. The choice among them involves a fundamental trade-off between geometric accuracy (RSMT > HPWL > QWL) and analytical tractability (QWL/LSE > HPWL > RSMT). Modern placement flows often use a hybrid approach, starting with a smooth quadratic or LSE model for [global placement](@entry_id:1125677) and refining the solution with the more accurate but non-differentiable HPWL metric in later stages.