## Introduction
The ability to accurately and efficiently simulate the behavior of neutrons within a nuclear reactor is fundamental to modern reactor design, safety analysis, and operation. The governing physics is described by the [neutron transport equation](@entry_id:1128709), which is computationally expensive to solve for realistic, three-dimensional core models. Nodal methods offer a powerful solution to this challenge by solving an approximation, the neutron diffusion equation, on a coarse spatial mesh with remarkable accuracy. The key to their success lies in a mathematical procedure known as **transverse integration**.

This article addresses the need for a detailed understanding of how this technique works. It bridges the gap between the complex three-dimensional problem and the highly efficient, coupled one-dimensional equations that nodal codes actually solve. By mastering the concepts presented, you will gain a deep appreciation for the theoretical underpinnings and practical power of modern reactor simulation tools.

The journey begins in the **Principles and Mechanisms** chapter, where we will derive the transversely integrated equations from the fundamental [neutron diffusion equation](@entry_id:1128691), dissect the critical role of the transverse leakage term, and explore the polynomial expansion methods used to solve the resulting system. Next, **Applications and Interdisciplinary Connections** will showcase how these principles are applied to solve full-core reactor problems, perform [pin power reconstruction](@entry_id:1129703), and handle complex geometries, while also drawing parallels to concepts in other fields of computational science. Finally, the **Hands-On Practices** section will allow you to apply your knowledge to solve concrete problems, solidifying your understanding of this essential computational method.

## Principles and Mechanisms

The accurate and efficient simulation of the neutron flux distribution within a [nuclear reactor core](@entry_id:1128938) is a cornerstone of reactor design, safety analysis, and operational management. The governing equation for this distribution is the [neutron transport equation](@entry_id:1128709), which is notoriously difficult to solve for realistic, three-dimensional systems. A common and effective simplification is the neutron diffusion equation, a second-order partial differential equation (PDE) that provides a good approximation in many reactor types. However, even solving the [multigroup diffusion](@entry_id:1128303) equation over a full reactor core with a fine spatial mesh is computationally prohibitive. Nodal methods were developed to address this challenge by solving the diffusion equation on a coarse spatial mesh, where each "node" typically corresponds to a single fuel assembly.

The power of nodal methods lies in their ability to achieve high accuracy on this coarse mesh. This is accomplished not by simplifying the underlying physics, but by reformulating the three-dimensional PDE into a set of coupled one-dimensional ordinary differential equations (ODEs) that are solved with high-order techniques. The key procedure that enables this [dimensional reduction](@entry_id:197644) is **transverse integration**. This chapter elucidates the fundamental principles and mechanisms of transverse integration techniques, forming the theoretical bedrock of modern nodal diffusion methods.

### The Principle of Dimensional Reduction: From PDE to ODE

The starting point for our analysis is the steady-state, multigroup neutron diffusion equation. For a specific energy group $g$, this equation represents a balance of neutron production and loss within an infinitesimal volume element. It is given by :

$$
-\nabla\cdot \big(D_g(\mathbf{r})\,\nabla\phi_g(\mathbf{r})\big)+\Sigma_{r,g}(\mathbf{r})\,\phi_g(\mathbf{r}) = \sum_{g' \neq g}\Sigma_{s,g' \to g}(\mathbf{r})\,\phi_{g'}(\mathbf{r}) + \frac{\chi_g}{k}\sum_{g'}\nu\,\Sigma_{f,g'}(\mathbf{r})\,\phi_{g'}(\mathbf{r})
$$

