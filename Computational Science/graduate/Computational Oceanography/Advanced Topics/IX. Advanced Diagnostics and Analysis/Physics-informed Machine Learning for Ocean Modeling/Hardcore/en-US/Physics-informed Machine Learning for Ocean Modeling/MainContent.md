## Introduction
The field of oceanography stands at a critical juncture, faced with the dual challenges of increasingly complex simulation models and an unprecedented wealth of observational data. While traditional numerical models provide a rigorous, physics-based understanding of ocean dynamics, they are computationally intensive and often struggle to incorporate sparse, noisy data effectively. Conversely, purely data-driven machine learning models excel at pattern recognition but often lack physical consistency, leading to predictions that can violate fundamental laws of nature and exhibit instability over long-term simulations. This gap creates a pressing need for a new modeling paradigm that synergistically combines the predictive power of machine learning with the robust constraints of physical law.

This article explores Physics-Informed Machine Learning (PIML), a transformative framework designed to bridge this gap. PIML embeds the governing equations of fluid dynamics—from local PDE constraints to global conservation laws—directly into the architecture and training process of neural networks. The result is a new generation of hybrid models that are not only data-driven but also physically consistent, robust, and interpretable. By systematically fusing data and physics, PIML offers a path toward more accurate ocean state estimation, reliable sub-grid scale parameterizations, and faster, more stable surrogate models for climate simulation.

To provide a comprehensive understanding of this powerful approach, this article is structured into three distinct chapters. First, **Principles and Mechanisms** will lay the theoretical foundation, detailing how fundamental [ocean dynamics](@entry_id:1129055) are encoded as physical priors and exploring the core computational paradigms like PINNs and Neural Operators. Next, **Applications and Interdisciplinary Connections** will showcase how these principles are applied to solve real-world problems in oceanography, from enhancing climate models to revolutionizing data assimilation. Finally, **Hands-On Practices** will provide a series of guided exercises, allowing you to translate theory into practice and build a working intuition for developing and validating PIML models.

## Principles and Mechanisms

The successful integration of machine learning with ocean modeling hinges upon a deep and principled fusion of data-driven methods with the fundamental laws of physics. This chapter elucidates the core principles and mechanisms that underpin this synergy. We will begin by reviewing the essential physical laws of ocean dynamics that serve as the foundation for any physics-informed model. Subsequently, we will explore the primary paradigms of [physics-informed machine learning](@entry_id:137926), detailing how these laws are encoded within different computational frameworks. Finally, we will address advanced topics and practical challenges, from enforcing symmetries by architectural design to quantifying uncertainty in a principled manner.

### Fundamental Ocean Dynamics as Physical Priors

Before constructing a machine learning model, one must first identify the immutable physical principles it must obey. For large-scale oceanography, the governing dynamics are captured by the [primitive equations](@entry_id:1130162), which themselves arise from a set of well-justified approximations to the full Navier-Stokes equations for a fluid on a rotating sphere.

#### The Boussinesq and Hydrostatic Approximations

The vastness of the ocean, with its immense horizontal scales compared to its vertical scale, and the relatively small density variations that drive its circulation, permit two powerful simplifications.

The **Boussinesq approximation** is applied to fluids where density variations, $\rho'$, are small compared to a constant reference density, $\rho_0$ (i.e., $|\rho'| / \rho_0 \ll 1$). This approximation systematically simplifies the governing equations by asserting that the impact of density variations is negligible except when coupled with gravity, where it creates buoyancy forces. The two primary consequences are: (1) density is replaced by the constant reference density $\rho_0$ in all inertial terms (e.g., the momentum advection term), and (2) the mass conservation equation simplifies to the incompressibility condition, $\nabla \cdot \mathbf{u} = 0$. The velocity field is thus treated as [divergence-free](@entry_id:190991) .

