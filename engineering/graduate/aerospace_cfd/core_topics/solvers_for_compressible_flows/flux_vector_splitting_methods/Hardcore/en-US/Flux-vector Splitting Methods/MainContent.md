## Introduction
The accurate numerical simulation of compressible fluid flows, governed by hyperbolic systems of conservation laws like the Euler equations, is a cornerstone of modern aerospace engineering. A fundamental challenge in this domain is creating numerical methods that respect the physical nature of wave propagation, where information travels along specific paths called characteristics. Standard central-difference schemes often fail this test, producing non-physical oscillations and failing to capture sharp discontinuities like shock waves. This knowledge gap necessitates the use of upwind methods, which are explicitly designed to honor the directional flow of information.

This article provides a detailed exploration of **Flux-Vector Splitting (FVS)**, a prominent and powerful family of upwind schemes. By delving into the theoretical underpinnings and practical applications of FVS, you will gain a robust understanding of how to build physically consistent and stable numerical solvers. The journey is structured across three chapters:

*   **Principles and Mechanisms** will lay the theoretical groundwork, starting from the concept of characteristic-based upwinding and proceeding to the detailed mechanics of the pioneering Steger-Warming and the smoother Van Leer splitting schemes.
*   **Applications and Interdisciplinary Connections** will showcase the versatility of FVS in solving classic gas dynamics problems, implementing robust boundary conditions, and its connection to advanced topics like kinetic theory, combustion, and all-speed algorithms.
*   **Hands-On Practices** will offer a series of guided exercises designed to solidify your understanding of the core concepts, from analyzing characteristic speeds to deriving fixes for common numerical issues.

We begin by examining the foundational principles that make flux splitting a cornerstone of modern CFD.

## Principles and Mechanisms

The numerical approximation of hyperbolic systems of conservation laws, such as the Euler equations governing inviscid fluid flow, presents a unique set of challenges rooted in the physics of wave propagation. Unlike parabolic or elliptic systems where information diffuses in all directions, hyperbolic systems convey information along specific paths in spacetime known as **characteristics**. A robust numerical method must respect this directional nature of information flow. This chapter delineates the foundational principles of characteristic-based upwinding and explores the mechanisms of **Flux-Vector Splitting (FVS)**, a prominent class of methods designed to embed this physical principle into the discretization of the governing equations.

### The Foundational Principle: Characteristic-Based Upwinding

A one-dimensional system of $m$ conservation laws can be expressed in its quasilinear form as:
$$
\frac{\partial U}{\partial t} + A(U)\frac{\partial U}{\partial x} = 0
$$
where $U(x,t) \in \mathbb{R}^m$ is the vector of conserved state variables, and $A(U) = \frac{\partial F(U)}{\partial U}$ is the **flux Jacobian** matrix corresponding to the physical flux vector $F(U)$. The system is termed **hyperbolic** if, for any physically admissible state $U$, the matrix $A(U)$ is diagonalizable and possesses a full set of $m$ real eigenvalues, denoted $\lambda_k(U)$ for $k = 1, \dots, m$.

The profound insight of characteristic theory is that such a system can be locally decoupled. By transforming the state variables $U$ into a set of **characteristic variables** $W$ using the eigenvectors of $A(U)$, the coupled system of $m$ equations transforms into a set of $m$ independent, scalar advection equations [@problem_id:3460009]:
$$
\frac{\partial w_k}{\partial t} + \lambda_k \frac{\partial w_k}{\partial x} = 0, \quad k=1, \dots, m
$$
Each equation describes a simple wave, where the quantity $w_k$ is transported without change at a constant speed, $\lambda_k$, along the characteristic lines defined by $x - \lambda_k t = \text{constant}$.

This mathematical decoupling reveals a fundamental physical principle: the total solution $U$ can be viewed as a superposition of $m$ distinct wave families, each propagating with its own speed and direction. The direction of propagation for each characteristic field is determined entirely by the **sign of its corresponding eigenvalue**:
- If $\lambda_k > 0$, the $k$-th wave propagates to the right (in the direction of increasing $x$).
- If $\lambda_k  0$, the $k$-th wave propagates to the left (in the direction of decreasing $x$).

