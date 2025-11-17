## Introduction
In the field of [computational fluid dynamics](@entry_id:142614) and other areas involving wave propagation, accurately simulating phenomena that feature both smooth regions and sharp discontinuities, like shock waves, is a central challenge. While [high-order numerical methods](@entry_id:142601) are desirable for their efficiency in resolving smooth flows, traditional linear schemes notoriously produce unphysical oscillations when encountering these discontinuities, rendering solutions unreliable. This knowledge gap—the need for a method that is both high-order accurate in smooth regions and robustly non-oscillatory at shocks—led to the development of powerful adaptive techniques.

This article provides a comprehensive exploration of one of the most successful solutions: the Weighted Essentially Non-Oscillatory (WENO) reconstruction method. By dynamically blending information from multiple stencils, WENO achieves the dual goal of [high-order accuracy](@entry_id:163460) and shock-capturing stability. The following chapters will guide you from fundamental principles to advanced applications.

The first chapter, **Principles and Mechanisms**, will dissect the core components of WENO, explaining how smoothness indicators and nonlinear weights work together to adaptively build a high-fidelity solution. We will explore the mathematical architecture that distinguishes smooth regions from discontinuities and its application to systems of equations. In **Applications and Interdisciplinary Connections**, we will broaden our view to see how this powerful framework is extended to handle complex geometries, enforce physical constraints like positivity, and form the basis of [well-balanced schemes](@entry_id:756694) in fields from astrophysics to geophysics. Finally, the **Hands-On Practices** section provides a series of targeted problems to apply these concepts, from deriving candidate polynomials to implementing [characteristic-wise reconstruction](@entry_id:747273) and analyzing the behavior of smoothness indicators.

## Principles and Mechanisms

In the preceding chapter, we introduced the foundational concepts of [finite volume](@entry_id:749401) and [finite difference methods](@entry_id:147158) for solving [hyperbolic conservation laws](@entry_id:147752). A crucial element of these methods, particularly for achieving [high-order accuracy](@entry_id:163460), is the reconstruction of solution data. Where [finite volume methods](@entry_id:749402) track cell-averaged quantities and [finite difference methods](@entry_id:147158) track point values, both ultimately require accurate estimates of the solution or its flux at intermediate locations, typically at the interfaces between cells. This chapter delves into the principles and mechanisms of one of the most successful and widely used families of [high-order reconstruction](@entry_id:750305) techniques: the Weighted Essentially Non-Oscillatory (WENO) schemes.

### The Role of Reconstruction in Numerical Schemes

Let us consider the semi-discrete finite volume formulation for a one-dimensional [scalar conservation law](@entry_id:754531), where the rate of change of the cell average $\bar{u}_i$ in cell $I_i = [x_{i-1/2}, x_{i+1/2}]$ is governed by the [numerical fluxes](@entry_id:752791), $\hat{f}$, at its interfaces:

$$
\frac{d\bar{u}_i}{dt} = -\frac{1}{\Delta x} \left( \hat{f}_{i+1/2} - \hat{f}_{i-1/2} \right)
$$

This formulation is conservative by construction. To compute the numerical flux $\hat{f}_{i+1/2}$, a Riemann solver is typically employed, which requires as input the state of the solution on the immediate left and right sides of the interface, denoted $u_{i+1/2}^{-}$ and $u_{i+1/2}^{+}$, respectively. The fundamental challenge is that our known quantities are the cell averages $\{\bar{u}_j\}$, not these specific point values.

**Reconstruction** is the procedure by which we approximate these required interface point values from the known cell averages. This is accomplished by constructing, for each cell $I_i$, a local [polynomial approximation](@entry_id:137391) $p_i(x)$ of the solution $u(x)$ that is consistent with the known data. The interface values are then obtained by evaluating the polynomials from adjacent cells at the interface: $u_{i+1/2}^{-} = p_i(x_{i+1/2})$ and $u_{i+1/2}^{+} = p_{i+1}(x_{i+1/2})$.

