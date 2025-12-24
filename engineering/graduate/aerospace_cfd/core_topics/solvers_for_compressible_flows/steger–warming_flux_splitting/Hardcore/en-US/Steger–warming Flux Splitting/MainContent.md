## Introduction
The Steger–Warming [flux splitting](@entry_id:637102) scheme is a foundational and robust numerical method in the field of computational fluid dynamics (CFD). It was developed to provide a stable and physically intuitive way to solve the Euler and Navier-Stokes equations, which are hyperbolic in nature and govern the complex phenomena of wave propagation, shocks, and contact discontinuities in fluid flow. The central challenge these equations present is ensuring that numerical solutions respect the directional flow of information dictated by the system's characteristic waves. Steger–Warming splitting addresses this by elegantly decomposing the flux vector itself into components that travel in opposite directions, providing a natural upwinding mechanism.

This article offers a graduate-level exploration of this pivotal method. We will move from the mathematical underpinnings to practical implementation and advanced considerations. In the "Principles and Mechanisms" chapter, you will learn how the scheme is derived from the characteristic theory of [hyperbolic systems](@entry_id:260647) and the homogeneity property of the Euler equations. The "Applications and Interdisciplinary Connections" chapter will demonstrate its use in multi-dimensional CFD solvers, boundary condition implementation, and even in fields outside of fluid dynamics. Finally, the "Hands-On Practices" section provides concrete problems to solidify your understanding of the core calculations. By the end, you will have a deep appreciation for both the power and the limitations of Steger–Warming splitting.

## Principles and Mechanisms

This chapter delves into the theoretical foundations and operational mechanisms of the Steger–Warming [flux splitting](@entry_id:637102) scheme. Building upon the introductory concepts of [hyperbolic conservation laws](@entry_id:147752), we will dissect the method from its basis in characteristic theory to its application in solving the compressible Euler equations. We will explore how the scheme leverages the eigenstructure of the governing equations to ensure physically consistent upwinding, and we will also examine its inherent limitations and the standard techniques developed to overcome them.

### The Foundation: Characteristic Decomposition of Hyperbolic Systems

A system of one-dimensional [hyperbolic conservation laws](@entry_id:147752) is expressed in the general form:
$$
\frac{\partial U}{\partial t} + \frac{\partial F(U)}{\partial x} = 0
$$
where $U$ is the vector of conserved state variables and $F(U)$ is the corresponding flux vector. Using the chain rule, this can be written in a quasi-[linear form](@entry_id:751308):
$$
\frac{\partial U}{\partial t} + A(U)\frac{\partial U}{\partial x} = 0
$$
Here, $A(U) = \frac{\partial F}{\partial U}$ is the **flux Jacobian** matrix. The term "hyperbolic" signifies a crucial property of this matrix: for any physically relevant state $U$, $A(U)$ is diagonalizable and possesses a full set of real eigenvalues. These eigenvalues, denoted $\lambda_i$, are the **[characteristic speeds](@entry_id:165394)** of the system, representing the speeds at which information propagates through the medium.

The [diagonalizability](@entry_id:748379) of $A(U)$ allows for its **[spectral decomposition](@entry_id:148809)**:
$$
A = R \Lambda R^{-1}
$$
The components of this decomposition are fundamental to understanding the physics of wave propagation:
-   $\Lambda$ is a diagonal matrix containing the eigenvalues ([characteristic speeds](@entry_id:165394)) of $A$: $\Lambda = \text{diag}(\lambda_1, \lambda_2, \dots, \lambda_m)$.
-   $R$ is the matrix whose columns are the **right eigenvectors** ($r_i$) of $A$. Each eigenvector represents a characteristic "mode" or the shape of a wave that propagates at the corresponding speed $\lambda_i$.
-   $R^{-1}$ is the matrix of **left eigenvectors** (as rows). This matrix acts as a [projection operator](@entry_id:143175). When applied to the vector of [conserved variables](@entry_id:747720) $U$, it transforms the physical variables into a set of **[characteristic variables](@entry_id:747282)**, $W = R^{-1}U$.

