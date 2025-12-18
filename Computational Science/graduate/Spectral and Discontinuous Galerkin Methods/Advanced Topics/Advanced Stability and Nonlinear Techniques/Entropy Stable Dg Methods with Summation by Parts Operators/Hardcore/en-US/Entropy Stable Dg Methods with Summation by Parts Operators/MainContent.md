## Introduction
The accurate simulation of systems governed by [hyperbolic conservation laws](@entry_id:147752), from [compressible fluid](@entry_id:267520) dynamics to [traffic flow](@entry_id:165354), presents a significant computational challenge. While [high-order methods](@entry_id:165413) like the Discontinuous Galerkin (DG) method offer superior accuracy, they can suffer from catastrophic instabilities when confronted with the shocks and discontinuities inherent in nonlinear problems. The key to developing robust schemes lies in satisfying a discrete analogue of a fundamental physical principle: the second law of thermodynamics. This article addresses the critical knowledge gap of how to construct DG schemes that are provably nonlinearly stable by design, rather than by ad-hoc fixes.

We will embark on a comprehensive exploration of entropy-stable DG methods built upon Summation-by-Parts (SBP) operators. The journey begins in the "Principles and Mechanisms" chapter, where we will dissect the algebraic foundation of SBP operators and the construction of entropy-conservative and entropy-stable numerical fluxes. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate the framework's power in handling complex geometries, physical boundary conditions, and even problems outside of traditional fluid dynamics. Finally, "Hands-On Practices" will ground these theoretical concepts in concrete computational exercises. This structured approach will equip the reader with the knowledge to build and analyze robust, high-order numerical schemes that are trustworthy by construction.

## Principles and Mechanisms

The formulation of robust and [high-order numerical methods](@entry_id:142601) for [hyperbolic conservation laws](@entry_id:147752) rests upon mimicking fundamental physical and mathematical principles at the discrete level. For nonlinear systems, the most critical of these is the [second law of thermodynamics](@entry_id:142732), which manifests as a non-decreasing [entropy condition](@entry_id:166346). This chapter delineates the core principles and mechanisms that enable the construction of Discontinuous Galerkin (DG) schemes that provably satisfy a [discrete entropy inequality](@entry_id:748505). The key components of this framework are Summation-by-Parts (SBP) operators, which provide a discrete analogue of [integration by parts](@entry_id:136350), and specially designed [numerical fluxes](@entry_id:752791) that control the production of entropy.

### The Summation-by-Parts Property in Discontinuous Galerkin Methods

At the heart of provably stable schemes lies the concept of a discrete operator that mimics the integration-by-parts formula. This is formalized by the **Summation-by-Parts (SBP)** property. For a one-dimensional DG method on a reference element, let nodal values of a function be represented by a vector $\boldsymbol{u}$. The discretization involves a [symmetric positive-definite](@entry_id:145886) [mass matrix](@entry_id:177093), $H$, which defines a discrete inner product, and a [differentiation matrix](@entry_id:149870), $D$. Typically, for nodal DG methods, $H$ is a [diagonal matrix](@entry_id:637782) whose entries are the [quadrature weights](@entry_id:753910). The pair $(H, D)$ is said to possess the SBP property if there exists a boundary matrix $B$ such that:

$$
H D + D^T H = B
$$

This identity is the discrete analogue of the continuous integration-by-parts rule $\int (u'v + uv') dx = [uv]_{\text{boundary}}$. The term $H D$ represents the action of differentiation, while $D^T H$ represents its transpose with respect to the inner product defined by $H$. The matrix $B$ isolates the effect of the operator to the element boundaries, which is crucial for coupling elements and proving stability.

A powerful and common way to construct such an operator in the context of a DG Spectral Element Method (DGSEM) is to use Legendre-Gauss-Lobatto (LGL) nodes and quadrature. For a [polynomial space](@entry_id:269905) of degree $p$, one uses the $p+1$ LGL nodes $\{r_i\}_{i=1}^{p+1}$ on the reference interval $[-1,1]$. The [mass matrix](@entry_id:177093) $H$ is diagonal with the LGL [quadrature weights](@entry_id:753910) $\{w_i\}$ as its entries, and the [differentiation matrix](@entry_id:149870) $D$ is the [spectral collocation](@entry_id:139404) [differentiation matrix](@entry_id:149870). The LGL [quadrature rule](@entry_id:175061) is exact for polynomials up to degree $2p-1$. Since the product of two polynomials of degree $p$ and $p-1$ has a degree of $2p-1$, the quadrature rule is exact enough to make the discrete integration-by-parts formula hold true. This [exactness](@entry_id:268999) directly gives rise to the SBP property, where the [boundary operator](@entry_id:160216) $B$ is a simple [diagonal matrix](@entry_id:637782) with non-zero entries only at the nodes corresponding to the physical boundaries of the element: $B = \operatorname{diag}(-1, 0, \dots, 0, 1)$ . A key feature of this construction is its accuracy: the differentiation operator $D$ is exact when applied to any polynomial of degree up to $p$, meaning the nodal truncation error for such polynomials is identically zero . Furthermore, under an [affine mapping](@entry_id:746332) from the reference element to any physical element $[a,b]$, the SBP property is preserved and the boundary matrix $B$ remains unchanged, demonstrating the robustness of this formulation .

