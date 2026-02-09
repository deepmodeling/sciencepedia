## Applications and Interdisciplinary Connections

Having established the fundamental principles and mechanisms distinguishing conservative and non-conservative formulations, we now turn to their practical application. The theoretical choice between expressing governing equations in terms of conserved variables (e.g., mass density $\rho$, momentum density $\rho \boldsymbol{u}$, total energy density $\rho E$) versus primitive variables (e.g., $\rho$, velocity $\boldsymbol{u}$, pressure $p$) is not merely a matter of mathematical convenience. This choice has profound and far-reaching consequences for the accuracy, stability, and physical fidelity of numerical simulations. Furthermore, it dictates how computational fluid dynamics (CFD) models interface with other physical systems and mathematical disciplines.

This chapter explores these consequences through a series of applications. We will demonstrate how the principle of conservation forms the bedrock of modern shock-capturing schemes, how it must be carefully extended to handle complex geometries and physical source terms, and how it informs the coupling of fluid dynamics with thermodynamics, solid mechanics, data science, and optimization. By examining these diverse contexts, we will illuminate the critical role that conservation laws play in the daily practice of computational science and engineering.

### Foundations of Modern Shock-Capturing Schemes

The accurate simulation of compressible flows, particularly those containing discontinuities such as shock waves and contact surfaces, is one of the primary achievements of modern CFD. This success is inextricably linked to the development of numerical schemes that are founded upon the conservative form of the governing equations.

#### The Finite Volume Method and Global Conservation

The most direct and powerful application of the integral conservation laws is found in the finite volume method (FVM). By discretizing the domain into a set of contiguous control volumes and applying the integral form of a conservation law to each, the FVM naturally ensures that the total amount of a conserved quantity within the computational domain changes only due to fluxes across the domain's boundaries.

Consider the one-dimensional conservation of mass. The semi-discrete update for the mass $M_i$ in cell $i$ is given by the net flux across its interfaces:
$$
\frac{\mathrm{d}M_{i}}{\mathrm{d}t} = F_{i-1/2} - F_{i+1/2}
$$
where $F_{i \pm 1/2}$ represents the mass flow rate at the cell faces. When we sum the change in mass over all cells in the domain, the interior fluxes cancel out in a telescoping sum:
$$
\sum_{i=1}^{N} \frac{\mathrm{d}M_{i}}{\mathrm{d}t} = \sum_{i=1}^{N} (F_{i-1/2} - F_{i+1/2}) = F_{1/2} - F_{N+1/2}
$$
This result demonstrates that the total rate of change of mass in the domain is precisely equal to the rate of mass entering at the left boundary minus the rate of mass exiting at the right boundary. This property of exact global conservation is guaranteed by the structure of the finite volume method, provided the numerical flux $F_{i+1/2}$ is uniquely defined at each interface. In contrast, schemes derived from non-conservative, differential forms of the equations, which approximate derivatives at grid points, generally lack this telescoping property and can therefore artificially create or destroy mass, momentum, and energy within the domain [@problem_id:3304182].

#### Roe's Linearization and Approximate Riemann Solvers

The design of high-resolution shock-capturing schemes, such as those based on Godunov's method and its numerous variants, relies heavily on the conservative formulation. These methods compute the flux at cell interfaces by solving, either exactly or approximately, a local Riemann problem. A cornerstone of this approach is Roe's approximate Riemann solver, which linearizes the hyperbolic system.

The ingenuity of Roe's method lies in constructing a special averaged state $(\tilde{\rho}, \tilde{u}, \tilde{H}, \dots)$ such that the flux difference between two states $\mathbf{U}_L$ and $\mathbf{U}_R$ is exactly related to the difference in states through a constant matrix $\tilde{\mathbf{A}}$, the Roe-averaged Jacobian:
$$
\mathbf{F}(\mathbf{U}_R) - \mathbf{F}(\mathbf{U}_L) = \tilde{\mathbf{A}}(\mathbf{U}_L, \mathbf{U}_R) (\mathbf{U}_R - \mathbf{U}_L)
$$
This property, known as the Roe property, is not a mere mathematical convenience. It ensures that if the states $\mathbf{U}_L$ and $\mathbf{U}_R$ satisfy the Rankine-Hugoniot jump conditions for a single discrete discontinuity, the numerical flux computed by the scheme will be consistent with the physical flux. This guarantees that the scheme will capture stationary shocks with no numerical dissipation and move shocks at the correct speed. A linearization based on primitive variables or a simple arithmetic average of conserved variables would fail to satisfy this crucial property, leading to incorrect shock speeds and strengths. Thus, the very architecture of these advanced schemes is predicated on the conservative form of the Euler equations [@problem_id:3304137].