The power of this transformation lies in its ability to decouple the complex, coupled system of partial differential equations. By substituting $U = RW$ into the quasi-linear equation and pre-multiplying by $R^{-1}$, we obtain:
$$
R^{-1}\left(\frac{\partial (RW)}{\partial t} + A \frac{\partial (RW)}{\partial x}\right) = 0
$$
Assuming the eigenvectors are locally constant (which is true for a linear system or can be assumed in a [local linearization](@entry_id:169489)), this simplifies to:
$$
\frac{\partial W}{\partial t} + (R^{-1} A R) \frac{\partial W}{\partial x} = 0 \implies \frac{\partial W}{\partial t} + \Lambda \frac{\partial W}{\partial x} = 0
$$
This is a system of $m$ uncoupled scalar advection equations for the [characteristic variables](@entry_id:747282) $w_i$:
$$
\frac{\partial w_i}{\partial t} + \lambda_i \frac{\partial w_i}{\partial x} = 0
$$
The solution to each of these is simply the advection of its initial profile: $w_i(x,t) = w_i(x-\lambda_i t, 0)$. The full solution in physical variables, $U(x,t)$, is then reconstructed by summing these advected characteristic fields, weighted by their corresponding eigenvectors:
$$
U(x,t) = RW(x,t) = \sum_{i=1}^m r_i w_i(x,t) = \sum_{i=1}^m r_i w_i(x-\lambda_i t, 0)
$$
This reveals the underlying physics: any state $U$ can be seen as a superposition of characteristic waves, each traveling independently at its own speed $\lambda_i$ without changing its shape.

To make this concrete, consider a simple linear system with a constant [coefficient matrix](@entry_id:151473), a useful analogue for understanding more complex systems . Let $U_t + A U_x = 0$ with the matrix $A = \begin{pmatrix} 2  1 \\ 0  -1 \end{pmatrix}$. The eigenvalues are found to be $\lambda_1 = 2$ and $\lambda_2 = -1$. The corresponding right eigenvectors are $r_1 = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$ and $r_2 = \begin{pmatrix} 1 \\ -3 \end{pmatrix}$. This gives the decomposition matrices:
$$
\Lambda = \begin{pmatrix} 2  0 \\ 0  -1 \end{pmatrix}, \quad R = \begin{pmatrix} 1  1 \\ 0  -3 \end{pmatrix}, \quad R^{-1} = \begin{pmatrix} 1  1/3 \\ 0  -1/3 \end{pmatrix}
$$
The solution consists of two waves: one associated with $r_1$ moving to the right at speed $2$, and another associated with $r_2$ moving to the left at speed $1$. The initial condition $U(x,0)$ determines the initial profiles of these two waves, $w_1(x,0)$ and $w_2(x,0)$, via the transformation $W(x,0) = R^{-1}U(x,0)$. The complete solution is then a superposition of these two waves advecting in opposite directions.

### The Steger–Warming Flux Splitting Principle

In a finite volume method, the primary task is to define a **numerical flux**, $F_{i+1/2}$, at the interface between two cells, that approximates the true flux. An **upwind** scheme accomplishes this by using information from the "upwind" side of the interface—the direction from which the flow is coming. This respects the directional nature of [information propagation](@entry_id:1126500) in [hyperbolic systems](@entry_id:260647).

Steger–Warming splitting is a specific type of upwind scheme known as **Flux Vector Splitting (FVS)**. The core idea of FVS is to split the physical [flux vector](@entry_id:273577) $F(U)$ itself into two parts:
-   $F^+(U)$, which contains the contributions from waves traveling to the right (positive [characteristic speeds](@entry_id:165394)).
-   $F^-(U)$, which contains the contributions from waves traveling to the left (negative [characteristic speeds](@entry_id:165394)).
Such that $F(U) = F^+(U) + F^-(U)$.

The [numerical flux](@entry_id:145174) at an interface between a left state $U_L$ and a right state $U_R$ is then constructed by taking the right-going part from the left state and the left-going part from the right state :
$$
F_{i+1/2} = F^+(U_L) + F^-(U_R)
$$
This construction intuitively enforces upwinding: any information that propagates to the right across the interface must originate from the left, and vice-versa.

The key property that allows for a direct splitting of the [flux vector](@entry_id:273577) for the Euler equations is its **homogeneity of degree one**. For a [perfect gas](@entry_id:1129510), the Euler flux vector satisfies $F(\alpha U) = \alpha F(U)$ for any scalar $\alpha > 0$. By Euler's homogeneous function theorem, this implies a direct linear relationship between the flux and the state at any point $U$  :
$$
F(U) = A(U)U
$$
This elegant property allows us to apply the [characteristic decomposition](@entry_id:747276) directly to the flux. By substituting $A = R \Lambda R^{-1}$, we get:
$$
F(U) = (R \Lambda R^{-1}) U
$$
The splitting is now performed on the diagonal matrix of eigenvalues, $\Lambda$. We define $\Lambda^+$ to contain the non-negative eigenvalues and $\Lambda^-$ to contain the non-positive (in this case, strictly negative) eigenvalues. This is formally done using the matrix absolute value $|\Lambda| = \text{diag}(|\lambda_i|)$:
$$
\Lambda^+ = \frac{1}{2}(\Lambda + |\Lambda|) \quad \text{and} \quad \Lambda^- = \frac{1}{2}(\Lambda - |\Lambda|)
$$
This leads directly to the definitions of the Steger–Warming split fluxes:
$$
F^+(U) = R \Lambda^+ R^{-1} U \quad \text{and} \quad F^-(U) = R \Lambda^- R^{-1} U
$$
We can also define the corresponding split Jacobian matrices, $A^\pm = R \Lambda^\pm R^{-1}$, such that $F^\pm(U) = A^\pm(U)U$. By construction, the eigenvalues of $A^+$ are all non-negative, and the eigenvalues of $A^-$ are all non-positive, ensuring the desired directional properties.

