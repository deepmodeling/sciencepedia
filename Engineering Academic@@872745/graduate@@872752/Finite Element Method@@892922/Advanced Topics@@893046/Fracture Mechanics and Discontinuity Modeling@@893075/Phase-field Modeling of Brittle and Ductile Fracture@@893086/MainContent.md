## Introduction
Modeling the initiation and propagation of cracks is a central challenge in solid mechanics and materials science. Traditional [fracture mechanics](@entry_id:141480) often relies on complex tracking of sharp, evolving discontinuities, posing significant computational hurdles. The [phase-field method](@entry_id:191689) offers a powerful and elegant alternative, recasting the difficult problem of a moving crack boundary into the more manageable evolution of a continuous [scalar field](@entry_id:154310) that represents damage. By treating fracture as a gradual process governed by the fundamental principles of [energy minimization](@entry_id:147698), this approach provides a unified framework capable of predicting complex fracture phenomena like [crack nucleation](@entry_id:748035), branching, and merging without ad-hoc criteria.

This article provides a graduate-level introduction to the theory and application of [phase-field fracture](@entry_id:178059) models. It bridges the gap between abstract mathematical concepts and practical engineering simulation by systematically building the reader's understanding across three comprehensive chapters. First, "Principles and Mechanisms" will lay the theoretical groundwork, deriving the governing equations from a variational [energy functional](@entry_id:170311) and exploring the core concepts of material degradation, [irreversibility](@entry_id:140985), and numerical implementation. Next, "Applications and Interdisciplinary Connections" will demonstrate the model's versatility, covering its calibration, extension to [ductile fracture](@entry_id:161045), and integration into multiphysics simulations like [chemo-mechanical failure](@entry_id:200018) in batteries. Finally, "Hands-On Practices" will offer a set of guided problems to solidify these concepts, challenging you to derive key equations and devise calibration strategies. By the end, you will have a robust understanding of how to formulate, implement, and apply [phase-field models](@entry_id:202885) to sophisticated fracture problems.

## Principles and Mechanisms

The phase-field methodology for [fracture mechanics](@entry_id:141480) recasts the complex problem of [crack nucleation](@entry_id:748035) and propagation into the framework of continuum mechanics and the [calculus of variations](@entry_id:142234). This is achieved by regularizing the sharp geometric discontinuity of a crack with a continuous scalar field, known as the **phase-field** or **damage field**, denoted by $d(\boldsymbol{x}, t)$. This field smoothly transitions between two states: the intact material, where $d=0$, and the fully fractured material, where $d=1$. The evolution of this field, coupled with the material's mechanical response, is governed by the minimization of a [total potential energy](@entry_id:185512) functional.

### The Variational Formulation of Fracture

At the heart of the phase-field approach lies a potential energy functional, $\Pi$, which incorporates the competing energetic contributions within a fracturing body. A stable state of the system, comprising the displacement field $\boldsymbol{u}$ and the phase-field $d$, corresponds to a minimum of this total energy. The functional is typically composed of three principal parts: the stored elastic energy, the energy dissipated by fracture, and the potential energy of external loads.

$$
\Pi(\boldsymbol{u}, d) = \Psi_{\mathrm{e}}(\boldsymbol{u}, d) + \Psi_{\mathrm{c}}(d, \nabla d) - \mathcal{W}_{\mathrm{ext}}(\boldsymbol{u})
$$

Here, $\Psi_{\mathrm{e}}$ is the total elastic energy of the body, $\Psi_{\mathrm{c}}$ is the total [fracture energy](@entry_id:174458) associated with the creation of crack surfaces, and $\mathcal{W}_{\mathrm{ext}}$ is the work done by external forces. We will now examine the construction of each of these terms in detail.

#### Elastic Energy and Material Degradation

As a material fractures, its ability to carry load degrades. This physical observation is modeled by reducing the stored elastic energy as a function of the phase-field variable $d$. The [strain energy density](@entry_id:200085) of the intact material, $\psi_0(\boldsymbol{\varepsilon})$, where $\boldsymbol{\varepsilon}(\boldsymbol{u}) = \frac{1}{2}(\nabla \boldsymbol{u} + \nabla \boldsymbol{u}^{\top})$ is the [small-strain tensor](@entry_id:754968), is modulated by a **degradation function**, $g(d)$. The total elastic energy is then expressed as an integral over the domain $\Omega$:

$$
\Psi_{\mathrm{e}}(\boldsymbol{u}, d) = \int_{\Omega} g(d) \psi_0(\boldsymbol{\varepsilon}(\boldsymbol{u})) \, \mathrm{d}\Omega
$$

The degradation function $g(d)$ is a monotonically decreasing function satisfying $g(0)=1$ (no degradation in the intact state) and $g(1) = \kappa \approx 0$ (near-total loss of stiffness in the fully broken state). A small residual stiffness $\kappa > 0$ is often retained to prevent [numerical ill-conditioning](@entry_id:169044) of the system matrices [@problem_id:2587001]. A common choice is the quadratic function $g(d)=(1-d)^2 + \kappa$.

A critical refinement to this model is necessary to reflect the reality that fracture in many materials is driven by tension, not compression. Cracks can close and transmit compressive stresses without further degradation. To capture this, the elastic energy density $\psi_0$ is additively decomposed into a **tensile part**, $\psi^+$, and a **compressive part**, $\psi^-$. Only the tensile part is degraded by the phase-field:

$$
\Psi_{\mathrm{e}}(\boldsymbol{u}, d) = \int_{\Omega} \left( g(d) \psi^{+}(\boldsymbol{\varepsilon}(\boldsymbol{u})) + \psi^{-}(\boldsymbol{\varepsilon}(\boldsymbol{u})) \right) \, \mathrm{d}\Omega
$$

Several methods exist for this decomposition. A widely used approach is the **spectral split**, where the [strain tensor](@entry_id:193332) $\boldsymbol{\varepsilon}$ is decomposed into its positive and negative parts based on its eigenvalues [@problem_id:2587012]. For an isotropic linear elastic material with Lamé parameters $\lambda$ and $\mu$, the tensile and compressive energy densities can be defined as:
$$
\psi^{+}(\boldsymbol{\varepsilon}) = \frac{\lambda}{2}\langle\operatorname{tr}\boldsymbol{\varepsilon}\rangle_{+}^{2} + \mu \operatorname{tr}(\boldsymbol{\varepsilon}^{+}:\boldsymbol{\varepsilon}^{+}), \quad \psi^{-}(\boldsymbol{\varepsilon}) = \frac{\lambda}{2}\langle\operatorname{tr}\boldsymbol{\varepsilon}\rangle_{-}^{2} + \mu \operatorname{tr}(\boldsymbol{\varepsilon}^{-}:\boldsymbol{\varepsilon}^{-})
$$
Here, $\langle x \rangle_{\pm}$ are the Macaulay brackets representing the positive and negative parts of a scalar, and $\boldsymbol{\varepsilon}^{\pm}$ are the positive and negative parts of the strain tensor, constructed from the positive/negative eigenvalues. This formulation ensures that only tensile strains contribute to the energy that drives damage. The resulting Cauchy stress tensor, $\boldsymbol{\sigma} = \partial\psi/\partial\boldsymbol{\varepsilon}$, correctly reflects the damaged response:
$$
\boldsymbol{\sigma} = g(d) \boldsymbol{\sigma}^{+} + \boldsymbol{\sigma}^{-}, \quad \text{where} \quad \boldsymbol{\sigma}^{\pm} = \frac{\partial \psi^{\pm}}{\partial \boldsymbol{\varepsilon}}
$$
This means that the compressive part of the stress remains unaffected by damage, while the tensile part is reduced according to the value of $d$ [@problem_id:2587012].

#### Regularization of Fracture Energy

The Griffith theory of fracture postulates that creating a new crack surface requires an energy proportional to the area of that surface. For a sharp crack surface $\Gamma$, this energy is $\int_{\Gamma} G_c \, \mathrm{d}S$, where $G_c$ is the critical energy release rate, a material property. The [phase-field model](@entry_id:178606) approximates this singular [surface integral](@entry_id:275394) with a volume integral using a **crack [surface density](@entry_id:161889) functional**, $\gamma(d, \nabla d)$. The total [fracture energy](@entry_id:174458) is then:

$$
\Psi_{\mathrm{c}}(d, \nabla d) = \int_{\Omega} G_c \gamma(d, \nabla d) \, \mathrm{d}\Omega
$$

