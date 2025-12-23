## Introduction
The accurate simulation of turbulent [reacting flows](@entry_id:1130631), such as those in engines and power plants, is a cornerstone of modern engineering and science. However, the vast range of scales inherent in turbulence makes its direct simulation computationally intractable for most practical scenarios. Consequently, computational fluid dynamics (CFD) relies on turbulence models to represent the effects of unresolved scales on the resolved flow. The central challenge in this endeavor is the **[turbulence closure problem](@entry_id:268973)**: the mathematical act of averaging the governing equations introduces new, unknown terms, leaving the system of equations incomplete. While classical models have been foundational, they often struggle to capture the complex physics of reacting flows, where turbulence, chemistry, and thermodynamics are intricately coupled.

This article explores a new frontier in turbulence modeling: the application of machine learning (ML) to overcome the limitations of traditional approaches. By leveraging high-fidelity data and embedding physical principles directly into their architecture, ML models offer a powerful pathway to creating more accurate and generalizable closures. Across three chapters, this article provides a comprehensive overview of this rapidly evolving field.

First, **Principles and Mechanisms** dissects the mathematical origin of the closure problem and establishes the fundamental physical principles—such as invariance properties and [realizability constraints](@entry_id:1130703)—that are essential for building robust ML models. Next, **Applications and Interdisciplinary Connections** transitions from theory to practice, detailing the complete workflow for developing and validating ML [closures](@entry_id:747387), from data generation to deployment, and highlights its transformative potential in fields ranging from combustion to climate science. Finally, **Hands-On Practices** provides a set of targeted exercises designed to solidify understanding of crucial concepts like feature engineering, source term closure, and physical realizability.

## Principles and Mechanisms

The formulation of predictive models for turbulent reacting flows rests upon a foundational challenge known as the **turbulence closure problem**. This problem is not an artifact of a particular numerical method, but rather an intrinsic consequence of applying averaging or filtering operations to the nonlinear governing equations of fluid motion. In this chapter, we will dissect the origin of this problem and explore the fundamental principles and mechanisms that guide the construction of [closure models](@entry_id:1122505), with a particular focus on modern, data-driven approaches that leverage machine learning.

### The Mathematical Origin of the Closure Problem

The governing equations for a compressible, multicomponent, reacting fluid—the conservation laws for mass, momentum, energy, and chemical species—are a system of nonlinear partial differential equations. Consider, for example, the convective transport term in the momentum equation, $\partial_j(\rho u_i u_j)$, or in the species transport equation, $\partial_j(\rho u_j Y_\alpha)$. These terms are nonlinear due to the products of field variables.

In the analysis of turbulent flows, we are typically interested in the behavior of the mean or large-scale components of the flow, not the instantaneous value at every point in space and time. To isolate these components, we apply a filtering or averaging operator, denoted by an overbar $\overline{(\cdot)}$, to the governing equations. This operator is linear, meaning $\overline{A+B} = \overline{A} + \overline{B}$. However, it does not commute with nonlinear operations. Specifically, for any two fluctuating quantities $A$ and $B$, the average of their product is not equal to the product of their averages:

$$
\overline{AB} \neq \overline{A}\overline{B}
$$

This simple inequality is the root of the entire closure problem. When we apply the averaging operator to a nonlinear term like $\rho u_i u_j$, we obtain $\overline{\rho u_i u_j}$. If we decompose the instantaneous fields into a mean part (e.g., $\overline{u_i}$) and a fluctuating part (e.g., $u_i'$), the averaged term expands to include correlations of these fluctuations. For example, using a simple Reynolds decomposition ($u_i = \overline{u_i} + u_i'$), the term $\overline{u_i u_j}$ becomes $\overline{(\overline{u_i} + u_i')(\overline{u_j} + u_j')} = \overline{u_i}\overline{u_j} + \overline{u_i' u_j'}$. The term $\overline{u_i' u_j'}$ is a new unknown—the **Reynolds stress tensor**—that represents the transport of momentum by turbulent fluctuations. It cannot be expressed in terms of the mean quantities for which we are solving, and thus the system of averaged equations is "unclosed" . An analogous procedure on the species transport equation gives rise to an unclosed **[turbulent scalar flux](@entry_id:1133523)**, $\overline{u_j' Y_\alpha'}$.

### Favre Averaging: A Strategy for Variable-Density Flows

