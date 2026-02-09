## Introduction
Flux Vector Splitting (FVS) techniques represent a cornerstone in the field of computational physics, providing a robust and physically intuitive approach for the numerical solution of hyperbolic conservation laws. These equations, which govern phenomena from gas dynamics to magnetohydrodynamics, are characterized by information propagating at finite speeds along distinct paths. The central challenge in simulating these systems is to create numerical schemes that respect this directional flow of information, preventing instabilities and non-physical oscillations. FVS addresses this by splitting the physical flux vector itself into parts corresponding to waves moving in different directions, forming the basis for stable "upwind" methods.

This article provides a detailed examination of FVS, from its theoretical foundations to its application in state-of-the-art computational methods. Across the following chapters, you will gain a deep understanding of this essential numerical tool. The "Principles and Mechanisms" chapter will lay the groundwork, exploring characteristic decomposition and detailing the formulation of the pioneering Steger-Warming and van Leer splitting schemes. The "Applications and Interdisciplinary Connections" chapter will demonstrate the versatility of FVS, showing how it is integrated into high-order Discontinuous Galerkin methods and adapted for complex systems like MHD and shallow water flows. Finally, the "Hands-On Practices" section will offer focused exercises to solidify your understanding of critical concepts like entropy fixes and the accurate resolution of contact waves.

## Principles and Mechanisms

Flux Vector Splitting (FVS) techniques represent a foundational class of upwind methods for the numerical discretization of hyperbolic [systems of conservation laws](@entry_id:755768). In the context of Discontinuous Galerkin (DG) and spectral methods, these techniques are instrumental in constructing numerical fluxes at element interfaces that respect the directional nature of information propagation inherent in such systems. This chapter elucidates the core principles of FVS, beginning with the concept of characteristic decomposition, proceeding to the formulation of classic splitting schemes, and concluding with a critical analysis of their properties and limitations.

### The Principle of Characteristic Decomposition

Hyperbolic conservation laws model phenomena where information propagates at finite speeds along specific paths known as characteristics. To understand and numerically model this behavior, we begin with the system of conservation laws in its quasi-linear form. For a system in $d$ spatial dimensions,
$$
\partial_t \boldsymbol{u} + \nabla \cdot \boldsymbol{f}(\boldsymbol{u}) = \boldsymbol{0}
$$
where $\boldsymbol{u} \in \mathbb{R}^m$ is the vector of conserved variables and $\boldsymbol{f}: \mathbb{R}^m \to \mathbb{R}^{m \times d}$ is the flux tensor, we can analyze the propagation of a plane wave in an arbitrary direction given by a unit normal vector $\boldsymbol{n} \in \mathbb{R}^d$. The dynamics along this direction are governed by the one-dimensional system:
$$
\partial_t \boldsymbol{u} + \partial_\xi ( \boldsymbol{f}(\boldsymbol{u})\boldsymbol{n} ) = \boldsymbol{0}
$$
where $\xi = \boldsymbol{x} \cdot \boldsymbol{n}$ is the coordinate in the direction $\boldsymbol{n}$. The term $\boldsymbol{f}_{\boldsymbol{n}}(\boldsymbol{u}) = \boldsymbol{f}(\boldsymbol{u})\boldsymbol{n}$ is the directional flux. The quasi-linear form of this equation is obtained by applying the chain rule:
$$
\partial_t \boldsymbol{u} + A_{\boldsymbol{n}}(\boldsymbol{u}) \partial_\xi \boldsymbol{u} = \boldsymbol{0}
$$
where $A_{\boldsymbol{n}}(\boldsymbol{u}) = \partial \boldsymbol{f}_{\boldsymbol{n}} / \partial \boldsymbol{u}$ is the **directional flux Jacobian**.

A system of conservation laws is defined as **hyperbolic** if, for any state $\boldsymbol{u}$ and any direction $\boldsymbol{n}$, the flux Jacobian matrix $A_{\boldsymbol{n}}(\boldsymbol{u})$ is **diagonalizable with a complete set of real eigenvalues** [@problem_id:3386749]. This property is not merely a mathematical convenience; it is the physical foundation of wave propagation. The eigenvalues $\lambda_k$ of $A_{\boldsymbol{n}}(\boldsymbol{u})$ are the **characteristic speeds**, representing the velocities at which distinct modes of information travel. The corresponding right eigenvectors, $\boldsymbol{r}_k$, define the **characteristic fields**, which are the specific combinations of state variables that propagate together as waves. The diagonalizability of $A_{\boldsymbol{n}}(\boldsymbol{u})$ guarantees that any small perturbation to the state $\boldsymbol{u}$ can be decomposed into a linear combination of these characteristic waves.