The **[hydrostatic approximation](@entry_id:1126281)** arises from a scale analysis of the vertical momentum equation. For large-scale oceanic motions, where the horizontal length scale $L$ is much greater than the vertical scale $H$, the vertical acceleration is orders of magnitude smaller than the vertical pressure gradient and the force of gravity. Neglecting these small terms reduces the vertical momentum equation to a simple diagnostic balance:
$$
\frac{\partial p}{\partial z} = - \rho g
$$
Here, $p$ is pressure, $z$ is the vertical coordinate, $\rho$ is the full density, and $g$ is the [acceleration due to gravity](@entry_id:173411). This approximation transforms the [vertical momentum equation](@entry_id:1133792) from a prognostic equation for vertical velocity into a diagnostic equation for pressure. In a Physics-Informed Neural Network (PINN), these two approximations would be enforced by adding their respective residuals, such as $R_{\text{mass}} = \nabla \cdot \mathbf{u}$ and $R_{\text{hyd}} = \partial p/\partial z + \rho g$, as penalty terms to the loss function .

#### Integral Conservation Laws

Beyond the local, [differential form](@entry_id:174025) of the governing equations, [integral conservation laws](@entry_id:202878) provide powerful global constraints on the dynamics. These invariants are often more robust and physically insightful than the local equations alone.

A cornerstone of stratified fluid dynamics is the energy budget. The [total mechanical energy](@entry_id:167353) of the system is partitioned into **Kinetic Energy (KE)**, the energy of motion, and **Gravitational Potential Energy (GPE)**, the energy stored by the vertical position of fluid parcels. A crucial concept is **Available Potential Energy (APE)**, which is the portion of the total GPE that is available for conversion into KE through adiabatic rearrangement of mass. The portion of GPE that cannot be converted is the background potential energy of a statically stable, minimum-energy reference state .

In an ideal (inviscid and adiabatic) Boussinesq fluid within a closed domain, the sum of total kinetic energy, $K = \int_V \frac{1}{2}\rho_0 |\mathbf{u}|^2 dV$, and total [available potential energy](@entry_id:1121282), $A$, is conserved. The conversion between these two reservoirs is governed by the **buoyancy flux**:
$$
C_P = \int_V \rho_0 b w \, dV
$$
where $b$ is buoyancy and $w$ is the vertical velocity. The energy budgets take the form $\frac{dK}{dt} = C_P$ and $\frac{dA}{dt} = -C_P$, clearly showing that $C_P$ represents the rate at which APE is converted into KE (if positive) or KE is converted into APE (if negative). Any physically consistent model must respect this energy pathway. Furthermore, irreversible processes like diapycnal mixing, parameterized by a diffusivity $\kappa$, act as a sink for APE, dissipating it into background potential energy and internal energy (heat) at a rate proportional to $\kappa$ and the square of buoyancy gradients .

