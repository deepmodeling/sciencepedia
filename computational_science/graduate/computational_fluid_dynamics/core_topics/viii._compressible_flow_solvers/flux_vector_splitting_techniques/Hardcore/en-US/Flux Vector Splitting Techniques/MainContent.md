## Introduction
In the field of Computational Fluid Dynamics (CFD), accurately simulating flows with sharp features like shock waves and [contact discontinuities](@entry_id:747781) is a primary challenge. Standard numerical methods can produce non-physical oscillations and fail to respect the directional nature of information flow inherent in fluid dynamics. Flux Vector Splitting (FVS) provides a powerful and physically intuitive paradigm to overcome this problem. It is a class of [upwind schemes](@entry_id:756378) designed to ensure stability and capture discontinuities by splitting the governing equations' flux terms according to the direction of wave propagation. This article provides a comprehensive overview of FVS techniques, from their theoretical underpinnings to their practical application in advanced simulations.

The following chapters will guide you through the core concepts of this essential numerical methodology. First, in "Principles and Mechanisms," we will delve into the mathematical foundation of FVS in the [hyperbolicity](@entry_id:262766) of conservation laws, dissecting the design and deficiencies of seminal schemes like Steger-Warming and the improvements offered by alternatives such as Van Leer splitting and AUSM. Next, "Applications and Interdisciplinary Connections" will explore how FVS is integrated into high-order methods for complex CFD problems and adapted for other scientific domains, including [geophysics](@entry_id:147342), plasma physics, and [combustion](@entry_id:146700). Finally, the "Hands-On Practices" section offers concrete problems to solidify your understanding of how these techniques are applied to derive and analyze numerical fluxes.

## Principles and Mechanisms

In the numerical solution of [hyperbolic conservation laws](@entry_id:147752), the construction of the [numerical flux](@entry_id:145174) at cell interfaces is of paramount importance. This flux function dictates the stability, accuracy, and physical fidelity of the resulting scheme. A central principle in designing such fluxes is **[upwinding](@entry_id:756372)**, which ensures that information is propagated in the correct physical direction, preventing the growth of non-physical oscillations and providing the necessary numerical dissipation to capture sharp features like shock waves. One of the most influential paradigms for achieving [upwinding](@entry_id:756372) in systems of equations is **Flux Vector Splitting (FVS)**. This chapter elucidates the fundamental principles and mechanisms underlying FVS techniques, from their theoretical foundations to the design and analysis of specific, widely used schemes.

### The Foundation: Hyperbolicity and Characteristic Decomposition

The very possibility of directional splitting is rooted in the mathematical property of **[hyperbolicity](@entry_id:262766)**. Consider a system of conservation laws in multiple spatial dimensions:
$$
\partial_t \boldsymbol{u} + \nabla \cdot \boldsymbol{f}(\boldsymbol{u}) = \boldsymbol{0}
$$
Here, $\boldsymbol{u}$ is the vector of conserved state variables, and $\boldsymbol{f}(\boldsymbol{u})$ is the flux tensor. To understand wave propagation in a specific direction, defined by a [unit normal vector](@entry_id:178851) $\boldsymbol{n}$, we examine the quasi-[linear form](@entry_id:751308) of the equation projected along this direction. This involves the **directional flux Jacobian**, defined as:
$$
A_{\boldsymbol{n}}(\boldsymbol{u}) = \frac{\partial (\boldsymbol{f}(\boldsymbol{u}) \boldsymbol{n})}{\partial \boldsymbol{u}}
$$
A system is defined as **hyperbolic** if, for any physically admissible state $\boldsymbol{u}$ and any direction $\boldsymbol{n}$, the flux Jacobian $A_{\boldsymbol{n}}(\boldsymbol{u})$ is diagonalizable with a complete set of real eigenvalues . This is a profound physical and mathematical condition. The real eigenvalues, denoted $\lambda_k$, represent the **[characteristic speeds](@entry_id:165394)** at which information propagates. The corresponding right eigenvectors, $\boldsymbol{r}_k$, form the basis of the **characteristic fields**, representing the distinct wave families of the system. For the one-dimensional Euler equations, for instance, the three eigenvalues are $\lambda_1 = u - a$, $\lambda_2 = u$, and $\lambda_3 = u + a$, corresponding to [acoustic waves](@entry_id:174227) traveling against and with the flow, and a contact wave traveling with the flow velocity, respectively. The existence of this real, complete eigenstructure is the bedrock upon which characteristic-based [upwinding](@entry_id:756372) and [flux vector splitting](@entry_id:749491) are built.

