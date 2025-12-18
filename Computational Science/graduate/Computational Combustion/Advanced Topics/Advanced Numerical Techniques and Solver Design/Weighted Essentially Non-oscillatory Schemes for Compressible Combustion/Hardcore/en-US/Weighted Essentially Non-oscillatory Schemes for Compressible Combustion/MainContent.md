## Introduction
Simulating [compressible combustion](@entry_id:1122756), with its volatile mix of shock waves and intricate flame fronts, is a grand challenge in computational science. The governing [reactive flow](@entry_id:1130651) equations demand numerical methods that can capture steep discontinuities without creating unphysical oscillations, yet remain highly accurate to resolve delicate chemical reaction zones. This necessity exposes a fundamental conflict between accuracy and stability, a problem that classical schemes struggle to overcome. Weighted Essentially Non-oscillatory (WENO) schemes have emerged as a powerful solution, providing the fidelity and robustness required for predictive simulations.

This article provides a comprehensive overview of WENO methods tailored for combustion. The journey begins in the **Principles and Mechanisms** section, where we will deconstruct the core idea of WENO, tracing its evolution from earlier methods and detailing its nonlinear weighting strategy. Next, the **Applications and Interdisciplinary Connections** section will demonstrate how these principles are put into practice to model complex phenomena like detonations and integrated into sophisticated simulation frameworks. Finally, the **Hands-On Practices** section will offer practical problems to reinforce these concepts. We will begin by exploring the fundamental principles that make WENO schemes a cornerstone of modern [computational combustion](@entry_id:1122776).

## Principles and Mechanisms

The accurate numerical simulation of [compressible combustion](@entry_id:1122756) phenomena, such as detonations and turbulent flames, presents a formidable challenge. The governing equations—the reactive Euler or Navier-Stokes equations—are a system of hyperbolic-[parabolic partial differential equations](@entry_id:753093) whose solutions exhibit a vast range of spatial and temporal scales. These solutions are characterized by the simultaneous presence of sharp, discontinuous features like shock waves and contact surfaces, and smooth but highly localized structures like reaction zones and diffusion layers. A numerical method must be able to capture the sharp discontinuities without introducing spurious, non-physical oscillations, while simultaneously resolving the smooth structures with high-order accuracy to correctly predict flame speeds, ignition delays, and chemical kinetics. This chapter delves into the principles and mechanisms of Weighted Essentially Non-Oscillatory (WENO) schemes, a class of high-order methods that have become a cornerstone of modern [computational combustion](@entry_id:1122776) for their ability to meet these dual requirements.

### The Challenge of High-Order Accuracy and Monotonicity

The fundamental difficulty in discretizing [hyperbolic conservation laws](@entry_id:147752), which form the convective backbone of the [reactive flow](@entry_id:1130651) equations, is encapsulated by **Godunov's theorem**. This theorem states that any linear numerical scheme that is monotone (i.e., does not create new [local extrema](@entry_id:144991)) can be at most first-order accurate . This is a severe limitation, as first-order schemes are too dissipative to accurately resolve the complex flow features in combustion. For instance, a first-order upwind scheme would smear a shock wave or a flame front over many grid cells, completely obscuring its internal structure.

To achieve higher-order accuracy, schemes must necessarily be non-monotone. Classical high-order linear schemes, like the Lax-Wendroff scheme, achieve second-order accuracy but are notorious for producing spurious oscillations (Gibbs phenomena) around discontinuities. These oscillations are not merely cosmetic defects; in a [reacting flow simulation](@entry_id:1130632), they can cause unphysical negative values for density or species mass fractions, or generate artificial temperature spikes that can erroneously trigger chemical reactions, leading to a complete failure of the simulation.