To make this concrete, let us consider the one-dimensional Euler equations of gas dynamics, a canonical example of a hyperbolic system. The state and flux vectors are:
$$
\boldsymbol{u} = \begin{pmatrix} \rho \\ \rho u \\ E \end{pmatrix}, \quad \boldsymbol{f}(\boldsymbol{u}) = \begin{pmatrix} \rho u \\ \rho u^2 + p \\ u(E + p) \end{pmatrix}
$$
where $\rho$ is the density, $u$ is the velocity, $E$ is the total energy per unit volume, and $p$ is the pressure, given by the equation of state for a calorically perfect gas, $p = (\gamma - 1)(E - \frac{1}{2}\rho u^2)$. The flux Jacobian $A = \partial \boldsymbol{f} / \partial \boldsymbol{u}$ can be derived through a change of variables to the primitive variables $(\rho, u, p)$ [@problem_id:3386765]. The resulting eigenvalues of $A$ are:
$$
\lambda_1 = u - a, \quad \lambda_2 = u, \quad \lambda_3 = u + a
$$
where $a = \sqrt{\gamma p / \rho}$ is the speed of sound. These three distinct real eigenvalues confirm the hyperbolic nature of the Euler equations. They correspond to:
1.  An acoustic wave traveling upstream relative to the flow, with speed $u-a$.
2.  An entropy wave traveling with the flow, with speed $u$.
3.  An acoustic wave traveling downstream relative to the flow, with speed $u+a$.

The corresponding right eigenvectors, which form the columns of the matrix $R$ in the spectral decomposition $A = R\Lambda R^{-1}$, are [@problem_id:3386765]:
$$
\boldsymbol{r}_1 = \begin{pmatrix} 1 \\ u-a \\ H-ua \end{pmatrix}, \quad \boldsymbol{r}_2 = \begin{pmatrix} 1 \\ u \\ \frac{1}{2}u^2 \end{pmatrix}, \quad \boldsymbol{r}_3 = \begin{pmatrix} 1 \\ u+a \\ H+ua \end{pmatrix}
$$
where $H = (E+p)/\rho$ is the total enthalpy. This eigenstructure provides a complete basis for decomposing the flow dynamics into right-traveling ($\lambda_3 > 0$ for subsonic flow), left-traveling ($\lambda_1  0$ for subsonic flow), and stationary ($\lambda_2$) components. This decomposition is the fundamental prerequisite for Flux Vector Splitting.

### Flux Splitting Based on Characteristic Direction

The central idea of Flux Vector Splitting is to decompose the physical flux vector $\boldsymbol{f}(\boldsymbol{u})$ into two or more parts, each associated with waves propagating in a specific set of directions. For a one-dimensional problem or at a planar interface, this simplifies to splitting the flux into a component $\boldsymbol{f}^+(\boldsymbol{u})$ carrying information to the right (in the direction of increasing $x$) and a component $\boldsymbol{f}^-(\boldsymbol{u})$ carrying information to the left. The split must satisfy the consistency condition $\boldsymbol{f}(\boldsymbol{u}) = \boldsymbol{f}^+(\boldsymbol{u}) + \boldsymbol{f}^-(\boldsymbol{u})$.

The key requirement for this split is that the Jacobian of the positive flux, $A^+ = \partial \boldsymbol{f}^+ / \partial \boldsymbol{u}$, must have only non-negative eigenvalues, while the Jacobian of the negative flux, $A^- = \partial \boldsymbol{f}^- / \partial \boldsymbol{u}$, must have only non-positive eigenvalues. This ensures that $\boldsymbol{f}^+$ truly governs right-going waves and $\boldsymbol{f}^-$ governs left-going waves.

With such a splitting, a naturally upwinded numerical flux $\hat{\boldsymbol{f}}$ at an interface separating a left state $\boldsymbol{u}_L$ and a right state $\boldsymbol{u}_R$ can be constructed by taking the right-going contributions from the left state and the left-going contributions from the right state [@problem_id:3386754]:
$$
\hat{\boldsymbol{f}}(\boldsymbol{u}_L, \boldsymbol{u}_R) = \boldsymbol{f}^+(\boldsymbol{u}_L) + \boldsymbol{f}^-(\boldsymbol{u}_R)
$$
This formulation ensures that information is drawn from its natural direction of origin, providing the stability necessary for discretizing hyperbolic systems.

