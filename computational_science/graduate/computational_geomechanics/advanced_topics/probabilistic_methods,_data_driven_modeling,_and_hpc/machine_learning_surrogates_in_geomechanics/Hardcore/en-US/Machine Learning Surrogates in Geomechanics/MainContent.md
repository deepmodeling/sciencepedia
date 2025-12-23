## Introduction
Machine learning (ML) surrogates are revolutionizing [computational geomechanics](@entry_id:747617) by offering a pathway to dramatically accelerate complex, high-fidelity simulations. These data-driven models promise to replace time-consuming solvers, unlocking the potential for extensive [uncertainty quantification](@entry_id:138597), rapid design optimization, and real-time analysis. However, this computational speed must not come at the cost of physical fidelity. The central challenge, which this article addresses, is how to construct surrogates that are not only fast but also robust, reliable, and consistent with the fundamental laws of mechanics.

This article provides a comprehensive guide to developing and deploying physics-informed ML surrogates. In **Principles and Mechanisms**, we will explore the foundational trade-offs between cost and accuracy and delve into the core techniques for embedding physical laws, from penalty-based methods like PINNs to architecturally-enforced constraints for objectivity and [thermodynamic consistency](@entry_id:138886). Following this, **Applications and Interdisciplinary Connections** will demonstrate the practical utility of these models across a range of geomechanical problems, including [constitutive modeling](@entry_id:183370), [poromechanics](@entry_id:175398), and dynamic analysis, and show how they enable higher-level tasks like optimization and reliability assessment. Finally, **Hands-On Practices** will offer a series of guided exercises to solidify these concepts, allowing you to build and validate your own physically-constrained surrogates.

## Principles and Mechanisms

The replacement of high-fidelity, physics-based simulations with machine learning (ML) surrogates represents a paradigm shift in [computational geomechanics](@entry_id:747617). The promise of accelerated computation—often by orders of magnitude—opens new frontiers for uncertainty quantification, inverse analysis, and large-scale design optimization. However, this promise is contingent on the surrogate's ability to provide not only fast but also accurate and physically plausible predictions. This chapter delves into the fundamental principles and mechanisms that govern the development and deployment of such surrogates, moving from the foundational justification for their use to the sophisticated techniques required to imbue them with physical realism.

### The Rationale for Surrogate Modeling: A Principled Trade-off

At its core, the decision to employ a surrogate model in place of a trusted high-fidelity solver, such as the Finite Element Method (FEM), is an engineering trade-off between computational cost and predictive accuracy. This decision must be grounded in a rigorous, quantitative framework.

#### Error Control and Epistemic Justification

A surrogate is only useful if its predictions are accurate enough for the intended application. Consider a geomechanical design problem where a key quantity of interest, derived from the [displacement field](@entry_id:141476) $\boldsymbol{u}$, must be known within a certain tolerance. The total error of the surrogate prediction $\hat{\boldsymbol{u}}$ with respect to the true physical solution $\boldsymbol{u}^{\star}$ must be bounded. This total error can be decomposed into two parts: the discretization error of the high-fidelity solver, $\boldsymbol{e}_h = \boldsymbol{u}_h - \boldsymbol{u}^{\star}$, and the surrogate's approximation error relative to the solver, $\boldsymbol{e}_s = \hat{\boldsymbol{u}} - \boldsymbol{u}_h$.

Using the triangle inequality, we can bound the total error in a suitable norm, such as the [energy norm](@entry_id:274966) $\|\cdot\|_E$:
$$
\|\hat{\boldsymbol{u}} - \boldsymbol{u}^{\star}\|_E = \|(\hat{\boldsymbol{u}} - \boldsymbol{u}_h) + (\boldsymbol{u}_h - \boldsymbol{u}^{\star})\|_E \le \|\hat{\boldsymbol{u}} - \boldsymbol{u}_h\|_E + \|\boldsymbol{u}_h - \boldsymbol{u}^{\star}\|_E
$$
If we can obtain a certified bound $\eta_h$ for the solver's error (e.g., via [a posteriori error estimation](@entry_id:167288)) and a bound $\delta$ for the surrogate's [generalization error](@entry_id:637724) (from validation), we have a certified upper bound on the total error: $\|\hat{\boldsymbol{u}} - \boldsymbol{u}^{\star}\|_E \le \delta + \eta_h$. The surrogate is epistemically warranted only if this combined error is less than the application's tolerance, $\varepsilon$. For instance, if a FEM solver has a certified error bound $\eta_h = 5 \times 10^{-3}$ and a trained surrogate has a [generalization error](@entry_id:637724) $\delta = 4 \times 10^{-3}$, the total error is bounded by $9 \times 10^{-3}$. This surrogate would be acceptable for a design task with an error tolerance of $\varepsilon = 10^{-2}$ .

