## Introduction
The Alternating Current Optimal Power Flow (AC OPF) problem is a fundamental challenge in energy systems, aiming to operate the power grid at minimum cost while respecting its physical laws. However, the inherent non-linear and non-convex nature of AC power flow equations renders the problem NP-hard, making it computationally intractable to guarantee a globally optimal solution for large-scale networks. This knowledge gap has traditionally been addressed with simplified models like the DC OPF, which sacrifice accuracy for speed and can lead to infeasible or suboptimal outcomes. This article addresses this challenge by providing a comprehensive overview of convex relaxations, a class of powerful mathematical techniques that transform the intractable AC OPF into a solvable convex problem.

Over the next three chapters, you will gain a deep understanding of this cutting-edge methodology. The journey begins in **Principles and Mechanisms**, where we will deconstruct the sources of non-convexity in AC power flow and detail the step-by-step formulation of the Semidefinite Programming (SDP) and Second-Order Cone Programming (SOCP) relaxations. Next, **Applications and Interdisciplinary Connections** will demonstrate the versatility of these methods, exploring their use in electricity markets for pricing, in system operations for ensuring dynamic stability and managing uncertainty, and in handling mixed-integer control decisions. Finally, **Hands-On Practices** provides a bridge from theory to application, guiding you through the formulation and numerical solution of AC OPF problems using these conic techniques.

## Principles and Mechanisms

The Alternating Current Optimal Power Flow (AC OPF) problem is a cornerstone of modern power system operation, seeking to determine an optimal generation dispatch that meets demand at minimum cost while respecting the physical laws and operational limits of the grid. As established in the introductory chapter, the AC OPF is notoriously difficult to solve due to inherent non-convexities. This chapter delves into the principles and mechanisms of convex relaxations, a powerful class of techniques that transform the intractable AC OPF problem into a solvable convex optimization problem, paving the way for both globally optimal solutions and profound economic insights.

### The Source of Non-Convexity in AC Power Flow

The fundamental challenge of AC OPF originates from the non-linear, non-convex relationship between power and voltage in alternating current circuits. To understand this, let us consider a network with a set of buses $\mathcal{N}$. The state of the system is described by the complex voltage phasors at each bus, $V_k = e_k + \mathrm{j} f_k$, where $e_k$ and $f_k$ are the real and imaginary parts of the voltage, respectively.

The relationship between the vector of injected currents $\mathbf{I}$ and the vector of bus voltages $\mathbf{V}$ is governed by the bus admittance matrix $\mathbf{Y} \in \mathbb{C}^{|\mathcal{N}| \times |\mathcal{N}|}$, a constant matrix that captures the network's topology and electrical properties: $\mathbf{I} = \mathbf{YV}$. The complex power injection at a bus $i$, $S_i = P_i + \mathrm{j} Q_i$, where $P_i$ and $Q_i$ are the active and reactive power, is defined as $S_i = V_i I_i^*$, where $I_i^*$ is the complex conjugate of the current injected at bus $i$.

By substituting the nodal equation $I_i = \sum_{j \in \mathcal{N}} Y_{ij} V_j$ into the power definition, we can express the power injection directly in terms of the voltage variables. As demonstrated in the detailed derivation [@problem_id:4081188], if we let $Y_{ij} = G_{ij} + \mathrm{j} B_{ij}$, the resulting expressions for active power $P_i$ and reactive power $Q_i$ are:

$$P_i = \sum_{j=1}^{n} \left[ G_{ij}(e_i e_j + f_i f_j) + B_{ij}(f_i e_j - e_i f_j) \right]$$

$$Q_i = \sum_{j=1}^{n} \left[ G_{ij}(f_i e_j - e_i f_j) - B_{ij}(e_i e_j + f_i f_j) \right]$$

These equations reveal the core difficulty: the power injections are **non-convex quadratic functions** of the voltage variables $(e_k, f_k)$. Consequently, the power balance constraints, which state that generation must equal load plus losses ($S_i^{\text{gen}} - S_i^{\text{load}} = S_i$), are non-convex quadratic equalities. Furthermore, operational constraints such as voltage magnitude limits, $\underline{V}_i \le |V_i| \le \overline{V}_i$, are also non-convex, as $|V_i| = \sqrt{e_i^2 + f_i^2}$. An optimization problem with a convex objective function but non-convex constraints, such as this one, is generally NP-hard, meaning it cannot be solved efficiently or reliably to global optimality.

### The Semidefinite Programming (SDP) Relaxation

To overcome the challenge of non-convexity, we can reformulate the problem in a higher-dimensional space through a technique called **lifting**. The central idea of the Semidefinite Programming (SDP) relaxation is to lift the problem from the space of voltage vectors into the space of matrices.

