## Introduction
High-order Discontinuous Galerkin (DG) methods are renowned for their efficiency and accuracy in simulating problems with smooth solutions. However, their power is challenged when confronting the sharp discontinuities inherent in [hyperbolic conservation laws](@entry_id:147752), such as shock waves in fluid dynamics. The use of smooth polynomial basis functions to represent these sharp features leads to the Gibbs phenomenon—spurious, non-physical oscillations that violate fundamental physical principles and can cause the simulation to fail. This creates a critical knowledge gap: how can we harness the accuracy of high-order methods while ensuring the physical robustness needed to capture shocks?

This article addresses this challenge by providing a comprehensive exploration of the subcell [finite volume](@entry_id:749401) (FV) limiting technique, a powerful hybrid strategy that resolves this conflict. Over the following chapters, you will gain a deep understanding of this essential numerical method. We will begin by examining the underlying **Principles and Mechanisms** that necessitate limiting and govern how it works. Next, we will explore its diverse **Applications and Interdisciplinary Connections**, demonstrating its versatility in fields from [computational fluid dynamics](@entry_id:142614) to [magnetohydrodynamics](@entry_id:264274). Finally, a series of **Hands-On Practices** will allow you to engage with the core mathematical concepts in a practical context.

## Principles and Mechanisms

High-order Discontinuous Galerkin (DG) methods offer exceptional accuracy for problems with smooth solutions. However, when applied to [hyperbolic conservation laws](@entry_id:147752) featuring [shock waves](@entry_id:142404) or other discontinuities, the inherent properties of their polynomial basis functions introduce significant challenges. This chapter elucidates the principles governing these challenges and details the mechanisms of [subcell finite volume limiting](@entry_id:755592), a powerful strategy designed to ensure the physical relevance and numerical stability of DG solutions in the presence of shocks.

### The Gibbs Phenomenon and its Physical Consequences

The core difficulty arises from a fundamental tenet of [approximation theory](@entry_id:138536): representing a [discontinuous function](@entry_id:143848), such as a shock profile, using a basis of smooth, continuous functions like polynomials inevitably produces the **Gibbs phenomenon**. When a DG method of polynomial degree $p \ge 1$ attempts to capture a sharp discontinuity within an element, the resulting polynomial approximation, $u_h(x)$, exhibits [spurious oscillations](@entry_id:152404) near the jump.

A critical feature of these oscillations is that their amplitude is of order one, meaning it is a significant fraction of the jump magnitude itself. While increasing the polynomial degree $p$ or refining the mesh can narrow the region where these oscillations occur, the amplitude of the primary overshoot and undershoot does not decay to zero . This lack of pointwise convergence at the discontinuity has severe physical and numerical consequences. The spurious oscillations can lead to non-physical solution states, such as negative density or pressure in simulations of the Euler equations. This behavior constitutes a violation of the **[discrete maximum principle](@entry_id:748510) (DMP)**, which requires the numerical solution to remain within physically meaningful bounds derived from the initial and boundary data .

The generation of these non-physical oscillations is not an incidental flaw but a direct consequence of Godunov's celebrated theorem, which states that any linear numerical scheme for conservation laws that is more than first-order accurate cannot be [monotonicity](@entry_id:143760)-preserving. A standard high-order DG scheme, being linear in this sense, is fundamentally non-monotone and will therefore create new extrema near sharp gradients. This instability is exacerbated under certain conditions, such as the use of non-dissipative central [numerical fluxes](@entry_id:752791) or the introduction of [aliasing](@entry_id:146322) errors from inexact numerical quadrature of nonlinear terms . Without a nonlinear stabilization mechanism, these oscillations can grow uncontrollably and destroy the solution.

### Physical Admissibility and Entropy Conditions

For nonlinear [hyperbolic conservation laws](@entry_id:147752), the challenges extend beyond [numerical stability](@entry_id:146550) to the physical correctness of the solution. The integral, or weak, formulation of a conservation law admits multiple solutions that satisfy the fundamental conservation property across a discontinuity, as expressed by the **Rankine-Hugoniot [jump condition](@entry_id:176163)**. For a [scalar conservation law](@entry_id:754531) $u_t + f(u)_x = 0$, this condition relates the shock propagation speed $s$ to the jump in the solution $[u] = u_R - u_L$ and the jump in the flux $[f(u)] = f(u_R) - f(u_L)$ via $s[u] = [f(u)]$ .

However, not all solutions satisfying this condition are physically realizable. For instance, expansion shocks, which violate the [second law of thermodynamics](@entry_id:142732), can be mathematically valid [weak solutions](@entry_id:161732). To select the single, physically relevant solution, an additional constraint known as an **[entropy condition](@entry_id:166346)** is required. For systems with a convex entropy function $\eta(u)$, this takes the form of an inequality, dictating that the total entropy within any domain can only decrease due to fluxes at the boundary.

A practical interpretation for shocks in systems with a convex flux is **Lax's [entropy condition](@entry_id:166346)**, which mandates that the [characteristic speeds](@entry_id:165394) on either side of the shock must be directed into the shock front. This ensures the shock is compressive and dissipates entropy, as is physically required. The spurious oscillations generated by an unlimited DG method can locally violate this [entropy condition](@entry_id:166346), producing regions of unphysical entropy creation and failing to converge to the correct, entropy-admissible weak solution .