In [reacting flows](@entry_id:1130631), particularly combustion, large temperature variations induce significant density changes. A typical premixed hydrocarbon-air flame can exhibit a density ratio of $\rho_{\mathrm{unburned}} / \rho_{\mathrm{burned}} \approx 7$. These strong [density fluctuations](@entry_id:143540) introduce additional complexity if standard Reynolds averaging is used. For instance, the averaged convective term $\overline{\rho u_i Y_k}$ expands into a proliferation of unclosed correlations, including not only the standard [turbulent scalar flux](@entry_id:1133523) but also terms like the turbulent mass flux $\overline{\rho' u_i'}$, the density-scalar correlation $\overline{\rho' Y_k'}$, and a triple correlation $\overline{\rho' u_i' Y_k'}$ .

To simplify the mathematical structure of the averaged equations, **density-weighted (or Favre) averaging** is almost universally employed. For any quantity $\phi$, its Favre average, $\tilde{\phi}$, is defined as:

$$
\tilde{\phi} = \frac{\overline{\rho \phi}}{\overline{\rho}}
$$

The corresponding fluctuation is $\phi'' = \phi - \tilde{\phi}$. A key property of this decomposition is that the density-weighted average of the fluctuation is zero: $\overline{\rho \phi''} = 0$.

Applying this to the convective [scalar transport](@entry_id:150360) term $\overline{\rho u_i Y_k}$ yields:
$$
\overline{\rho u_i Y_k} = \overline{\rho(\tilde{u}_i + u_i'')(\tilde{Y}_k + Y_k'')} = \overline{\rho}\tilde{u}_i\tilde{Y}_k + \tilde{u}_i\overline{\rho Y_k''} + \tilde{Y}_k\overline{\rho u_i''} + \overline{\rho u_i'' Y_k''}
$$
Because the density-weighted fluctuation averages are zero, this simplifies dramatically to:
$$
\overline{\rho u_i Y_k} = \overline{\rho}\tilde{u}_i\tilde{Y}_k + \overline{\rho u_i'' Y_k''}
$$

The Favre-averaged transport equation now contains only two terms arising from convection: the transport of the mean scalar by the mean mass flux, $\overline{\rho}\tilde{u}_i\tilde{Y}_k$, which is resolved, and a single unclosed term, $\overline{\rho u_i'' Y_k''}$, which is the Favre-averaged [turbulent scalar flux](@entry_id:1133523). This clean separation is a significant advantage over Reynolds averaging . It is crucial to note that Favre averaging does not eliminate the closure problem; it merely rearranges it into a more manageable form. The unclosed terms—the Favre-averaged Reynolds stress tensor $\overline{\rho u_i'' u_j''}$ and the [turbulent scalar flux](@entry_id:1133523) $\overline{\rho u_j'' Y_\alpha''}$—persist and require modeling.

### Unclosed Terms in RANS and LES

The closure problem manifests differently depending on the averaging strategy.

In **Reynolds-Averaged Navier-Stokes (RANS)**, the averaging is performed over time, space, or an ensemble, aiming to resolve only the steady or slowly varying mean flow. The unclosed Reynolds stress tensor, $R_{ij} = \overline{\rho u_i'' u_j''}$, represents the collective effect of the entire spectrum of turbulent eddies. Classical [closures](@entry_id:747387) like the **Boussinesq hypothesis** model this tensor by drawing an analogy to viscous stress, assuming it is proportional to the mean rate-of-strain tensor $\tilde{S}_{ij}$:
$$
R_{ij} - \frac{1}{3}R_{kk}\delta_{ij} \approx -2\mu_t \tilde{S}_{ij}
$$
This assumes the turbulent transport is isotropic, a premise that fails severely in reacting flows where phenomena like buoyancy, dilatation, and baroclinic torque induce significant anisotropy  .

In **Large-Eddy Simulation (LES)**, the averaging takes the form of a low-pass [spatial filter](@entry_id:1132038), designed to separate the flow into large, resolved eddies and small, subgrid-scale (SGS) eddies. The goal is to resolve the large, energy-containing motions directly and model the effects of the smaller, more universal subgrid scales. The primary unclosed term in the filtered momentum equation is the **SGS stress tensor**, $\tau_{ij}^{sgs} = \overline{\rho}(\widetilde{u_i u_j} - \tilde{u}_i \tilde{u}_j)$. This tensor represents the transfer of momentum between the resolved and unresolved scales of motion.

The action of the SGS stresses on the resolved flow is best understood through the resolved kinetic energy budget. The rate of energy transfer from the resolved scales to the subgrid scales, denoted as the SGS dissipation rate $\Pi_{sgs}$, is given by the contraction $\Pi_{sgs} = \tau_{ij}^{sgs} \tilde{S}_{ij}$. In the classical [turbulence energy cascade](@entry_id:171686), there is a net flux of energy from large to small scales, so on average, $\langle \Pi_{sgs} \rangle > 0$. However, locally and transiently, energy can flow from small to large scales, a phenomenon known as **backscatter**, where $\Pi_{sgs}  0$ . Simple models like the Smagorinsky model are purely dissipative (i.e., they enforce $\Pi_{sgs} \ge 0$) and cannot capture this important physical effect .

An additional complexity in LES arises on [non-uniform grids](@entry_id:752607), where the filter width $\Delta(\mathbf{x})$ varies in space. Here, the filtering and differentiation operators do not commute. The **[commutation error](@entry_id:747514)**, $\mathcal{C}_i[\phi] = \widetilde{\partial_i \phi} - \partial_i \tilde{\phi}$, is not zero. Its leading-order contribution is proportional to the gradient of the filter width and the curvature of the filtered field, $\mathcal{C}_i[\phi] \sim \nabla \Delta \cdot \nabla^2 \phi$ . These terms, along with further complications from density gradients in Favre-filtered equations, introduce additional unclosed contributions that a high-fidelity closure model must account for .

### Turbulence-Chemistry Interaction

In reacting flows, the most challenging closure problem arises from the chemical source terms, $\dot{\omega}_\alpha$. These terms are typically highly nonlinear functions of species concentrations and temperature, often involving exponential Arrhenius kinetics. Due to this nonlinearity, the filtered reaction rate is not equal to the reaction rate evaluated at the filtered concentrations and temperature:

$$
\tilde{\dot{\omega}}_\alpha \neq \dot{\omega}_\alpha(\tilde{\mathbf{Y}}, \tilde{T})
$$

This inequality arises because subgrid fluctuations in temperature and composition can significantly alter the mean reaction rate . A formal way to express the filtered source term is through the subfilter-scale probability density function (PDF), $\mathcal{P}(\mathbf{Y}, T | \tilde{\boldsymbol{\phi}})$:

$$
\tilde{\dot{\omega}}_\alpha = \frac{1}{\overline{\rho}} \overline{\rho \dot{\omega}_\alpha} = \iint \dot{\omega}_\alpha(\mathbf{Y}, T) \mathcal{P}(\mathbf{Y}, T | \tilde{\boldsymbol{\phi}}) \, d\mathbf{Y} \, dT
$$

This equation states that the filtered reaction rate is the expectation of the instantaneous rate, conditioned on the resolved-scale state $\tilde{\boldsymbol{\phi}}$. An intuitive way to see the origin of the closure term is via a Taylor series expansion of $\dot{\omega}_\alpha$ around the filtered state. This reveals that the leading-order correction to the naive approximation $\dot{\omega}_\alpha(\tilde{\mathbf{Y}}, \tilde{T})$ involves the subfilter covariances of the scalars, such as $\widetilde{Y_s'' T''}$, multiplied by the second derivatives of the reaction [rate function](@entry_id:154177) . The task of a machine learning closure for chemistry is therefore to learn the [conditional expectation](@entry_id:159140) $\mathbb{E}[\dot{\omega}_\alpha | \tilde{\boldsymbol{\phi}}]$, implicitly capturing the effects of all subfilter moments on the nonlinear chemistry.

### Principles of Physics-Constrained Machine Learning Closures

A machine learning model, such as a neural network, is a powerful [universal function approximator](@entry_id:637737). However, if trained naively on simulation data, it is likely to produce physically inconsistent and unstable results. To create robust closures, the model's architecture and training process must be deeply informed by the underlying physics.

#### Invariance Properties

The governing equations of fluid dynamics obey fundamental symmetries of nature, which must be respected by any valid closure model . Key among these are:

-   **Galilean Invariance:** The model's predictions must be independent of the [constant velocity](@entry_id:170682) of the reference frame. This means the model must not depend on absolute velocities, but only on velocity gradients, differences, or other Galilean-invariant quantities.
-   **Rotational Invariance (Objectivity):** The model's predictive relationship must be independent of the coordinate system's orientation. This is a critical constraint, particularly for tensor-valued quantities like the Reynolds stress.

To enforce [rotational invariance](@entry_id:137644), ML models must be constructed from **[scalar invariants](@entry_id:193787)**. For [closures](@entry_id:747387) that depend on the local velocity gradient tensor, $\nabla \tilde{\mathbf{u}}$, we first decompose it into its symmetric part (the [strain-rate tensor](@entry_id:266108), $\tilde{\mathbf{S}}$) and its antisymmetric part (the rotation-rate tensor, $\tilde{\mathbf{R}}$). A complete set of independent [scalar invariants](@entry_id:193787) up to second order can be formed from these tensors:
$$
\mathcal{I} = \{ [\mathrm{tr}(\tilde{\mathbf{S}})]^2, \mathrm{tr}(\tilde{\mathbf{S}}^2), \mathrm{tr}(\tilde{\mathbf{R}}^2) \}
$$
Note that for [compressible flows](@entry_id:747589), $\mathrm{tr}(\tilde{\mathbf{S}}) = \nabla \cdot \tilde{\mathbf{u}}$ is nonzero, so its square is an independent invariant representing dilatation. Any trace involving a single $\tilde{\mathbf{R}}$ or an odd number of them is zero, and $\mathrm{tr}(\tilde{\mathbf{S}}\tilde{\mathbf{R}})$ is identically zero due to symmetry properties . An ML model that takes only these invariants as input is guaranteed to be rotationally invariant.

For tensor-valued [closures](@entry_id:747387), such as for the Reynolds stress, a more general approach is to use a **tensor [basis expansion](@entry_id:746689)**. The predicted tensor is expressed as a linear combination of a basis of tensors, where the coefficients are functions of the [scalar invariants](@entry_id:193787) :
$$
\boldsymbol{\tau}^{sgs} = \sum_{n=1}^{N} \alpha_n(\mathcal{I}) \mathbf{T}^{(n)}
$$
The basis tensors $\mathbf{T}^{(n)}$ are constructed from products of $\tilde{\mathbf{S}}$ and $\tilde{\mathbf{R}}$ (e.g., $\tilde{\mathbf{S}}$, $\tilde{\mathbf{S}}^2$, $\tilde{\mathbf{S}}\tilde{\mathbf{R}} - \tilde{\mathbf{R}}\tilde{\mathbf{S}}$, etc.). This framework allows the model to represent complex anisotropic states, such as stress-strain misalignment, which are impossible to capture with simple eddy-viscosity models . In reacting flows, this basis must be augmented with tensors constructed from other relevant vectors, like the gradient of density or [progress variable](@entry_id:1130223), to capture effects like buoyancy and [baroclinicity](@entry_id:1121342) .

#### Scale Consistency

In LES, a closure model should represent the physics at the filter scale, $\Delta$, and should not be explicitly dependent on the numerical grid resolution. If dimensional features like the resolved strain rate $S$ are fed directly to an ML model, the model may simply learn a [spurious correlation](@entry_id:145249) with the grid size. To avoid this and promote generalizability across different grids, input features must be nondimensionalized using local, physically relevant scales . The characteristic length scale is the filter width, $\Delta$, and the characteristic velocity scale of eddies at this scale can be taken as $u_\Delta \sim \sqrt{k}$, where $k$ is the resolved [turbulent kinetic energy](@entry_id:262712). This defines a local eddy turnover time scale, $t_\Delta = \Delta / \sqrt{k}$. All features should be made dimensionless using these scales, for example:

-   Dimensionless strain rate: $S^* = S \cdot t_\Delta = S \Delta / \sqrt{k}$
-   Dimensionless scalar gradient: $|\nabla Z|^* = |\nabla Z| \cdot \Delta$

#### Realizability Constraints

Closure models must produce physically plausible outputs. This property is known as **[realizability](@entry_id:193701)**. For example, predicted species mass fractions must be non-negative and sum to one, and the Reynolds stress tensor must be positive semi-definite (corresponding to non-negative turbulent kinetic energies). Naive ML models do not guarantee these constraints. They must be enforced "by construction" through specialized network architectures or output layers .

-   **Mass Fractions:** To enforce $0 \le \tilde{Y}_\alpha \le 1$ and $\sum_\alpha \tilde{Y}_\alpha = 1$, the final layer of a neural network can apply a **[softmax function](@entry_id:143376)**. Given unconstrained outputs (logits) $\ell_\alpha$, the mass fractions are computed as $\tilde{Y}_\alpha = \exp(\ell_\alpha) / \sum_\beta \exp(\ell_\beta)$.
-   **Elemental Conservation:** Chemical source terms must conserve atomic elements. This is a linear constraint on the source term vector: $A\tilde{\boldsymbol{\dot{\omega}}} = \mathbf{0}$, where $A$ is the [elemental composition matrix](@entry_id:1124364). This can be strictly enforced by having the network predict coefficients $\mathbf{z}$ in a basis for the **nullspace** of $A$. If the columns of a matrix $N$ span this nullspace (i.e., $AN = 0$), then the source term vector can be constructed as $\tilde{\boldsymbol{\dot{\omega}}} = N\mathbf{z}$, which automatically satisfies the constraint.

By embedding these principles of invariance, consistency, and realizability directly into the structure of machine learning models, we can move beyond black-box approximators to develop robust, generalizable, and physically faithful [closures](@entry_id:747387) for the next generation of [turbulent reacting flow](@entry_id:1133520) simulations.