#### Boundary Conditions and Conservation

The principle of conservation must extend to the boundaries of the computational domain. The implementation of physical boundary conditions requires careful consideration of the interplay between primitive and conserved variables. For instance, to model a solid, perfectly reflecting wall, the physical intuition of reversing the normal velocity component is naturally expressed in primitive variables. For a ghost cell state $(\rho_g, u_g, p_g)$ adjacent to an interior cell $(\rho_1, u_1, p_1)$, one sets $\rho_g = \rho_1$, $p_g = p_1$, and $u_g = -u_1$.

However, the numerical flux at the wall must be computed from the corresponding conserved variable states. This consistent transformation ensures that the physical boundary condition is correctly enforced. For a properly designed numerical flux, such as the Rusanov or HLLC flux, this procedure results in exactly zero mass flux through the wall, upholding the conservation principle at the domain boundary [@problem_id:3304144].

Conversely, a naive treatment of boundaries can violate conservation. Consider an inflow boundary where primitive variables are specified. A conservative treatment would use these primitive values to compute a flux of conserved variables into the domain. A non-conservative approach, however, might use simple extrapolation of primitive variables to ghost cells to compute spatial derivatives. Such a method can introduce a significant mass imbalance, as the discretely computed mass change within the boundary cell will not, in general, equal the physical mass flux entering the domain. This discrepancy arises because the discrete approximation of the non-conservative equations does not possess the telescoping flux property that is fundamental to conservation [@problem_id:3304121].

### Handling Complex Geometries and Source Terms

Real-world engineering and scientific problems rarely occur in simple Cartesian domains and often involve physical source terms like gravity or chemical reactions. Extending conservative methods to these scenarios reveals further subtleties.

#### Conservation Laws on Curvilinear Grids and the Geometric Conservation Law (GCL)

To apply finite volume or finite difference methods to domains with complex, curved boundaries, a coordinate transformation is typically employed, mapping the physical domain $(x, y, z)$ to a structured computational domain $(\xi, \eta, \zeta)$. When a conservation law of the form $\partial_t \mathbf{U} + \nabla \cdot \mathbf{F} = \mathbf{0}$ is transformed into this new coordinate system, it retains its conservative structure, but with a modified conserved variable and transformed fluxes:
$$
\partial_{t}\big(J \mathbf{U}\big) + \partial_{\xi}\big(\hat{\mathbf{F}}\big) + \partial_{\eta}\big(\hat{\mathbf{G}}\big) + \partial_{\zeta}\big(\hat{\mathbf{H}}\big) = 0
$$
Here, $J$ is the Jacobian of the coordinate transformation, and the new conserved variable is $\hat{\mathbf{U}} = J\mathbf{U}$. The transformed fluxes $\hat{\mathbf{F}}, \hat{\mathbf{G}}, \hat{\mathbf{H}}$ are linear combinations of the original Cartesian fluxes, with coefficients determined by the metrics of the transformation (e.g., $x_\xi, y_\eta$, etc.) [@problem_id:3304138].

This transformation introduces a critical requirement for the numerical discretization. In the continuous sense, the metric terms satisfy certain identities (e.g., $\partial_\xi(J\nabla\xi) + \partial_\eta(J\nabla\eta) + \partial_\zeta(J\nabla\zeta) = \mathbf{0}$). Because of these identities, a uniform freestream flow (constant $\mathbf{U}$ and $\mathbf{F}$) is an exact solution to the transformed equations. However, if the discrete operators used to approximate the metric terms (e.g., from the grid point coordinates) are not consistent with the discrete operators used to approximate the flux divergence, the discrete version of these geometric identities may not hold.

This inconsistency leads to a situation where the numerical scheme fails to preserve a uniform freestream. Even with constant flow variables, the discrete flux divergence will be non-zero, acting as a spurious, grid-induced source term that contaminates the solution. To prevent this, the numerical scheme must satisfy the **Geometric Conservation Law (GCL)**, which demands that the geometric terms be discretized in a manner that exactly satisfies the discrete metric identities. This ensures that a uniform flow remains uniform, a fundamental test of a scheme's robustness on curvilinear grids [@problem_id:3304146] [@problem_id:3304191].