### The Subcell Finite Volume Limiting Strategy

To overcome these fundamental limitations, a hybrid strategy known as **subcell [finite volume](@entry_id:749401) (FV) limiting** is employed. The core idea is to retain the high-order DG method in regions where the solution is smooth, thereby capitalizing on its efficiency and high accuracy, but to locally and adaptively switch to a more robust, lower-order method within cells that contain discontinuities. This is achieved by implementing a three-stage process for each time step:

1.  **Detection**: An algorithm, or "sensor," identifies the "troubled cells" that may contain shocks or other sharp features requiring stabilization.

2.  **Limiting**: Within each troubled cell, the high-order DG update is discarded. Instead, the solution is represented by its averages on a finer subgrid and evolved using a robust, conservative [finite volume](@entry_id:749401) scheme.

3.  **Reconstruction**: After the FV update, a new high-order DG polynomial is reconstructed from the evolved subcell data in a conservative manner, allowing the cell to seamlessly transition back to the high-order DG scheme if the solution within it becomes smooth again.

The following sections detail the principles and mechanisms of each of these stages.

### Mechanism I: Detection of Troubled Cells

A crucial component of an effective limiting strategy is the ability to reliably distinguish cells containing discontinuities from those where the solution is smooth. Two prominent philosophies for this detection process are [modal analysis](@entry_id:163921) and a posteriori physical admissibility checks.

#### The Persson-Peraire Modal Decay Sensor

This approach is based on the spectral properties of the polynomial representation. For a solution that is smooth within an element $K$, the energy contained in the [modal coefficients](@entry_id:752057), $\hat{u}_k$, of an orthonormal polynomial expansion $u_h = \sum_k \hat{u}_k \phi_k$, decays rapidly as the mode number $k$ (and thus polynomial degree) increases. In contrast, if the solution contains a discontinuity, the spectral decay is very slow, and a significant fraction of the total energy remains in the highest-order modes.

The **Persson-Peraire modal decay sensor** quantifies this behavior by computing the ratio of the energy in the highest mode to the total energy of the solution within the cell. The sensor value, $S_K$, is typically defined on a logarithmic scale:
$$
S_K = \log_{10} \left( \frac{|\hat{u}_N|^2}{\sum_{k=0}^N |\hat{u}_k|^2} \right)
$$
where $N$ is the polynomial degree. For a smooth solution, $S_K$ will be a large negative number, whereas for a shocked solution, $S_K$ will be a negative number much closer to zero. A cell is then declared "troubled" if its sensor value exceeds a predefined negative threshold, i.e., $S_K > \tau$. This provides a robust, scale-invariant method for flagging cells that require limiting .

#### A Posteriori Admissibility Checks (MOOD)

An alternative and more direct approach is the **Multi-dimensional Optimal Order Detection (MOOD)** strategy. Instead of inferring non-smoothness from spectral coefficients, MOOD performs a direct check on the physical admissibility of a candidate solution. The procedure is as follows: first, a candidate high-order solution for the next time step, $u_h^*$, is computed using the standard DG scheme. This candidate is then projected onto a subcell grid and checked against a set of predefined **admissibility criteria**. These criteria typically include:

-   **Positivity**: Physical quantities like density and pressure must remain positive.
-   **Local Discrete Maximum Principle**: Scalar fields must remain within local bounds determined by neighboring cell averages.
-   **Discrete Entropy Inequality**: The cell-averaged entropy must not increase.

If the candidate solution fails any of these checks on any subcell within the element, the entire DG update for that cell is rejected, and the cell is flagged as "troubled." This a posteriori approach ensures that limiting is only applied when a physical or numerical violation is imminent, making it highly effective and efficient .

### Mechanism II: The Limiting Step: Conservative Subcell FV Evolution

Once a cell is identified as troubled, the high-order DG representation is replaced by a piecewise-constant representation on a grid of subcells, which is then evolved using a robust [finite volume method](@entry_id:141374).

#### Conservative Projection to Subcells

The first step is to project the DG polynomial $u_h(\boldsymbol{x}) = \sum_{k=0}^{N_p-1} \hat{u}_k \phi_k(\boldsymbol{x})$ onto a partition of the DG element $K$ into non-overlapping subcells $\{S_i\}$. This projection must be **conservative**, meaning the total mass (or any other conserved quantity) within the element must be preserved. The cell average, $\bar{u}$, is directly related to the zeroth modal coefficient, $\hat{u}_0$, in an $L^2(K)$-orthonormal basis by $\hat{u}_0 = \sqrt{|K|} \bar{u}$. Preservation of the cell average is therefore equivalent to preserving the zeroth modal coefficient. The conservation condition requires that the sum of the quantities in the subcells equals the total quantity in the original cell:
$$
\sum_{i=1}^{N_s} |S_i| \bar{u}_i = |K| \bar{u}
$$
where $\bar{u}_i$ is the average value in subcell $S_i$ .