The accuracy of this reconstruction is paramount. If the reconstruction procedure is of order $p$, it means that in smooth regions of the flow, the reconstructed point values approximate the true solution with an error of $\mathcal{O}(\Delta x^p)$: $u_{i+1/2}^{\mp} = u(x_{i+1/2}) + \mathcal{O}(\Delta x^p)$. Through a consistent [numerical flux](@entry_id:145174) function, this accuracy translates directly to the numerical flux itself, $\hat{f}_{i+1/2} = f(u(x_{i+1/2})) + \mathcal{O}(\Delta x^p)$. The flux difference in the [finite volume](@entry_id:749401) update then approximates the derivative of the flux, and the local truncation error of the [spatial discretization](@entry_id:172158) becomes $\mathcal{O}(\Delta x^p)$. Therefore, the order of the reconstruction directly controls the spatial accuracy of the entire numerical scheme [@problem_id:3392131] [@problem_id:3392105].

### From ENO to WENO: The Pursuit of Non-Oscillatory High Order

Achieving [high-order accuracy](@entry_id:163460) is not as simple as using a wide stencil to construct a high-degree polynomial. While this approach, known as a linear scheme, works well for smooth solutions, it fails spectacularly in the presence of discontinuities like [shock waves](@entry_id:142404). A high-degree polynomial forced to fit data across a sharp jump will inevitably produce large, [spurious oscillations](@entry_id:152404), a phenomenon related to the Gibbs effect, which can render the numerical solution useless.

The first major breakthrough in overcoming this was the development of **Essentially Non-Oscillatory (ENO)** schemes. The core idea of ENO is adaptive stenciling. To reconstruct a value at an interface, several candidate stencils of a given size are considered. The ENO algorithm then applies a selection criterion—for instance, choosing the stencil over which the solution is "smoothest" by measuring the magnitude of [divided differences](@entry_id:138238)—and uses only the polynomial from that single chosen stencil. By adaptively selecting stencils that do not cross a discontinuity, ENO methods effectively avoid interpolating across sharp gradients and thus suppress the large Gibbs-type oscillations.

**Weighted Essentially Non-Oscillatory (WENO)** schemes represent a significant improvement upon the ENO concept. Instead of a "hard" switch between stencils, WENO computes a convex combination of the polynomials from *all* candidate stencils. Each candidate polynomial is assigned a nonlinear **weight** that depends on its local smoothness. This approach offers several advantages:
1.  **Robustness:** The smooth blending of stencils avoids the potential for instabilities or loss of accuracy that can occur when the ENO selection criterion abruptly changes stencils.
2.  **Higher Accuracy:** By using a specific convex combination, WENO schemes can achieve a higher [order of accuracy](@entry_id:145189) in smooth regions than the underlying candidate polynomials. For example, a fifth-order WENO scheme is built from a combination of third-order candidate polynomials.

In essence, while ENO *selects* the best stencil, WENO computes a *weighted average* of all stencils, where the weights are designed to be close to pre-defined optimal values in smooth regions and to automatically vanish for stencils that cross a discontinuity. This dual objective—achieving optimal high order in smooth regions and robustly avoiding oscillations at discontinuities—is the hallmark of the WENO methodology [@problem_id:3392118].

### The Architecture of WENO Reconstruction

Let us now dissect the components of a typical WENO scheme, using the popular fifth-order Jiang-Shu formulation (WENO5-JS) as our primary example. To reconstruct the left-state $u_{i+1/2}^{-}$ at the interface, the scheme uses cell averages from a five-point global stencil $\{ \bar{u}_{i-2}, \bar{u}_{i-1}, \bar{u}_i, \bar{u}_{i+1}, \bar{u}_{i+2} \}$. This global stencil is partitioned into three overlapping three-point sub-stencils, each used to construct a quadratic candidate polynomial.

#### Smoothness Indicators ($\beta_k$)

The heart of the WENO weighting mechanism lies in the ability to quantify the "smoothness" of the solution on each sub-stencil. This is the role of the **smoothness indicators**, denoted $\beta_k$. For each candidate polynomial $p_k(x)$ (where $k$ indexes the sub-stencil), the indicator $\beta_k$ measures its oscillatory content. The formulation proposed by Jiang and Shu defines these indicators as the scaled sum of the squared $L^2$-norms of the derivatives of the polynomial over a cell:

$$
\beta_k = \sum_{\ell=1}^{r-1} \int_{I_i} \Delta x^{2\ell-1} \left( \frac{d^\ell p_k(x)}{dx^\ell} \right)^2 dx
$$

Here, $r-1$ is the degree of the polynomials (for WENO5, $r-1=2$). A function with high-frequency oscillations will have large derivatives, resulting in a large value for $\beta_k$. Conversely, a smooth, slowly varying function will yield a small $\beta_k$. For a uniform grid, these integrals can be computed exactly, yielding discrete formulas for the smoothness indicators in terms of the cell averages. For the fifth-order left-biased reconstruction at $x_{i+1/2}$, the three indicators are [@problem_id:3392181]:

$$
\beta_0 = \frac{13}{12}(\bar{u}_{i-2} - 2\bar{u}_{i-1} + \bar{u}_i)^2 + \frac{1}{4}(\bar{u}_{i-2} - 4\bar{u}_{i-1} + 3\bar{u}_i)^2 \\
\beta_1 = \frac{13}{12}(\bar{u}_{i-1} - 2\bar{u}_i + \bar{u}_{i+1})^2 + \frac{1}{4}(\bar{u}_{i-1} - \bar{u}_{i+1})^2 \\
\beta_2 = \frac{13}{12}(\bar{u}_i - 2\bar{u}_{i+1} + \bar{u}_{i+2})^2 + \frac{1}{4}(3\bar{u}_i - 4\bar{u}_{i+1} + \bar{u}_{i+2})^2
$$

In regions where the solution is smooth, these indicators scale as $\beta_k = \mathcal{O}(\Delta x^2)$. If a stencil crosses a discontinuity of magnitude $\mathcal{O}(1)$, the indicator becomes $\mathcal{O}(1)$. This difference in scaling is what allows the scheme to distinguish smooth from non-smooth regions.

#### Nonlinear Weights ($\omega_k$)

The **nonlinear weights**, $\omega_k$, are constructed from the smoothness indicators. The final reconstruction is a convex combination:

$$
u_{i+1/2}^{-} = \sum_{k=0}^{2} \omega_k u_{i+1/2}^{(k)}
$$

where $u_{i+1/2}^{(k)}$ are the third-order accurate interface values obtained from the individual candidate polynomials. The weights are calculated as follows:

$$
\omega_k = \frac{\alpha_k}{\sum_{j=0}^{2} \alpha_j} \quad \text{with} \quad \alpha_k = \frac{d_k}{(\varepsilon + \beta_k)^p}
$$

Let's break down the components of the unnormalized weights $\alpha_k$ [@problem_id:3392174] [@problem_id:3392104]:
*   The **ideal weights**, $d_k$ (also denoted $\gamma_k$), are positive constants that sum to one. For the fifth-order left-biased scheme, they are $d_0=0.1$, $d_1=0.6$, $d_2=0.3$. These values are not arbitrary; they are precisely chosen so that the [linear combination](@entry_id:155091) $\sum d_k u_{i+1/2}^{(k)}$ cancels lower-order error terms to yield a fifth-order accurate approximation. They represent the target weighting in smooth regions.
*   The **[regularization parameter](@entry_id:162917)**, $\varepsilon$, is a small positive number (e.g., $\varepsilon = 10^{-6}$) whose sole purpose is to prevent division by zero in the denominator, which would occur if a stencil were perfectly smooth (e.g., a linear function), causing $\beta_k=0$.
*   The **exponent**, $p$ (typically $p=2$), controls the sensitivity of the weights to the smoothness indicators. A larger value of $p$ more strongly penalizes stencils with larger $\beta_k$, leading to a sharper distinction between smooth and non-smooth stencils.