#### Computational Complexity and Net Speedup

The second condition for adopting a surrogate is [computational efficiency](@entry_id:270255). The significant upfront cost of training a surrogate, $C_{\mathrm{off}}$, which includes generating training data via expensive high-fidelity simulations, must be amortized over a sufficient number of queries. Let $C_{\mathrm{FEM}}$ be the cost of one [high-fidelity simulation](@entry_id:750285) and $C_{\mathrm{sur}}$ be the cost of one surrogate evaluation. For a total of $M$ queries, the surrogate is advantageous if:
$$
C_{\mathrm{off}} + M C_{\mathrm{sur}}  M C_{\mathrm{FEM}}
$$
This defines a break-even point for the number of queries, $M^{\star} = \frac{C_{\mathrm{off}}}{C_{\mathrm{FEM}} - C_{\mathrm{sur}}}$. If the anticipated number of queries $M$ is greater than $M^{\star}$, the surrogate approach is computationally cheaper. The net [speedup](@entry_id:636881), which accounts for the training overhead, is given by $S_{\mathrm{net}} = \frac{M C_{\mathrm{FEM}}}{C_{\mathrm{off}} + M C_{\mathrm{sur}}}$ . This analysis is critical for justifying the significant initial investment in surrogate development.

### Foundational Approaches to Model Acceleration

Within the landscape of accelerated computation, it is essential to distinguish purely data-driven surrogates from physics-based model reduction techniques.

A **Machine Learning Surrogate**, in its most common form, is a non-intrusive, data-driven approximation of the input-to-output map of a high-fidelity solver. The solver is treated as a "black box" that generates training examples. The surrogate, often a neural network, learns a parametric map $\widehat{\mathcal{S}}_{\boldsymbol{\phi}}$ from problem inputs (e.g., material parameters $\boldsymbol{\theta}$, boundary conditions, loads) directly to the solution fields (e.g., displacement $\hat{\boldsymbol{u}}$). At query time, the surrogate provides an approximate solution via a fast forward pass, completely bypassing the need to solve the governing Partial Differential Equations (PDEs). The physics is only implicitly encoded in the training data .

In contrast, a **Reduced-Order Model (ROM)**, such as one based on Proper Orthogonal Decomposition (POD), is an intrusive, physics-based approach. It first constructs a low-dimensional basis from a set of high-fidelity solution "snapshots". The full solution is then approximated as a linear combination of these basis vectors, $\boldsymbol{u} \approx \mathbf{V} \boldsymbol{q}$, where $\boldsymbol{q}$ is a vector of reduced coordinates. At query time, the original governing equations are projected onto this reduced basis (a Galerkin projection), yielding a much smaller system of equations that is solved for $\boldsymbol{q}$. Thus, a ROM still solves the physical equations, but in a compressed form. The primary distinction is that a ROM enforces the physics explicitly at query time (in a weak sense), whereas a purely data-driven surrogate does not .

### Methods for Incorporating Physical Laws

A purely data-driven surrogate trained on input-output data alone may produce physically inconsistent results, especially when extrapolating outside the training distribution. A central theme in [scientific machine learning](@entry_id:145555) is the development of methods to embed physical knowledge into the surrogate, ensuring its predictions are not just statistically plausible but also physically meaningful.

#### Physics as Penalty: The Physics-Informed Neural Network (PINN)

One of the most prominent paradigms for creating physics-aware surrogates is the **Physics-Informed Neural Network (PINN)**. Instead of being trained on pre-computed solution data, a PINN is trained to directly satisfy the governing physical laws. The neural network itself, $u_{\theta}(\boldsymbol{x}, t)$, represents the solution field. Its parameters $\boldsymbol{\theta}$ are optimized by minimizing a loss function composed of the residuals of the governing PDEs, boundary conditions, and initial conditions, evaluated at a set of collocation points.