### The Flux Vector Splitting Paradigm

Flux Vector Splitting (FVS) proposes a direct and intuitive way to enforce [upwinding](@entry_id:756372). The core idea is to decompose the physical [flux vector](@entry_id:273577), $\boldsymbol{F}(\boldsymbol{u})$, into two or more parts, each associated with waves traveling in a specific direction. For a one-dimensional system or at an interface with normal $\boldsymbol{n}$, this decomposition is typically into a forward-propagating flux, $\boldsymbol{F}^+$, and a backward-propagating flux, $\boldsymbol{F}^-$.
$$
\boldsymbol{F}(\boldsymbol{u}) = \boldsymbol{F}^+(\boldsymbol{u}) + \boldsymbol{F}^-(\boldsymbol{u})
$$
This splitting must be constructed such that the Jacobian of the forward flux, $\partial \boldsymbol{F}^+ / \partial \boldsymbol{u}$, has only non-negative eigenvalues, while the Jacobian of the backward flux, $\partial \boldsymbol{F}^- / \partial \boldsymbol{u}$, has only non-positive eigenvalues.

Once such a split is defined, the numerical flux $\hat{\boldsymbol{F}}$ at an interface between a left state $\boldsymbol{U}_L$ and a right state $\boldsymbol{U}_R$ is constructed by taking the forward-propagating contributions from the left (upwind) state and the backward-propagating contributions from the right (upwind) state:
$$
\hat{\boldsymbol{F}}( \boldsymbol{U}_L, \boldsymbol{U}_R ) = \boldsymbol{F}^+(\boldsymbol{U}_L) + \boldsymbol{F}^-(\boldsymbol{U}_R)
$$
This construction ensures that information is always drawn from the direction whence it came, providing inherent stability. This approach is fundamentally different from **Flux Difference Splitting (FDS)** methods, such as the popular Roe solver. FDS schemes do not split the [flux vector](@entry_id:273577) itself; instead, they construct an approximate solution to the local Riemann problem at the interface and derive the flux from the resulting wave structure . FVS, in contrast, operates on the flux vectors of the left and right states independently before combining them.

### Steger-Warming Splitting: A Direct Characteristic Approach

One of the earliest and most direct implementations of FVS is the **Steger-Warming scheme**. It leverages a special property of the Euler equations: the flux vector $\boldsymbol{F}(\boldsymbol{U})$ is a homogeneous function of degree one in the conservative variables $\boldsymbol{U}$. By Euler's homogeneous function theorem, this implies that $\boldsymbol{F}(\boldsymbol{U}) = \boldsymbol{A}(\boldsymbol{U})\boldsymbol{U}$, where $\boldsymbol{A} = \partial \boldsymbol{F} / \partial \boldsymbol{U}$ is the flux Jacobian.

This property allows the flux itself to be split by splitting the Jacobian. Using the [spectral decomposition](@entry_id:148809) $\boldsymbol{A} = \boldsymbol{R}\boldsymbol{\Lambda}\boldsymbol{R}^{-1}$, Steger and Warming proposed splitting the diagonal eigenvalue matrix $\boldsymbol{\Lambda}$ based on the sign of its entries:
$$
\boldsymbol{\Lambda} = \boldsymbol{\Lambda}^+ + \boldsymbol{\Lambda}^-
$$
where $\boldsymbol{\Lambda}^+_{ii} = \max(0, \lambda_i)$ and $\boldsymbol{\Lambda}^-_{ii} = \min(0, \lambda_i)$. This is equivalent to using the splitting function $\lambda^{\pm} = (\lambda \pm |\lambda|)/2$. This leads to split Jacobians $\boldsymbol{A}^{\pm} = \boldsymbol{R}\boldsymbol{\Lambda}^{\pm}\boldsymbol{R}^{-1}$, and consequently, split fluxes:
$$
\boldsymbol{F}^{\pm}(\boldsymbol{U}) = \boldsymbol{A}^{\pm}(\boldsymbol{U})\boldsymbol{U}
$$
The split flux can be expressed as a sum over the characteristic fields. By decomposing the state vector $\boldsymbol{U}$ into the basis of right eigenvectors, $\boldsymbol{U} = \sum_i \alpha_i \boldsymbol{r}_i$, the positive split flux becomes :
$$
\boldsymbol{F}^+(\boldsymbol{U}) = \sum_{i=1}^{m} \lambda_i^+ \alpha_i \boldsymbol{r}_i
$$
For the 1D Euler equations, this leads to the explicit formula:
$$
F^{+}(U) = \frac{\rho}{2\gamma} \frac{u-a+|u-a|}{2} \begin{pmatrix} 1 \\ u-a \\ H-ua \end{pmatrix} + \rho\frac{\gamma-1}{\gamma} \frac{u+|u|}{2} \begin{pmatrix} 1 \\ u \\ \frac{u^2}{2} \end{pmatrix} + \frac{\rho}{2\gamma} \frac{u+a+|u+a|}{2} \begin{pmatrix} 1 \\ u+a \\ H+ua \end{pmatrix}
$$
where $H$ is the [total enthalpy](@entry_id:197863) per unit mass. This formula transparently shows how each characteristic wave's contribution to the flux is included only if its propagation speed is positive.

