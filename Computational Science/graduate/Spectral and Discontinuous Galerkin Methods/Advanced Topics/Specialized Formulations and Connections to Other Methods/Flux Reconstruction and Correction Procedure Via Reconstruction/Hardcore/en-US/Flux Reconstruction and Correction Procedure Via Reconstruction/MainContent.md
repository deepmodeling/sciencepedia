## Introduction
The Flux Reconstruction (FR) method, also known as the Correction Procedure via Reconstruction (CPR), represents a modern and powerful paradigm for constructing high-order accurate [numerical methods for conservation laws](@entry_id:752804). It stands out by providing a unifying framework that not only encompasses well-established schemes like Discontinuous Galerkin (DG) and Spectral Difference (SD) but also offers a conceptually direct, strong-form collocation approach. The central challenge in computational science is developing methods that are both highly accurate and robust enough to handle the complex physics and geometries of real-world problems, from [shockwaves](@entry_id:191964) in [supersonic flight](@entry_id:270121) to [fluid-structure interaction](@entry_id:171183) in [biomechanics](@entry_id:153973). The FR/CPR framework directly addresses this need by creating a flexible blueprint for building schemes with tailored properties, such as low [numerical dispersion](@entry_id:145368) and proven stability for nonlinear phenomena.

This article will guide you through this versatile framework, from its foundational concepts to its advanced applications. The journey is structured into three distinct chapters. In "Principles and Mechanisms," we will dissect the core idea of reconstructing a continuous flux using correction functions and explore the mathematical machinery that ensures conservation and stability, including the crucial roles of Summation-by-Parts (SBP) operators and entropy analysis. Following this, "Applications and Interdisciplinary Connections" will showcase the power and flexibility of FR/CPR by examining its use in solving challenging problems in [computational fluid dynamics](@entry_id:142614), handling complex and moving geometries, and coupling disparate physical models. Finally, "Hands-On Practices" will offer a series of guided problems to help solidify your theoretical understanding and build practical implementation skills. We begin by delving into the fundamental principles that make the FR/CPR framework a cornerstone of modern high-order methods.

## Principles and Mechanisms

The Flux Reconstruction (FR) method, also known as the Correction Procedure via Reconstruction (CPR), provides a unifying framework for developing high-order accurate [numerical schemes](@entry_id:752822) for conservation laws. Its core principle is to directly reconstruct a globally continuous flux from a discontinuous solution representation, thereby circumventing the [weak formulation](@entry_id:142897) typical of Discontinuous Galerkin (DG) methods while retaining their key advantages, such as geometric flexibility and amenability to [parallel computation](@entry_id:273857). This chapter elucidates the fundamental principles and mechanisms of the FR/CPR framework, from the basic construction to advanced concepts of stability and conservation for [nonlinear systems](@entry_id:168347).

### The Core Mechanism: Reconstructing a Continuous Flux

Consider a one-dimensional [scalar conservation law](@entry_id:754531) on a domain partitioned into non-overlapping elements:
$$
\frac{\partial u}{\partial t} + \frac{\partial f(u)}{\partial x} = 0
$$
Within each physical element, an [affine mapping](@entry_id:746332) transforms the coordinates to a reference element, typically the interval $\xi \in [-1, 1]$. The conservation law on this reference element becomes:
$$
\frac{\partial u}{\partial t} + \frac{1}{J_e} \frac{\partial f(u)}{\partial \xi} = 0
$$
where $J_e$ is the constant Jacobian of the mapping. In a high-order nodal method, the solution $u(\xi, t)$ within the element is approximated by a polynomial $u_h(\xi, t)$ of degree $p$, which is uniquely defined by its values at a set of $p+1$ distinct solution points $\{\xi_j\}_{j=0}^p$.

Since the solution polynomial $u_h$ is generally discontinuous at the element interfaces ($\xi = \pm 1$), the corresponding physical flux, $F_h(\xi) = f(u_h(\xi, t))$, is also discontinuous. A simple differentiation of $F_h$ would be ill-defined and would not account for information from neighboring elements. The central idea of Flux Reconstruction is to remedy this by constructing a new, element-local, "corrected" flux polynomial, which we denote as $q_h(\xi)$. This corrected flux must satisfy two [critical properties](@entry_id:260687): it must be a polynomial, and its values at the element boundaries must match a common, single-valued [numerical flux](@entry_id:145174), $\widehat{f}$, that is shared with adjacent elements.