The exact subcell averages, $\bar{u}_i$, can be computed directly from the DG [modal coefficients](@entry_id:752057) $\hat{u}_k$. This involves pre-calculating mass matrices that represent the integral of each basis function over each subcell. Given the DG solution on a physical element $K$ mapped from a reference element $\hat{K}$ with Jacobian determinant $w(\boldsymbol{\xi})$, the subcell average $u_i$ is given by a [linear combination](@entry_id:155091) of the [modal coefficients](@entry_id:752057):
$$
u_i = \frac{1}{W_i} \sum_{k=0}^{N_p-1} \hat{u}_k M_{ik}
$$
where $W_i = \int_{\hat{S}_i} w(\boldsymbol{\xi})\, \mathrm{d}\boldsymbol{\xi}$ is the weighted volume of the reference subcell and $M_{ik} = \int_{\hat{S}_i} \hat{\phi}_k(\boldsymbol{\xi}) w(\boldsymbol{\xi})\, \mathrm{d}\boldsymbol{\xi}$ is the subcell mass integral for basis function $\hat{\phi}_k$ .

#### Robust Subcell Evolution

The subcell averages are then evolved forward in time using a conservative finite volume update. For an explicit first-order [time discretization](@entry_id:169380), the update for subcell $i$ takes the form:
$$
u_i^{n+1} = u_i^n - \frac{\Delta t}{|S_i|} \sum_{f \subset \partial S_i} |f| \hat{f}(u_i, u_{n(f)}; \boldsymbol{n}_f)
$$
where the sum is over the faces $f$ of the subcell boundary $\partial S_i$, $u_{n(f)}$ is the state in the neighboring subcell, and $\hat{f}$ is a **numerical flux** .

The key to the robustness of the limiter is the choice of a **monotone numerical flux**, such as the Godunov flux or the more dissipative but simpler local Lax-Friedrichs (Rusanov) flux. A monotone flux has the property that it does not create new [local extrema](@entry_id:144991) in the solution. This property is precisely what is needed to suppress Gibbs oscillations and enforce a [discrete maximum principle](@entry_id:748510). When used in a conservative FV scheme, a monotone flux guarantees that the scheme converges to the correct entropy-admissible solution. This stability is conditional upon a Courant-Friedrichs-Lewy (CFL) condition, which for a scheme like Rusanov's takes the form $\frac{\Delta t}{|S_i|} \sum_{f} |f| \lambda_f \le 1$, where $\lambda_f$ is an estimate of the local [wave speed](@entry_id:186208) normal to the face .

#### Subcell Partitioning and Time-Step Compatibility

A practical question is how many subcells, $N_s$, to use. A crucial consideration is **time-step compatibility**. The time-step restriction for an explicit DG scheme of degree $k$ on an element of size $h$ typically scales as $\Delta t_{\mathrm{DG}} \propto h/(a(2k+1))$. The time-step restriction for the subcell FV scheme scales as $\Delta t_{\mathrm{FV}} \propto \Delta x / a$, where $\Delta x = h/N_s$ is the subcell width. To ensure that activating the limiter does not force a reduction in the global time step, we must have $\Delta t_{\mathrm{FV}} \ge \Delta t_{\mathrm{DG}}$. This leads to the criterion $N_s \le 2k+1$. Choosing $N_s = 2k+1$ makes the time-step limits approximately equal, achieving perfect compatibility while providing sufficient resolution to capture the sub-elemental structure that triggered the limiter .

### Mechanism III: Reconstruction and Hierarchical Limiting

After the FV step has produced updated subcell averages, a new DG polynomial must be reconstructed for the next time step. This reconstruction must be **conservative**, at a minimum preserving the new cell average computed from the subcell data. This allows the scheme to seamlessly revert to [high-order accuracy](@entry_id:163460) in cells where shocks have dissipated or moved away .

To further refine the limiting process and minimize the introduction of unnecessary [numerical dissipation](@entry_id:141318), advanced **hierarchical fallback strategies** can be employed. Instead of immediately reverting to a first-order FV scheme, these strategies use a cascade of less intrusive interventions. A typical hierarchy is:

1.  **Level 0 (Attempt High-Order)**: Compute the unlimited high-order DG update.
2.  **Level 1 (Attempt Blending)**: If the Level 0 candidate fails admissibility checks, do not discard it entirely. Instead, blend it via a convex combination with a provably admissible low-order solution: $u^{\text{new}} = \alpha u^{\text{HO}} + (1-\alpha) u^{\text{LO}}$. The largest blending parameter $\alpha \in [0,1]$ that restores admissibility is chosen, thus retaining as much high-order information as possible.
3.  **Level 2 (Fallback to FV)**: If blending fails even for $\alpha=0$ (implying the low-order solution itself may be problematic under the current time step), only then discard the solution and re-compute the update using the robust subcell FV method as a final, guaranteed-safe fallback.

This tiered approach ensures that the scheme is as accurate as possible, but as dissipative as necessary, providing a robust and optimal framework for simulating [hyperbolic systems](@entry_id:260647) with strong discontinuities .