### Deficiencies of Early FVS Schemes

While elegant and robust, the Steger-Warming scheme and similar early FVS methods suffer from significant deficiencies that limit their accuracy.

#### Non-[differentiability](@entry_id:140863) and Entropy Violation

The primary flaw in the Steger-Warming splitting lies in its use of the [absolute value function](@entry_id:160606), $\lambda^{\pm} = (\lambda \pm |\lambda|)/2$. The [absolute value function](@entry_id:160606) is not differentiable at the origin. This mathematical "kink" has severe physical consequences. Whenever a characteristic speed $\lambda_k$ passes through zero—for example, at a [sonic point](@entry_id:755066) where $u-a=0$ or a stagnation point where $u=0$—the corresponding split flux $\boldsymbol{F}^{\pm}$ is not continuously differentiable with respect to the state variables $\boldsymbol{U}$ .

This lack of smoothness has two major negative effects. First, for [implicit solvers](@entry_id:140315) that use Newton's method, the Jacobian of the numerical residual becomes discontinuous at these points. This can stall or destroy the quadratic convergence of the Newton solver. Second, and more critically, the [numerical dissipation](@entry_id:141318) associated with that characteristic field vanishes precisely at the [sonic point](@entry_id:755066) . This absence of dissipation allows the numerical scheme to admit non-physical, entropy-violating solutions, most notably **expansion shocks** in transonic rarefactions . Physical laws require such expansions to be smooth, continuous waves (rarefaction fans), but the numerical scheme, lacking the necessary dissipative mechanism at the [sonic point](@entry_id:755066), can form a stationary, discontinuous jump. This necessitates the use of an "[entropy fix](@entry_id:749021)," an artificial modification to ensure the dissipation does not vanish.

#### Excessive Numerical Dissipation

Paradoxically, while FVS schemes can have too little dissipation at sonic points, they often have far too much in other important regimes, particularly at low flow speeds. The [numerical viscosity](@entry_id:142854) of an [upwind scheme](@entry_id:137305) is proportional to the magnitude of the [characteristic speeds](@entry_id:165394). The numerical diffusion coefficient, $\nu_{\text{num}}$, can be modeled as:
$$
\nu_{\text{num}} \propto \Delta x \cdot \max_k(|\lambda_k|)
$$
For the Euler equations, the largest eigenvalues are always the acoustic ones, $u \pm a$. Therefore, $\max_k(|\lambda_k|) = |u| + a$. In the **low Mach number limit** ($M = |u|/a \to 0$), the flow velocity $|u|$ becomes negligible compared to the sound speed $a$. However, the numerical diffusion remains large, scaling with $a_0 \Delta x / 2$.

A formal analysis shows that the ratio of this [numerical diffusion](@entry_id:136300) to the physical acoustic scale, $a_0 \Delta x$, approaches a constant ($1/2$) as $M \to 0$. In contrast, the ratio to the physical convective scale, $|u_0| \Delta x$, diverges as $1/(2M)$ .
$$
R_{\text{convective}}(M) = \frac{\nu_{\text{num}}}{|u_{0}|\Delta x} = \frac{M+1}{2M} \to \infty \quad \text{as} \quad M \to 0
$$
This means that for slow flows, the numerical diffusion completely overwhelms the physical convection, leading to severe smearing of [contact discontinuities](@entry_id:747781), shear layers, and boundary layers, where accuracy is often paramount .

### Van Leer Splitting: A Smooth Alternative

To remedy the non-differentiability of the Steger-Warming scheme, Bram van Leer developed an alternative FVS approach based on a crucial design principle: the split fluxes must be continuously differentiable ($C^1$) functions of the [state variables](@entry_id:138790), particularly through sonic points. Instead of splitting based on the eigenvalues directly, van Leer constructed polynomial [splitting functions](@entry_id:161308) of the Mach number $M$.

