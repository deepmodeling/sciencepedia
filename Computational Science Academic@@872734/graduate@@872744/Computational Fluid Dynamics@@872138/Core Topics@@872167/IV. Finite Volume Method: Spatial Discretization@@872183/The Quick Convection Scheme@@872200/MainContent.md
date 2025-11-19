## Introduction
The [discretization](@entry_id:145012) of [convective transport](@entry_id:149512) terms is a central challenge in computational fluid dynamics (CFD), requiring a delicate balance between numerical accuracy and stability. While low-order [upwind schemes](@entry_id:756378) are robust but overly diffusive, smearing sharp physical gradients, standard [higher-order schemes](@entry_id:150564) often introduce unphysical oscillations in [convection-dominated flows](@entry_id:169432). This knowledge gap necessitates advanced methods that can deliver high fidelity without sacrificing stability. The Quadratic Upstream Interpolation for Convective Kinematics (QUICK) scheme emerges as a powerful solution, offering higher-order accuracy by leveraging an upwind-biased quadratic interpolation.

This article provides a graduate-level examination of the QUICK scheme, structured to guide the reader from fundamental theory to advanced application. The first chapter, **Principles and Mechanisms**, will dissect the scheme's core, from its mathematical derivation to a rigorous analysis of its accuracy, dispersion, and stability properties. Next, **Applications and Interdisciplinary Connections** will explore how the scheme performs in practice, detailing crucial implementation strategies like [deferred correction](@entry_id:748274) and [flux limiting](@entry_id:749486), and showcasing its use in diverse fields such as [turbulence modeling](@entry_id:151192) and [high-performance computing](@entry_id:169980). Finally, **Hands-On Practices** will offer a series of guided problems to solidify understanding by implementing and analyzing the scheme's behavior in canonical test cases. This structured approach will build a comprehensive understanding of not just the QUICK scheme itself, but also the broader principles of designing and implementing high-resolution numerical methods in modern CFD.

## Principles and Mechanisms

In the [discretization](@entry_id:145012) of convection terms within the Finite Volume Method (FVM), a fundamental challenge lies in balancing numerical accuracy with stability. Lower-order schemes, such as the [first-order upwind scheme](@entry_id:749417), guarantee boundedness and prevent [spurious oscillations](@entry_id:152404) but at the cost of excessive numerical diffusion, which smears sharp gradients. Conversely, higher-order non-dissipative schemes like second-order [central differencing](@entry_id:173198) preserve sharp profiles better but are prone to unphysical oscillations, especially in regions of high gradients or for [convection-dominated flows](@entry_id:169432). This trade-off motivates the development of higher-order [upwind schemes](@entry_id:756378) designed to achieve high accuracy while retaining a degree of stability from the [upwinding](@entry_id:756372) concept.

The **Quadratic Upstream Interpolation for Convective Kinematics (QUICK)** scheme, introduced by B. P. Leonard, is a prominent example of such a method. It aims to combine the accuracy of a third-order method with the stabilizing influence of [upwinding](@entry_id:756372). This chapter will detail the principles of the QUICK scheme, from its fundamental derivation to its performance characteristics and practical limitations.

### The Foundation: Upstream-Biased Quadratic Interpolation

The core idea of the QUICK scheme is to approximate the value of a transported scalar, $\phi_f$, at a control volume face by evaluating a quadratic polynomial that has been fitted to three nearby cell-center values. The key to the scheme's character is its **upwind bias**: the set of three points is chosen to include two nodes on the upstream side of the face and one on the downstream side. This selection provides information about the curvature of the profile while anchoring the interpolation in the direction from which the flow originates.

Let us consider a one-dimensional, uniform grid with cell centers denoted by indices. For a face $f$ located midway between cell centers $P$ (parent) and $E$ (east), the convective mass flux is $F_f$. A positive flux, $F_f > 0$, indicates flow from left to right (from $P$ to $E$), while a negative flux, $F_f  0$, indicates flow from right to left.