The first successful attempts to create high-order, [non-oscillatory schemes](@entry_id:1128816) led to the development of **Total Variation Diminishing (TVD)** schemes in the 1980s. A scheme is TVD if the [total variation](@entry_id:140383) of the discrete solution, $TV(u) = \sum_i |u_{i+1} - u_i|$, does not increase in time. TVD schemes, such as those based on the Monotonic Upstream-centered Scheme for Conservation Laws (MUSCL) with [slope limiters](@entry_id:638003), cleverly circumvent Godunov's theorem by introducing nonlinearity. The scheme is high-order in smooth regions but the 'limiter' function nonlinearly reduces the scheme's order to first-order near sharp gradients to suppress oscillations and enforce the TVD condition . While a major breakthrough, TVD schemes have a critical drawback: to prevent the formation of new extrema, the limiter function must clip the solution at smooth [local maxima and minima](@entry_id:274009). As a consequence, any TVD scheme degenerates to [first-order accuracy](@entry_id:749410) at smooth critical points, a property that can compromise the accuracy of resolving curved flame fronts or turbulent eddies.

### The Essentially Non-Oscillatory (ENO) Philosophy

The limitations of TVD schemes motivated the development of **Essentially Non-Oscillatory (ENO)** schemes. The philosophy of ENO is fundamentally different: instead of starting with a high-order scheme and adding dissipation to control oscillations, ENO constructs a high-order approximation from the outset using only "smooth" data. The core idea is to adaptively choose a reconstruction stencil that avoids crossing any large gradients or discontinuities.

In a finite-volume framework, we work with cell averages, $\bar{u}_j$. To compute the flux at an interface, say $x_{i+1/2}$, we need to reconstruct point values $u_{i+1/2}^{-}$ (the state to the left of the interface) and $u_{i+1/2}^{+}$ (the state to the right). An ENO reconstruction of order $r$ accomplishes this by constructing a polynomial of degree $r-1$ using data from a stencil of $r$ contiguous cells. The key is the selection of this stencil.

The ENO stencil [selection algorithm](@entry_id:637237) proceeds hierarchically. To build an $r$-point stencil for the state $u_{i+1/2}^{-}$, it starts with the cell immediately to the left, $I_i$. It then adds one cell at a time, at each step choosing between the next available cell to the left and the next to the right. The choice is made by selecting the candidate stencil that is "smoother," as measured by the magnitude of a Newton divided difference. This process ensures that the final stencil is the smoothest possible among all candidates of size $r$ containing cell $I_i$.

Let us illustrate this for a third-order ($r=3$) reconstruction using the cell-average data from a hypothetical reaction front :
$$
\bar{u}_{i-2} = 1.0, \quad \bar{u}_{i-1} = 1.0, \quad \bar{u}_{i} = 1.2, \quad \bar{u}_{i+1} = 5.0, \quad \bar{u}_{i+2} = 5.0
$$
A steep gradient is clearly visible between cells $I_i$ and $I_{i+1}$.

1.  **Initial Stencil ($r=1$):** The stencil must contain the cell to the left of the interface, so we start with $\{i\}$.

2.  **Extension to $r=2$:** We choose between stencils $\{i-1, i\}$ and $\{i, i+1\}$. We compare the magnitude of the first differences:
    -   Variation on the left: $|\bar{u}_i - \bar{u}_{i-1}| = |1.2 - 1.0| = 0.2$.
    -   Variation on the right: $|\bar{u}_{i+1} - \bar{u}_i| = |5.0 - 1.2| = 3.8$.
    Since $0.2  3.8$, the leftward extension is smoother. The stencil becomes $\{i-1, i\}$.

3.  **Extension to $r=3$:** We now choose between stencils $\{i-2, i-1, i\}$ and $\{i-1, i, i+1\}$. We compare the magnitude of the second differences:
    -   Variation on the left: $|\bar{u}_i - 2\bar{u}_{i-1} + \bar{u}_{i-2}| = |1.2 - 2(1.0) + 1.0| = |0.2| = 0.2$.
    -   Variation on the right: $|\bar{u}_{i+1} - 2\bar{u}_i + \bar{u}_{i-1}| = |5.0 - 2(1.2) + 1.0| = |3.6| = 3.6$.
    Again, the leftward extension is smoother ($0.2  3.6$).