#### Well-Balanced Schemes for Systems with Source Terms

Many physical systems, such as those in atmospheric science, oceanography, and astrophysics, are governed by conservation laws that include source terms. A common example is the Euler equations with gravity:
$$
\frac{\partial \mathbf{U}}{\partial t} + \frac{\partial \mathbf{F}(\mathbf{U})}{\partial x} = \mathbf{S}(\mathbf{U})
$$
These systems often admit non-trivial steady-state solutions where the flux gradient exactly balances the source term. For the Euler equations with gravity, this is the state of hydrostatic equilibrium, where $\frac{dp}{dx} = -\rho g$.

A standard numerical scheme, even if conservative, may fail to preserve such a steady state. The truncation error of the discrete flux divergence will generally not be identical to the truncation error of the discrete source term, leading to a non-zero numerical residual that generates spurious oscillations or flows. This can be a catastrophic failure in applications where the flow is a small perturbation away from a background equilibrium.

To overcome this, **well-balanced schemes** are designed. The core idea is to construct the discretization of the flux gradient and the source term in a coupled manner, such that they are guaranteed to cancel each other out for the exact steady-state solution. For example, in a finite volume context, one can define the momentum source term as the exact integral of the continuous pressure gradient across the cell, ensuring a perfect balance with the interface pressure fluxes evaluated from the exact hydrostatic profile [@problem_id:3304184] [@problem_id:3304126]. Conversely, using a naive primitive-variable formulation with a simple central difference for the pressure gradient will inevitably fail this balance, generating spurious velocities from a state of rest [@problem_id:3304203].

### Multi-Physics and Interdisciplinary Frontiers

The choice of formulation becomes even more critical when CFD is coupled with other physics or integrated into broader engineering and scientific workflows. These interdisciplinary connections often push the concepts of conservation and variable choice to their limits.

#### Thermodynamics and Real Fluids: The Problem of Variable Choice

In simulations involving fluids under extreme conditions, such as transcritical injection or high-energy-density physics, the ideal gas law is insufficient, and complex, nonlinear equations of state (EOS) are required. This introduces a challenging dilemma. On one hand, formulating the equations in terms of conserved variables $(\rho, \rho\boldsymbol{u}, \rho E)$ is crucial for capturing shocks correctly. On the other hand, the numerical diffusion inherent in most schemes causes a linear mixing of these conserved variables in regions of high gradients.

When this numerically mixed state, e.g., $(\rho, \rho E)_{\text{mix}} = \alpha (\rho, \rho E)_L + (1-\alpha) (\rho, \rho E)_R$, is passed to a highly nonlinear EOS to recover pressure, the resulting pressure $p_{\text{rec}} = p(\rho_{\text{mix}}, E_{\text{mix}})$ is generally not a linear average of the original pressures. This inconsistency can generate large, spurious pressure oscillations at material interfaces (like contact discontinuities) where pressure should be constant. In some cases, advancing a set of primitive variables (e.g., $\rho, \boldsymbol{u}, p$) can mitigate this specific problem, as the linear numerical mixing of a constant pressure field trivially preserves its constancy. This reveals a difficult trade-off between satisfying the conservation laws for shock capturing and maintaining thermodynamic consistency across contact discontinuities, a topic of active research [@problem_id:3304127].

#### Multiphase Flows and Non-Conservative Systems

The classical theory of conservation laws applies to systems that can be written in divergence form. However, many important multi-physics models do not fit this structure. A prime example is the Baer-Nunziato model for two-phase compressible flow. This model consists of separate sets of conservation laws for each phase, coupled by interfacial source terms representing the exchange of momentum and energy.

Crucially, some of these source terms take the form of **non-conservative products**, such as $p_I \nabla \alpha_k$, where $p_I$ is an interfacial pressure and $\alpha_k$ is a phase volume fraction. This term, a product of a state variable and a state variable gradient, cannot be written in divergence form. In the presence of discontinuities (where $\nabla\alpha_k$ behaves like a Dirac delta function), the mathematical meaning of such a product is ambiguous. Standard conservative schemes are not applicable. Capturing the correct weak solutions for such systems requires advanced **path-conservative schemes**, which are designed based on a more general theory of hyperbolic systems and require defining a "path" in state-space to resolve the ambiguity of the non-conservative product at jumps [@problem_id:3304135].

