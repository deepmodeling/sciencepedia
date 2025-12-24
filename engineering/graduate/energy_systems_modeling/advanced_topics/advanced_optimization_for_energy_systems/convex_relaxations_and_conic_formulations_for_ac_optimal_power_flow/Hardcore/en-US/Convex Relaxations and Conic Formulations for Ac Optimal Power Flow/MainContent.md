## Introduction
The Alternating Current Optimal Power Flow (AC OPF) problem is a fundamental challenge in energy systems, aiming to operate the power grid at minimum cost while respecting its physical laws. However, the inherent non-linear and non-convex nature of AC [power flow equations](@entry_id:1130035) renders the problem NP-hard, making it computationally intractable to guarantee a globally optimal solution for large-scale networks. This knowledge gap has traditionally been addressed with simplified models like the DC OPF, which sacrifice accuracy for speed and can lead to infeasible or suboptimal outcomes. This article addresses this challenge by providing a comprehensive overview of [convex relaxations](@entry_id:636024), a class of powerful mathematical techniques that transform the intractable AC OPF into a solvable convex problem.

Over the next three chapters, you will gain a deep understanding of this cutting-edge methodology. The journey begins in **Principles and Mechanisms**, where we will deconstruct the sources of non-convexity in AC power flow and detail the step-by-step formulation of the Semidefinite Programming (SDP) and Second-Order Cone Programming (SOCP) relaxations. Next, **Applications and Interdisciplinary Connections** will demonstrate the versatility of these methods, exploring their use in electricity markets for pricing, in system operations for ensuring dynamic stability and managing uncertainty, and in handling mixed-integer control decisions. Finally, **Hands-On Practices** provides a bridge from theory to application, guiding you through the formulation and numerical solution of AC OPF problems using these conic techniques.

## Principles and Mechanisms

The Alternating Current Optimal Power Flow (AC OPF) problem is a cornerstone of modern power system operation, seeking to determine an optimal generation dispatch that meets demand at minimum cost while respecting the physical laws and operational limits of the grid. As established in the introductory chapter, the AC OPF is notoriously difficult to solve due to inherent non-convexities. This chapter delves into the principles and mechanisms of [convex relaxations](@entry_id:636024), a powerful class of techniques that transform the intractable AC OPF problem into a solvable convex optimization problem, paving the way for both globally optimal solutions and profound economic insights.

### The Source of Non-Convexity in AC Power Flow

The fundamental challenge of AC OPF originates from the non-linear, non-convex relationship between power and voltage in alternating current circuits. To understand this, let us consider a network with a set of buses $\mathcal{N}$. The state of the system is described by the complex voltage [phasors](@entry_id:270266) at each bus, $V_k = e_k + \mathrm{j} f_k$, where $e_k$ and $f_k$ are the real and imaginary parts of the voltage, respectively.

The relationship between the vector of injected currents $\mathbf{I}$ and the vector of bus voltages $\mathbf{V}$ is governed by the bus [admittance matrix](@entry_id:270111) $\mathbf{Y} \in \mathbb{C}^{|\mathcal{N}| \times |\mathcal{N}|}$, a constant matrix that captures the network's topology and electrical properties: $\mathbf{I} = \mathbf{YV}$. The [complex power](@entry_id:1122734) injection at a bus $i$, $S_i = P_i + \mathrm{j} Q_i$, where $P_i$ and $Q_i$ are the [active and reactive power](@entry_id:746237), is defined as $S_i = V_i I_i^*$, where $I_i^*$ is the [complex conjugate](@entry_id:174888) of the current injected at bus $i$.

By substituting the nodal equation $I_i = \sum_{j \in \mathcal{N}} Y_{ij} V_j$ into the power definition, we can express the power injection directly in terms of the voltage variables. As demonstrated in the detailed derivation , if we let $Y_{ij} = G_{ij} + \mathrm{j} B_{ij}$, the resulting expressions for active power $P_i$ and reactive power $Q_i$ are:

$$P_i = \sum_{j=1}^{n} \left[ G_{ij}(e_i e_j + f_i f_j) + B_{ij}(f_i e_j - e_i f_j) \right]$$

$$Q_i = \sum_{j=1}^{n} \left[ G_{ij}(f_i e_j - e_i f_j) - B_{ij}(e_i e_j + f_i f_j) \right]$$

These equations reveal the core difficulty: the power injections are **non-convex quadratic functions** of the voltage variables $(e_k, f_k)$. Consequently, the power balance constraints, which state that generation must equal load plus losses ($S_i^{\text{gen}} - S_i^{\text{load}} = S_i$), are non-convex quadratic equalities. Furthermore, operational constraints such as voltage magnitude limits, $\underline{V}_i \le |V_i| \le \overline{V}_i$, are also non-convex, as $|V_i| = \sqrt{e_i^2 + f_i^2}$. An optimization problem with a convex objective function but non-convex constraints, such as this one, is generally NP-hard, meaning it cannot be solved efficiently or reliably to global optimality.

### The Semidefinite Programming (SDP) Relaxation

To overcome the challenge of non-[convexity](@entry_id:138568), we can reformulate the problem in a higher-dimensional space through a technique called **lifting**. The central idea of the Semidefinite Programming (SDP) relaxation is to lift the problem from the space of voltage vectors into the space of matrices.

Let us define a matrix $W \in \mathbb{C}^{n \times n}$ as the [outer product](@entry_id:201262) of the voltage vector $v = [V_1, \dots, V_n]^T$ with its [conjugate transpose](@entry_id:147909): $W = v v^H$. The entries of this matrix are $W_{ij} = V_i V_j^*$. This lifting is a remarkable change of variables. The problematic quadratic terms in the [power flow equations](@entry_id:1130035) are transformed into linear terms in the entries of $W$. For example:
- The squared voltage magnitude at bus $i$ is $|V_i|^2 = V_i V_i^* = W_{ii}$. The non-convex voltage magnitude constraints $\underline{V}_i^2 \le |V_i|^2 \le \overline{V}_i^2$ become simple linear [box constraints](@entry_id:746959) on the diagonal elements of $W$: $\underline{V}_i^2 \le W_{ii} \le \overline{V}_i^2$ .
- The complex power injection at bus $i$ becomes an [affine function](@entry_id:635019) of the elements of $W$: $S_i = \sum_{j \in \mathcal{N}} Y_{ij}^* W_{ij}$ .
- Similarly, quantities like line power flow and power losses become affine functions of $W$. For a line with series [admittance](@entry_id:266052) $y_{ij}$, the active power loss is $P_{\text{loss}} = \text{Re}\{ (V_i-V_j)(y_{ij}(V_i-V_j))^* \}$. If $y_{ij}$ is a pure conductance $g$, this simplifies to $P_{\text{loss}} = g|V_i-V_j|^2 = g(W_{ii} + W_{jj} - 2\text{Re}(W_{ij}))$, which is a linear function of the elements of $W$ .

This lifting procedure isolates the entire non-[convexity](@entry_id:138568) of the original problem into the definition of the matrix $W$ itself. By construction, the matrix $W=vv^H$ has two key properties: it is **Hermitian positive semidefinite** ($W \succeq 0$), and it has **rank one** ($\mathrm{rank}(W)=1$). The constraint $W \succeq 0$ is a convex constraint, while the constraint $\mathrm{rank}(W)=1$ is non-convex.

The SDP relaxation is achieved by simply dropping, or **relaxing**, the non-convex [rank-one constraint](@entry_id:1130565) and retaining only the convex constraints . The resulting optimization problem is:
- Minimize a convex cost function (which is typically linear or quadratic in the now-linear power variables).
- Subject to:
    - Affine power balance equality constraints in $W$.
    - Linear voltage magnitude [inequality constraints](@entry_id:176084) in $W$.
    - Convex line flow [inequality constraints](@entry_id:176084) in $W$.
    - The convex conic constraint $W \succeq 0$.