The mechanism is elegant. In a smooth region, all $\beta_k$ are small ($\mathcal{O}(\Delta x^2)$). The $\varepsilon$ term is negligible, and the $\beta_k$ values are similar, causing the nonlinear weights $\omega_k$ to converge to the ideal weights $d_k$, thus achieving fifth-order accuracy. Near a discontinuity, if stencil $S_k$ crosses the jump, its $\beta_k$ becomes large ($\mathcal{O}(1)$). The denominator $(\varepsilon + \beta_k)^p$ becomes huge, driving $\alpha_k$ and consequently $\omega_k$ towards zero. The scheme automatically gives almost no weight to the oscillatory polynomial, thus preserving the non-oscillatory property.

### Application to Hyperbolic Systems

Real-world problems in fluid dynamics are almost always described by [systems of conservation laws](@entry_id:755768), such as the Euler equations. Applying the WENO methodology to systems requires additional considerations related to the physical propagation of information.

#### Flux Splitting for Upwinding

The WENO reconstruction uses stencils that are biased in a particular direction (e.g., left-biased for $u_{i+1/2}^{-}$). This implicit directionality must be aligned with the physical direction of wave propagation. For a scalar equation, this direction is given by the sign of the [characteristic speed](@entry_id:173770) $f'(u)$. If $f'(u)$ can change sign within the domain (a [transonic flow](@entry_id:160423), for example), a single fixed-bias reconstruction is unstable.

The solution is to use **[flux splitting](@entry_id:637102)**. The physical flux $f(u)$ is split into two parts, $f(u) = f^+(u) + f^-(u)$, where the Jacobian of $f^+$ has only non-negative eigenvalues and the Jacobian of $f^-$ has only non-positive eigenvalues. A common and simple method is the global **Lax-Friedrichs splitting**:

$$
f^{\pm}(u) = \frac{1}{2}(f(u) \pm \alpha u)
$$

To ensure the required sign properties of the eigenvalues, the parameter $\alpha$ must be chosen as an upper bound on the [characteristic speeds](@entry_id:165394): $\alpha \ge \max_u |f'(u)|$. With this split, one can safely apply a left-biased WENO reconstruction to the components of $f^+$ (which represent right-going information) and a right-biased reconstruction to the components of $f^-$ (representing left-going information). The final [numerical flux](@entry_id:145174) is the sum of the reconstructed split fluxes: $\hat{f}_{i+1/2} = \hat{f}^+_{i+1/2} + \hat{f}^-_{i+1/2}$ [@problem_id:3392145].

#### Characteristic-wise Reconstruction

For a system of $m$ equations, such as the Euler equations where $u = (\rho, \rho v, E)^T$, a physical discontinuity (e.g., a shock wave) is associated with a single characteristic field. However, this discontinuity will generally manifest as jumps in all components of the conservative variable vector $u$. A naive **component-wise WENO reconstruction**, applied independently to each component of $u$, would therefore "see" a discontinuity in every equation. This triggers the non-oscillatory mechanism for all fields, even those that are physically smooth across that particular wave. This cross-contamination can lead to excessive numerical dissipation and even [spurious oscillations](@entry_id:152404).

A physically more astute and numerically superior approach is **[characteristic-wise reconstruction](@entry_id:747273)**. The procedure at each interface involves:
1.  **Local Linearization:** Approximate the system locally by $u_t + A(u^*) u_x = 0$, where $A(u) = \partial f / \partial u$ is the flux Jacobian evaluated at an averaged state $u^*$.
2.  **Projection:** Decompose the Jacobian $A(u^*) = R \Lambda L$, where $R$ and $L$ are the matrices of right and left eigenvectors, and $\Lambda$ is the diagonal matrix of eigenvalues ([characteristic speeds](@entry_id:165394)). Project the data from the reconstruction stencil into the characteristic fields by multiplying by the left eigenvector matrix, $L$.
3.  **Scalar Reconstruction:** Apply the scalar WENO reconstruction algorithm independently to each of the $m$ [characteristic variables](@entry_id:747282). Since the system is locally decoupled in these variables, a discontinuity in one characteristic field does not affect the reconstruction of the others.
4.  **Projection Back:** Transform the reconstructed interface values of the [characteristic variables](@entry_id:747282) back to the conservative variables by multiplying by the right eigenvector matrix, $R$.