This reconstruction is achieved by adding a correction polynomial to the interior physical flux $F_h(\xi)$ . The correction is designed to adjust the values of the flux at the boundaries without necessarily altering the interior representation. The general form of the corrected flux $q_h(\xi)$ is given by:
$$
q_h(\xi) = F_h(\xi) + \big(\widehat{f}_L - F_h(-1)\big) g_L(\xi) + \big(\widehat{f}_R - F_h(1)\big) g_R(\xi)
$$
Here, $\widehat{f}_L$ and $\widehat{f}_R$ are the numerical fluxes at the left ($\xi=-1$) and right ($\xi=1$) interfaces, respectively. These are computed using the solution traces from both sides of the interface, e.g., $\widehat{f}_L = \widehat{f}(u_h^{\text{left}}(1), u_h^{\text{current}}(-1))$. The terms $F_h(-1)$ and $F_h(1)$ are the values of the physical flux polynomial from within the [current element](@entry_id:188466) at these same interfaces. The differences, $(\widehat{f}_L - F_h(-1))$ and $(\widehat{f}_R - F_h(1))$, represent the "flux jumps" that must be corrected.

The functions $g_L(\xi)$ and $g_R(\xi)$ are the **correction functions**. They are polynomials (typically of degree $p+1$) that are instrumental in enforcing the boundary conditions on the corrected flux. To ensure that $q_h(\xi)$ matches the [numerical fluxes](@entry_id:752791) at the interfaces, these correction functions must satisfy a minimal set of endpoint conditions :
$$
\begin{cases}
g_L(-1) = 1 \\
g_L(1) = 0
\end{cases}
\quad \text{and} \quad
\begin{cases}
g_R(-1) = 0 \\
g_R(1) = 1
\end{cases}
$$
With these conditions, it is straightforward to verify that the corrected flux $q_h(\xi)$ has the desired properties:
- At $\xi = -1$: $q_h(-1) = F_h(-1) + (\widehat{f}_L - F_h(-1)) \cdot 1 + (\widehat{f}_R - F_h(1)) \cdot 0 = \widehat{f}_L$.
- At $\xi = 1$: $q_h(1) = F_h(1) + (\widehat{f}_L - F_h(-1)) \cdot 0 + (\widehat{f}_R - F_h(1)) \cdot 1 = \widehat{f}_R$.

Since the [numerical flux](@entry_id:145174) $\widehat{f}$ has a single value at each interface, the corrected flux polynomial $q_h(\xi)$ is continuous across element boundaries by construction. With this continuous flux in hand, the semi-discrete form of the conservation law is formulated in a strong, collocation form by requiring the governing equation to hold at each solution point $\xi_j$:
$$
\frac{d}{dt} u_h(\xi_j, t) = -\frac{1}{J_e} \frac{\partial q_h}{\partial \xi}(\xi_j, t), \quad j=0, \dots, p
$$
This yields a system of ordinary differential equations (ODEs) for the nodal solution values, which can be integrated forward in time using a suitable numerical scheme.

### The Computational Machinery of Flux Reconstruction

The abstract formulation of the corrected flux and its derivative must be translated into concrete matrix and vector operations for computational implementation. In a nodal framework, polynomials are represented by their values at the solution points. The operation of differentiation can thus be represented by a **[differentiation matrix](@entry_id:149870)**, denoted by $D$. If a vector $\mathbf{u}$ contains the values of a polynomial $u_h(\xi)$ at the nodes $\{\xi_j\}$, then the [matrix-vector product](@entry_id:151002) $D \mathbf{u}$ yields a vector containing the values of the derivative $\partial_\xi u_h(\xi)$ at those same nodes.

The calculation of the term $\partial_\xi q_h$ in the semi-discrete update proceeds in two parts: the volume contribution and the correction contribution .

The **volume contribution** arises from the derivative of the interior physical flux polynomial, $\partial_\xi F_h(\xi)$. This is computed as follows:
1.  From the vector of nodal solution values $\mathbf{u} = [u_h(\xi_0), \dots, u_h(\xi_p)]^T$, compute the nodal physical flux values pointwise: $\mathbf{F} = [f(u_h(\xi_0)), \dots, f(u_h(\xi_p))]^T$.
2.  The nodal values of the derivative of the polynomial interpolating $\mathbf{F}$ are then given by the [matrix-vector product](@entry_id:151002) $D\mathbf{F}$.

The **correction contribution** arises from differentiating the correction terms in the formula for $q_h$. This involves the nodal values of the derivatives of the correction functions, $\mathbf{g}'_L$ and $\mathbf{g}'_R$. The full expression for the nodal values of the derivative of the corrected flux is:
$$
\mathbf{q}'_h = D\mathbf{F} + \big(\widehat{f}_L - F_h(-1)\big) \mathbf{g}'_L + \big(\widehat{f}_R - F_h(1)\big) \mathbf{g}'_R
$$
The semi-discrete ODE system for the vector of nodal unknowns $\mathbf{u}$ is then written compactly as:
$$
\frac{d\mathbf{u}}{dt} = -\frac{1}{J_e} \mathbf{q}'_h
$$
For a simple case, such as a [linear advection equation](@entry_id:146245) with a $p=1$ [polynomial approximation](@entry_id:137391), this entire procedure can be condensed into a single matrix operator that acts on the solution values in the [current element](@entry_id:188466) and its immediate neighbors, revealing a finite-difference-like stencil that couples the elements .