This approach treats the physical laws as "soft constraints" enforced via penalty terms in the loss function. For a general time-dependent problem, the total [loss function](@entry_id:136784) for a PINN takes the form:
$$
\mathcal{L}(\boldsymbol{\theta}) = w_{\mathrm{pde}}\mathcal{L}_{\mathrm{pde}} + w_{\mathrm{bc}}\mathcal{L}_{\mathrm{bc}} + w_{\mathrm{ic}}\mathcal{L}_{\mathrm{ic}}
$$
where $\mathcal{L}_{\mathrm{pde}}$ is the [mean squared error](@entry_id:276542) of the PDE residuals in the domain, $\mathcal{L}_{\mathrm{bc}}$ is the [mean squared error](@entry_id:276542) of the boundary condition mismatches, and $\mathcal{L}_{\mathrm{ic}}$ is the [mean squared error](@entry_id:276542) of the initial condition mismatches.

A canonical example in [geomechanics](@entry_id:175967) is the coupled theory of **Biot [poroelasticity](@entry_id:174851)**, which governs the interaction between fluid flow and solid deformation in a porous medium. The unknown fields are the solid displacement $\boldsymbol{u}(\boldsymbol{x},t)$ and the pore pressure $p(\boldsymbol{x},t)$. A PINN for this system must enforce two coupled PDEs simultaneously . The residuals for the momentum balance and fluid mass conservation are:
$$
\boldsymbol{r}_m := \nabla \cdot \big(\boldsymbol{\sigma}'(\boldsymbol{u}) - \alpha p \boldsymbol{I}\big) + \boldsymbol{b}
$$
$$
r_f := \alpha \dot{\varepsilon}_v(\boldsymbol{u}) + \frac{1}{M}\dot{p} - \nabla \cdot \Big(\frac{k}{\mu}\nabla p\Big) - q
$$
Here, $\boldsymbol{\sigma}'$ is the [effective stress](@entry_id:198048), $\alpha$ is the Biot coefficient, $\varepsilon_v$ is the [volumetric strain](@entry_id:267252), $M$ is the Biot modulus, $k$ is the permeability, and $\mu$ is the [fluid viscosity](@entry_id:261198). The total loss function for the PINN would include the mean squared norms of these two residuals over the spatio-temporal domain, plus additional terms for all mechanical and hydraulic boundary conditions (both Dirichlet and Neumann) and the initial conditions for both $\boldsymbol{u}$ and $p$ .

A critical challenge in training PINNs for multi-physics problems is the balancing of the various loss terms, which may have different physical units and magnitudes. A naive summation can lead to one term dominating the gradient, preventing the network from learning the other aspects of the physics. Robust training requires sophisticated **weighting strategies**. A common approach is to first non-dimensionalize the equations to bring all terms to a similar [order of magnitude](@entry_id:264888). This can be followed by adaptive weighting schemes that dynamically adjust the weights $w_i$ during training, for instance by balancing the magnitude of the gradients from each loss term or by using uncertainty-based methods that learn the weights as part of the optimization .

#### Physics as Architecture: Hard-Constrained Models

An alternative to penalizing physical violations is to design the surrogate's architecture such that it satisfies physical laws by construction. These "hard-constrained" models offer guarantees of physical consistency for any input.

##### Objectivity and Frame Indifference

A fundamental requirement for any [constitutive model](@entry_id:747751) is **[material frame indifference](@entry_id:166014)**, or **objectivity**. This principle states that the material response should not depend on the observer's [rigid body motion](@entry_id:144691). For a constitutive map from strain $\boldsymbol{\varepsilon}$ to stress $\boldsymbol{\sigma}$, this is expressed as the **rotational equivariance** condition:
$$
\boldsymbol{\sigma}(\mathbf{Q}\boldsymbol{\varepsilon}\mathbf{Q}^{T}) = \mathbf{Q}\boldsymbol{\sigma}(\boldsymbol{\varepsilon})\mathbf{Q}^{T} \quad \forall \mathbf{Q} \in \mathrm{SO}(3)
$$
where $\mathbf{Q}$ is any [proper rotation](@entry_id:141831) matrix. Several architectural strategies can enforce this condition exactly :
1.  **Invariant Feature Representation**: For [isotropic materials](@entry_id:170678), the stress can be represented as a function of [scalar invariants](@entry_id:193787) of the strain tensor (e.g., $I_1 = \mathrm{tr}(\boldsymbol{\varepsilon})$, $J_2 = \frac{1}{2}\mathrm{tr}[(\mathrm{dev}\,\boldsymbol{\varepsilon})^2]$) combined with an equivariant tensor basis (e.g., $\{\mathbf{I}, \boldsymbol{\varepsilon}, \boldsymbol{\varepsilon}^2\}$). A surrogate can learn the scalar coefficients of this basis as functions of the invariants, guaranteeing [isotropy](@entry_id:159159) and objectivity.
2.  **Spectral Decomposition**: The strain tensor can be decomposed into its eigenvalues ([principal strains](@entry_id:197797)) $\boldsymbol{\Lambda}$ and eigenvectors ([principal directions](@entry_id:276187)) $\mathbf{V}$, such that $\boldsymbol{\varepsilon} = \mathbf{V}\boldsymbol{\Lambda}\mathbf{V}^T$. A surrogate can map the eigenvalues (which are rotational invariants) to principal stresses $\boldsymbol{\sigma}_p$, and the final stress is reconstructed as $\boldsymbol{\sigma} = \mathbf{V}\boldsymbol{\sigma}_p\mathbf{V}^T$. This enforces co-axiality of [stress and strain](@entry_id:137374) and guarantees an isotropic, objective response.
3.  **Equivariant Layers**: A more general approach is to construct the neural network from layers that are inherently $\mathrm{SO}(3)$-equivariant. These layers are designed to respect the tensorial nature of their inputs and outputs, ensuring that the entire network satisfies the [equivariance](@entry_id:636671) condition by construction.

In contrast, simply training a standard network with rotated data ([data augmentation](@entry_id:266029)) provides no guarantee of exact objectivity .

##### Thermodynamic Consistency

Constitutive models must also obey the laws of thermodynamics. For an [isothermal process](@entry_id:143096), the **Clausius-Duhem inequality** requires that the rate of [mechanical dissipation](@entry_id:169843), $\mathcal{D}$, be non-negative:
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
where $\psi$ is the Helmholtz free energy density. Using the Coleman-Noll procedure, this inequality can be decomposed into a non-dissipative part, which defines the stress as a derivative of the free energy $\boldsymbol{\sigma} = \partial\psi/\partial\boldsymbol{\varepsilon}^{\mathrm{e}}$, and a dissipative part, $\mathcal{D} = \mathbf{Y} \cdot \dot{\mathbf{z}} \ge 0$, where $\mathbf{Y} = -\partial\psi/\partial\mathbf{z}$ are the [thermodynamic forces](@entry_id:161907) conjugate to the internal variables $\mathbf{z}$ .

A thermodynamically consistent surrogate must satisfy these conditions. This can be achieved architecturally:
1.  **Potential-Based Models**: The free energy $\psi$ and a dissipation potential $\phi$ can be represented by neural networks. Crucially, if $\psi$ is represented by an **Input Convex Neural Network (ICNN)**, its [convexity](@entry_id:138568) (a condition for [material stability](@entry_id:183933)) is guaranteed. The stress $\boldsymbol{\sigma}$ and forces $\mathbf{Y}$ are then obtained by [automatic differentiation](@entry_id:144512). The evolution of internal variables can be defined by a [normality rule](@entry_id:182635), $\mathbf{Y} \in \partial \phi(\dot{\mathbf{z}})$, which ensures $\mathcal{D} \ge 0$.
2.  **Constrained Evolution Laws**: A simpler approach is to assume a specific form for the evolution law, such as a [linear relationship](@entry_id:267880) $\mathbf{Y} = \mathbf{L} \dot{\mathbf{z}}$. Non-negative dissipation, $\mathcal{D} = \dot{\mathbf{z}}^T \mathbf{L} \dot{\mathbf{z}} \ge 0$, is then guaranteed by parameterizing the matrix $\mathbf{L}$ to be symmetric [positive semi-definite](@entry_id:262808) (e.g., via a Cholesky-type decomposition $\mathbf{L} = \mathbf{M}^T\mathbf{M}$) .
3.  **Linear Viscoelasticity**: In simpler models like [linear viscoelasticity](@entry_id:181219), the stress may be given by $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon} + \boldsymbol{\eta}:\dot{\boldsymbol{\varepsilon}}$. Here, dissipation is $\mathcal{D} = (\boldsymbol{\eta}:\dot{\boldsymbol{\varepsilon}}):\dot{\boldsymbol{\varepsilon}}$, and non-negativity is ensured by constraining the viscosity tensor $\boldsymbol{\eta}$ to be [positive semi-definite](@entry_id:262808) .