This formulation constitutes a **Semidefinite Program**, which is a class of convex optimization problem that can be solved efficiently to global optimality. The solution to this relaxed problem, $W^*$, provides a lower bound on the optimal cost of the original AC OPF. The crucial question of when this bound is tight—that is, when the solution $W^*$ happens to be rank-one and thus corresponds to a physical voltage state—will be addressed in a later section.

### The Second-Order Cone Programming (SOCP) Relaxation

While the SDP relaxation is powerful, solving large-scale SDPs can be computationally demanding. The **Second-Order Cone Programming (SOCP) relaxation** offers a more computationally tractable alternative. SOCP can be seen as a further relaxation of SDP that is exact for certain network topologies, most notably radial (tree-structured) networks.

The most common SOCP formulation for OPF uses a **branch flow model**. Instead of bus voltages, the primary variables are the power flows ($p_{ij}, q_{ij}$) and squared current magnitude ($\ell_{ij}$) for each line (branch) $(i, j)$, along with the squared voltage magnitudes ($v_i$) at each bus.

The derivation of the SOCP relaxation begins with the same fundamental power definition, $S_{ij} = V_i I_{ij}^*$. Taking the squared magnitude of this identity gives $|S_{ij}|^2 = |V_i|^2 |I_{ij}|^2$. In terms of the branch flow variables, this is an exact but non-convex equality :

$p_{ij}^2 + q_{ij}^2 = v_i \ell_{ij}$

The non-[convexity](@entry_id:138568) arises from the bilinear term $v_i \ell_{ij}$. The SOCP relaxation is born from relaxing this equality to an inequality:

$p_{ij}^2 + q_{ij}^2 \le v_i \ell_{ij}$

This single step is the core of the relaxation. The set of points $(p_{ij}, q_{ij}, v_i, \ell_{ij})$ satisfying this inequality, along with the physical non-negativity constraints $v_i \ge 0$ and $\ell_{ij} \ge 0$, forms a convex cone known as a **[rotated second-order cone](@entry_id:637080)** . Any physically feasible operating point that satisfies the original equality will naturally satisfy this inequality, meaning the relaxation enlarges the feasible set.

This central conic constraint is complemented by two other sets of constraints that are linear in the branch flow variables:
1.  **Power Balance:** At each bus, the sum of incoming power flows from lines, plus local generation, must equal the sum of outgoing power flows to other lines, plus local load. These are linear "book-keeping" equations.
2.  **Voltage Drop:** The relationship between the voltage magnitudes at the two ends of a line can be expressed as an exact affine equation involving the power flow and current on that line. For a line $(i,j)$ with impedance $r_{ij} + \mathrm{j}x_{ij}$, this relation is :
    $v_j = v_i - 2(r_{ij} p_{ij} + x_{ij} q_{ij}) + (r_{ij}^2+x_{ij}^2) \ell_{ij}$

The complete SOCP-relaxed OPF problem is to minimize a convex cost function subject to these rotated cone constraints and the linear power balance and voltage drop equations . This formulation can be solved very efficiently by modern optimization solvers.

### Theoretical Foundations and Guarantees

The utility of [convex optimization](@entry_id:137441) stems from its powerful [duality theory](@entry_id:143133). For a convex problem that satisfies certain regularity conditions, the optimal value of the primal problem (the minimization problem we formulated) is equal to the optimal value of its corresponding [dual problem](@entry_id:177454). This property is called **[strong duality](@entry_id:176065)**.

A [sufficient condition](@entry_id:276242) for strong [duality in convex optimization](@entry_id:164483) is **Slater's condition**. For the SDP relaxation of AC OPF, Slater's condition is satisfied if there exists a matrix $W^*$ that is **strictly feasible**: it must be strictly [positive definite](@entry_id:149459) ($W^* \succ 0$) and satisfy all [inequality constraints](@entry_id:176084) with strict inequality (e.g., $(V_k^{\min})^2  W_{kk}^*  (V_k^{\max})^2$), while satisfying all equality constraints exactly . For most practical power systems, such a point can be readily found, guaranteeing that the SDP relaxation has a zero [duality gap](@entry_id:173383) and its [dual variables](@entry_id:151022) are well-behaved .