#### Fluid-Structure Interaction: Coupling Conservative and Non-Conservative Solvers

Fluid-Structure Interaction (FSI) is a classic multi-physics problem where a fluid solver is coupled to a solid mechanics solver. Often, the CFD solver is based on a conservative formulation (advancing $\rho, \rho\boldsymbol{u}, \rho E$), while the structural solver is based on a non-conservative, primitive-variable formulation (advancing displacement, velocity, and computing stress from strain).

Ensuring the stability and physical accuracy of the coupled system requires a careful formulation of the interface conditions. To conserve energy across the fluid-solid interface, the power (rate of work) lost by the fluid must equal the power gained by the solid. This requires satisfying both kinematic continuity (equal velocities) and dynamic continuity (equal tractions) at the interface. The exchanged power density, given by the product of the traction vector and the interface velocity, $\dot{W} = (\boldsymbol{\sigma}_f \cdot \boldsymbol{n}) \cdot \boldsymbol{u}$, must be consistently supplied as a source to the solid solver and removed as a sink from the fluid solver. Expressing this power term requires translating between the variables natural to each solver, for instance, writing the fluid-side power in terms of the conserved momentum $\boldsymbol{m}$ and density $\rho$ [@problem_id:3304212].

#### Data Assimilation: Conservation as a Constraint

In fields like weather forecasting and oceanography, data assimilation techniques are used to combine sparse, noisy observations with numerical model predictions to produce an optimal estimate of the state of the system. This is often framed as a Bayesian inference problem. For instance, one might have satellite observations of temperature ($T$) and wind speed ($u$), which are primitive variables.

The analysis or update step seeks a posterior state that is a best fit to both the model forecast (the prior) and the observations, weighted by their respective uncertainties. In this context, fundamental physical principles can be enforced as powerful constraints. Global conservation of mass, momentum, or energy, which can be expressed as linear constraints on the state vector (e.g., $\sum u_i = 0$ for a velocity perturbation in a closed domain), can be incorporated into the optimization problem using Lagrange multipliers. Enforcing these conservation laws not only ensures the physical realism of the resulting analysis but also serves to reduce the uncertainty of the final state estimate. By explicitly adding information to the system, these constraints reduce the posterior variance of unobserved state variables, demonstrating a synergistic link between physical conservation principles and statistical estimation theory [@problem_id:3304204].

#### Adjoint-Based Design Optimization: The Importance of Adjoint Consistency

A final frontier is the use of CFD in automated design optimization, where the goal is to find the shape or operating conditions that optimize a specific objective, such as minimizing drag or maximizing lift. Gradient-based optimization algorithms require the sensitivity of the objective function with respect to a large number of design parameters. The adjoint method provides an exceptionally efficient way to compute these gradients.

The discrete adjoint equations are derived from the discretized governing equations. A crucial finding is that the choice of the primal discretization—conservative versus non-conservative—directly impacts the resulting discrete adjoint system. Consequently, the sensitivity gradients computed using a conservative formulation and its corresponding adjoint will differ from those computed using a non-conservative formulation. This difference, termed **adjoint inconsistency**, can be significant, especially for shock-dominated flows where the objective function is sensitive to shock position and strength. Since the conservative formulation provides a more physically faithful representation of the flow physics across discontinuities, its corresponding adjoint system generally yields more reliable gradients for optimization. This highlights that the choice of formulation not only affects the accuracy of the forward simulation but also the accuracy and reliability of the entire design optimization loop [@problem_id:3304152].

### Conclusion

The distinction between conservative and non-conservative formulations, and the associated choice of primitive versus conserved variables, is far from a mere academic detail. As we have seen, these concepts are central to the entire enterprise of computational fluid dynamics. They are fundamental to the design of accurate shock-capturing schemes, the robust handling of complex geometries, the physically consistent treatment of source terms, and the successful coupling of CFD with other scientific and engineering disciplines. A deep understanding of these principles is indispensable for any computational scientist seeking to develop, analyze, or apply numerical methods to the complex challenges of modern fluid dynamics.