##### Material Stability

For elastoplastic materials, stability is often expressed through **Drucker's postulate**, which requires that for any infinitesimal cycle of [plastic loading](@entry_id:753518) and unloading, the net work done is non-negative. For [rate-independent plasticity](@entry_id:754082), this leads to the condition $d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}^{\mathrm{p}} \ge 0$. A more general condition, based on Hill's criterion, requires that the second-order work $d^2W = \frac{1}{2} d\boldsymbol{\sigma} : d\boldsymbol{\varepsilon}$ be non-negative for any strain increment $d\boldsymbol{\varepsilon}$.

When the constitutive response is linearized as $d\boldsymbol{\sigma} = \mathbf{C} d\boldsymbol{\varepsilon}$, where $\mathbf{C}$ is the algorithmic tangent [stiffness matrix](@entry_id:178659) (in Voigt notation), this stability requirement implies that the [quadratic form](@entry_id:153497) $(d\boldsymbol{\varepsilon})^T \mathbf{C} (d\boldsymbol{\varepsilon})$ must be non-negative. This in turn requires the symmetric part of the [tangent stiffness](@entry_id:166213), $\mathbf{C}_{\mathrm{s}} = \frac{1}{2}(\mathbf{C} + \mathbf{C}^T)$, to be **[positive semi-definite](@entry_id:262808)**. This is equivalent to requiring all eigenvalues of $\mathbf{C}_{\mathrm{s}}$ to be non-negative . A surrogate that outputs a tangent stiffness can be constrained or validated by checking this property. For instance, if a surrogate predicts the plane-strain tangent matrix $\mathbf{C}^{\mathrm{ML}} = \begin{pmatrix} 12  5  0.2 \\ 4  10  0.3 \\ 0  0  3 \end{pmatrix}$, its symmetric part $\mathbf{C}_{\mathrm{s}} = \begin{pmatrix} 12  4.5  0.1 \\ 4.5  10  0.15 \\ 0.1  0.15  3 \end{pmatrix}$ can be computed. The [smallest eigenvalue](@entry_id:177333) of this matrix is approximately $2.997$, which is positive, confirming the stability of the predicted response for that state .