This principle is the bedrock of **upwind methods**. In a finite volume discretization, the numerical flux $F_{i+1/2}$ at the interface between cell $i$ (with state $U_L$) and cell $i+1$ (with state $U_R$) must be computed in a way that respects the origin of information. The upwinding principle dictates that for any wave component arriving at the interface, its contribution to the flux must be determined using data from the cell it came *from*—its upwind cell. Consequently, right-moving wave contributions ($\lambda_k > 0$) must be based on the left state $U_L$, while left-moving wave contributions ($\lambda_k  0$) must be based on the right state $U_R$.

For the one-dimensional Euler equations of gas dynamics, the system is hyperbolic with three eigenvalues: $\lambda_1 = u - a$, $\lambda_2 = u$, and $\lambda_3 = u + a$, where $u$ is the fluid velocity and $a$ is the speed of sound. These correspond to a left-propagating acoustic wave, a convective wave (transporting entropy and contact discontinuities), and a right-propagating acoustic wave, respectively. An upwind scheme must therefore disentangle these three wave contributions and source them from the correct direction based on the signs of $u-a$, $u$, and $u+a$ [@problem_id:3960897].

### Flux-Vector Splitting: A Mechanism for Upwinding

Flux-vector splitting (FVS) provides a direct and intuitive way to implement the upwinding principle. The core idea is to decompose the physical flux vector $F(U)$ itself into two components: a forward (or positive) flux $F^+(U)$ and a backward (or negative) flux $F^-(U)$, such that $F(U) = F^+(U) + F^-(U)$. This split is designed such that the Jacobian of $F^+$, denoted $A^+ = \partial F^+ / \partial U$, has only non-negative eigenvalues, while the Jacobian of $F^-$, denoted $A^- = \partial F^- / \partial U$, has only non-positive eigenvalues.

With such a split in hand, an upwind numerical flux at an interface between a left state $U_L$ and a right state $U_R$ is naturally constructed as:
$$
F_{i+1/2} = F^+(U_L) + F^-(U_R)
$$
This elegant formula perfectly embodies the upwind principle: the right-going part of the flux ($F^+$) is evaluated using the state from the left ($U_L$), and the left-going part ($F^-$) is evaluated using the state from the right ($U_R$).

It is pedagogically useful to contrast FVS with the other major family of upwind schemes, **Flux-Difference Splitting (FDS)** [@problem_id:3960863]. While FVS splits the flux vector at a single point in state space (e.g., evaluating $F^+(U_L)$ and $F^-(U_R)$ separately), FDS methods approximate the solution to the Riemann problem defined by the two states $(U_L, U_R)$ at the interface. FDS analyzes the flux *difference* across the interface, $F(U_R) - F(U_L)$, using a local linearization (e.g., a Roe matrix) that is a function of both states. This makes FDS methods inherently "aware" of the wave structure connecting the two states, an advantage that will be discussed later. This chapter, however, will focus on the principles and mechanisms of FVS.

### The Steger-Warming Splitting

The pioneering FVS scheme was developed by Joseph Steger and Robert Warming. It provides a systematic method for constructing the split fluxes $F^+$ and $F^-$ based on the eigensystem of the flux Jacobian $A(U)$.