To make this concrete, let's consider a polynomial approximation of degree $p=3$ on Gauss-Lobatto-Legendre (GLL) nodes. The state is given by the polynomial $u(\xi) = \xi^3 - \xi$ and the physical flux is $f(u) = u^2$. The nodal values of the state and flux are computed, yielding a nodal [flux vector](@entry_id:273577) $\mathbf{F}$. The volume contribution to the flux derivative at the nodes is then simply $D\mathbf{F}$, where $D$ is the $4 \times 4$ [differentiation matrix](@entry_id:149870) for $p=3$ GLL nodes. For the interior node $\xi_1 = -1/\sqrt{5}$, this calculation yields a specific value, demonstrating the direct application of the [differentiation matrix](@entry_id:149870) to the nodal [flux vector](@entry_id:273577) .

### The FR Framework: A Family of Schemes

The endpoint conditions on the correction functions $g_L$ and $g_R$ do not uniquely define them. This freedom of choice is one of the most powerful features of the FR/CPR framework. By selecting different correction functions (of degree $p+1$ or higher), one can generate a vast family of [high-order schemes](@entry_id:750306), each with distinct numerical properties such as stability, dissipation, and dispersion. This perspective elevates FR from a single method to a general procedure for constructing schemes.

Many well-known high-order methods can be recovered as special instances within this framework. For example, specific choices of correction functions can make the FR scheme equivalent to a particular nodal Discontinuous Galerkin (DG) scheme or a Spectral Difference (SD) scheme.

This flexibility allows for the optimization of schemes for specific applications. Often, correction functions are defined as part of a one-parameter family. By tuning this parameter, one can continuously morph the scheme from one type to another (e.g., from a DG-type to an SD-type scheme) and explore the properties of the intermediate schemes . For problems where [wave propagation](@entry_id:144063) is dominant, such as in [linear advection](@entry_id:636928), Fourier analysis (or Bloch wave analysis) can be used to study the scheme's **[dispersion error](@entry_id:748555)**—the difference between the numerical and exact wave speeds. One can then search for the parameter value that minimizes this error over a range of wavenumbers, leading to an optimized, low-dispersion scheme.

### Stability and Conservation

Two of the most important properties of any numerical scheme for conservation laws are conservation and stability. The FR framework is designed to ensure these properties through careful construction.

#### Conservation

A scheme is conservative if the time rate of change of the integral of the solution over the entire domain depends only on the fluxes at the domain boundaries. In FR, conservation is a direct consequence of the [flux reconstruction](@entry_id:147076) process itself. By constructing a flux polynomial $q_h$ that is continuous at element interfaces, we ensure that the flux leaving one element is precisely the flux entering the next. When the semi-discrete equation is integrated over an element, the change in the cell average is related only to the flux values at its boundaries. Summing over all elements in the domain results in a [telescoping sum](@entry_id:262349) where all internal interface fluxes cancel, leaving only the contributions at the physical domain boundaries. This guarantees that the total mass (or charge, momentum, etc.) is conserved by the [semi-discretization](@entry_id:163562). This property is fundamental to the structure of FR and holds regardless of aliasing errors that may arise from nonlinearities . For systems of equations, the [numerical flux](@entry_id:145174) $\widehat{f}(u^-, u^+)$ must satisfy two key properties: consistency with the physical flux ($ \widehat{f}(u,u) = f(u) $) and a single-valued normal flux at interfaces, which ensures the telescoping cancellation .

#### Linear Stability and Summation-by-Parts

For a scheme to be useful, it must be stable, meaning that errors do not grow unboundedly in time. The stability of FR schemes is deeply connected to the theory of **Summation-by-Parts (SBP)** operators. An SBP operator is a discrete [differentiation operator](@entry_id:140145) that mimics the property of [integration by parts](@entry_id:136350) discretely. When the solution points, [quadrature weights](@entry_id:753910), and correction functions are chosen appropriately, the FR spatial operator can be shown to satisfy an SBP property with respect to a discrete norm defined by the [quadrature weights](@entry_id:753910).

This property is invaluable for performing [energy stability](@entry_id:748991) analysis. For the [linear advection equation](@entry_id:146245), $u_t + a u_x = 0$, one can analyze the [time evolution](@entry_id:153943) of the discrete energy, often defined as the squared $L^2$-norm of the solution. The SBP property allows the rate of change of energy to be expressed solely in terms of boundary and interface contributions .