It is crucial to distinguish FVS from another major class of upwind schemes: **Approximate Riemann Solvers (ARS)**, also known as Flux Difference Splitting schemes [@problem_id:3386754]. While FVS schemes split the flux vector $\boldsymbol{f}(\boldsymbol{u})$ at a single point in state space, ARS schemes (such as the Roe solver) directly approximate the solution to the local Riemann problem posed by the discontinuity between $\boldsymbol{u}_L$ and $\boldsymbol{u}_R$. They compute the numerical flux based on the wave structure (speeds and strengths) that resolves the jump $\boldsymbol{u}_R - \boldsymbol{u}_L$. In essence, FVS is a "pointwise" split of the flux function, whereas ARS is a "wave-based" approximation of the interaction between two states.

### The Steger-Warming Splitting Scheme

The Steger-Warming scheme is a pioneering FVS method that formalizes the splitting process directly through the spectral decomposition of the flux Jacobian [@problem_id:3320850]. The approach begins by splitting the diagonal matrix of eigenvalues, $\Lambda$, into its positive and negative parts:
$$
\Lambda = \Lambda^+ + \Lambda^-
$$
where $\Lambda^+ = \text{diag}(\max(0, \lambda_k))$ and $\Lambda^- = \text{diag}(\min(0, \lambda_k))$. This allows the Jacobian matrix itself to be split:
$$
A = A^+ + A^-, \quad \text{where} \quad A^\pm = R \Lambda^\pm R^{-1}
$$
The matrices $A^+$ and $A^-$ inherit their eigenspectra from $\Lambda^+$ and $\Lambda^-$, respectively, ensuring that $A^+$ has only non-negative eigenvalues and $A^-$ has only non-positive eigenvalues. An equivalent and compact way to write this is using the matrix absolute value $|A| = R|\Lambda|R^{-1}$:
$$
A^\pm = \frac{1}{2}(A \pm |A|)
$$

For flux functions that are homogeneous of degree one in the state variables, such as the Euler fluxes, we have the property $\boldsymbol{f}(\boldsymbol{u}) = A(\boldsymbol{u})\boldsymbol{u}$. This allows a natural definition of the split fluxes:
$$
\boldsymbol{f}^\pm(\boldsymbol{u}) = A^\pm(\boldsymbol{u})\boldsymbol{u}
$$
The complete formula for the positive split flux, $F^+(U)$, can be derived by first decomposing the state vector $U$ into the basis of right eigenvectors, applying the positive split eigenvalues, and then summing the results. This yields an explicit expression for the split flux as a weighted sum of the eigenvectors, where the weights depend on the positive parts of the characteristic speeds [@problem_id:3386784]. For the 1D Euler equations, this results in the expression:
$$
F^{+}(U) = \frac{\rho}{2\gamma} \frac{u-a+|u-a|}{2} \begin{pmatrix} 1 \\ u-a \\ H-ua \end{pmatrix} + \rho\frac{\gamma-1}{\gamma} \frac{u+|u|}{2} \begin{pmatrix} 1 \\ u \\ \frac{u^2}{2} \end{pmatrix} + \frac{\rho}{2\gamma} \frac{u+a+|u+a|}{2} \begin{pmatrix} 1 \\ u+a \\ H+ua \end{pmatrix}
$$
This formula clearly shows how each characteristic field (represented by its eigenvector) contributes to the positive flux only when its corresponding wave speed is positive.

### The van Leer Splitting Scheme

While conceptually elegant, the Steger-Warming scheme suffers from significant drawbacks. The use of the absolute value function in the eigenvalue splitting, $\lambda_k^\pm = \frac{1}{2}(\lambda_k \pm |\lambda_k|)$, renders the split fluxes non-differentiable at any point where an eigenvalue passes through zero (a "sonic point"). This can cause numerical glitches and degrade the convergence of implicit solvers.

The van Leer FVS scheme was designed specifically to remedy this issue by constructing split fluxes that are continuously differentiable ($C^1$) with respect to the state variables, particularly across sonic transitions [@problem_id:3386746]. Instead of a sharp, sign-based split of eigenvalues, van Leer proposed using smooth polynomial functions of the Mach number, $M=u/a$, to partition the flux.

The core of the method is the design of a smooth splitting function. For a generic non-dimensional eigenvalue $z$ (such as $M$ or $M \pm 1$), the positive split $z^+(z)$ is constructed to be $C^1$ at the sonic points $z = \pm 1$. This is achieved by finding a polynomial of minimal degree for the subsonic range $|z|  1$ that smoothly connects the supersonic forms ($z^+(z)=z$ for $z \ge 1$ and $z^+(z)=0$ for $z \le -1$). This derivation yields the classic van Leer splitting function [@problem_id:3386746]:
$$
z^{+}(z) = 
\begin{cases} 
0   \text{if } z \leq -1 \\ 
\frac{1}{4}(z+1)^2   \text{if } |z|  1 \\ 
z   \text{if } z \geq 1 
\end{cases}
$$
This function and its first derivative are continuous everywhere, providing the desired smoothness.