For a linear system with flux $F(U) = AU$, where $A$ is a constant, diagonalizable matrix with eigendecomposition $A = R \Lambda R^{-1}$, the splitting is defined at the level of the Jacobian. The eigenvalue matrix $\Lambda$ is split into its positive and negative parts, $\Lambda^+$ and $\Lambda^-$, whose diagonal entries are $\max(\lambda_k, 0)$ and $\min(\lambda_k, 0)$, respectively. An equivalent and powerful definition is [@problem_id:3960878]:
$$
\Lambda^{\pm} = \frac{1}{2}(\Lambda \pm |\Lambda|)
$$
where $|\Lambda|$ is the diagonal matrix of absolute eigenvalues, $|\lambda_k|$. The split Jacobians are then constructed by transforming back to the physical basis:
$$
A^{\pm} = R \Lambda^{\pm} R^{-1}
$$
These matrices possess several important properties. By construction, $A = A^+ + A^-$, ensuring the splitting is consistent. Furthermore, the matrices are "orthogonal" in the sense that their product is zero: $A^+ A^- = A^- A^+ = 0$, because $\Lambda^+ \Lambda^-$ is the zero matrix. The split fluxes are simply $F^{\pm}(U) = A^{\pm} U$. The resulting numerical flux $F_{i+1/2} = A^+U_L + A^-U_R$ is both **conservative** (as it depends only on adjacent states) and **consistent** with the physical flux, meaning $F(U,U) = AU = F(U)$ [@problem_id:3960878].

For nonlinear systems like the Euler equations, Steger and Warming leveraged the **homogeneity property** of the flux vector for an ideal gas, which states that $F(U) = A(U)U$. This allows a direct extension of the linear splitting:
$$
F^{\pm}(U) = A^{\pm}(U) U
$$
where $A^{\pm}(U)$ are derived from the local eigenvalues of $A(U)$ at each point. This scheme robustly applies upwinding to each characteristic field [@problem_id:3828166].

A concrete application of this splitting is the apportionment of the pressure term in the momentum flux of the Euler equations [@problem_id:3960885]. The total momentum flux is $F_2 = \rho u^2 + p$. The Steger-Warming scheme implicitly splits the pressure term $p$ into contributions $p^+$ and $p^-$. A detailed derivation shows that these split pressures can be expressed in a compact, universal form valid for all Mach numbers:
$$
p^+ = \frac{p}{4a} (2a + |u+a| - |u-a|)
$$
$$
p^- = \frac{p}{4a} (2a - |u+a| + |u-a|)
$$
These formulae demonstrate how the split is directly controlled by the local velocity $u$ and sound speed $a$, which together determine the signs of the acoustic eigenvalues.

### The Van Leer Splitting: A Quest for Smoothness

While groundbreaking, the Steger-Warming splitting has notable deficiencies. Its reliance on the absolute value function, which has a discontinuous derivative at zero, means the split fluxes $F^{\pm}$ are not continuously differentiable ($C^1$) when an eigenvalue passes through zero. This occurs at **sonic points** and can introduce numerical artifacts, such as oscillations or a loss of convergence, particularly in transonic flows.

To address this, Bram van Leer developed an alternative FVS scheme with the specific design goal of ensuring the split fluxes are smooth ($C^1$) everywhere, including at sonic points [@problem_id:3960877]. Instead of splitting the Jacobian, van Leer constructed the split fluxes directly based on the local Mach number, $M = u/a$. For the 1D Euler equations, this involves defining **split Mach functions** $M^{\pm}(M)$ and **split pressure functions** $P^{\pm}(M)$ using carefully chosen polynomials.

The widely used van Leer splitting functions are:
- For the mass flux (related to Mach number):
  - If $|M| \ge 1$: $M^+ = \frac{1}{2}(M+|M|)$, $M^- = \frac{1}{2}(M-|M|)$
  - If $|M|  1$: $M^+ = \frac{1}{4}(M+1)^2$, $M^- = -\frac{1}{4}(M-1)^2$
- For the pressure flux:
  - If $|M| \ge 1$: $P^+ = \frac{1}{2}(1+\text{sign}(M))$, $P^- = \frac{1}{2}(1-\text{sign}(M))$
  - If $|M|  1$: The original paper provides a linear split, but a common choice that also ensures $C^1$ continuity of the full flux vector is $P^{\pm}(M) = \frac{1}{2}(1 \pm M)$. However, the most famous formulation leading to a smooth Jacobian uses higher-order polynomials for the pressure contribution as well. The split Mach functions above are the iconic part of the scheme.