The final chosen stencil is $\{i-2, i-1, i\}$. The algorithm has successfully selected a stencil that lies entirely in the smooth region upstream of the steep gradient. A quadratic polynomial is then uniquely defined by requiring its averages over these three cells to match the given data, and this polynomial can be evaluated at $x_{i+1/2}$ to yield the reconstructed state $u_{i+1/2}^{-}$. For this specific data and a standard finite-volume reconstruction, the result is $u_{i+1/2}^{-} = \frac{41}{30}$ .

By adaptively selecting the stencil, ENO schemes avoid the accuracy degradation at smooth [extrema](@entry_id:271659) that plagues TVD schemes. However, the stencil selection process can be overly sensitive, and the resulting accuracy of the scheme can be non-uniform as the stencil may abruptly shift from one time step to the next, even in smooth flows.

### The WENO Principle: Weighted Averaging for Optimal Accuracy

**Weighted Essentially Non-Oscillatory (WENO)** schemes improve upon ENO by replacing the hard-logic stencil selection with a smooth, nonlinear weighting procedure. Instead of picking just one "best" stencil, WENO considers all possible candidate stencils and assigns each a weight. The final reconstruction is a convex combination of the reconstructions from all candidate stencils. This averaging process leads to a more robust and slightly more accurate scheme than ENO.

A fifth-order WENO scheme ($2k-1=5 \implies k=3$), for example, considers the three candidate 3-point stencils that were available in the ENO example: $S_0=\{i-2, i-1, i\}$, $S_1=\{i-1, i, i+1\}$, and $S_2=\{i, i+1, i+2\}$. For each stencil $S_k$, a quadratic reconstruction polynomial $p_k(x)$ is formed. The final reconstructed value is:
$$
u_{i+1/2} = \omega_0 p_0(x_{i+1/2}) + \omega_1 p_1(x_{i+1/2}) + \omega_2 p_2(x_{i+1/2})
$$
The key lies in the definition of the **nonlinear weights** $\omega_k$. They are constructed to satisfy two competing goals:
1.  **In smooth regions**, the weights should converge to a set of pre-defined **optimal linear weights**, $d_k$. These linear weights are chosen such that the combination $\sum d_k p_k(x)$ exactly reproduces a single, higher-degree polynomial on the largest possible stencil (a [5-point stencil](@entry_id:174268) in this case), yielding the optimal order of accuracy, which is $2k-1=5$.
2.  **Near discontinuities**, the weights for stencils that cross the discontinuity should become vanishingly small, effectively removing their contribution and preventing oscillations.

The classical WENO-JS formulation by Jiang and Shu achieves this with the following procedure :
$$
\omega_k = \frac{\alpha_k}{\sum_{j} \alpha_j} \quad \text{with} \quad \alpha_k = \frac{d_k}{(\varepsilon + \beta_k)^p}
$$
Here, $d_k$ are the optimal linear weights (for 5th order, $d_0=0.1, d_1=0.6, d_2=0.3$ for a reconstruction at the right edge of cell $i$). The parameter $\varepsilon$ is a small positive number (e.g., $10^{-6}$) to prevent division by zero, and $p$ is an integer exponent (typically $p=2$) that controls the sensitivity of the weights.