Let us define a matrix $W \in \mathbb{C}^{n \times n}$ as the outer product of the voltage vector $v = [V_1, \dots, V_n]^T$ with its conjugate transpose: $W = v v^H$. The entries of this matrix are $W_{ij} = V_i V_j^*$. This lifting is a remarkable change of variables. The problematic quadratic terms in the power flow equations are transformed into linear terms in the entries of $W$. For example:
- The squared voltage magnitude at bus $i$ is $|V_i|^2 = V_i V_i^* = W_{ii}$. The non-convex voltage magnitude constraints $\underline{V}_i^2 \le |V_i|^2 \le \overline{V}_i^2$ become simple linear box constraints on the diagonal elements of $W$: $\underline{V}_i^2 \le W_{ii} \le \overline{V}_i^2$ [@problem_id:4081200].
- The complex power injection at bus $i$ becomes an affine function of the elements of $W$: $S_i = \sum_{j \in \mathcal{N}} Y_{ij}^* W_{ij}$ [@problem_id:4081200].
- Similarly, quantities like line power flow and power losses become affine functions of $W$. For a line with series admittance $y_{ij}$, the active power loss is $P_{\text{loss}} = \text{Re}\{ (V_i-V_j)(y_{ij}(V_i-V_j))^* \}$. If $y_{ij}$ is a pure conductance $g$, this simplifies to $P_{\text{loss}} = g|V_i-V_j|^2 = g(W_{ii} + W_{jj} - 2\text{Re}(W_{ij}))$, which is a linear function of the elements of $W$ [@problem_id:4081221].

This lifting procedure isolates the entire non-convexity of the original problem into the definition of the matrix $W$ itself. By construction, the matrix $W=vv^H$ has two key properties: it is **Hermitian positive semidefinite** ($W \succeq 0$), and it has **rank one** ($\mathrm{rank}(W)=1$). The constraint $W \succeq 0$ is a convex constraint, while the constraint $\mathrm{rank}(W)=1$ is non-convex.

The SDP relaxation is achieved by simply dropping, or **relaxing**, the non-convex rank-one constraint and retaining only the convex constraints [@problem_id:4081192]. The resulting optimization problem is:
- Minimize a convex cost function (which is typically linear or quadratic in the now-linear power variables).
- Subject to:
    - Affine power balance equality constraints in $W$.
    - Linear voltage magnitude inequality constraints in $W$.
    - Convex line flow inequality constraints in $W$.
    - The convex conic constraint $W \succeq 0$.

This formulation constitutes a **Semidefinite Program**, which is a class of convex optimization problem that can be solved efficiently to global optimality. The solution to this relaxed problem, $W^*$, provides a lower bound on the optimal cost of the original AC OPF. The crucial question of when this bound is tight—that is, when the solution $W^*$ happens to be rank-one and thus corresponds to a physical voltage state—will be addressed in a later section.

### The Second-Order Cone Programming (SOCP) Relaxation

While the SDP relaxation is powerful, solving large-scale SDPs can be computationally demanding. The **Second-Order Cone Programming (SOCP) relaxation** offers a more computationally tractable alternative. SOCP can be seen as a further relaxation of SDP that is exact for certain network topologies, most notably radial (tree-structured) networks.

The most common SOCP formulation for OPF uses a **branch flow model**. Instead of bus voltages, the primary variables are the power flows ($p_{ij}, q_{ij}$) and squared current magnitude ($\ell_{ij}$) for each line (branch) $(i, j)$, along with the squared voltage magnitudes ($v_i$) at each bus.

The derivation of the SOCP relaxation begins with the same fundamental power definition, $S_{ij} = V_i I_{ij}^*$. Taking the squared magnitude of this identity gives $|S_{ij}|^2 = |V_i|^2 |I_{ij}|^2$. In terms of the branch flow variables, this is an exact but non-convex equality [@problem_id:4081216]:

$p_{ij}^2 + q_{ij}^2 = v_i \ell_{ij}$

The non-convexity arises from the bilinear term $v_i \ell_{ij}$. The SOCP relaxation is born from relaxing this equality to an inequality:

$p_{ij}^2 + q_{ij}^2 \le v_i \ell_{ij}$

This single step is the core of the relaxation. The set of points $(p_{ij}, q_{ij}, v_i, \ell_{ij})$ satisfying this inequality, along with the physical non-negativity constraints $v_i \ge 0$ and $\ell_{ij} \ge 0$, forms a convex cone known as a **rotated second-order cone** [@problem_id:4081173]. Any physically feasible operating point that satisfies the original equality will naturally satisfy this inequality, meaning the relaxation enlarges the feasible set.

This central conic constraint is complemented by two other sets of constraints that are linear in the branch flow variables:
1.  **Power Balance:** At each bus, the sum of incoming power flows from lines, plus local generation, must equal the sum of outgoing power flows to other lines, plus local load. These are linear "book-keeping" equations.
2.  **Voltage Drop:** The relationship between the voltage magnitudes at the two ends of a line can be expressed as an exact affine equation involving the power flow and current on that line. For a line $(i,j)$ with impedance $r_{ij} + \mathrm{j}x_{ij}$, this relation is [@problem_id:4081216]:
    $v_j = v_i - 2(r_{ij} p_{ij} + x_{ij} q_{ij}) + (r_{ij}^2+x_{ij}^2) \ell_{ij}$

