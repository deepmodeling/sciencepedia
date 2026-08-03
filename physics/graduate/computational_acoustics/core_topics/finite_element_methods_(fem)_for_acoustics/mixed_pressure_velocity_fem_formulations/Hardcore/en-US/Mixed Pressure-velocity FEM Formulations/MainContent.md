## Introduction
The accurate simulation of wave propagation is a fundamental task in computational acoustics, with applications ranging from architectural design to underwater sonar. While the second-order scalar wave equation is widely used, a more fundamental approach involves directly solving for both acoustic pressure and particle velocity. This leads to a first-order system that, when discretized using a mixed finite element method, provides significant advantages in physical fidelity, particularly in enforcing boundary conditions and ensuring conservation properties. This article addresses the knowledge gap between standard FEM and this advanced formulation, providing a comprehensive guide to its theory and application.

The following sections are structured to build a robust understanding of the mixed pressure-velocity method. The first section, "Principles and Mechanisms," lays the mathematical groundwork, deriving the governing equations and introducing the critical concepts of weak formulations, natural function spaces like $H(\mathrm{div})$, and the LBB stability condition. The second section, "Applications and Interdisciplinary Connections," demonstrates the method's power in practice, exploring advanced modeling techniques like Perfectly Matched Layers (PMLs) and revealing its deep connections to other fields such as computational fluid dynamics and solid mechanics. Finally, "Hands-On Practices" offers exercises designed to solidify theoretical knowledge through practical problem-solving. We begin by examining the core principles that define this powerful numerical framework.

## Principles and Mechanisms

The accurate numerical simulation of acoustic phenomena is a cornerstone of modern engineering and physics. While the scalar wave equation provides a powerful description for many scenarios, a more fundamental approach involves resolving both the acoustic pressure and the particle velocity fields. This leads to a first-order system of equations, which, when discretized using a mixed finite element method (FEM), offers distinct advantages, particularly in handling boundary conditions and ensuring local conservation properties. This chapter elucidates the core principles and mathematical mechanisms that underpin the mixed pressure-velocity formulation.

### The First-Order System of Linear Acoustics

The propagation of small-amplitude sound waves in an inviscid, compressible fluid is governed by the fundamental principles of mass and momentum conservation. When these principles are linearized around a quiescent ambient state (characterized by constant density $\rho_0$ and constant sound speed $c$), they yield a coupled system of first-order partial differential equations for the acoustic pressure perturbation $p(\mathbf{x}, t)$ and the particle velocity $\mathbf{v}(\mathbf{x}, t)$.

The first equation, derived from Newton's second law, represents the **conservation of momentum**. It states that the inertial force per unit volume on a fluid parcel is balanced by forces arising from the pressure gradient and any external body forces $\mathbf{f}(\mathbf{x}, t)$. The linearized momentum equation is:
$$ \rho_0 \frac{\partial \mathbf{v}}{\partial t} + \nabla p = \mathbf{f} $$
Here, $\rho_0 \partial_t \mathbf{v}$ is the inertial term, and $\nabla p$ represents the force density exerted by the pressure field. Each term in this equation has units of force per unit volume (e.g., $\mathrm{N}/\mathrm{m}^3$).

The second equation arises from the **conservation of mass** (the continuity equation), combined with a thermodynamic equation of state. For isentropic processes, the pressure and density perturbations are linearly related by $p = c^2 \rho'$. Combining this with the linearized continuity equation yields:
$$ \frac{1}{\rho_0 c^2} \frac{\partial p}{\partial t} + \nabla \cdot \mathbf{v} = s' $$
Here, $\nabla \cdot \mathbf{v}$ is the divergence of the velocity field, representing the rate of volumetric expansion per unit volume. The term $s'$ represents a source of mass injection. It is common to write this equation by multiplying through by the bulk modulus $K = \rho_0 c^2$, resulting in a form where the source term $s = K s'$ has units of pressure rate (e.g., $\mathrm{Pa}/\mathrm{s}$) [@problem_id:4128945]:
$$ \frac{1}{K} \frac{\partial p}{\partial t} + \nabla \cdot \mathbf{v} = s' \quad \text{or equivalently} \quad \frac{\partial p}{\partial t} + K \nabla \cdot \mathbf{v} = s $$
This coupled system of equations constitutes the strong form of first-order linear acoustics. A key property of this system is its description of acoustic energy. The acoustic energy density, $e = \frac{1}{2}\rho_0 |\mathbf{v}|^2 + \frac{1}{2K}p^2$, which is the sum of kinetic and potential energy densities, obeys a conservation law involving the acoustic energy flux (or intensity) $\mathbf{J} = p\mathbf{v}$.