The most important component is the **smoothness indicator**, $\beta_k$. It is designed to measure the oscillatory content of the solution on the candidate stencil $S_k$. For a [finite-difference](@entry_id:749360) setting, the indicators are defined as a scaled sum of the squared $L^2$-norms of the derivatives of the reconstruction polynomial $p_k(x)$ over its stencil :
$$
\beta_k = \sum_{l=1}^{k-1} \int_{x_{i-1/2}}^{x_{i+1/2}} (\Delta x)^{2l-1} \left( \frac{d^l p_k(x)}{dx^l} \right)^2 dx
$$
When expressed in terms of the grid point values $q_j$, these integrals evaluate to compact formulas. For the three candidate stencils of a fifth-order scheme, they are:
$$
\begin{align}
\beta_0 = \frac{13}{12}(q_{i-2}-2q_{i-1}+q_i)^2 + \frac{1}{4}(q_{i-2}-4q_{i-1}+3q_i)^2 \\
\beta_1 = \frac{13}{12}(q_{i-1}-2q_i+q_{i+1})^2 + \frac{1}{4}(q_{i-1}-q_{i+1})^2 \\
\beta_2 = \frac{13}{12}(q_i-2q_{i+1}+q_{i+2})^2 + \frac{1}{4}(3q_i-4q_{i+1}+q_{i+2})^2
\end{align}
$$
Each term in these formulas is a squared [finite difference approximation](@entry_id:1124978) of a first or second derivative. Therefore, if the function is smooth on a stencil (e.g., constant or linear), its derivatives are small, and $\beta_k$ will be small (specifically, $\beta_k = \mathcal{O}(\Delta x^2)$). If the stencil crosses a shock, the differences become large, and $\beta_k$ becomes large ($\beta_k = \mathcal{O}(1)$).

The weighting mechanism now becomes clear. In smooth regions, all $\beta_k$ are small and of the same order. The $\varepsilon$ term may dominate if the solution is very smooth, and the weights $\omega_k$ approximate the optimal linear weights $d_k$, yielding fifth-order accuracy. Near a shock, if stencil $S_k$ crosses the discontinuity, its $\beta_k$ becomes large. The large denominator $(\varepsilon + \beta_k)^p$ drives the unnormalized weight $\alpha_k$ to near zero. Consequently, the final weight $\omega_k$ is also near zero, and the oscillatory contribution from that stencil is effectively removed from the final reconstruction. This local, adaptive weighting allows WENO to be "Essentially Non-Oscillatory" without enforcing a global TVD condition, thereby avoiding the accuracy loss at extrema that affects TVD schemes .

### Application to Systems of Compressible Flow Equations

Extending the scalar WENO reconstruction to a system of equations like the reactive Euler equations requires additional steps. A naive component-wise application of the scalar algorithm to each conserved variable (density, momentum, energy, etc.) is problematic. A single physical feature, like a shock wave, is a discontinuity in multiple variables, but the relationships between them are governed by the underlying wave physics. Applying the smoothness indicators independently to each component can lead to inconsistent stencil choices and weights across the components, generating spurious pressure or velocity oscillations, particularly at material contact surfaces .

#### Characteristic-Wise Reconstruction

The proper way to apply WENO to a system is through **[characteristic-wise reconstruction](@entry_id:747273)**. The principle is to locally transform the governing equations into a set of uncoupled, scalar advection equations, apply the robust scalar WENO algorithm to each, and then transform back. This is achieved by [local linearization](@entry_id:169489) .

At each cell interface $x_{i+1/2}$, the system $U_t + F(U)_x = 0$ is approximated by a linear system $U_t + A_{i+1/2} U_x = 0$, where $A_{i+1/2}$ is the flux Jacobian $\partial F/\partial U$ evaluated at a suitable averaged state (e.g., a Roe average of $U_i$ and $U_{i+1}$). Since the system is hyperbolic, the Jacobian is diagonalizable:
$$
A_{i+1/2} = R_{i+1/2} \Lambda_{i+1/2} L_{i+1/2}
$$
where $\Lambda$ is the diagonal matrix of eigenvalues (wave speeds), $R$ is the matrix of right eigenvectors, and $L=R^{-1}$ is the matrix of left eigenvectors. By defining the **[characteristic variables](@entry_id:747282)** $V = L U$, the system locally decouples into a set of scalar advection equations, $V_t + \Lambda V_x = 0$.