This procedure aligns the nonlinear weighting of the WENO scheme with the physical wave structure of the system. It isolates discontinuities within their respective characteristic families, allowing smooth waves to be reconstructed with full [high-order accuracy](@entry_id:163460) while the non-smooth wave is handled robustly. This leads to a significant reduction in spurious oscillations and a sharper resolution of physical phenomena [@problem_id:3392133].

### Advanced Topics and Modern Variants

The classical WENO scheme, while highly successful, is not without its subtleties and limitations, which has spurred continued research and refinement.

#### Total Variation and the "Essentially Non-Oscillatory" Property

A numerical scheme is called **Total Variation Diminishing (TVD)** if the [total variation](@entry_id:140383) of the discrete solution, $TV(u) = \sum_i |u_{i+1} - u_i|$, does not increase in time. Godunov's theorem famously proved that any linear TVD scheme is at most first-order accurate. WENO schemes achieve high order by virtue of their nonlinearity, but this very nonlinearity means they are **not strictly TVD**.

It is possible to construct scenarios, most notably involving smooth extrema (critical points where $u_x=0$), where a high-order WENO scheme can cause a small, bounded increase in the total variation. This typically manifests as a slight sharpening or "clipping" of a smooth peak. A classic counterexample is the evolution of a simple sine wave, where the total variation can slightly increase near the crests and troughs [@problem_id:3392120].

This is why the schemes are called *Essentially* Non-Oscillatory. The crucial achievement of WENO is not the strict enforcement of a TVD property, but the suppression of the large, $\mathcal{O}(1)$, Gibbs-type oscillations that plague linear schemes at discontinuities. The small, bounded oscillations or increases in total variation that may occur are on the order of the scheme's truncation error and do not compromise the solution's stability or qualitative correctness.

#### Accuracy Degradation at Critical Points

The Achilles' heel of the classical WENO-JS scheme is its performance at smooth critical points. The design of the smoothness indicators $\beta_k$ can lead them to misinterpret certain smooth profiles, causing an unintended loss of accuracy. For the fifth-order scheme, a detailed [asymptotic analysis](@entry_id:160416) reveals:
*   At a simple critical point where $u'=0$ but $u'' \neq 0$, the [order of accuracy](@entry_id:145189) degrades from fifth to fourth.
*   At a double critical point where $u'=u''=0$ but $u''' \neq 0$ (e.g., for a function like $u(x) = x^3$), the degradation is more severe. The smoothness indicators can differ by orders of magnitude even though the function is perfectly smooth, fooling the weighting mechanism into thinking some stencils are "less smooth" than others. This causes the nonlinear weights $\omega_k$ to fail to converge to the ideal weights $d_k$. The scheme effectively collapses to the third-order accuracy of a single candidate stencil, a significant loss from its designed fifth-order performance [@problem_id:3392134].

#### The WENO-Z Improvement

To address this accuracy degradation, improved variants of WENO have been developed. A prominent example is the **WENO-Z** scheme. The key innovation is to make the nonlinear weights sensitive not only to the local smoothness on each sub-stencil but also to a higher-order, "global" measure of smoothness across the entire stencil. The WENO-Z weights take the form:

$$
\alpha_k = d_k \left( 1 + \left( \frac{\tau_{2r-1}}{\beta_k + \varepsilon} \right)^p \right)
$$

For the fifth-order scheme, the global smoothness indicator is $\tau_5 = |\beta_0 - \beta_2|$. This term is of a higher asymptotic order in $\Delta x$ than the individual $\beta_k$ in smooth regions. At a critical point, the additive term in the parentheses acts as a small correction that is nearly uniform across the stencils, pushing the nonlinear weights back towards the ideal weights and restoring the full fifth-order accuracy. Near a discontinuity, the term is designed such that the scheme's non-oscillatory properties are retained. The development of WENO-Z and other advanced variants highlights the ongoing effort to create numerical methods that are not only high-order and robust but also uniformly accurate for a wide range of solution structures [@problem_id:3392157].