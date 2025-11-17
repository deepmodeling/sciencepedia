## Introduction
In the application of the Finite Volume Method (FVM) to transport phenomena, the conservation law is integrated over discrete control volumes, resulting in a balance between transport across boundaries and generation or destruction within the volume itself. This internal generation or destruction is encapsulated by the [source term](@entry_id:269111). While flux [discretization](@entry_id:145012) often receives primary attention, the numerical treatment of the [source term](@entry_id:269111) is equally critical and poses unique challenges. Improper [discretization](@entry_id:145012) can introduce significant errors, numerical instability, or lead to solutions that violate fundamental physical principles like positivity or [equilibrium states](@entry_id:168134).

This article provides a comprehensive guide to the theory and practice of [source term discretization](@entry_id:755076) in FVM. It addresses the core problem of how to approximate the [volume integral](@entry_id:265381) of the source term accurately and how to integrate the resulting system of [ordinary differential equations](@entry_id:147024) robustly in time. By navigating these challenges, you will gain the skills to build reliable and physically consistent numerical models for a wide range of scientific and engineering problems.

The following chapters will guide you through this topic systematically. "Principles and Mechanisms" will lay the foundation, covering quadrature methods for integrating the source term and the critical implications of stiffness on temporal stability. "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied to ensure physical realism, exploring well-balanced and [positivity-preserving schemes](@entry_id:753612) in fields from [chemical engineering](@entry_id:143883) to [computational finance](@entry_id:145856). Finally, "Hands-On Practices" will provide practical exercises to solidify your understanding of source term linearization and its role in building stable [implicit solvers](@entry_id:140315).

## Principles and Mechanisms

In the preceding chapter, we established that the Finite Volume Method (FVM) is founded upon the integral form of a conservation law over a discrete control volume $V_P$. For a general scalar transport equation, this balance takes the form:

$$
\frac{\mathrm{d}}{\mathrm{d}t} \int_{V_P} \phi \, \mathrm{d}V + \oint_{\partial V_P} \boldsymbol{J} \cdot \boldsymbol{n} \, \mathrm{d}A = \int_{V_P} S \, \mathrm{d}V
$$

Here, $\phi$ is the conserved scalar, $\boldsymbol{J}$ is its total flux, and $S$ is the volumetric source or sink term. The left-hand side, representing accumulation and transport, is handled by discretizing the [flux integral](@entry_id:138365) into a sum over the faces of the [control volume](@entry_id:143882). The right-hand side, representing the total rate of generation or destruction of $\phi$ within the volume, is the **source term**. Its proper discretization is crucial for the accuracy, stability, and physical fidelity of the overall numerical scheme. This chapter details the principles and mechanisms governing the numerical treatment of this [volume integral](@entry_id:265381).

### Approximating the Source Integral: Quadrature Methods

The fundamental task in [source term discretization](@entry_id:755076) is to approximate the [volume integral](@entry_id:265381) $\int_{V_P} S(\phi, \boldsymbol{x}, t) \, \mathrm{d}V$. A common starting point is to express this integral as the product of the control volume's measure $|V_P|$ and the cell-averaged source, $\overline{S}_P$:

$$
\int_{V_P} S(\phi, \boldsymbol{x}, t) \, \mathrm{d}V = \overline{S}_P |V_P|
$$

where $\overline{S}_P = \frac{1}{|V_P|} \int_{V_P} S(\phi, \boldsymbol{x}, t) \, \mathrm{d}V$. The challenge then becomes one of approximating $\overline{S}_P$. This is a problem of **[numerical quadrature](@entry_id:136578)**.

The simplest and most widely used method is the **centroid rule**, also known as the [midpoint rule](@entry_id:177487). This rule approximates the integral of a function over the volume by evaluating the function at the volume's centroid, $\boldsymbol{x}_P$, and multiplying by the volume's measure:

$$
\int_{V_P} S(\boldsymbol{x}) \, \mathrm{d}V \approx S(\boldsymbol{x}_P) |V_P|
$$

where the [centroid](@entry_id:265015) is defined as $\boldsymbol{x}_P = \frac{1}{|V_P|} \int_{V_P} \boldsymbol{x} \, \mathrm{d}V$. While this may seem like a crude approximation, it possesses remarkably powerful properties.

For a spatially uniform source, $S(\boldsymbol{x}) = S_0$, the centroid rule is not an approximation but is exact. The integral is simply $\int_{V_P} S_0 \, \mathrm{d}V = S_0 \int_{V_P} \mathrm{d}V = S_0 |V_P|$, a result that holds regardless of the complexity of the mesh geometry [@problem_id:3444829].