The computational procedure is as follows  :
1.  At each interface $x_{i+1/2}$, compute an average state and the corresponding Jacobian $A_{i+1/2}$ and its eigen-decomposition $(R, \Lambda, L)_{i+1/2}$. For multi-dimensional problems, this must be done for the Jacobian of the flux normal to the interface, $A_n = \partial(F \cdot n) / \partial U$ .
2.  For each cell $j$ in the reconstruction stencil, project the cell-averaged [conserved variables](@entry_id:747720) $\bar{U}_j$ into characteristic space: $\bar{V}_j = L_{i+1/2} \bar{U}_j$.
3.  For each component $p$ of the [characteristic variables](@entry_id:747282), apply the scalar WENO reconstruction algorithm to the set $\{\bar{V}^{(p)}_j\}$ to obtain the interface values $V_{i+1/2}^{(p),-}$ and $V_{i+1/2}^{(p),+}$.
4.  Assemble the vectors of reconstructed [characteristic variables](@entry_id:747282), $V_{i+1/2}^{-}$ and $V_{i+1/2}^{+}$.
5.  Transform these back to physical space: $U_{i+1/2}^{-} = R_{i+1/2} V_{i+1/2}^{-}$ and $U_{i+1/2}^{+} = R_{i+1/2} V_{i+1/2}^{+}$.
6.  Finally, feed these left and right states into an approximate Riemann solver to compute the [numerical flux](@entry_id:145174) $\hat{F}_{i+1/2}$.

This procedure ensures that the nonlinear weighting is applied to the fields that actually carry the waves, decoupling their interactions and significantly reducing [spurious oscillations](@entry_id:152404). For this to be accurate, especially in combustion, the eigenvalues (e.g., $u, u \pm c$) must be computed using a realistic equation of state where the speed of sound $c$ depends on local temperature and composition .

#### Flux Splitting

An alternative to the full [characteristic decomposition](@entry_id:747276), which can be computationally expensive, is to use **[flux splitting](@entry_id:637102)**. A common and simple approach is the **Local Lax-Friedrichs (LLF)** or Rusanov splitting. The physical flux $F(U)$ is split into two parts, $F^{+}$ and $F^{-}$, which are guaranteed to have non-negative and non-positive eigenvalues, respectively. This means $F^{+}$carries information to the right, and $F^{-}$ carries information to the left.
$$
F^{\pm}(U) = \frac{1}{2} (F(U) \pm \alpha U)
$$
The dissipation coefficient $\alpha$ must be chosen to be greater than or equal to the largest local [wave speed](@entry_id:186208). At an interface $x_{i+1/2}$, it is chosen as $\alpha_{i+1/2} = \max(|u_i|+c_i, |u_{i+1}|+c_{i+1})$ .

With this split, the total numerical flux is the sum of two upwind-biased reconstructions: the $F^{+}$ flux is reconstructed using a left-biased stencil (e.g., from cells $i, i-1, \dots$), and the $F^{-}$ flux is reconstructed using a right-biased stencil (from cells $i+1, i+2, \dots$). The WENO algorithm is applied to each component of $F^{+}$ and $F^{-}$ separately. While simpler than a full [characteristic decomposition](@entry_id:747276), this component-wise reconstruction of split fluxes can still be prone to oscillations and is generally less robust. A hybrid approach, where the split fluxes $F^{\pm}$ are themselves projected into a characteristic basis before reconstruction, combines the advantages of both methods .

### Advanced Topics and Refinements

The classical WENO-JS scheme, while powerful, has known deficiencies and sensitivities that have motivated further research and the development of improved variants.

#### The Role of Tuning Parameters $\epsilon$ and $p$