The subsonic polynomials are specifically designed to smoothly match both the value and the first derivative of the supersonic functions at $|M|=1$. This $C^1$ continuity ensures that the numerical flux Jacobian is also continuous, which is crucial for the stability and robustness of numerical solvers, especially implicit methods that rely on the Jacobian for matrix inversion [@problem_id:3960877].

### Pathologies and Advanced Concepts

Despite their successes, early FVS methods exhibit several known pathologies that have motivated the development of more advanced schemes.

#### The Entropy Condition and Expansion Shocks

Physical solutions to the Euler equations must satisfy the Second Law of Thermodynamics, which for inviscid flow manifests as the **entropy condition**: entropy cannot decrease along fluid particle paths. For a numerical scheme, this is formalized as a **discrete entropy inequality** [@problem_id:3960833]. A numerical scheme's stability is provided by its intrinsic **numerical dissipation**. This dissipation is also what allows the scheme to produce entropy and capture shock waves correctly. A problem arises when the numerical dissipation vanishes where it shouldn't. In schemes like Steger-Warming (and many FDS schemes like Roe's), the dissipation for each characteristic field is proportional to $|\lambda_k|$. In a transonic expansion fan, a characteristic speed $\lambda_k$ smoothly passes through zero. At this sonic point, the dissipation vanishes, allowing the formation of a non-physical, entropy-violating stationary discontinuity known as an **expansion shock**. An **entropy fix** is a modification that adds a small amount of dissipation near sonic points to prevent $|\lambda_k|$ from becoming zero, thereby ensuring the correct physical behavior. Van Leer's scheme, by virtue of its smooth splitting, has a more graceful behavior at sonic points and is less prone to producing such strong non-physical solutions.

#### Inaccuracy at Low Mach Numbers

A particularly severe failure of the Steger-Warming scheme occurs in the nearly incompressible regime ($M \to 0$). A **modified equation analysis** reveals that the artificial viscosity introduced by the scheme scales inversely with the Mach number [@problem_id:3960868]. The artificial viscosity coefficient for the fast-moving acoustic waves behaves as:
$$
\nu_{\text{acoustic}} \sim \frac{\Delta x}{M}
$$
As $M \to 0$, this numerical viscosity becomes enormous, overwhelming the physical viscosity (if present) and the convective dynamics. This excessive diffusion on the acoustic waves contaminates the entire solution, destroying the accuracy for the physically important convective phenomena. This failure motivated schemes designed specifically for all-speed flows.

#### Dissipation of Contact Discontinuities

Another weakness of FVS is its handling of **linearly degenerate fields**, such as the contact wave ($\lambda=u$) in the Euler equations. These waves, which include contact discontinuities and shear layers, should propagate without dissipation. However, FVS methods are generally "blind" to the detailed wave structure connecting two states. They apply dissipation based only on the local eigenvalues. For a contact wave with $u \approx 0$, the scheme will split the flux into both $F^+$ and $F^-$ components, effectively upwinding from both directions and introducing significant numerical diffusion that smears the discontinuity. In contrast, FDS schemes like Roe's method can, under ideal conditions, recognize a contact wave as a single eigenvector and resolve it perfectly with no dissipation [@problem_id:3960863].

#### A Look Ahead: The AUSM Family

The limitations of classical FVS led to the development of hybrid schemes like the **Advection Upstream Splitting Method (AUSM)**. AUSM retains the simplicity of FVS but incorporates physical insight from FDS [@problem_id:4003799]. Its key innovation is to split the numerical flux into a **convective part** and a **pressure part**. The convective flux is upwinded based on the fluid velocity $u$, while the pressure flux is upwinded based on the acoustic speeds. This separation allows for independent control of dissipation for convective and acoustic phenomena. It can dramatically reduce the artificial diffusion on contact waves and, by careful design of the pressure splitting, can also cure the low-Mach number inaccuracies that plague the Steger-Warming scheme, preventing issues like pressure-velocity decoupling on collocated grids [@problem_id:4003799]. AUSM and its descendants represent a significant step in the evolution of flux splitting methods, demonstrating the ongoing effort to create numerical schemes that are robust, accurate, and physically faithful across a wide range of flow regimes.