Here, $\phi_g(\mathbf{r})$ is the **neutron [scalar flux](@entry_id:1131249)** in group $g$ at position $\mathbf{r}$ (units of $n \cdot \mathrm{cm}^{-2} \cdot \mathrm{s}^{-1}$), which represents the total path length traveled by neutrons of energy group $g$ per unit volume per unit time. The other terms are:
- $D_g(\mathbf{r})$: the **diffusion coefficient** (units of $\mathrm{cm}$), which characterizes the rate of [neutron diffusion](@entry_id:158469).
- $\Sigma_{r,g}(\mathbf{r})$: the **macroscopic removal cross section** (units of $\mathrm{cm}^{-1}$), representing the probability per unit path length that a neutron is removed from group $g$ by either absorption ($\Sigma_{a,g}$) or scattering to another group $g'$ ($\Sigma_{s,g \to g'}$).
- $\Sigma_{s,g' \to g}(\mathbf{r})$: the **macroscopic [scattering cross section](@entry_id:150101)** from group $g'$ into group $g$.
- $\nu\Sigma_{f,g'}(\mathbf{r})$: the **macroscopic neutron production cross section**, giving the rate of new neutrons produced by fissions induced by neutrons in group $g'$.
- $\chi_g$: the **fission spectrum fraction**, a dimensionless quantity representing the fraction of fission neutrons born into energy group $g$.
- $k$: the **[effective multiplication factor](@entry_id:1124188)**, a dimensionless eigenvalue that determines the criticality of the reactor.

In nodal methods, the reactor is divided into coarse, typically rectangular, nodes. A fundamental assumption is that within each node, the material properties (all cross sections and the diffusion coefficient) are **piecewise constant**, meaning they are spatially uniform within that node. The neutron flux $\phi_g(\mathbf{r})$, however, is a spatially varying function that must be solved for.

The core idea of transverse integration is to reduce the dimensionality of this 3D PDE by integrating it over the directions "transverse" to a chosen coordinate axis. For instance, to obtain a 1D equation in the $x$-direction for a node spanning the region $[0, h_x] \times [0, h_y] \times [0, h_z]$, we can define a transverse [integration operator](@entry_id:272255) $T_x[\cdot]$ :

$$
T_x[f](x) \equiv \frac{1}{A_{yz}} \int_{0}^{h_z} \int_{0}^{h_y} f(x,y,z) \, dy \, dz
$$

where $A_{yz} = h_y h_z$ is the transverse cross-sectional area. Applying this operator to the entire diffusion equation term by term, and using the property that integration and differentiation can be interchanged for the axial direction, we obtain:

$$
- \frac{d}{dx}\left( D_g \frac{d \bar{\phi}_g(x)}{dx} \right) + \Sigma_{r,g} \bar{\phi}_g(x) = \bar{S}_g(x) - \bar{L}_g^T(x)
$$

where $\bar{\phi}_g(x) = T_x[\phi_g](x)$ is the transversely-averaged flux, $\bar{S}_g(x) = T_x[S_g](x)$ is the transversely-averaged source term (from scattering and fission), and $\bar{L}_g^T(x)$ is the **transversely-averaged transverse leakage term**. This new term arises from the integration of the transverse components of the divergence operator:

$$
\bar{L}_g^T(x) = \frac{1}{A_{yz}} \int_{0}^{h_z} \int_{0}^{h_y} \left[ -\frac{\partial}{\partial y}\left(D_g\frac{\partial\phi_g}{\partial y}\right) - \frac{\partial}{\partial z}\left(D_g\frac{\partial\phi_g}{\partial z}\right) \right] dy \, dz
$$

It is conventional to move this leakage term to the right-hand side of the equation, where it acts as a known source or sink in the 1D problem. The final 1D nodal balance equation takes the form:

$$
- \frac{d}{dx}\left( D_g \frac{d \bar{\phi}_g(x)}{dx} \right) + \Sigma_{r,g} \bar{\phi}_g(x) = \bar{S}_g(x) + L_g^T(x)
$$

where $L_g^T(x) = - \bar{L}_g^T(x)$. At this point, the transformation from a 3D PDE to a 1D ODE is mathematically exact. The challenge of nodal methods is not in this derivation, but in finding a way to accurately approximate the unknown transverse leakage term $L_g^T(x)$.

### The Transverse Leakage Term: Physical and Mathematical Characterization

The transverse leakage term, $L_g^T(x)$, is the single most important concept in transverse integration. It is the term that couples the 1D equation in one direction to the behavior of the flux in the other two directions. Without it, the method would incorrectly assume the problem is separable into three independent 1D problems.

By applying the Divergence Theorem in the 2D transverse plane (or, equivalently, the Fundamental Theorem of Calculus along each transverse dimension), the definition of the leakage can be transformed from a [volume integral](@entry_id:265381) of derivatives to a [surface integral](@entry_id:275394) of currents . For a 2D problem being reduced to 1D, the transverse leakage simplifies to:

$$
L_{T,g}(x) = \frac{1}{h_y} \int_{y_1}^{y_2} \left( -\frac{\partial}{\partial y} \left( D_g \frac{\partial \phi_g}{\partial y} \right) \right) dy = \frac{1}{h_y} \left[ J_{y,g}(x,y_1) - J_{y,g}(x,y_2) \right]
$$

where $J_{y,g} = -D_g \partial\phi_g/\partial y$ is the [neutron current](@entry_id:1128689) in the $y$-direction. This expression reveals the physical meaning of the transverse leakage: it is the **net current of neutrons streaming into a 1D slice at position $x$ through its transverse faces**. It represents a source of neutrons if the inflow is greater than the outflow, and a sink if the outflow is greater.

The properties of the transverse leakage are dictated by the physical situation. For example, if a node has a **[reflective boundary condition](@entry_id:1130780)** on a transverse face (e.g., at $y=y_2$), the normal component of the current is zero, $J_{y,g}(x,y_2) = 0$. If both transverse faces are reflective, the entire transverse leakage term becomes identically zero, $L_{T,g}(x) = 0$, correctly reflecting that there is no net neutron exchange in the transverse direction .

The smoothness of $L_g^T(x)$ as a function of the axial coordinate $x$ is also a critical property. If the material properties and geometry of the transverse plane are constant along the $x$-axis within a node, the solution to the elliptic diffusion PDE, $\phi_g(x,y,z)$, will be a smooth (infinitely differentiable) function of $x$. Since $L_g^T(x)$ is derived from $\phi_g$ through linear operations ([differentiation and integration](@entry_id:141565)), it too will be a smooth function of $x$ . However, in some reactor designs, the material layout in the transverse plane may change at a specific axial location, for instance, at the boundary between a fuel region and a reflector region. If the material properties within the transverse plane, such as $D_g(y,z)$, change abruptly at an [axial plane](@entry_id:924455) $x=x^*$, the transverse leakage term $L_g^T(x)$ will exhibit a **[jump discontinuity](@entry_id:139886)** at that point, even though the flux $\phi_g$ itself remains continuous . This behavior must be handled correctly by the numerical scheme.

### The Nodal Expansion Method (NEM): Approximating the Solution

The derived 1D nodal equation is exact, but it is not closed; it contains two unknowns, the averaged flux $\bar{\phi}_g(x)$ and the transverse leakage $L_g^T(x)$. The **Nodal Expansion Method (NEM)** is a powerful framework for solving this equation by approximating these unknown functions.

In NEM, the 1D averaged flux $\bar{\phi}_g(\xi)$ within a node is expanded in a [basis of polynomials](@entry_id:148579) over a normalized local coordinate $\xi \in [-1, 1]$. While simple monomials ($\{1, \xi, \xi^2, \dots\}$) could be used, **Legendre polynomials** $\{P_n(\xi)\}$ are far superior due to their [orthogonality property](@entry_id:268007) over the interval $[-1, 1]$ with a unity weight function:

$$
\int_{-1}^{1} P_i(\xi) P_j(\xi) \, d\xi = \frac{2}{2i+1} \delta_{ij}
$$

A typical flux expansion in modern nodal codes is of third or fourth order :
$$
\bar{\phi}_g(\xi) \approx A_0 P_0(\xi) + A_1 P_1(\xi) + A_2 P_2(\xi) + A_3 P_3(\xi)
$$

Simultaneously, the transverse leakage term $L_g^T(\xi)$ is also approximated by a low-order polynomial, typically quadratic:
$$
L_g^T(\xi) \approx C_0 P_0(\xi) + C_1 P_1(\xi) + C_2 P_2(\xi)
$$

The coefficients of these expansions are determined by enforcing a set of constraints. Some coefficients are determined by physical boundary conditions (e.g., average flux values at the node interfaces). The remaining "internal" coefficients are determined by a **[method of weighted residuals](@entry_id:169930) (MWR)**. This method requires that the error, or residual, of the approximated 1D equation be orthogonal to a set of chosen [test functions](@entry_id:166589).

The choice of test functions is critical. To guarantee two essential properties—(1) that the node-average neutron balance is satisfied exactly, and (2) that the moments of the source term are captured without error (aliasing)—a **Galerkin method** is employed, where the test functions are the same as the basis functions: the Legendre polynomials . Using $P_0(\xi)=1$ as the first test function ensures that the integrated (zeroth moment) form of the balance equation is satisfied exactly. Using $P_1(\xi)$ and $P_2(\xi)$ as test functions ensures that the first and second moments of the leakage polynomial are projected uniquely onto the corresponding [moment equations](@entry_id:149666), a direct consequence of orthogonality.

This leads to a crucial insight regarding the necessary order of the leakage approximation . If we use a high-order (e.g., cubic) flux expansion and a Galerkin method with test functions up to quadratic order ($P_0, P_1, P_2$), the second-moment equation will involve terms from the quadratic part of the flux ($A_2 P_2$) and the quadratic part of the leakage ($C_2 P_2$). If we were to use an insufficient, linear approximation for the leakage ($C_2=0$), the MWR constraint would artificially force the quadratic component of the flux to zero ($A_2=0$), severely compromising the accuracy of the method. Therefore, to be compatible with a high-order flux expansion, the transverse leakage approximation **must** be at least quadratic. This ensures the flux shape within the node is flexible enough to accurately represent the true solution.

### The Iterative Solution Strategy: Dimensional Splitting

Transverse integration produces a set of three 1D equations, one for each spatial direction. The equation for the $x$-direction contains a transverse leakage term $L_x^T$ that depends on the flux behavior in the $y$ and $z$ directions. Similarly, the $y$-equation depends on $x$ and $z$, and the $z$-equation on $x$ and $y$. This creates a coupled system.

This system is solved using an iterative **[dimensional splitting](@entry_id:748441)** strategy . The procedure is as follows:
1.  Make an initial guess for the transverse leakage functions in all directions, e.g., $L_x^{(0)}, L_y^{(0)}, L_z^{(0)}$.
2.  Solve the 1D nodal equations for the $x$-direction for all nodes in the core, treating $L_x^{(0)}$ as a known source term. This yields an updated set of 1D flux moments in the $x$-direction.
3.  Using the updated flux information, reconstruct an approximation of the 3D flux distribution and use it to compute new estimates for the transverse leakages for the *next* direction, say $L_y^{(1)}$.
4.  Solve the 1D nodal equations for the $y$-direction for all nodes, using $L_y^{(1)}$ as the source term.
5.  Repeat for the $z$-direction, generating $L_z^{(1)}$ and solving the $z$-directed equations.
6.  This completes one "outer" iteration. The entire $x \to y \to z$ sweep is repeated, each time using the most recently computed flux profiles to update the leakage terms for the subsequent direction, until the leakage functions (and other flux moments) converge to a steady value.

A common misconception is that this iterative splitting introduces an error, similar to the [commutator error](@entry_id:747515) in ADI methods for time-dependent problems. This is not the case. The transverse integration procedure is an exact reformulation of the steady-state PDE. The iterative scheme is simply a method for solving the resulting system of coupled, [non-linear equations](@entry_id:160354). At the **fixed point** of the iteration (i.e., at convergence), the leakage terms used as input to the 1D solvers are precisely the same as those calculated from the resulting 3D [flux reconstruction](@entry_id:147076). At this point, the solution simultaneously satisfies the exact 1D balance equations in all three directions. This is equivalent to satisfying the [weak form](@entry_id:137295) of the original 3D diffusion equation, meaning the method is fully **consistent** with the original PDE .

### Application to Realistic Systems: Homogenization and Discontinuity Factors

The discussion so far has implicitly assumed that the material properties within a node are uniform. In a real reactor, a fuel assembly is a highly heterogeneous structure containing fuel pins, guide tubes, and moderator. To apply the nodal method, these heterogeneous properties must be replaced by equivalent, **homogenized** constant parameters for the entire node.

The primary goal of homogenization is to preserve the node-integrated reaction rates. This is achieved by defining the homogenized cross sections using **flux weighting**. The homogenized macroscopic cross section for a reaction $r$ (e.g., absorption) is defined as the total heterogeneous reaction rate in the node divided by the total heterogeneous flux in the node :
$$
\Sigma_{r,h}^g = \frac{\int_{V_N} \Sigma_r^g(\mathbf{r}) \phi_{\text{het}}^g(\mathbf{r})\, dV}{\int_{V_N} \phi_{\text{het}}^g(\mathbf{r})\, dV}
$$
Here, $\phi_{\text{het}}^g(\mathbf{r})$ is the detailed flux profile within the heterogeneous node, obtained from a separate, high-fidelity "reference" calculation (typically a 2D transport calculation for a single assembly).

While this procedure preserves reaction rates, it creates a new problem. The flux profile in the homogenized model, $\phi_{\text{hom}}^g$, is smooth, whereas the true flux $\phi_{\text{het}}^g$ has a complex shape. Consequently, the face-averaged flux at the node boundary in the homogenized model will not match the true face-averaged flux: $\langle \phi_{\text{hom}}^g \rangle_f \neq \langle \phi_{\text{het}}^g \rangle_f$. If we enforce continuity of the homogenized flux between adjacent nodes, we will be using the wrong flux values to compute the inter-nodal leakage, thereby spoiling the accuracy of the [global solution](@entry_id:180992).

To resolve this, **Assembly Discontinuity Factors (ADFs)**, denoted $\delta_f^g$, are introduced  . An ADF is defined for each face of the node as the ratio of the "true" heterogeneous face-averaged flux to the homogenized face-averaged flux, both determined from the reference calculation:
$$
\delta_f^g = \frac{\langle \phi_{\text{het}}^g \rangle_f}{\langle \phi_{\text{hom}}^g \rangle_f}
$$
In the global coarse-mesh nodal calculation, physical continuity of current is still enforced on the homogenized currents. However, the condition for continuity of flux is modified. Instead of enforcing $\langle \phi_{\text{hom},i}^g \rangle_f = \langle \phi_{\text{hom},j}^g \rangle_f$ for adjacent nodes $i$ and $j$, we enforce continuity of the "true" flux by applying the ADFs:
$$
\delta_{f,i}^g \langle \phi_{\text{hom},i}^g \rangle_f = \delta_{f,j}^g \langle \phi_{\text{hom},j}^g \rangle_f
$$
This corrected interface condition ensures that the leakage between nodes in the coarse-mesh model is consistent with the underlying heterogeneous physics, thereby preserving the accuracy of both reaction rates and leakage balance across the entire reactor core.

### Boundary Conditions in the Transversely-Integrated Framework

A final practical consideration is the treatment of external boundary conditions of the reactor core. The physical boundary conditions are specified on the 2D surfaces of the 3D domain. To be consistent, these must also be transversely integrated to yield 1D boundary conditions for the nodal equations.

Consider a general Robin-type boundary condition on a face at $x=0$, which is uniform along the transverse direction $y$:
$$
\alpha \,\phi(0,y) + \beta \,J_x(0,y) = 0
$$
To obtain the corresponding 1D boundary condition, we simply apply the transverse [integration operator](@entry_id:272255) to this equation . Integrating over $y$ and dividing by the height $h_y$ gives:
$$
\alpha \left( \frac{1}{h_y} \int_{0}^{h_y} \phi(0,y)\,dy \right) + \beta \left( \frac{1}{h_y} \int_{0}^{h_y} J_x(0,y)\,dy \right) = 0
$$
Recognizing the terms in parentheses as the definitions of the transversely-averaged flux $\bar{\phi}(0)$ and transversely-averaged current $\overline{J}_x(0)$, we arrive at the consistent 1D boundary condition:
$$
\alpha \,\bar{\phi}(0) + \beta \,\overline{J}_x(0) = 0
$$
Furthermore, Fick's Law also holds for the averaged quantities, $\overline{J}_x(x) = -D \frac{d\bar{\phi}}{dx}$, allowing the boundary condition to be expressed purely in terms of the averaged flux $\bar{\phi}(x)$ and its derivative:
$$
\alpha \,\bar{\phi}(0) - \beta \,D \,\frac{d\bar{\phi}}{dx}\bigg|_{x=0} = 0
$$
This systematic procedure ensures that the 1D nodal equations are solved subject to boundary conditions that are mathematically and physically consistent with the original 3D problem.