The most important theoretical question, however, is that of **[exactness](@entry_id:268999)**, also known as **AC-feasible recovery**. When is the solution of the relaxed problem also a [feasible solution](@entry_id:634783) for the original non-convex AC OPF problem?
-   For the SDP relaxation, exactness occurs if the optimal matrix $W^*$ has rank one.
-   For the SOCP relaxation, exactness occurs if the cone constraint $p_{ij}^2 + q_{ij}^2 \le v_i \ell_{ij}$ is binding (holds with equality) for all lines at the optimum.

If a relaxation is exact, we can recover a physically realizable set of complex voltages $\{V_i\}$ from the solution. This is because the rank-one condition $W=vv^H$ (or its SOCP equivalent) ensures that the magnitudes and phases of the underlying voltages are mutually consistent . It has been proven that the SOCP and SDP relaxations are guaranteed to be exact for networks with a **radial (tree) topology** . For meshed networks, exactness is not guaranteed in general but often holds in practice for many [transmission systems](@entry_id:1133376) under normal operating conditions. More general [sufficient conditions](@entry_id:269617) for [exactness](@entry_id:268999) in meshed networks exist, requiring that the voltage [phase angle](@entry_id:274491) differences implied by the solution are consistent around all cycles in the network .

### Advanced Topics and Applications

#### Computational Efficiency and Sparsity

The primary computational bottleneck in the SDP relaxation is the constraint $W \succeq 0$, which involves a matrix whose size is the number of buses in the network. For a large network, this becomes intractable. However, power grids are extremely sparse: each bus is connected to only a few others. This sparsity can be exploited.

The theory of **[chordal graphs](@entry_id:275709)** and [positive semidefinite matrix](@entry_id:155134) completion provides a principled way to decompose the large SDP constraint into a set of smaller, coupled SDP constraints . The procedure involves finding a **chordal completion** of the network graph (adding edges to eliminate long cycles) and then enforcing the PSD condition only on the submatrices of $W$ corresponding to the **maximal cliques** of the [chordal graph](@entry_id:267949).

This decomposition has a profound implication: for a radial (tree) network, which is naturally chordal, the maximal cliques are simply the edges. The decomposition of the $W \succeq 0$ constraint results in a set of $2 \times 2$ PSD constraints. A $2 \times 2$ PSD constraint is equivalent to a [second-order cone](@entry_id:637114) constraint . Thus, for radial networks, [chordal decomposition](@entry_id:1122389) shows that the SDP relaxation is mathematically equivalent to the SOCP relaxation. For meshed networks, [chordal decomposition](@entry_id:1122389) provides a further relaxation that is computationally much faster than the full SDP, at the potential cost of a less [tight bound](@entry_id:265735).

#### Economic Interpretation: Locational Marginal Prices

Perhaps the most significant practical outcome of [convex relaxations](@entry_id:636024) is their ability to produce meaningful economic signals. In a convex optimization problem, the **[dual variables](@entry_id:151022)** (or Lagrange multipliers) associated with equality constraints have a precise economic interpretation: they are the marginal cost of enforcing that constraint.

When applied to the power balance constraint at a specific bus, the dual variable represents the marginal cost of supplying one additional megawatt of power at that location. This value is known as the **Locational Marginal Price (LMP)** . The LMP is composed of three components: the [marginal cost of energy](@entry_id:1127618), the marginal cost of congestion, and the marginal cost of losses. Because the [convex relaxations](@entry_id:636024) provide a globally optimal solution and well-defined [dual variables](@entry_id:151022) (thanks to [strong duality](@entry_id:176065)), they can be used to calculate stable, transparent, and economically efficient prices for electricity, a critical function in modern restructured [electricity markets](@entry_id:1124241) . This ability to seamlessly integrate [engineering physics](@entry_id:264215) with economic principles is a testament to the power and elegance of conic formulations for AC Optimal Power Flow.