More impressively, the centroid rule is also exact for any source term that is a linear (or affine) function of position. Consider a source of the form $S(\boldsymbol{x}) = \alpha + \boldsymbol{\beta} \cdot \boldsymbol{x}$. Its exact cell average can be derived directly from the definition of the [centroid](@entry_id:265015) [@problem_id:3444824]:
$$
\overline{S}_P = \frac{1}{|V_P|} \int_{V_P} (\alpha + \boldsymbol{\beta} \cdot \boldsymbol{x}) \, \mathrm{d}V = \frac{1}{|V_P|} \left( \alpha \int_{V_P} \mathrm{d}V + \boldsymbol{\beta} \cdot \int_{V_P} \boldsymbol{x} \, \mathrm{d}V \right)
$$
$$
\overline{S}_P = \frac{1}{|V_P|} \left( \alpha |V_P| + \boldsymbol{\beta} \cdot (|V_P| \boldsymbol{x}_P) \right) = \alpha + \boldsymbol{\beta} \cdot \boldsymbol{x}_P = S(\boldsymbol{x}_P)
$$
This [exactness](@entry_id:268999) for polynomials of degree one is a cornerstone of the FVM's accuracy. For a general smooth [source function](@entry_id:161358) $S(\boldsymbol{x})$ in a [shape-regular mesh](@entry_id:174867) of characteristic size $h$, this property ensures that the local error of the centroid rule is second-order. Specifically, a Taylor series expansion of $S(\boldsymbol{x})$ around $\boldsymbol{x}_P$ reveals that the leading error term involves quadratic terms, leading to a local absolute error that scales as $\mathcal{O}(h^{d+2})$, where $d$ is the spatial dimension [@problem_id:3444833].

For applications requiring higher accuracy, more sophisticated **composite quadrature** rules can be employed. A general polyhedral cell can be partitioned into simpler shapes, such as tetrahedra, and a high-degree quadrature rule (e.g., a Gaussian quadrature variant) can be applied to each sub-element. If a [quadrature rule](@entry_id:175061) is exact for all polynomials up to degree $p$, and the [source function](@entry_id:161358) $S$ is sufficiently smooth (at least $C^{p+1}$), the local [absolute error](@entry_id:139354) of the composite scheme will scale as $\mathcal{O}(h^{d+p+1})$ [@problem_id:3444833].

### Discretization of Non-Smooth and Singular Sources

The assumption of a smooth source term is frequently violated in practice. Two common cases are point sources and sources with jump discontinuities.

A **point source** located at $\boldsymbol{x}_0$ with strength $q$ is modeled using the Dirac delta distribution, $S(\boldsymbol{x}) = q \delta(\boldsymbol{x} - \boldsymbol{x}_0)$. The defining property of the delta distribution is its sifting integral: $\int_V \phi(\boldsymbol{x}) \delta(\boldsymbol{x} - \boldsymbol{x}_0) \, \mathrm{d}V = \phi(\boldsymbol{x}_0)$ if $\boldsymbol{x}_0$ is in the interior of $V$. Applying this to the FVM [source term](@entry_id:269111), we find that the exact integral source for cell $V_P$ is simply $q$ if $\boldsymbol{x}_0 \in V_P$ and $0$ otherwise.

The primary principle for discretizing a [point source](@entry_id:196698) is to preserve **global conservation**. The discrete sources must sum to the total physical source, i.e., $\sum_P S_P |V_P| = q$.
*   If the source point $\boldsymbol{x}_0$ lies strictly within a single [control volume](@entry_id:143882) $V_{P_0}$, the most direct conservative approach is to assign the entire source strength to that cell: $S_{P_0}|V_{P_0}| = q$, and $S_P|V_P| = 0$ for all other cells $P \neq P_0$ [@problem_id:3444828].
*   If $\boldsymbol{x}_0$ lies on a face or vertex shared by $m$ cells, the strength $q$ must be distributed among these cells using weights $w_i$ that sum to one ($\sum_{i=1}^m w_i = 1$). A common choice is to weight by the fractional volume or area. The discrete source for each involved cell $V_{P_i}$ is then $S_{P_i}|V_{P_i}| = w_i q$. This ensures that $\sum_i S_{P_i}|V_{P_i}| = q \sum_i w_i = q$, maintaining global conservation [@problem_id:3444828].

While this discrete representation appears crude, it is **weakly consistent**. As the mesh is refined ($h \to 0$), the action of the discrete source on a discrete test function converges to the action of the continuous delta distribution on the continuous [test function](@entry_id:178872), ensuring the correct physical behavior in the limit [@problem_id:3444828].