For the simple linear system discussed previously , this procedure gives:
$$
\Lambda^+ = \begin{pmatrix} 2  0 \\ 0  0 \end{pmatrix}, \quad \Lambda^- = \begin{pmatrix} 0  0 \\ 0  -1 \end{pmatrix}
$$
And the split matrices become:
$$
A^+ = R \Lambda^+ R^{-1} = \begin{pmatrix} 2  2/3 \\ 0  0 \end{pmatrix}, \quad A^- = R \Lambda^- R^{-1} = \begin{pmatrix} 0  1/3 \\ 0  -1 \end{pmatrix}
$$
Note that $A^+ + A^- = A$, ensuring consistency.

### Application to the Euler Equations

To apply the Steger–Warming method to the compressible Euler equations, the first step is to determine the eigenvalues of the flux Jacobian $A(U)$. A detailed derivation, often performed by transforming the equations into primitive variables $(\rho, u, p)$, shows that the three [characteristic speeds](@entry_id:165394) are :
$$
\lambda_1 = u - a, \quad \lambda_2 = u, \quad \lambda_3 = u + a
$$
where $a = \sqrt{\gamma p / \rho}$ is the local speed of sound. These correspond physically to two **acoustic waves** propagating at speeds $u \pm a$ relative to the fluid, and one **entropy/contact wave** advecting with the fluid speed $u$.

The power and physical intuition of the Steger–Warming splitting become exceptionally clear in supersonic flow . Consider a rightward-moving [supersonic flow](@entry_id:262511), where the fluid velocity $u$ is greater than the speed of sound $a$ (i.e., Mach number $M = u/a > 1$). In this case, all three eigenvalues are positive:
-   $\lambda_1 = u - a > 0$
-   $\lambda_2 = u > 0$
-   $\lambda_3 = u + a > 0$

Since all eigenvalues are positive, the eigenvalue matrices for any state $U$ in this regime simplify dramatically:
$$
\Lambda^+(U) = \Lambda(U) \quad \text{and} \quad \Lambda^-(U) = 0
$$
Consequently, the split fluxes become:
$$
F^+(U) = R \Lambda R^{-1} U = A U = F(U) \quad \text{and} \quad F^-(U) = R(0)R^{-1}U = 0
$$
Now, consider the [numerical flux](@entry_id:145174) $F_{i+1/2} = F^+(U_L) + F^-(U_R)$ at an interface where both the left and right states are supersonic. The flux becomes:
$$
F_{i+1/2} = F(U_L) + 0 = F(U_L)
$$
This result is physically perfect. In a [supersonic flow](@entry_id:262511), information can only travel downstream. The state at any point is determined exclusively by the upstream conditions. The Steger–Warming flux automatically captures this causality by making the interface flux dependent only on the upstream state $U_L$. Any information from the downstream state $U_R$ is completely disregarded, eliminating any possibility of non-physical "backflow" of information.

### Practical Challenges and Refinements

While elegant and physically intuitive in cases like supersonic flow, the Steger–Warming scheme suffers from significant drawbacks in other regimes, particularly near sonic transitions and for certain wave types. A robust implementation requires addressing these issues.

#### Continuity, Sonic Points, and the Entropy Fix

A critical issue arises when an eigenvalue passes through zero. This occurs at **sonic points**, where $u=a$ (so $\lambda_1=0$) or $u=-a$ (so $\lambda_3=0$), and at **[stagnation points](@entry_id:276398)**, where $u=0$ (so $\lambda_2=0$). The [splitting functions](@entry_id:161308), which depend on $|\lambda_i|$ or $\max(0, \lambda_i)$, are continuous but crucially are **not differentiable** at $\lambda_i=0$ .