### The Imperative of Entropy Stability

While SBP operators provide the necessary algebraic structure, the motivation for their use stems from the distinct stability requirements of linear and [nonlinear conservation laws](@entry_id:170694). The stability concept for linear systems is often not sufficient for [nonlinear systems](@entry_id:168347), which can develop shock waves and other discontinuities.

For a linear symmetric hyperbolic system, $u_t + A u_x = 0$ with $A=A^T$, stability can be established by examining the [time evolution](@entry_id:153943) of the discrete **$L^2$ energy**, $\mathcal{E} = \boldsymbol{u}^T H \boldsymbol{u} = ||\boldsymbol{u}||_H^2$. A semi-discrete scheme is **energy stable** if it can be shown that $\frac{d\mathcal{E}}{dt} \le 0$. This proof typically involves multiplying the semi-discrete equation by $\boldsymbol{u}^T$ and using the SBP property to express the spatial operator's contribution as boundary and interface terms, which are then controlled by an appropriate dissipative [numerical flux](@entry_id:145174) (e.g., an [upwind flux](@entry_id:143931)).

For a [nonlinear system](@entry_id:162704) of conservation laws, $u_t + f(u)_x = 0$, this $L^2$ energy is generally not a conserved or decaying quantity. Instead, physical solutions are governed by an [entropy condition](@entry_id:166346), which requires that a chosen convex mathematical entropy $U(u)$ does not increase in time (for smooth flows) or is dissipated at shocks. A semi-discrete scheme is **entropy stable** if it satisfies a discrete version of the [entropy inequality](@entry_id:184404), $\frac{d\mathcal{S}}{dt} \le 0$, where $\mathcal{S} = \sum_i w_i U(u_i)$ is the total discrete entropy. Establishing this property requires a different analytical path: one multiplies the semi-discrete equation by the transpose of the **entropy variables**, defined as $v(u) = \nabla_u U(u)$.

The distinction is critical. An SBP-DG scheme that is provably $L^2$-stable for a linearized version of a nonlinear system is not guaranteed to be entropy-stable for the full nonlinear system. A canonical example is the system of compressible Euler equations. A scheme using a Roe flux, which is derived from a [local linearization](@entry_id:169489), can be shown to be stable in the $L^2$ sense for that linearized system. However, without modification, it is known to admit entropy-violating solutions (such as expansion shocks) for the full nonlinear Euler equations. Therefore, linear stability is a necessary but insufficient condition for nonlinear problems . The explicit enforcement of a [discrete entropy inequality](@entry_id:748505) is paramount.

### The Cornerstone of Stability: Entropy Conservation

The modern path to constructing [entropy-stable schemes](@entry_id:749017) begins by first designing a scheme that is **entropy conservative**. This means the scheme conserves the total discrete entropy exactly, without numerical dissipation. While not sufficient for shock-capturing, it forms a non-dissipative baseline upon which physical dissipation can be precisely added.

The construction of [entropy-conservative fluxes](@entry_id:749013) stems from a key identity in the continuous theory. Associated with an entropy pair $(U(u), F(u))$ and flux $f(u)$ is the **entropy potential**, defined as:

$$
\psi(u) = v(u)^T f(u) - F(u)
$$

where $v(u) = \nabla_u U(u)$ are the entropy variables. These quantities are related through the fundamental identity $\partial_x \psi(u) = (\partial_x v(u))^T f(u)$ . The goal is to create a two-point [numerical flux](@entry_id:145174), $f^{ec}(u_L, u_R)$, that satisfies a discrete analogue of this identity at an interface between a left state $u_L$ and a right state $u_R$. This leads to Tadmor's condition for an **entropy-conservative (EC) flux** :

$$
(v(u_R) - v(u_L))^T f^{ec}(u_L, u_R) = \psi(u_R) - \psi(u_L)
$$

Any symmetric and consistent [numerical flux](@entry_id:145174) that satisfies this identity for all input states is, by definition, entropy conservative. When used in an SBP-DG scheme, the sum of entropy changes across all interfaces forms a [telescoping sum](@entry_id:262349) involving the potential $\psi$, leading to exact conservation of the discrete entropy (up to physical boundary terms).

To make this concept concrete, consider the inviscid Burgers' equation, $u_t + \partial_x(\frac{1}{2}u^2) = 0$, with the quadratic entropy $U(u) = \frac{1}{2}u^2$. The corresponding entropy flux is $F(u) = \frac{1}{3}u^3$. The entropy variable is simply $v(u) = u$, and the entropy potential is $\psi(u) = v(u)f(u) - F(u) = u(\frac{1}{2}u^2) - \frac{1}{3}u^3 = \frac{1}{6}u^3$. Plugging these into Tadmor's condition and solving for the flux gives the canonical entropy-conservative flux for Burgers' equation :