For source terms with **jump discontinuities** across an interface, standard [quadrature rules](@entry_id:753909) that do not explicitly account for the interface geometry will exhibit poor performance. Even if a high-degree polynomial [quadrature rule](@entry_id:175061) is used, the error will be dominated by the mis-estimation of the sub-volumes on either side of the jump. This typically leads to a degradation of the local absolute error to first order, $\mathcal{O}(h^d)$, irrespective of the formal degree of the quadrature rule [@problem_id:3444833]. Accurate results in such cases require specialized interface-aware quadrature methods.

### Temporal Discretization and the Challenge of Stiffness

Once the spatial source integral is approximated, the FVM equation becomes a system of coupled [ordinary differential equations](@entry_id:147024) (ODEs) in time, one for each cell average $u_P(t)$. This is the **Method of Lines** formulation:
$$
\frac{\mathrm{d} u_P}{\mathrm{d} t} = G_P(t) + S_P(u_P, t)
$$
where $G_P(t)$ represents the discretized flux divergence and $S_P(u_P, t)$ is the approximation of the cell-averaged source per unit volume [@problem_id:3444862]. This ODE must then be integrated in time.

The source term's dependence on the unknown $u_P$ can be treated **explicitly** or **implicitly**.
*   An **explicit** treatment (e.g., Forward Euler) evaluates the source at the known time level $n$: $\frac{u_P^{n+1} - u_P^n}{\Delta t} = \dots + S_P(u_P^n, t^n)$.
*   An **implicit** treatment (e.g., Backward Euler) evaluates the source at the unknown time level $n+1$: $\frac{u_P^{n+1} - u_P^n}{\Delta t} = \dots + S_P(u_P^{n+1}, t^{n+1})$.

To understand the profound consequences of this choice, we analyze the [linear test equation](@entry_id:635061) $\frac{du}{dt} = \lambda u$, where $\lambda \in \mathbb{C}$ represents an eigenvalue of the source term's [linearization](@entry_id:267670). The time step update can be written as $u^{n+1} = R(z) u^n$, where $z = \lambda \Delta t$ and $R(z)$ is the **amplification factor**. For a stable numerical scheme, the magnitude of the [amplification factor](@entry_id:144315) must be less than or equal to one, $|R(z)| \le 1$.

For the explicit Forward Euler method, $u^{n+1} = u^n + \Delta t (\lambda u^n)$, so the amplification factor is $R_{\text{exp}}(z) = 1+z$ [@problem_id:3444876]. For a physical decay process where $\lambda$ is a large negative real number, the stability condition $|1 + \lambda \Delta t| \le 1$ requires $\lambda \Delta t \ge -2$, or $\Delta t \le 2/|\lambda|$. This imposes a severe restriction on the time step size $\Delta t$.

In contrast, for the implicit Backward Euler method, $u^{n+1} = u^n + \Delta t (\lambda u^{n+1})$, the [amplification factor](@entry_id:144315) is $R_{\text{imp}}(z) = \frac{1}{1-z}$ [@problem_id:3444876]. For any $\lambda$ with a negative real part ($\text{Re}(\lambda)  0$), $|R(z)| \le 1$ for any positive time step $\Delta t > 0$. The method is [unconditionally stable](@entry_id:146281) for decaying processes.

This brings us to the concept of **stiffness**. A source term is considered **stiff** if its [linearization](@entry_id:267670) possesses eigenvalues with large negative real parts. These eigenvalues correspond to very fast-decaying physical phenomena (e.g., fast chemical reactions, [frictional damping](@entry_id:189251)). While these processes quickly reach equilibrium, an [explicit time-stepping](@entry_id:168157) method would be forced to use an extremely small $\Delta t$ dictated by the fastest time scale (largest $|\lambda|$) to maintain stability, making the simulation prohibitively expensive. This limitation is fundamental to all explicit methods, including high-order Runge-Kutta schemes, which have bounded [stability regions](@entry_id:166035) [@problem_id:3444879]. Therefore, for problems with stiff source terms, an **implicit treatment is essential** for computational efficiency.

Higher-order schemes like the second-order **Crank-Nicolson** method, which averages the source term between time levels $n$ and $n+1$, offer a compromise. For the test equation, its [amplification factor](@entry_id:144315) is $R_{\text{CN}}(z) = \frac{1+z/2}{1-z/2}$ [@problem_id:3444862]. Like Backward Euler, it is A-stable (unconditionally stable for $\text{Re}(\lambda)  0$), but it does not damp the stiffest modes as strongly, which can sometimes lead to oscillations.

### Advanced Discretization Strategies