This lack of smoothness has a severe numerical consequence. The amount of numerical dissipation (or viscosity) introduced by an [upwind scheme](@entry_id:137305) for a given characteristic field is proportional to the absolute value of its eigenvalue, $|\lambda_i|$. In the unmodified Steger–Warming scheme, this dissipation vanishes for the characteristic field whose speed is zero. This can allow the numerical solution to form stationary, discontinuous solutions to [rarefaction waves](@entry_id:168428). Such solutions, known as **expansion shocks**, violate the second law of thermodynamics (the Lax [entropy condition](@entry_id:166346)) and are non-physical  .

The solution is to introduce an **[entropy fix](@entry_id:749021)**. The goal is to modify the splitting to ensure that the numerical dissipation never vanishes completely. This is typically achieved by replacing the [absolute value function](@entry_id:160606) $|\lambda_i|$ with a smoothed approximation, denoted $|\lambda_i|_\epsilon$, that is strictly positive. A widely used example is the Harten-Hyman [entropy fix](@entry_id:749021) :
$$
|\lambda_i|_\epsilon = \begin{cases} \frac{\lambda_i^2 + \epsilon^2}{2\epsilon},  & \text{if } |\lambda_i|  \epsilon \\ |\lambda_i|,  \text{if } |\lambda_i| \ge \epsilon \end{cases}
$$
where $\epsilon$ is a small positive parameter, often chosen based on the local wave speeds. This function is continuously differentiable and satisfies $|\lambda_i|_\epsilon(0) = \epsilon/2 > 0$. By using this modified function to construct the matrix $|\Lambda|_\epsilon$, and subsequently the split fluxes $F_\epsilon^\pm$, one ensures a baseline level of dissipation is always present, preventing the formation of expansion shocks and restoring the correct physical behavior in transonic rarefactions.

#### Smearing of Contact Discontinuities

The second major weakness of the Steger–Warming scheme is its excessive numerical diffusion of **contact discontinuities** . A contact discontinuity is a jump in density (and temperature) across which pressure and velocity are constant. It is associated with the linearly degenerate characteristic field, $\lambda_2 = u$. An exact solution would advect this discontinuity as a perfectly sharp front.

However, the Steger–Warming scheme introduces dissipation proportional to $|\lambda_2| = |u|$. For a stationary or slow-moving contact, this dissipation might be small, but for a contact moving at a significant velocity, the dissipation is substantial. This causes the sharp jump in density to be smeared out, or diffused, over several grid cells, leading to a significant loss of accuracy.

To mitigate this, several strategies have been developed:
1.  **Contact Sensor:** One approach is to design a "sensor" that detects the presence of a contact wave, typically by checking for a large jump in density accompanied by a very small jump in pressure. The dissipation for the $\lambda_2$ field can then be selectively reduced or eliminated when the sensor is active .
2.  **Hybrid Schemes:** A more sophisticated approach is to blend the Steger–Warming flux with a flux from a different numerical scheme that is known to resolve contacts well, such as the HLLC (Harten-Lax-van Leer-Contact) or AUSM (Advection Upstream Splitting Method) schemes. The blending is controlled by a sensor, such that the robust but dissipative Steger–Warming flux is used in regions with strong shocks, while the more accurate contact-resolving flux is used in regions dominated by contact waves .

### Context: Flux Vector vs. Flux Difference Splitting

Finally, it is useful to place Steger–Warming splitting in the broader context of [upwind methods](@entry_id:756376) . It belongs to the family of **Flux Vector Splitting (FVS)** schemes. A separate family of methods is known as **Flux Difference Splitting (FDS)**, with the most famous example being Roe's approximate Riemann solver.

For linear, constant-coefficient systems, the two approaches are identical. For nonlinear systems like the Euler equations, they diverge. FDS schemes linearize the problem *across* the interface by defining a special "Roe-averaged" Jacobian, $\tilde{A}$, that exactly satisfies the [jump condition](@entry_id:176163) $F(U_R) - F(U_L) = \tilde{A}(U_R - U_L)$. The upwind splitting is then performed on this single average matrix.

In contrast, Steger–Warming FVS, by exploiting the homogeneity property, avoids the need to construct a special averaged matrix. It performs two separate linearizations, one at the left state $U_L$ and one at the right state $U_R$, and combines the results. This makes the scheme conceptually simpler and often easier to extend to multiple dimensions and more complex equations of state. The trade-off is that FVS schemes are typically more dissipative than FDS schemes, particularly at [contact discontinuities](@entry_id:747781) and shear waves. The choice between these families of schemes depends on the specific requirements of the application, balancing the need for robustness against the desire for high accuracy.