$$
f^{ec}(u_L, u_R) = \frac{u_L^2 + u_L u_R + u_R^2}{6}
$$

### Taming Nonlinearities: Aliasing, Split Forms, and the SBP-DG Connection

A critical challenge arises when discretizing the volume term $\int \phi_i \partial_x f(u) dx$ within an element. A standard collocation approach evaluates the flux function at the nodes, $f(u_i)$, and then applies the [differentiation matrix](@entry_id:149870). However, if $u$ is a polynomial of degree $p$, the nonlinear function $f(u)$ is generally not a polynomial of degree $p$. The process of representing $f(u)$ by its values at the collocation nodes effectively projects it back into the degree-$p$ [polynomial space](@entry_id:269905). This projection introduces **aliasing errors**, where high-frequency content in $f(u)$ is misrepresented as low-frequency modes. This [aliasing](@entry_id:146322) can introduce spurious, non-physical energy and destroy the delicate entropy balance, leading to instability .

We can observe this phenomenon directly. For the Burgers' equation with $p=3$ on LGL nodes, if we take the solution to be the polynomial $u(x) = x^3 - x$, the exact volume entropy production integrated over the element is zero. However, a standard collocated discretization produces a spurious, non-zero entropy production rate of $\frac{16}{375}$, an error attributable entirely to the [quadrature rule](@entry_id:175061)'s inability to exactly integrate the high-degree polynomial that arises in the entropy analysis .

The solution to this [aliasing](@entry_id:146322) problem is to abandon the standard collocation formulation of the volume term and instead adopt a **split form** or **flux differencing** approach. This involves rewriting the volume derivative operator using the two-point EC flux derived previously. For a DGSEM using an SBP operator, the volume term's contribution to the evolution of the solution at node $i$ is constructed as :

$$
[\boldsymbol{V}]_i = -\sum_{j=1}^{p+1} 2 S_{ij} f^{ec}(u_i, u_j)
$$

where $S = \frac{1}{2}(HD - (HD)^T)$ is the skew-symmetric part of the SBP operator. By construction, this formulation is discretely conservative within the element. When analyzing the entropy, the combination of the skew-symmetry of the operator $S$ and the symmetry of the flux $f^{ec}$ ensures that all internal contributions cancel out in a [telescoping sum](@entry_id:262349). This renders the volume term entropy-conservative by construction, effectively [de-aliasing](@entry_id:748234) the formulation and establishing a direct link between the DGSEM and SBP [finite difference methods](@entry_id:147158) . This algebraic cancellation relies on the SBP property, which in turn relies on the quadrature rule being sufficiently accurate. For polynomial data of degree $p$, the underlying quadrature must be exact for polynomials of degree at least $2p-1$ for the discrete properties to perfectly mirror the continuous ones . LGL quadrature, with its exactness of $2p-1$, is thus a natural choice.

### From Conservation to Dissipation: Completing the Entropy-Stable Scheme

While an entropy-[conservative scheme](@entry_id:747714) is stable for smooth flows, it does not include the physical dissipation necessary to handle shocks and other discontinuities. To create a fully **entropy-stable (ES) scheme**, we must introduce a dissipation mechanism. This is achieved by augmenting the entropy-conservative flux, particularly at the interfaces between elements.

A common approach is to define an entropy-stable flux $f^{es}$ by adding a specific dissipative term to the EC flux:

$$
f^{es}(u_L, u_R) = f^{ec}(u_L, u_R) - \frac{1}{2} \alpha(u_L, u_R) (v_R - v_L)
$$

Here, $\alpha \ge 0$ is a dissipation coefficient, often related to the local wave speeds (e.g., the Lax-Friedrichs speed), and $v_R-v_L$ is the jump in the entropy variables across the interface. The contribution of this flux to the entropy balance at an interface is found by evaluating $(v_R - v_L)^T f^{es}$. Due to the entropy-conservative property of $f^{ec}$, the only part that contributes to entropy change is the dissipative term. The resulting interface entropy dissipation, $D$, is given by:

$$
D = - (v_R - v_L)^T [f^{es} - f^{ec}] = - (v_R - v_L)^T \left( - \frac{1}{2} \alpha (v_R - v_L) \right) = \frac{1}{2} \alpha (v_R - v_L)^T (v_R - v_L)
$$

Since $\alpha \ge 0$ and $(v_R - v_L)^T(v_R - v_L) \ge 0$, this term is guaranteed to be non-negative. This ensures that the scheme produces entropy at discontinuities where the entropy variables have a jump, satisfying the second law of thermodynamics at the discrete level. For the Burgers' equation with a Lax shock, this [dissipation rate](@entry_id:748577) becomes $D = \frac{1}{2} \max(|u_L|, |u_R|) (u_L - u_R)^2$, demonstrating that the amount of dissipation is directly proportional to the local [wave speed](@entry_id:186208) and the square of the shock strength . By combining the entropy-conservative split-form for the [volume integrals](@entry_id:183482) with this entropy-stable flux at the interfaces, we arrive at a [semi-discretization](@entry_id:163562) that is guaranteed to be nonlinearly stable.