A widely adopted form, stemming from the work of Ambrosio and Tortorelli, is:
$$
\gamma(d, \nabla d) = \frac{1}{c_w} \left( \frac{w(d)}{\ell} + \ell |\nabla d|^2 \right)
$$
This functional introduces a characteristic **length scale**, $\ell > 0$, which controls the width of the regularized or "smeared" crack band. The term $|\nabla d|^2$ penalizes sharp changes in the phase-field, enforcing a smooth transition from $d=0$ to $d=1$. The term $w(d)$ is a potential that drives the phase-field towards the broken state, with properties $w(0)=0$ and $w(1)=1$. Common choices include the AT1 model where $w(d)=d$ [@problem_id:2586959] and the AT2 model where $w(d)=d^2$ [@problem_id:2587001, @problem_id:2587020].

The dimensionless constant $c_w$ is a calibration parameter chosen to ensure that the regularized model converges to the correct Griffith [fracture energy](@entry_id:174458). To determine its value, one can analyze a stationary one-dimensional crack profile $d(x)$ transitioning from $d=1$ to $d=0$. By solving the Euler-Lagrange equation for the functional $\int_{-\infty}^{\infty} (w(d)/\ell + \ell(d')^2) \, \mathrm{d}x$ and enforcing the energy equivalence $\int_{-\infty}^{\infty} G_c \gamma(d(x), d'(x)) \, \mathrm{d}x = G_c$, we can derive a general expression for $c_w$. This procedure yields $c_w = 4 \int_0^1 \sqrt{w(d)} \, \mathrm{d}d$ [@problem_id:2587018]. For the common family of potentials $w(d)=d^p$, this integral can be evaluated to give a [closed-form expression](@entry_id:267458):
$$
c_w = \frac{8}{p+2}
$$
For the AT1 model ($p=1$), $c_w=8/3$, while for a variant of the AT2 model ($p=2$), $c_w=2$.

### Governing Equations from Variational Principles

The equilibrium state of the system $(\boldsymbol{u}, d)$ is found by applying the principle of stationary potential energy, which states that the [first variation](@entry_id:174697) of the total functional $\Pi(\boldsymbol{u}, d)$ must vanish for any admissible variations $\delta \boldsymbol{u}$ and $\delta d$.

$$
\delta \Pi = \frac{\partial \Pi}{\partial \boldsymbol{u}}[\delta \boldsymbol{u}] + \frac{\partial \Pi}{\partial d}[\delta d] = 0
$$

By considering variations with respect to $\boldsymbol{u}$ and $d$ independently, we derive the coupled governing equations.

#### Mechanical Equilibrium

The variation with respect to the [displacement field](@entry_id:141476) $\boldsymbol{u}$ yields the [weak form](@entry_id:137295) of [mechanical equilibrium](@entry_id:148830), also known as the [principle of virtual work](@entry_id:138749). For a test function $\delta\boldsymbol{u}$ that respects the [essential boundary conditions](@entry_id:173524), this is [@problem_id:2587001]:

$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}, d) : \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) \, \mathrm{d\Omega} - \int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d\Omega} - \int_{\partial\Omega_t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}S = 0
$$

Here, $\boldsymbol{b}$ is a [body force](@entry_id:184443) and $\bar{\boldsymbol{t}}$ is a prescribed traction on the Neumann boundary $\partial\Omega_t$. Applying the divergence theorem, one obtains the strong form of the [equilibrium equation](@entry_id:749057), $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}$ in $\Omega$, and the [natural boundary condition](@entry_id:172221) $\boldsymbol{\sigma}\boldsymbol{n} = \bar{\boldsymbol{t}}$ on $\partial\Omega_t$.

#### Phase-Field Evolution