For a nondimensionalized eigenvalue $z$ (e.g., $M$ or $M \pm 1$), the positive split $z^+$ is defined piece-wise. For [supersonic flow](@entry_id:262511) ($z \ge 1$), it is simply $z$; for opposing supersonic flow ($z \le -1$), it is $0$. The key innovation is the subsonic part ($|z|  1$), which is a polynomial designed to smoothly connect the supersonic branches in both value and slope. To satisfy the four conditions ($P(\pm 1)$ and $P'(\pm 1)$ must match the supersonic forms), a quadratic polynomial is sufficient :
$$
z^{+}(z) = 
\begin{cases} 
0  \text{if } z \leq -1 \\ 
\frac{1}{4}(z+1)^2  \text{if } |z|  1 \\ 
z  \text{if } z \geq 1 
\end{cases}
$$
This function is $C^1$ everywhere. Applying this principle to the mass and momentum fluxes of the Euler equations yields the celebrated **van Leer [flux vector splitting](@entry_id:749491)**. For instance, the mass and pressure fluxes are split using polynomial functions of the Mach number that are smooth across $M=\pm 1$ . Because of this smoothness, the van Leer scheme provides a continuous Jacobian for [implicit solvers](@entry_id:140315) and avoids the specific numerical glitches at sonic points that plague the Steger-Warming scheme  .

### Beyond Characteristics: The AUSM Physical Splitting

A separate class of schemes, known as the **Advection Upstream Splitting Method (AUSM)** family, adopts a different philosophical approach. Instead of a mathematical decomposition based on characteristics, it splits the flux based on its underlying physical mechanisms: **convection** and **pressure** . The Euler flux vector can be written as:
$$
\boldsymbol{F}(\boldsymbol{U}) = \boldsymbol{F}_c + \boldsymbol{F}_p = u \begin{pmatrix} \rho \\ \rho u \\ E \end{pmatrix} + \begin{pmatrix} 0 \\ p \\ pu \end{pmatrix}
$$
Here, $\boldsymbol{F}_c$ represents the [convective transport](@entry_id:149512) of mass, momentum, and energy with the bulk flow velocity $u$, while $\boldsymbol{F}_p$ represents the flux due to the pressure field (pressure force and [pressure work](@entry_id:265787)). The AUSM methodology then designs separate, appropriate [upwinding](@entry_id:756372) strategies for the convective part (which is purely one-sided) and the pressure part (which has acoustic properties and propagates in both directions). This physical separation can improve accuracy for [contact discontinuities](@entry_id:747781) and often behaves more robustly in low-Mach regimes compared to classical FVS schemes.

### The Role of Dissipation in High-Order Methods

The upwind dissipation introduced by FVS schemes is not merely an artifact; it is a crucial mechanism for stability. The FVS numerical flux can be generically expressed as a central part plus a dissipation term:
$$
\hat{\boldsymbol{F}}(\boldsymbol{U}_L, \boldsymbol{U}_R) \approx \frac{1}{2}\left(\boldsymbol{F}(\boldsymbol{U}_L) + \boldsymbol{F}(\boldsymbol{U}_R)\right) - \frac{1}{2}|\boldsymbol{A}|(\boldsymbol{U}_R - \boldsymbol{U}_L)
$$
where $|\boldsymbol{A}| = \boldsymbol{R}|\boldsymbol{\Lambda}|\boldsymbol{R}^{-1}$ is the matrix absolute value of the Jacobian . This dissipation term acts like a penalty on jumps in the solution at cell interfaces. Crucially, the dissipation is **anisotropic**; it damps each characteristic field in proportion to its wave speed $|\lambda_k|$. This selective damping is far more sophisticated than a simple scalar [artificial viscosity](@entry_id:140376) and is a hallmark of [upwind methods](@entry_id:756376).

In the context of modern high-order methods like the Discontinuous Galerkin (DG) method, this interface dissipation is essential for suppressing spurious Gibbs-type oscillations that arise when representing discontinuities with high-degree polynomials. However, the interface flux is not a panacea. While it provides stability between elements, it cannot by itself control oscillations that form *within* an element when a very strong shock is present. For such cases, the [upwind flux](@entry_id:143931) must be complemented by nonlinear **limiters** or artificial viscosity techniques to ensure robust and physically meaningful solutions .