#### Derivation on a Uniform Grid

To derive the classic QUICK formula, we can use Lagrange interpolation. Let the uniform grid spacing be $\Delta x$.

**Case 1: Positive Flow ($F_f > 0$)**

For flow from left to right across face $f$, the two upstream nodes are the cell centers $W$ (west of $P$) and $P$. The single downstream node is $E$. The face $f$ is located at $x_f = x_P + \Delta x/2$. To find the interpolated value $\phi_f$, we construct a quadratic polynomial passing through the values $\phi_W$, $\phi_P$, and $\phi_E$ at locations $x_W = x_P - \Delta x$, $x_P$, and $x_E = x_P + \Delta x$. Evaluating this polynomial at $x_f$ yields the face value:

$$
\phi_f = -\frac{1}{8}\phi_W + \frac{6}{8}\phi_P + \frac{3}{8}\phi_E
$$

This expression is the cornerstone of the QUICK scheme. It is a weighted average of the three cell-center values. Notice the presence of a negative coefficient for the far-upstream node $\phi_W$, a feature that will have significant consequences for the scheme's boundedness, as we will discuss later.

**Case 2: Negative Flow ($F_f  0$)**

If the flow is from right to left across face $f$, the upstream direction is reversed. The two upstream nodes are now $EE$ (east of $E$) and $E$, and the single downstream node is $P$. The corresponding stencil is $\{P, E, EE\}$. By symmetry, or by a similar derivation using Lagrange interpolation on the points $\phi_P$, $\phi_E$, and $\phi_{EE}$ at locations $x_P$, $x_E = x_P + \Delta x$, and $x_{EE} = x_P + 2\Delta x$, we find the face value for negative flow:

$$
\phi_f = \frac{3}{8}\phi_P + \frac{6}{8}\phi_E - \frac{1}{8}\phi_{EE}
$$

This formula is a mirror image of the one for positive flow, again featuring a negative coefficient for the far-upstream node, which is now $\phi_{EE}$.

#### The Assembled Semi-Discrete Operator

In a [finite volume](@entry_id:749401) context, the rate of change of the scalar in cell $P$ is determined by the net flux across its faces. For a 1D problem with constant advection velocity $a > 0$ and cell volume $\Delta x$, the semi-discrete equation is:

$$
\frac{d\phi_P}{dt} = -\frac{F_e - F_w}{\Delta x} = -\frac{a(\phi_e - \phi_w)}{\Delta x}
$$

Here, $\phi_e$ is the value at the east face (between $P$ and $E$) and $\phi_w$ is the value at the west face (between $W$ and $P$). Applying the QUICK formula for positive flow to both faces gives:

$$
\phi_e = -\frac{1}{8}\phi_W + \frac{6}{8}\phi_P + \frac{3}{8}\phi_E
$$
$$
\phi_w = -\frac{1}{8}\phi_{WW} + \frac{6}{8}\phi_W + \frac{3}{8}\phi_P
$$

Substituting these into the conservation equation results in a discrete operator that involves five cell-center values, from $\phi_{WW}$ to $\phi_E$. The semi-discrete equation for cell $P$ (or cell $i$ in [index notation](@entry_id:191923)) becomes:

$$
\frac{d\phi_i}{dt} = -\frac{a}{8\Delta x} \left( 3\phi_{i+1} + 3\phi_i - 7\phi_{i-1} + \phi_{i-2} \right)
$$

This [five-point stencil](@entry_id:174891) reveals that the [discretization](@entry_id:145012) at a given cell depends not only on its immediate neighbors but also on nodes further upstream.

### Analysis of Accuracy and Error

A key motivation for using the QUICK scheme is its high formal [order of accuracy](@entry_id:145189). We can quantify this, along with its inherent [numerical errors](@entry_id:635587), through Taylor series and Fourier analysis.

#### Order of Accuracy