The variation with respect to the phase-field $d$ (with [test function](@entry_id:178872) $\delta d$) yields the evolution equation for damage. Using an AT2 formulation as an example, the variation of the fracture energy is $\int_{\Omega} G_c (d/\ell \cdot \delta d + \ell \nabla d \cdot \nabla \delta d) \, \mathrm{d}\Omega$. Combining this with the variation of the degraded elastic energy, $\int_{\Omega} g'(d) \psi_0 \delta d \, \mathrm{d}\Omega$, and integrating the gradient term by parts yields the strong form of the phase-field equation and its [natural boundary condition](@entry_id:172221) [@problem_id:2587001]:
$$
G_c \left( \frac{d}{\ell} - \ell \Delta d \right) + g'(d) \psi_0 = 0 \quad \text{in } \Omega
$$
$$
\nabla d \cdot \boldsymbol{n} = 0 \quad \text{on } \partial\Omega
$$
The term $g'(d)\psi_0$ is the thermodynamic driving force for fracture; damage increases when the stored elastic energy is sufficient to overcome the resistance posed by the [fracture energy](@entry_id:174458) terms. This balance allows the [phase-field model](@entry_id:178606) to predict a physically meaningful material strength. For instance, in a one-dimensional bar under [uniaxial tension](@entry_id:188287), a stability analysis of the homogeneous state can be performed to find the critical stress $\sigma_c$ at which damage initiates. For the AT2 model with a quadratic degradation function, this yields [@problem_id:2587010, @problem_id:2587016]:
$$
\sigma_c = \frac{3\sqrt{3}}{16}\sqrt{\frac{EG_c}{\ell}}
$$
This expression shows how the emergent [material strength](@entry_id:136917) depends on fundamental material properties ($E, G_c$) and the regularization length scale ($\ell$).

### Irreversibility and Time-Discretized Evolution

Fracture is a dissipative process; once a crack forms, it cannot heal. This physical constraint of **[irreversibility](@entry_id:140985)** must be enforced on the phase-field, i.e., $\dot{d} \ge 0$. In a quasi-static, time-discretized setting, this translates to the condition that the damage at the current time step, $d_n$, must be greater than or equal to the damage at the previous step, $d_{n-1}$.

To properly handle this in the context of loading and unloading, the damage driving force cannot be the current elastic energy $\psi^+(\boldsymbol{\varepsilon}(\boldsymbol{u}_n))$, as this would allow for "healing" if the load were reduced. Instead, [damage evolution](@entry_id:184965) is driven by the maximum tensile energy experienced up to that point in time. This is achieved by introducing a **history field** $H$ [@problem_id:2586983, @problem_id:2586959]:

$$
H_n(\boldsymbol{x}) = \max_{\tau \le t_n} \psi^{+}(\boldsymbol{\varepsilon}(\boldsymbol{u}(\boldsymbol{x}, \tau)))
$$

In the incremental problem for finding $(\boldsymbol{u}_n, d_n)$, the term $\psi^{+}(\boldsymbol{\varepsilon}(\boldsymbol{u}_n))$ in the phase-field equation is replaced by the known history field $H_n$. The problem for $d_n$ then becomes one of minimizing the energy functional subject to the inequality constraint $d_n \ge d_{n-1}$. This leads to a **[variational inequality](@entry_id:172788)** rather than an equality for the phase-field weak form [@problem_id:2586983].

For simple cases, such as the local (0D) problem at a single material point, this constrained minimization problem can be solved in [closed form](@entry_id:271343). For an AT2 model, the incremental energy to be minimized is a convex quadratic function of $d$. The unconstrained minimizer $d_{\text{unc}}$ can be found by setting the derivative to zero. The constrained solution $d_n^\star$ is then the projection of $d_{\text{unc}}$ onto the admissible set $[d_{n-1}, 1]$. This results in the update rule [@problem_id:2586971]:

$$
d_n^\star = \max\left(d_{n-1}, d_{\text{unc}}\right) = \max\left(d_{n-1}, \frac{2 H_n \ell}{2 H_n \ell + G_c}\right)
$$
This expression elegantly captures the essence of irreversible [damage evolution](@entry_id:184965): the damage either stays the same or increases to a new value determined by the peak load experienced.

### Numerical Implementation and Advanced Concepts

The weak forms of the governing equations are the foundation for the Finite Element Method (FEM). The continuous fields $\boldsymbol{u}$ and $d$ are discretized using shape functions, transforming the partial differential equations into a system of coupled, nonlinear algebraic equations for the nodal degrees of freedom.

#### Finite Element Discretization

The bilinear form of the phase-field weak equation, $a(d, w) = \int_{\Omega} (G_c \ell \nabla d \cdot \nabla w + \frac{G_c}{\ell} d w) \mathrm{d}x$, gives rise to the element "stiffness" matrix for the phase-field problem. For a 1D linear element of length $h$, the gradient term contributes a matrix proportional to $\frac{G_c \ell}{h}$, while the mass-like term contributes a matrix proportional to $\frac{G_c h}{\ell}$. Assembling these for an interior node reveals how the discrete operator depends on material parameters ($G_c, \ell$) and the mesh size ($h$) [@problem_id:2587020].