Beyond basic quadrature and stability considerations, advanced techniques are often required to ensure that the numerical solution respects fundamental physical principles or captures specific equilibrium behaviors.

#### Positivity and Boundedness Preservation

For many physical quantities, such as concentrations or densities, the solution $\phi$ must be non-negative. Standard implicit discretizations can sometimes produce unphysical negative values. To prevent this, a robust **source term linearization** technique, popularized by Patankar, is employed [@problem_id:3444882].

The [source term](@entry_id:269111) $S(u_P)$ is linearized as $S(u_P) \approx a_P u_P + b_P$. Substituting this into the FVM algebraic system moves the $a_P u_P$ part to the left-hand side (implicitly) while keeping the $b_P$ part on the right-hand side (explicitly). To guarantee a non-negative solution from the resulting linear system, two conditions must be met:
1.  **$a_P \le 0$**: This ensures that the [source term](@entry_id:269111)'s contribution strengthens the matrix diagonal, promoting stability and boundedness.
2.  **$b_P \ge 0$**: This ensures that the explicit part of the source term, which appears on the right-hand side of the linear system, is non-negative.

These two rules guide the treatment of different source types:
*   For a **production term** ($S(u) \ge 0$), the standard practice is to set $a_P = 0$. This trivially satisfies the first rule. The [linearization](@entry_id:267670) becomes $b_P = S(u_P)$, which is non-negative by definition, satisfying the second rule. Thus, production terms are typically treated fully explicitly.
*   For a **destruction term** ($S(u) \le 0$), a portion of the source must be treated implicitly to satisfy the rules. A choice for $a_P$ is made such that $a_P \le 0$ and the resulting $b_P = S(u_P) - a_P u_P$ is non-negative. This ensures that the destructive nature of the source enhances the stability of the numerical scheme while preserving positivity.

#### Well-Balanced Schemes for Equilibrium Problems

In many physical systems, a non-trivial steady state is achieved through a delicate balance between flux gradients and source terms, i.e., $\nabla \cdot \boldsymbol{F}(u^\star) = S(u^\star)$. Examples include the [hydrostatic balance](@entry_id:263368) in atmospheric or oceanic models. A standard FVM scheme, by discretizing the flux and source terms independently, introduces different truncation errors for each. This mismatch can destroy the perfect balance at the discrete level, leading to spurious [numerical oscillations](@entry_id:163720) or flow away from the true physical equilibrium [@problem_id:3444853].

A **[well-balanced scheme](@entry_id:756693)** is a numerical method specifically designed to exactly preserve such steady states. The core principle is to abandon the separate discretization of flux and source. Instead, the discrete [source term](@entry_id:269111) is constructed to be algebraically compatible with the discrete flux divergence, such that for the discrete steady state, their sum is exactly zero by design [@problem_id:3444853] [@problem_id:3444835].

A powerful method for achieving this is **source term absorption**. If the source term can be expressed as the divergence of another vector field, $S = \nabla \cdot \boldsymbol{G}$, the governing equation becomes a homogeneous conservation law: $\nabla \cdot (\boldsymbol{F} - \boldsymbol{G}) = 0$. The FVM is then applied to the modified flux $\boldsymbol{H} = \boldsymbol{F} - \boldsymbol{G}$. This approach has several advantages [@problem_id:3444835]:
*   **Exact Balance**: If the physical equilibrium is characterized by $\boldsymbol{F}(u^\star) = \boldsymbol{G}(u^\star)$, then the modified flux $\boldsymbol{H}(u^\star)$ is identically zero. Any consistent FVM discretization of this zero flux will also be zero, thus perfectly preserving the equilibrium.
*   **Discrete Conservation**: By treating the source as part of a flux, it automatically inherits the perfect conservation properties of the FVM. The discrete source contributions form a [telescoping sum](@entry_id:262349) across the mesh, ensuring that the total source is correctly accounted for globally.
*   **Nonlinear Consistency**: When solving the resulting nonlinear system (e.g., with Newton's method), it is crucial that the Jacobian matrix used in the solver is the true derivative of the well-balanced residual. An inconsistent linearization can compromise the solver's ability to find the exact discrete equilibrium, negating the benefits of the formulation [@problem_id:3444835].

In summary, the [discretization](@entry_id:145012) of source terms is a multi-faceted problem. While simple quadrature may suffice for well-behaved sources, robust schemes must consider issues of stability and stiffness, physical constraints like positivity, and the preservation of important [equilibrium states](@entry_id:168134). The choice of discretization strategy is therefore not merely a matter of [numerical analysis](@entry_id:142637) but is deeply intertwined with the underlying physics of the problem being solved.