### The Mixed Weak Formulation and Natural Function Spaces

To solve this system using the finite element method, we first reformulate it in a "weak" or variational form. This is achieved by multiplying the equations by suitable test functions and integrating over the domain $\Omega$. This process has the profound consequence of relaxing the smoothness requirements on the solution variables, which in turn dictates the choice of function spaces.

Let us consider the time-harmonic case, where fields vary as $e^{\mathrm{i}\omega t}$, so $\partial_t$ is replaced by $\mathrm{i}\omega$. The system becomes:
$$ \mathrm{i}\omega \rho_0 \mathbf{v} + \nabla p = \mathbf{0} $$
$$ \mathrm{i}\omega K^{-1} p + \nabla \cdot \mathbf{v} = 0 $$
We seek a solution pair $(p, \mathbf{v})$ in some function spaces $(Q, V)$. Let's test the momentum equation with a vector test function $\mathbf{w} \in V$ and the continuity equation with a scalar test function $q \in Q$:
$$ (\mathrm{i}\omega \rho_0 \mathbf{v}, \mathbf{w})_{\Omega} + (\nabla p, \mathbf{w})_{\Omega} = 0 $$
$$ (\mathrm{i}\omega K^{-1} p, q)_{\Omega} + (\nabla \cdot \mathbf{v}, q)_{\Omega} = 0 $$
Here, $(\cdot, \cdot)_{\Omega}$ denotes the standard $L^2(\Omega)$ inner product. The term $(\nabla p, \mathbf{w})_{\Omega}$ presents a challenge: if we want to seek a pressure solution $p$ that is not necessarily differentiable in the classical sense, this term is not well-defined. The core idea of the mixed formulation is to use integration by parts (via Green's identity) to transfer the gradient operator from the pressure $p$ to the test function $\mathbf{w}$:
$$ (\nabla p, \mathbf{w})_{\Omega} = - (p, \nabla \cdot \mathbf{w})_{\Omega} + \langle p, \mathbf{w} \cdot \mathbf{n} \rangle_{\partial\Omega} $$
where $\mathbf{n}$ is the outward unit normal on the boundary $\partial\Omega$, and $\langle \cdot, \cdot \rangle_{\partial\Omega}$ is a boundary pairing. The weak form of the momentum equation thus becomes:
$$ (\mathrm{i}\omega \rho_0 \mathbf{v}, \mathbf{w})_{\Omega} - (p, \nabla \cdot \mathbf{w})_{\Omega} + \langle p, \mathbf{w} \cdot \mathbf{n} \rangle_{\partial\Omega} = 0 $$

This manipulation elegantly reveals the "natural" function spaces for the mixed formulation [@problem_id:4128946]. For the term $(p, \nabla \cdot \mathbf{w})_{\Omega}$ to be well-defined for a pressure $p$ in the most general space of square-integrable functions, $L^2(\Omega)$, we must require that the divergence of the velocity test function, $\nabla \cdot \mathbf{w}$, is also a square-integrable function. This leads directly to the definition of the Sobolev space **$H(\mathrm{div};\Omega)$** for the velocity field:
$$ H(\mathrm{div};\Omega) = \{ \mathbf{v} \in (L^2(\Omega))^d : \nabla \cdot \mathbf{v} \in L^2(\Omega) \} $$
This space contains all vector fields that, along with their divergence, are square-integrable. Correspondingly, the natural space for the pressure is simply **$L^2(\Omega)$**. The choice of the pair $(V, Q) = (H(\mathrm{div};\Omega), L^2(\Omega))$ is thus fundamental to the mixed pressure-velocity formulation [@problem_id:4128948].

A crucial property of the $H(\mathrm{div};\Omega)$ space concerns the boundary term $\langle p, \mathbf{w} \cdot \mathbf{n} \rangle_{\partial\Omega}$. While functions in $H(\mathrm{div};\Omega)$ are not necessarily continuous and may not have pointwise values at the boundary, a fundamental trace theorem states that the normal component $\mathbf{w} \cdot \mathbf{n}$ has a well-defined trace on $\partial\Omega$. This trace, however, is not a regular function but a distribution in the space $H^{-1/2}(\partial\Omega)$, the dual space of $H^{1/2}(\partial\Omega)$. This allows for the mathematically rigorous imposition of boundary conditions on the normal component of velocity, which are treated as **essential boundary conditions** on the space $V$ [@problem_id:4128979].

The elegance of this structure can be appreciated through the lens of the **de Rham complex**, which organizes fundamental differential operators and their corresponding function spaces. For three-dimensional domains, this sequence is:
$$ H^1(\Omega) \xrightarrow{\nabla} H(\mathrm{curl};\Omega) \xrightarrow{\nabla \times} H(\mathrm{div};\Omega) \xrightarrow{\nabla \cdot} L^2(\Omega) $$
The mixed pressure-velocity formulation directly utilizes the final map in this sequence, pairing the spaces $H(\mathrm{div};\Omega)$ and $L^2(\Omega)$ through the divergence operator, which perfectly aligns with the structure of the underlying physics [@problem_id:4128946].

### The LBB Condition and Well-Posedness

Establishing a weak formulation is not sufficient to guarantee a unique and stable solution. The well-posedness of the resulting saddle-point problem is governed by a critical compatibility condition between the velocity and pressure spaces, known as the **Ladyzhenskaya-Babuška-Brezzi (LBB)** condition, or the inf-sup condition. For the continuous problem, this condition states that there exists a constant $\beta > 0$ such that [@problem_id:4128967]:
$$ \inf_{q \in L^2_0(\Omega)} \sup_{\mathbf{w} \in H(\mathrm{div};\Omega)} \frac{(\nabla \cdot \mathbf{w}, q)_{\Omega}}{\|\mathbf{w}\|_{H(\mathrm{div};\Omega)} \|q\|_{L^2(\Omega)}} \ge \beta $$
(The pressure space is taken as $L^2_0(\Omega)$, the space of $L^2$ functions with zero mean, if the pressure is only defined up to a constant, e.g., in a domain with purely Neumann boundary conditions).

Physically, the LBB condition ensures that the pressure acts as a stable Lagrange multiplier for the mass conservation constraint. It guarantees that for any admissible pressure field $q$, a velocity field $\mathbf{w}$ can be found whose divergence can "represent" $q$ and whose magnitude is controlled. Mathematically, this is equivalent to the existence of a continuous right-inverse for the divergence operator. If this condition were to fail, the pressure solution would be unconstrained, leading to non-physical, spurious solutions [@problem_id:4128967].

### Discretization and Stable Finite Element Pairs

When we discretize the problem using the finite element method, we seek solutions in finite-dimensional subspaces $V_h \subset H(\mathrm{div};\Omega)$ and $Q_h \subset L^2(\Omega)$. The choice of these discrete spaces is paramount, as they must not only approximate the continuous spaces well but must also satisfy a discrete version of the LBB condition, uniformly with respect to the mesh size $h$.

#### Conformity

A first requirement is that the discrete velocity space $V_h$ must be a **conforming** subspace of $H(\mathrm{div};\Omega)$. For a function pieced together from polynomials on each element of a mesh, membership in $H(\mathrm{div};\Omega)$ requires that the **normal component of the vector field be continuous across all inter-element faces**. This is a weaker condition than full vector continuity (required for $H^1$-conforming elements) but is precisely what is needed for the weak formulation to be valid. If a non-conforming space is used (e.g., standard continuous $\mathbb{P}_1$ Lagrange elements), the distributional divergence acquires singular jump terms at element interfaces, which breaks the structure of the discrete system and generally leads to instability [@problem_id:4128962].

#### Stable Element Pairs and Spurious Modes

The discrete LBB condition imposes a strong compatibility requirement on the pair $(V_h, Q_h)$. A powerful and intuitive way to satisfy this condition is to choose pairs such that the divergence of the discrete velocity space is exactly the discrete pressure space:
$$ \nabla \cdot V_h = Q_h $$
This condition, which can be formalized using the concept of a discrete exact sequence, guarantees LBB stability. It ensures that there are no non-zero pressure functions in $Q_h$ that are "invisible" to the velocity space, i.e., orthogonal to the entire range of the discrete divergence operator. Such functions, if they exist, are called **spurious pressure modes** and manifest as non-physical oscillations (e.g., checkerboard patterns) in the numerical solution [@problem_id:4128949].

Several families of $H(\mathrm{div})$-conforming finite elements have been designed to form stable pairs with corresponding pressure spaces.

*   **Raviart-Thomas (RT) Elements:** The RT elements of order $k$ (denoted $\mathrm{RT}_k$) are a foundational choice. On a simplex (triangle or tetrahedron) $K$, the local space consists of vector polynomials $\mathbf{v}(\mathbf{x}) = \mathbf{p}_k(\mathbf{x}) + q_k(\mathbf{x})\mathbf{x}$, where $\mathbf{p}_k$ is a vector of polynomials of degree at most $k$ and $q_k$ is a scalar polynomial of degree at most $k$. The degrees of freedom are chosen as moments of the normal flux on each face, which explicitly enforces normal continuity. A key property is that $\nabla \cdot \mathrm{RT}_k = \mathbb{P}_k^{\mathrm{disc}}$, the space of discontinuous piecewise polynomials of degree $k$. Therefore, the pair $(\mathrm{RT}_k, \mathbb{P}_k^{\mathrm{disc}})$ is a stable element choice [@problem_id:4128978] [@problem_id:4128951].

*   **Brezzi-Douglas-Marini (BDM) Elements:** Another family of stable elements. For BDM elements of order $k$, the property is $\nabla \cdot \mathrm{BDM}_k = \mathbb{P}_{k-1}^{\mathrm{disc}}$. Thus, the pair $(\mathrm{BDM}_k, \mathbb{P}_{k-1}^{\mathrm{disc}})$ is stable [@problem_id:4128951].

Using an incompatible pair, such as continuous $\mathbb{P}_1$ vector fields for velocity with discontinuous $\mathbb{P}_1$ scalars for pressure, leads to instability. Here, the divergence of the velocity space is the space of discontinuous constants ($\mathbb{P}_0^{\mathrm{disc}}$), which is a strict subspace of the chosen pressure space, leading to spurious modes [@problem_id:4128949].

### Stabilization Techniques

In practice, it can be desirable to use simple, equal-order element pairs (e.g., continuous $\mathbb{P}_1$ for both velocity and pressure) that are known to violate the LBB condition. To prevent the resulting instabilities, a **stabilization** term can be added to the formulation.

A common technique is **grad-div stabilization**. This involves adding a penalty term to the velocity-velocity block of the bilinear form:
$$ S_{\gamma}((\mathbf{v}_h, p_h), (\mathbf{w}_h, q_h)) = \gamma (\nabla \cdot \mathbf{v}_h, \nabla \cdot \mathbf{w}_h)_{\Omega} $$
where $\gamma > 0$ is a user-defined stabilization parameter. This term penalizes velocity solutions with large or highly oscillatory divergence, thereby indirectly controlling the pressure field and suppressing spurious modes. It also helps in the nearly incompressible limit (low frequency or high bulk modulus), where the physical constraint $\nabla \cdot \mathbf{v} \approx 0$ must be enforced numerically. It is important to note that this form of stabilization is formally **inconsistent**, as it modifies the original governing equation by adding a term that is not zero for the exact solution. This introduces a small modeling error, representing a trade-off between simplicity of implementation and formal accuracy [@problem_id:4128960].