#### Solution Strategies

Solving the coupled nonlinear system for displacements and phase-field can be approached in two main ways [@problem_id:2586966]:
1.  **Monolithic Solvers**: These methods solve for all unknowns $(\boldsymbol{U}, \boldsymbol{D})$ simultaneously, typically using a Newton-Raphson method. This requires the assembly of the full tangent (Jacobian) matrix, including the off-diagonal coupling blocks $\boldsymbol{K}_{ud}$ and $\boldsymbol{K}_{du}$. When the full, consistent tangent is used, Newton's method exhibits local [quadratic convergence](@entry_id:142552), which is robust and efficient. This approach is particularly advantageous for strongly coupled problems, such as [ductile fracture](@entry_id:161045) where [damage and plasticity](@entry_id:203986) are intertwined [@problem_id:2586966].
2.  **Staggered Solvers**: Also known as alternate minimization, these methods solve the mechanical and phase-field problems sequentially and iteratively within each time step. One solves for $\boldsymbol{U}_{k+1}$ holding $\boldsymbol{D}_k$ fixed, then solves for $\boldsymbol{D}_{k+1}$ holding $\boldsymbol{U}_{k+1}$ fixed. This procedure is equivalent to a block Gauss-Seidel iteration and is often easier to implement as it decouples the large system into smaller, potentially linear or simpler nonlinear problems. However, its convergence is only linear and is conditional upon the spectral radius of the [iteration matrix](@entry_id:637346) being less than one. For models where the [energy functional](@entry_id:170311) is separately convex in $\boldsymbol{u}$ and $d$, the staggered scheme is guaranteed to be energy-dissipating with each iteration, which promotes stability [@problem_id:2586966].

#### Rate-Dependent Formulations

While the variational approach described above is rate-independent, a **viscous** or **rate-dependent** regularization is often introduced for the phase-field evolution. This can be for physical reasons (modeling viscous fracture) or for numerical regularization, improving the stability and convergence of the solver. In this framework, one defines a dissipative microforce $\pi^d = \eta \dot{d}$, where $\eta$ is a viscosity parameter. The local [dissipation rate](@entry_id:748577) density is then $\mathcal{D} = \eta \dot{d}^2$. The [microforce balance](@entry_id:202908) yields an [ordinary differential equation](@entry_id:168621) for the [damage evolution](@entry_id:184965), for example, $\eta \dot{d} = (1-d)E\varepsilon^2 - \frac{G_c}{\ell}d$ for a spatially uniform state [@problem_id:2586975]. This transforms the problem from a [variational inequality](@entry_id:172788) to a system of [differential-algebraic equations](@entry_id:748394).

#### Mesh Dependency and Regularization

A central purpose of the [phase-field model](@entry_id:178606) is to act as a regularization technique, mitigating the [pathological mesh dependence](@entry_id:183356) that plagues local continuum damage models. The length scale $\ell$ is the key.
- For [brittle fracture](@entry_id:158949), treating $\ell$ as a fixed material parameter and refining the mesh such that the element size $h$ is significantly smaller than $\ell$ (e.g., $h \le \ell/2$) leads to mesh-objective results for both the global response and the crack path geometry [@problem_id:2586965].
- A common pitfall is to set $\ell$ proportional to $h$. This leads to a model where the predicted material strength diverges as the mesh is refined, failing to converge to a physically meaningful solution [@problem_id:2586965].
- For efficiency, **[adaptive mesh refinement](@entry_id:143852) (AMR)** is a powerful strategy. The mesh is refined only in the vicinity of the crack path, guided by an [error indicator](@entry_id:164891) based on the phase-field gradient. This delivers mesh-independent results with a fraction of the computational cost of a uniformly fine mesh [@problem_id:2586965].
- In the context of **[ductile fracture](@entry_id:161045)**, where plasticity and damage are coupled, the phase-field regularization of damage is often not sufficient. If the underlying plasticity model exhibits local softening, it introduces its own source of [mesh dependency](@entry_id:198563). A robust, mesh-objective simulation of [ductile fracture](@entry_id:161045) requires the regularization of all softening mechanisms, for instance, by coupling a phase-field damage model with a nonlocal plasticity model [@problem_id:2586965].