This analysis reveals the crucial role of the numerical flux.
- If a **central flux** is used at interfaces, the SBP analysis shows that the semi-discrete operator is skew-adjoint with respect to the discrete [energy inner product](@entry_id:167297). This implies that the discrete energy is exactly conserved, and the eigenvalues of the operator are purely imaginary. The scheme is therefore non-dissipative and neutrally stable.
- If an **[upwind flux](@entry_id:143931)** is used, the analysis shows that the operator gains a symmetric part that is negative semi-definite. This leads to a decrease in discrete energy over time ($\frac{dE}{dt} \le 0$). The scheme is dissipative, and its eigenvalues have non-positive real parts. This numerical dissipation is essential for damping spurious, high-frequency oscillations and enhancing robustness.

The choice of solution points also has significant implications. Using **Gauss-Lobatto-Legendre (GLL)** points, which include the endpoints $\xi = \pm 1$, is common because it simplifies the connection to nodal DG-SBP schemes and the insertion of interface fluxes. However, schemes based on **Gauss-Legendre (GL)** points, which are all interior to the element, can offer superior quadrature accuracy and often exhibit better spectral properties, such as lower [dispersion error](@entry_id:748555), making them attractive for [wave propagation](@entry_id:144063) problems .

### Extension to Nonlinear Systems

Extending the FR framework to nonlinear [systems of conservation laws](@entry_id:755768), such as the Euler equations of gas dynamics, introduces significant challenges, primarily related to nonlinear stability. Shocks and other discontinuities can cause naive [high-order schemes](@entry_id:750306) to fail catastrophically. The key to robustly handling such phenomena lies in satisfying a discrete version of the Second Law of Thermodynamics, which manifests as an **[entropy stability](@entry_id:749023)** condition.

#### Entropy Stability

For a system of conservation laws, a convex scalar function of the solution, called the entropy $U(\boldsymbol{q})$, is known to satisfy an inequality of the form $\partial_t U(\boldsymbol{q}) + \partial_x F(\boldsymbol{q}) \le 0$, where $F(\boldsymbol{q})$ is the corresponding entropy flux. A numerical scheme is called entropy stable if it preserves this inequality at the discrete level, ensuring that entropy can only be produced, not destroyed.

A powerful method for constructing entropy-stable FR schemes involves combining three key ingredients  :
1.  **Entropy Variables**: The scheme is formulated in terms of entropy variables $\boldsymbol{v} = \partial U/\partial \boldsymbol{q}$, rather than the conservative variables $\boldsymbol{q}$.
2.  **SBP Operator**: The FR volume discretization is constructed to have the skew-symmetric SBP property.
3.  **Entropy-Conservative Flux**: A special two-point numerical flux $\boldsymbol{f}^{\mathrm{ec}}(\boldsymbol{q}_L, \boldsymbol{q}_R)$ is used that is designed to be exactly entropy conservative, meaning it satisfies a specific algebraic relation known as Tadmor's identity.

When these components are combined, the skew-symmetry of the SBP volume operator ensures that the volume terms perfectly conserve entropy. The total change in entropy is then governed entirely by the numerical flux at the interfaces. By using an entropy-conservative flux, one can build a scheme that exactly conserves entropy ($\frac{dS}{dt} = 0$). To achieve true [entropy stability](@entry_id:749023) ($\frac{dS}{dt} \le 0$), a dissipative term is added to the [numerical flux](@entry_id:145174), carefully designed to provide the necessary [entropy production](@entry_id:141771) at discontinuities like shocks.

#### Practical Considerations: Aliasing and Curved Meshes

The practical application of FR to complex problems involves further considerations. When dealing with nonlinear fluxes, the product of polynomials can result in a higher-degree polynomial that cannot be exactly represented in the chosen approximation space. This can lead to **aliasing errors**, which may destabilize the scheme. While simply using a more accurate quadrature rule (over-integration) can resolve this, more sophisticated and efficient approaches involve using **split-form** or skew-symmetric discretizations of the nonlinear terms, which can be constructed to be stable by design, even in the presence of [aliasing](@entry_id:146322) .

Furthermore, when applying FR methods to problems on non-uniform, [curvilinear meshes](@entry_id:748122), the transformation from physical to reference coordinates introduces geometric metric terms. For the numerical scheme to correctly preserve even the simplest solution, such as a uniform free-stream flow ($u = \text{const}$), the discrete operators and the discrete representation of the metric terms must satisfy a compatibility condition known as the **discrete Geometric Conservation Law (GCL)** . Failure to satisfy the discrete GCL results in spurious source terms that can corrupt the solution, even for very simple flows. Satisfying this law requires either a specific, mimetic construction of the [discrete metric](@entry_id:154658) terms (e.g., from a discrete curl form) or a modification of the discrete operators to be compatible with the geometry representation. This is a critical aspect for ensuring the accuracy and robustness of [high-order methods](@entry_id:165413) on complex geometries.