#### Physics as Solver: Hybrid Models

A third strategy combines the strengths of traditional solvers and machine learning. In this **hybrid approach**, an ML model learns only a specific component of the physics, such as a complex [constitutive law](@entry_id:167255) $\boldsymbol{\sigma}_{\phi}(\boldsymbol{\varepsilon})$, while being embedded within a conventional numerical solver (e.g., FEM). The solver's role is to enforce the governing balance laws and boundary conditions exactly (in a weak sense) by solving the discretized system of equations. The training of the ML parameters $\boldsymbol{\phi}$ is then performed in an "outer loop," for example by minimizing the difference between the overall system's response (e.g., predicted boundary tractions) and experimental observations. In this paradigm, the PDE residual does not appear in the training loss of the ML model; it is instead driven to zero by the inner solver .

### Implications for Training and Evaluation

The choice of how to incorporate physics has profound consequences for the training process and the ultimate reliability of the surrogate.

#### Hard vs. Soft Constraints and Convergence

The theoretical underpinnings of PDEs, such as the **coercivity** of the [elliptic operator](@entry_id:191407) in linear elasticity, are crucial for the well-posedness of the physical problem. Coercivity guarantees that a unique, stable solution exists. When using a hard-constrained architecture that ensures the [elasticity tensor](@entry_id:170728) $C$ remains symmetric and positive-definite, the underlying physical problem remains well-posed throughout training. This translates to a better-conditioned optimization landscape for the neural network, as the Jacobian of the physics residual is prevented from becoming singular. This leads to more stable and efficient training .