The error of a [polynomial interpolation](@entry_id:145762) scheme can be found from its [remainder term](@entry_id:159839). For a quadratic polynomial interpolating a smooth function $\phi(x)$ at three points, the [interpolation error](@entry_id:139425) is proportional to the third derivative of the function, $\phi'''(x)$. A detailed Taylor [series expansion](@entry_id:142878) reveals that for a uniform grid, the error in the QUICK face value approximation is:

$$
\phi_f^{\text{QUICK}} - \phi(x_f) = C h^3 \phi'''(x_f) + O(h^4)
$$

where $h$ is the grid spacing and $C$ is a constant. This shows that the face value interpolation is **third-order accurate**. This [high-order accuracy](@entry_id:163460) in approximating the face value is what leads to the scheme's ability to resolve complex flows with fewer grid points compared to lower-order methods.

#### Numerical Diffusion and Dispersion

Any numerical scheme for convection introduces errors that can be categorized as either dissipative (smearing gradients, like physical diffusion) or dispersive (creating spurious oscillations, or phase errors). Fourier analysis provides a powerful tool to quantify these errors.

By substituting a single Fourier mode, $u_j(t) = \hat{u}(t)\exp(i k x_j)$, into the semi-discrete QUICK operator, we can analyze how the scheme treats waves of different wavenumbers $k$. This analysis shows that the dissipative part of the QUICK scheme can be represented by an **equivalent [numerical viscosity](@entry_id:142854)**, $\nu_{\text{num}}$:

$$
\nu_{\text{num}}(k, \Delta x) = \frac{a \Delta x}{8} (1 - \cos(k \Delta x))
$$

This term is interesting for several reasons. First, unlike the constant [numerical viscosity](@entry_id:142854) of the [first-order upwind scheme](@entry_id:749417), it is dependent on the [wavenumber](@entry_id:172452) $k$. It provides the most dissipation for the shortest resolvable wavelength on the grid ($k\Delta x = \pi$) and zero dissipation for the longest wavelengths ($k\Delta x \to 0$). Second, the term is part of a more [complex structure](@entry_id:269128) that, when fully analyzed, shows QUICK has an anti-diffusive component that counteracts the excessive diffusion of the [first-order upwind scheme](@entry_id:749417).

The dispersive error is quantified by the **numerical group velocity**, $v_g(\theta)$, where $\theta = k\Delta x$. This velocity determines how fast [wave packets](@entry_id:154698) of a certain [wavenumber](@entry_id:172452) propagate. For the exact [advection equation](@entry_id:144869), the [group velocity](@entry_id:147686) is constant and equal to the physical advection speed, $u$. For a numerical scheme, any deviation $v_g(\theta) \neq u$ causes wave components to travel at incorrect speeds, leading to a distortion of the solution profile known as dispersion. For small wavenumbers (long wavelengths), the group velocity error for QUICK is:

$$
v_{g}^{\text{QUICK}}(\theta) - u = -u \frac{\theta^2}{8} + O(\theta^4)
$$

This leading-order error of $O(\theta^2)$ is significantly smaller than the error for a standard [second-order central difference](@entry_id:170774) scheme, for which the error term is $-u\frac{\theta^2}{2}$. The QUICK scheme is therefore substantially less dispersive, which is one of its major advantages. The smaller group velocity error means that different wave components are transported at more consistent speeds, preserving the shape of resolved features more accurately.

### Practical Implementation and Limitations

Despite its high accuracy and low dispersion, the pure QUICK scheme suffers from a major drawback that limits its use in its raw form: it is not guaranteed to be bounded.

#### Boundedness and the Discrete Maximum Principle

A desirable property of any [convection scheme](@entry_id:747849) is that it satisfies a **Discrete Maximum Principle (DMP)**. This means that for a problem without sources, the numerical solution at a new time step should be bounded by the maximum and minimum values of the solution at the previous time step. In essence, the scheme should not create new, unphysical peaks or valleys.