The behavior of the WENO-JS weights is highly sensitive to the parameters $\varepsilon$ and $p$.
- The power **$p$** controls the degree of discrimination. A larger $p$ (e.g., $p=2$ or $p=4$) makes the weights more sensitive to differences in the smoothness indicators. This leads to a sharper resolution of discontinuities but can decrease robustness, as the scheme may overreact to small amounts of numerical noise, especially on under-resolved grids .
- The parameter **$\varepsilon$** was originally introduced simply to avoid division by zero. However, it plays a crucial role in the scheme's behavior. If $\varepsilon$ is very small compared to the smoothness indicators $\beta_k$, the scheme is highly sensitive and sharp, but can be unstable. If $\varepsilon$ is chosen to be large (e.g., on the order of the $\beta_k$ values in smooth regions), the scheme becomes more like a linear scheme, losing its sharp non-oscillatory character but gaining robustness. A common practice is to choose a fixed, small $\varepsilon$ (e.g., $10^{-6}$). However, some analysis suggests scaling $\varepsilon$ with the grid spacing, such as $\varepsilon \sim \mathcal{O}(\Delta x^2)$, can improve the scheme's behavior at [critical points](@entry_id:144653) .

A concrete example from  illustrates this trade-off. For smoothness indicators $\beta_0 = 10^{-8}, \beta_1 = 10^{-6}, \beta_2 = 10^{-4}$:
- Case I: $(\varepsilon, p) = (10^{-12}, 2)$. This aggressive choice yields weights $\mathbf{w} \approx (0.9994, 0.0006, 0.0)$, showing extreme preference for the smoothest stencil.
- Case II: $(\varepsilon, p) = (10^{-6}, 1)$. This more moderate choice yields weights $\mathbf{w} \approx (0.2463, 0.7463, 0.0074)$, which are much closer to the optimal linear weights $\mathbf{d}=(0.1, 0.6, 0.3)$.
Case I will be sharper but potentially less stable than Case II.

#### Accuracy Degradation at Critical Points and Improved Schemes

A significant theoretical deficiency of the WENO-JS scheme is its loss of accuracy at smooth [critical points](@entry_id:144653) (where the first derivative of the solution is zero, but higher derivatives are not). For a WENO scheme with formal accuracy of $2k-1$ in general smooth regions, the order degrades to just $k$ at these points . This is because the smoothness indicators all become very small, and the standard weighting formula fails to make the nonlinear weights converge to the optimal linear weights at the required rate.

Several "improved" WENO schemes have been designed to fix this issue.
- **Mapped WENO (WENO-M):** Proposed by Henrick, Aslam, and Powers, this approach takes the final WENO-JS weights $\omega_k$ and passes them through a specially designed mapping function, $g_k(\omega_k)$, before re-normalization. This function is constructed to satisfy several mathematical properties, including $g_k(d_k)=d_k$ and having vanishing first and second derivatives at $d_k$. This ensures that the mapped weights approach the optimal weights much more rapidly in smooth regions, restoring the full $2k-1$ order of accuracy everywhere. A valid mapping function for this purpose is given by :
$$
g_k(\omega_k) = \frac{\omega_k ( d_k + d_k^2 - 3 d_k \omega_k + \omega_k^2 )}{d_k^2 + \omega_k ( 1 - 2 d_k )}
$$
- **WENO-Z:** Proposed by Borges et al., this scheme takes a different approach by modifying the definition of the un-normalized weights $\alpha_k$. It introduces a *global* smoothness indicator, $\tau$, which is a measure of the difference in smoothness across the entire large stencil (e.g., $\tau_5 = |\beta_0 - \beta_2|$ for the 5th order case). The weights are redefined as :
$$
\alpha_k^{\text{Z}} = d_k \left( 1 + \left( \frac{\tau_5}{\beta_k + \epsilon} \right)^p \right)
$$
At a critical point, all $\beta_k$ and $\tau_5$ become small, but $\tau_5$ vanishes faster than $\beta_k$. This causes the term in the parenthesis to rapidly approach 1, forcing the weights $\omega_k^{\text{Z}}$ to approach the optimal weights $d_k$ at the rate required to restore full $2k-1$ accuracy .

These improved schemes offer higher fidelity in resolving complex smooth flow features, which is critical for problems in turbulence and combustion, while retaining the excellent shock-capturing properties of the original WENO-JS formulation.