In contrast, soft penalty approaches allow the optimizer to explore non-physical parameter regimes where, for example, the elasticity tensor is not positive-definite. In these regions, the physical problem becomes ill-posed, [coercivity](@entry_id:159399) is lost, and the optimization landscape becomes ill-conditioned, featuring flat regions or extremely narrow valleys that can stall [gradient-based methods](@entry_id:749986). Attempting to fix this with very large penalty weights introduces its own form of [ill-conditioning](@entry_id:138674) due to the disparate scales of the physics loss and the penalty loss. Therefore, enforcing physical constraints by architectural design is generally superior from an optimization standpoint .

#### Choosing Appropriate Error Metrics

Evaluating the accuracy of a surrogate that outputs a field requires careful selection of error metrics. The common mean-squared-error, equivalent to the squared $L^2(\Omega)$-norm of the displacement error, $\|\hat{\boldsymbol{u}} - \boldsymbol{u}^{\star}\|_{L^2(\Omega)}^2$, measures the average squared distance between the predicted and true displacement fields. However, this metric alone is insufficient, as it provides no direct control over the error in the derivatives of the displacement, and thus no control over the error in strain or stress .

A more physically meaningful metric is the **[energy norm](@entry_id:274966)** of the error:
$$
\|\hat{\boldsymbol{u}} - \boldsymbol{u}^{\star}\|_E^2 = \int_{\Omega} \boldsymbol{\varepsilon}(\hat{\boldsymbol{u}} - \boldsymbol{u}^{\star}) : \mathbb{C} : \boldsymbol{\varepsilon}(\hat{\boldsymbol{u}} - \boldsymbol{u}^{\star}) \, \mathrm{d}\Omega
$$
This norm directly measures the error in the stored elastic energy associated with the error field. For a kinematically admissible surrogate solution, the squared energy error is directly proportional to the error in the total potential energy functional: $\|\hat{\boldsymbol{u}}-\boldsymbol{u}^\star\|_{E}^2 = 2\big(J(\hat{\boldsymbol{u}})-J(\boldsymbol{u}^\star)\big)$ . The [energy norm](@entry_id:274966) also admits an equivalent representation in terms of stress error and the compliance tensor $\mathbb{S} = \mathbb{C}^{-1}$:
$$
\|\hat{\boldsymbol{u}}-\boldsymbol{u}^\star\|_{E}^2 = \int_{\Omega}\big(\boldsymbol{\sigma}(\hat{\boldsymbol{u}})-\boldsymbol{\sigma}(\boldsymbol{u}^\star)\big):\mathbb{S}:\big(\boldsymbol{\sigma}(\hat{\boldsymbol{u}})-\boldsymbol{\sigma}(\boldsymbol{u}^\star)\big)\,\mathrm{d}\Omega
$$
This dual perspective highlights that controlling the error in the [energy norm](@entry_id:274966) simultaneously controls errors in both strain and stress, making it a far more comprehensive and reliable metric for geomechanical applications .

#### Case Study: Gaussian Processes with Physical Priors

The principles of building physics into a model's architecture are not limited to neural networks. **Gaussian Processes (GPs)** are a powerful non-parametric Bayesian method for [surrogate modeling](@entry_id:145866). Physical priors can be encoded into the GP's **kernel function**, which defines the covariance between outputs at different input points.

For instance, when creating a GP surrogate to predict the directional Young's modulus $E(\mathbf{n})$ from microstructural features, one can design a kernel that respects the physics of the problem :
*   **Smoothness**: Instead of the infinitely smooth squared exponential kernel, a **Matérn kernel** can be used to reflect the finite differentiability expected of effective material properties.
*   **Geometric Structure**: The inputs may live on non-Euclidean manifolds. For a loading direction $\mathbf{n}$ on the unit sphere $\mathbb{S}^2$ or a [fabric tensor](@entry_id:181734) $\mathbf{F}$ on the manifold of [symmetric positive-definite](@entry_id:145886) tensors $\mathbb{S}_{++}^3$, the kernel should use appropriate geodesic or Riemannian distances instead of a simple Euclidean distance. A composite kernel can be constructed as a product of kernels on each input space, ensuring the geometry of each descriptor is respected. This allows the model to correctly learn how properties like porosity, fabric, and loading direction interact to determine the material response .

By carefully selecting and combining these principles and mechanisms, it is possible to construct ML surrogates for geomechanics that are not only computationally efficient but also robust, reliable, and consistent with the fundamental laws of physics.