The complete SOCP-relaxed OPF problem is to minimize a convex cost function subject to these rotated cone constraints and the linear power balance and voltage drop equations [@problem_id:4081192]. This formulation can be solved very efficiently by modern optimization solvers.

### Theoretical Foundations and Guarantees

The utility of convex optimization stems from its powerful duality theory. For a convex problem that satisfies certain regularity conditions, the optimal value of the primal problem (the minimization problem we formulated) is equal to the optimal value of its corresponding dual problem. This property is called **strong duality**.

A sufficient condition for strong duality in convex optimization is **Slater's condition**. For the SDP relaxation of AC OPF, Slater's condition is satisfied if there exists a matrix $W^*$ that is **strictly feasible**: it must be strictly positive definite ($W^* \succ 0$) and satisfy all inequality constraints with strict inequality (e.g., $(V_k^{\min})^2  W_{kk}^*  (V_k^{\max})^2$), while satisfying all equality constraints exactly [@problem_id:4081205]. For most practical power systems, such a point can be readily found, guaranteeing that the SDP relaxation has a zero duality gap and its dual variables are well-behaved [@problem_id:4081205].

The most important theoretical question, however, is that of **exactness**, also known as **AC-feasible recovery**. When is the solution of the relaxed problem also a feasible solution for the original non-convex AC OPF problem?
-   For the SDP relaxation, exactness occurs if the optimal matrix $W^*$ has rank one.
-   For the SOCP relaxation, exactness occurs if the cone constraint $p_{ij}^2 + q_{ij}^2 \le v_i \ell_{ij}$ is binding (holds with equality) for all lines at the optimum.

If a relaxation is exact, we can recover a physically realizable set of complex voltages $\{V_i\}$ from the solution. This is because the rank-one condition $W=vv^H$ (or its SOCP equivalent) ensures that the magnitudes and phases of the underlying voltages are mutually consistent [@problem_id:4081177]. It has been proven that the SOCP and SDP relaxations are guaranteed to be exact for networks with a **radial (tree) topology** [@problem_id:4081177]. For meshed networks, exactness is not guaranteed in general but often holds in practice for many transmission systems under normal operating conditions. More general sufficient conditions for exactness in meshed networks exist, requiring that the voltage phase angle differences implied by the solution are consistent around all cycles in the network [@problem_id:4081177].

### Advanced Topics and Applications

#### Computational Efficiency and Sparsity

The primary computational bottleneck in the SDP relaxation is the constraint $W \succeq 0$, which involves a matrix whose size is the number of buses in the network. For a large network, this becomes intractable. However, power grids are extremely sparse: each bus is connected to only a few others. This sparsity can be exploited.

The theory of **chordal graphs** and positive semidefinite matrix completion provides a principled way to decompose the large SDP constraint into a set of smaller, coupled SDP constraints [@problem_id:4081212]. The procedure involves finding a **chordal completion** of the network graph (adding edges to eliminate long cycles) and then enforcing the PSD condition only on the submatrices of $W$ corresponding to the **maximal cliques** of the chordal graph.

This decomposition has a profound implication: for a radial (tree) network, which is naturally chordal, the maximal cliques are simply the edges. The decomposition of the $W \succeq 0$ constraint results in a set of $2 \times 2$ PSD constraints. A $2 \times 2$ PSD constraint is equivalent to a second-order cone constraint [@problem_id:4081212]. Thus, for radial networks, chordal decomposition shows that the SDP relaxation is mathematically equivalent to the SOCP relaxation. For meshed networks, chordal decomposition provides a further relaxation that is computationally much faster than the full SDP, at the potential cost of a less tight bound.

#### Economic Interpretation: Locational Marginal Prices

Perhaps the most significant practical outcome of convex relaxations is their ability to produce meaningful economic signals. In a convex optimization problem, the **dual variables** (or Lagrange multipliers) associated with equality constraints have a precise economic interpretation: they are the marginal cost of enforcing that constraint.

When applied to the power balance constraint at a specific bus, the dual variable represents the marginal cost of supplying one additional megawatt of power at that location. This value is known as the **Locational Marginal Price (LMP)** [@problem_id:4081225]. The LMP is composed of three components: the marginal cost of energy, the marginal cost of congestion, and the marginal cost of losses. Because the convex relaxations provide a globally optimal solution and well-defined dual variables (thanks to strong duality), they can be used to calculate stable, transparent, and economically efficient prices for electricity, a critical function in modern restructured electricity markets [@problem_id:4081225]. This ability to seamlessly integrate engineering physics with economic principles is a testament to the power and elegance of conic formulations for AC Optimal Power Flow.