The full van Leer scheme for the Euler equations applies this principle to split the mass and energy fluxes, resulting in a more complex but smoother formulation than Steger-Warming. For example, the split mass fluxes are constructed based on Mach number splits, and the split momentum flux involves a corresponding smooth pressure split [@problem_id:3387432]. The final upwind flux $\hat{F} = F^{+}(U_L) + F^{-}(U_R)$ is then formed in the usual way.

### Analysis of Properties and Pathologies

A deeper understanding of FVS requires a critical analysis of their properties, including their dissipative nature and their behavior in challenging flow regimes.

#### Numerical Dissipation

Upwind schemes inherently introduce numerical dissipation, which is necessary for stability and to capture sharp gradients like shocks without spurious oscillations. The dissipative mechanism of FVS can be revealed by rewriting the numerical flux in terms of a central average and a dissipative term. For any FVS scheme, the numerical flux can be expressed as [@problem_id:3386755]:
$$
\hat{\boldsymbol{f}}(\boldsymbol{u}_L, \boldsymbol{u}_R) \approx \frac{1}{2}(\boldsymbol{f}(\boldsymbol{u}_L) + \boldsymbol{f}(\boldsymbol{u}_R)) - \frac{1}{2}|A|(\boldsymbol{u}_R - \boldsymbol{u}_L)
$$
The second term represents the numerical dissipation. The matrix $|A| = R|\Lambda|R^{-1}$ is positive semi-definite, ensuring that this term removes energy from the solution, damping high-frequency oscillations that manifest as large jumps ($\boldsymbol{u}_R - \boldsymbol{u}_L$) across element interfaces. This dissipation is **anisotropic**: it acts on each characteristic field in proportion to the magnitude of its characteristic speed, $|\lambda_k|$. This is a desirable property, as it applies strong damping to fast-moving waves (like acoustic waves) while applying less damping to slow-moving waves (like entropy or shear waves).

#### Pathologies at Sonic and Stagnation Points

A major failing of early FVS schemes like Steger-Warming is their behavior at points where a characteristic speed is zero.
1.  **The Entropy Problem**: In a transonic rarefaction, an eigenvalue (e.g., $\lambda = u-a$) passes through zero. At the point where $\lambda=0$, the numerical dissipation for that characteristic field, proportional to $|\lambda|$, vanishes completely. This lack of dissipation allows the numerical scheme to form a non-physical, stationary "expansion shock," which violates the second law of thermodynamics (the entropy condition). To correct this, schemes like Roe's method and Steger-Warming require an **entropy fix**, which artificially "fattens" the absolute value function near zero to ensure a minimum level of dissipation is always present. Schemes like van Leer's, by virtue of their smooth polynomial construction, are designed to intrinsically avoid this issue [@problem_id:3320900].

2.  **Differentiability and Implicit Solvers**: As previously mentioned, the non-differentiability of the Steger-Warming split fluxes at sonic points poses a serious problem for implicit solvers that use Newton-Raphson methods. These solvers require the assembly of a Jacobian of the numerical residual, which is not continuously defined if the flux functions are not $C^1$. This can cause the Newton solver to stall or fail to converge quadratically. The $C^1$ continuity of van Leer's splitting was a crucial innovation that makes it far more suitable for implicit methods [@problem_id:3320867].

3.  **Low-Mach Number Dissipation**: A common criticism of standard FVS schemes is their excessive dissipation in low-speed, nearly incompressible flows. The numerical diffusion coefficient, which scales with the largest eigenvalue, is on the order of the sound speed, $\nu_{num} \propto a \Delta x$. However, the physical transport speed is the flow velocity, $u$. As the Mach number $M = u/a \to 0$, the ratio of numerical diffusion to physical convection, $\nu_{num}/(u\Delta x)$, scales as $1/M$ and diverges. This means the numerical diffusion overwhelms the physical convection, leading to a significant loss of accuracy for advected quantities [@problem_id:3320857]. This has motivated the development of many modern "low-Mach" or "all-speed" schemes.

In the context of high-order DG methods, FVS schemes provide the necessary dissipation at element interfaces to ensure stability. However, this interface dissipation alone is often insufficient to control the large, non-physical oscillations (Gibbs phenomenon) that can arise when a strong shock is represented by a high-degree polynomial *within* a single element. Therefore, for robust shock capturing, FVS must be complemented by nonlinear control mechanisms, such as limiters or artificial viscosity, that act inside the elements to enforce monotonicity [@problem_id:3386755].