A sufficient condition for a scheme to satisfy the DMP is for its matrix of coefficients to be an M-matrix, which requires (among other things) that all off-diagonal coefficients be non-positive. Let's examine the discrete equation derived for QUICK:

$$
\frac{1}{8}\phi_{i-2} - \frac{7}{8}\phi_{i-1} + \frac{3}{8}\phi_i + \frac{3}{8}\phi_{i+1} = 0
$$

When arranged into the standard form $\sum_j a_{ij} \phi_j = 0$, the coefficients influencing $\phi_i$ are $a_{i,i-2} = 1/8$, $a_{i,i-1} = -7/8$, $a_{i,i} = 3/8$, and $a_{i,i+1} = 3/8$. We can immediately see that two off-diagonal coefficients, corresponding to neighbors $\phi_{i-2}$ and $\phi_{i+1}$, are positive. This violates the M-matrix condition.

The consequence of this violation is that the QUICK scheme is not guaranteed to be bounded. The presence of negative coefficients in the underlying interpolation formulas (e.g., $-\frac{1}{8}\phi_W$) is the root cause. This can lead to notorious **overshoots and undershoots** (Gibbs-type oscillations) in the vicinity of sharp gradients or discontinuities.

This non-monotonic behavior is an inherent property of the [spatial discretization](@entry_id:172158) operator. It is crucial to understand that no choice of [time integration](@entry_id:170891) scheme can remedy this fundamental flaw. While the semi-discrete QUICK operator is energy-stable (the $\ell_2$-norm of the solution does not grow), this does not prevent the growth of total variation, which is what characterizes the oscillations. Energy stability and [monotonicity](@entry_id:143760) are distinct properties, and a time integrator can only follow the dynamics dictated by the spatial operator. It cannot make a non-monotone spatial scheme monotone. This limitation necessitates the use of [flux limiters](@entry_id:171259), which blend QUICK with a bounded lower-order scheme to suppress oscillations, a topic discussed in subsequent chapters.

#### Extension to General Grids

Real-world CFD applications involve non-uniform and multi-dimensional grids. The principles of QUICK can be extended to these more complex scenarios.

On a **non-uniform 1D grid**, where the cell spacings are $h_{-} = x_i - x_{i-1}$ and $h_{+} = x_{i+1} - x_i$, the interpolation coefficients become functions of the [grid stretching](@entry_id:170494) ratios. The derivation via Lagrange interpolation remains valid, and importantly, the [interpolation error](@entry_id:139425) remains third-order, $O(h^3)$, where $h$ is a characteristic grid size.

In **two or three dimensions**, the QUICK scheme is applied on a face-by-face basis. For each face, the interpolation is performed along a 1D coordinate line that is normal to the face. The required cell-center values (two upstream, one downstream) are identified by projecting the centers of neighboring cells onto this line. This reduces the multi-dimensional problem locally to a 1D interpolation, allowing the same fundamental logic to apply.

#### Boundary Conditions and Global Accuracy

A final practical issue is the application of QUICK near domain boundaries. The standard three-point stencil requires nodes that may not exist (e.g., the $W$ node for a cell adjacent to an inlet boundary). In these boundary-adjacent cells, the scheme must be modified. Typically, a lower-order [upwind scheme](@entry_id:137305) or a one-sided quadratic formula is employed.

This local modification has global consequences. If a second-order accurate scheme is used in a boundary region of fixed physical width, it introduces a [local truncation error](@entry_id:147703) of $O(h^2)$. While the error in the interior of the domain remains higher-order, the lower-order error from the boundary region "pollutes" the entire solution. For the steady advection equation, this results in the **global error** for the entire simulation being reduced to second order, i.e., $O(h^2)$. Thus, even though QUICK is often called a third-order scheme based on its interior-point accuracy, the global accuracy in a practical implementation is often limited to second order by the boundary treatment.