Another profound invariant is **Ertel's Potential Vorticity (PV)**. For a Boussinesq fluid, it is defined as:
$$
q = \frac{(\nabla \times \mathbf{u} + f \hat{\mathbf{k}}) \cdot \nabla b}{\rho_0} = \frac{\boldsymbol{\omega}_a \cdot \nabla b}{\rho_0}
$$
where $\boldsymbol{\omega}_a$ is the absolute vorticity (the sum of the fluid's relative vorticity and the planetary vorticity $f \hat{\mathbf{k}}$). Ertel's theorem states that in an adiabatic, [inviscid flow](@entry_id:273124), PV is materially conserved, meaning it is constant along fluid parcel trajectories:
$$
\frac{Dq}{Dt} = \frac{\partial q}{\partial t} + \mathbf{u} \cdot \nabla q = 0
$$
This makes PV an exceptionally powerful dynamical tracer. A machine learning model that conserves PV is likely to produce far more physically realistic and stable long-term simulations of phenomena like [geostrophic turbulence](@entry_id:1125619) .

### Core Paradigms of Physics-Informed Machine Learning

With this physical foundation, we can now explore the primary computational paradigms for integrating these principles into machine learning models.

#### Solving Differential Equations: The PINN Framework

The most direct approach to creating a physics-informed model is the **Physics-Informed Neural Network (PINN)**. The central idea is to use a neural network, $u_{\boldsymbol{\theta}}(\mathbf{x}, t)$, not as a discrete data-to-[data mapping](@entry_id:895128), but as a continuous and differentiable representation of the solution to a partial differential equation (PDE) .

The engine that powers PINNs is **Automatic Differentiation (AD)**. AD is a set of techniques for numerically evaluating the derivative of a function specified by a computer program. For a PINN, we can visualize the computation as a graph flowing from the input coordinates $(\mathbf{x}, t)$ and network parameters $\boldsymbol{\theta}$ through the network layers to the output $u_{\boldsymbol{\theta}}$. AD allows us to compute the exact derivatives of this output with respect to the input coordinates (e.g., $\partial u_{\boldsymbol{\theta}} / \partial t$, $\nabla u_{\boldsymbol{\theta}}$) to form the PDE residual. The most common form, **reverse-mode AD** (also known as [backpropagation](@entry_id:142012)), is exceptionally efficient for this task. It computes the gradient of a single scalar output (the loss) with respect to a vast number of inputs (the parameters $\boldsymbol{\theta}$) in a single backward pass through the [computational graph](@entry_id:166548). Its computational cost is a small constant multiple of the forward pass, irrespective of the number of parameters, making the training of large networks feasible .

Once the PDE residual, boundary condition misfits, and initial condition misfits are computed, they can be incorporated into a loss function. There are two primary strategies for this enforcement :

1.  **Soft Enforcement**: This is the most common method, where the squared residuals are added as penalty terms to the total loss function. For example, $\mathcal{L} = \mathcal{L}_{\text{PDE}} + \mathcal{L}_{\text{BC}} + \mathcal{L}_{\text{IC}}$. The training process then attempts to minimize this composite loss, driving all residuals towards zero simultaneously. The physics is satisfied approximately, to the degree that the optimization is successful.

2.  **Hard Enforcement**: This strategy involves designing the network architecture such that a constraint is satisfied exactly, by construction, for any value of the network parameters $\boldsymbol{\theta}$. This is typically achieved by formulating an **ansatz**. For instance, to enforce a boundary condition $u(x,0)=g(x)$, one might formulate the network output as $\hat{u}_{\boldsymbol{\theta}}(x,t) = g(x) + t \cdot N_{\boldsymbol{\theta}}(x,t)$, where $N_{\boldsymbol{\theta}}$ is a standard neural network. This form guarantees the boundary condition is met regardless of the output of $N_{\boldsymbol{\theta}}$. While powerful for simple constraints like boundary conditions, hard enforcement of a complex PDE across the entire domain is generally intractable.

#### Learning Solution Operators: The Neural Operator Framework

An alternative paradigm is to learn the solution operator itself. A **Neural Operator (NO)** is a [deep learning architecture](@entry_id:634549) designed to learn the mapping between [entire functions](@entry_id:176232). For instance, in a coastal modeling problem governed by $-\nabla \cdot (\kappa \nabla \psi) = f$ with boundary condition $\psi|_{\partial \Omega} = g$, an NO could learn the operator $S: (f, g) \mapsto \psi$ .

This approach fundamentally differs from the PINN philosophy. A PINN is trained to find the solution $\psi$ for a *single* instance of the forcing $f$ and boundary condition $g$. If $f$ or $g$ changes, the PINN must be retrained. In contrast, an NO is trained on a dataset of many $(f_i, g_i) \to \psi_i$ pairs. Once trained, it can infer the solution for a *new* unseen $(f,g)$ in a single, rapid [forward pass](@entry_id:193086).

This makes NOs particularly advantageous for **many-query scenarios**, such as [uncertainty quantification](@entry_id:138597), [optimal control](@entry_id:138479), or data assimilation, where the same forward model must be solved repeatedly with different inputs. The substantial upfront cost of training the operator, $C_{\text{train}}$, is amortized over a large number of queries, $N_q$. The break-even point against solving each query with a PINN (cost $C_{\text{opt}}$) occurs when the NO's total cost, $C_{\text{train}} + N_q \cdot C_{\text{infer}}$, becomes lower. Given that inference cost $C_{\text{infer}}$ is typically much smaller than optimization cost $C_{\text{opt}}$, NOs become computationally superior for a sufficiently large number of queries . However, this advantage relies on the critical assumption that the query distribution is well-covered by the training distribution and the NO's [generalization error](@entry_id:637724) is acceptably low.

#### Learning from Data: Hybrid Modeling and System Identification

In many practical scenarios, we have both a trusted, albeit incomplete, physical model and a wealth of observational or high-fidelity simulation data. In these cases, ML can be used to augment the physical model or discover new physics from the data.

**Hybrid modeling** refers to the paradigm where a machine learning model learns a specific component *within* a traditional numerical PDE solver, rather than replacing the solver entirely. A prime example is learning **subgrid-scale (SGS) [closures](@entry_id:747387)** for turbulence . In coarse-resolution ocean models, the effects of unresolved turbulent eddies on the resolved flow must be parameterized. Traditionally, this is done with heuristic models for **eddy viscosity** (for momentum) and **eddy diffusivity** (for tracers), which relate unresolved fluxes to gradients of resolved fields . In a hybrid approach, an ML model can learn a more accurate and [complex mapping](@entry_id:178665) from resolved flow features to these unresolved fluxes. This approach is powerful because the model retains the robust structure of the numerical solver, which can guarantee properties like mass conservation, while the ML component provides a data-informed enhancement. It is crucial, however, that the learned closure itself respects physical principles, such as being purely dissipative (requiring a non-negative eddy viscosity/diffusivity) to prevent the unphysical generation of energy  .

A different data-centric paradigm is **system identification**, which aims to discover the governing equations directly from data. The **Sparse Identification of Nonlinear Dynamics (SINDy)** framework is a leading method for this task . SINDy operates on the assumption that the governing dynamics are sparse in the space of possible functions. The procedure is as follows:
1.  From spatiotemporal data of a field $c(\mathbf{x}, t)$, numerically compute its time derivative, $\partial_t c$. Noise-robust differentiation methods are essential for this step.
2.  Construct a large candidate library, $\mathbf{\Theta}$, of potential terms that could appear on the right-hand side of the PDE. This library should be physics-informed, including terms that respect [dimensional consistency](@entry_id:271193), conservation laws, and physical symmetries (e.g., advection $-\nabla \cdot (\mathbf{u}c)$, isotropic diffusion $\kappa \nabla^2 c$).
3.  Solve the linear system $\partial_t c = \mathbf{\Theta} \boldsymbol{\xi}$ for the coefficient vector $\boldsymbol{\xi}$ using a [sparse regression](@entry_id:276495) technique, such as the Least Absolute Shrinkage and Selection Operator (LASSO). This finds a parsimonious model by driving most of the coefficients in $\boldsymbol{\xi}$ to exactly zero.
The result is a simple, interpretable PDE that best explains the observed dynamics, balancing accuracy with [model complexity](@entry_id:145563).

### Advanced Mechanisms and Practical Challenges

Building robust and reliable [physics-informed models](@entry_id:753434) for the ocean requires addressing a set of more advanced challenges, from enforcing subtle symmetries to handling multi-scale dynamics and quantifying uncertainty.

#### Architectural Enforcement of Physical Symmetries

While physical laws can be enforced softly via the loss function, [fundamental symmetries](@entry_id:161256) of the governing equations are often best guaranteed by embedding them directly into the model's architecture. Two such critical symmetries in fluid dynamics are **Galilean invariance** and **rotational [equivariance](@entry_id:636671)** .

**Galilean invariance** is the principle that the laws of physics are the same in all inertial (non-accelerating) [reference frames](@entry_id:166475). This means a physical model's output should not depend on the absolute velocity of the observer. An ML model can be made Galilean invariant by construction if its inputs are restricted to quantities that are themselves invariant, such as velocity gradients ($\nabla \mathbf{u}$) or relative velocities between points.

**Rotational equivariance** (or covariance) means that if the inputs to a model are rotated, the output should rotate in a corresponding manner. For example, in an isotropic 2D flow, rotating the input velocity field should result in an identically rotated output tendency field. This property can be enforced using **Group-Equivariant Neural Networks (G-CNNs)**. These networks employ specialized convolutional filters (steerable kernels) that are designed to respect the transformation properties of the rotation group (e.g., $SO(2)$ in the plane), ensuring that the equivariance property holds throughout the network. Such architectures are more data-efficient and generalize better because they have the correct physical structure built-in.

#### Taming Stiffness in Multi-Scale Dynamics

Ocean dynamics are inherently multi-scale. For instance, a stably [stratified flow](@entry_id:202356) involves slow advective processes coexisting with fast internal gravity waves. When the time scales are widely separated, the system of PDEs becomes mathematically **stiff**. For a PINN, this stiffness translates into a highly ill-conditioned [loss landscape](@entry_id:140292), which can lead to **gradient pathologies** during training .

A naive [non-dimensionalization](@entry_id:274879) of the equations may result in certain terms in the PDE residuals having coefficients that are orders of magnitude larger than others. The loss function becomes dominated by these terms, and the gradients sent to the optimizer are similarly unbalanced and explosive. This can cause the training to stagnate or fail entirely.

Several strategies can mitigate this pathology:
1.  **Physics-Informed Scaling**: Non-dimensionalize the governing equations using the *fastest* relevant time scale in the system (e.g., the buoyancy period $1/N$). This rescales the operator so that its fast dynamics have eigenvalues of order one, improving the conditioning of the problem.
2.  **Loss Weighting**: The weights of different residual terms in the loss function ($\lambda_i$) are critical hyperparameters. Instead of being set arbitrarily, they should be chosen based on physical principles. For example, scaling the residuals such that their contributions to the system's energy budget are of comparable magnitude provides a robust, physically grounded method for balancing the loss function .
3.  **Architectural Choices**: The network ansatz itself can be modified to simplify the problem. For 2D [incompressible flow](@entry_id:140301), parameterizing the velocity field using a [streamfunction](@entry_id:1132499), $\mathbf{u} = (\partial_z \psi, -\partial_x \psi)$, enforces the continuity equation exactly, removing one residual from the loss function and reducing the complexity of the optimization landscape .

#### A Principled Approach to Uncertainty Quantification

A deterministic prediction from an ML model is of limited scientific value without an estimate of its uncertainty. Uncertainty in modeling can be broadly classified into two types :

*   **Aleatoric Uncertainty**: This is the inherent, irreducible randomness in a system or its observation. It can arise from measurement noise, or from unresolved physical processes that appear stochastic from the model's perspective.
*   **Epistemic Uncertainty**: This is uncertainty due to a lack of knowledge. It stems from having limited data to constrain the model, or from the model's own structural imperfections. This type of uncertainty is reducible with more data or better physical constraints.

The **Bayesian PINN** provides a formal probabilistic framework for quantifying these uncertainties. Instead of learning a single set of network weights, a Bayesian PINN learns a posterior probability distribution over the weights, which in turn induces a posterior distribution over the solution function, $p(u \mid \text{Data}, \text{Physics})$. This is achieved by combining a [prior belief](@entry_id:264565) about the function, $p(u)$, with likelihoods that quantify how probable the evidence is, given a particular function $u$. Crucially, both the measurement data and the physical laws are treated as sources of evidence, each with its own likelihood, $p(\text{Data} \mid u)$ and $p(\text{Physics} \mid u)$, respectively.

This framework naturally separates the two types of uncertainty. The data likelihood term, $p(\text{Data} \mid u)$, is constructed based on a model of the observation noise, $\epsilon$. By allowing the noise variance to vary in space and time (i.e., using a **heteroscedastic** noise model), one can capture complex, state-dependent aleatoric uncertainty. The epistemic uncertainty, on the other hand, is captured by the spread or variance of the posterior distribution $p(u \mid \text{Data}, \text{Physics})$ itself. Where data and physics provide strong constraints, the posterior will be sharply peaked with low variance. In regions of sparse data or where the physics is less constraining, the posterior will be broader, reflecting our greater uncertainty about the true solution .