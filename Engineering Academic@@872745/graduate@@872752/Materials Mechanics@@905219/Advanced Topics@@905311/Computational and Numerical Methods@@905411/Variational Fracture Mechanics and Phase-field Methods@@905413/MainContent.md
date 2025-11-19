## Introduction
Predicting the initiation and propagation of cracks is a central challenge in [materials mechanics](@entry_id:189503) and structural engineering. While classical [linear elastic fracture mechanics](@entry_id:172400) (LEFM) offers powerful tools for analyzing structures with pre-existing cracks, it struggles to address complex scenarios involving arbitrary crack initiation, branching, and [coalescence](@entry_id:147963). To overcome these limitations, a more general paradigm is needed—one that treats fracture not as a special condition but as an emergent outcome of a system's evolution toward a state of lower energy. This article explores such a paradigm: [variational fracture mechanics](@entry_id:196925) and its most powerful computational implementation, the [phase-field method](@entry_id:191689).

This comprehensive guide will equip you with a deep understanding of this modern approach to fracture simulation. The journey is structured into three distinct chapters. First, **Principles and Mechanisms** will lay the theoretical groundwork, starting from Griffith's energetic principle and advancing to the Francfort-Marigo variational framework and its phase-field regularization. We will dissect the key components, from crack [surface density](@entry_id:161889) functionals to strategies for handling [tension-compression asymmetry](@entry_id:201728) and ensuring damage [irreversibility](@entry_id:140985). Next, **Applications and Interdisciplinary Connections** will showcase the method's versatility, demonstrating how it is used to model complex phenomena like [hydraulic fracturing](@entry_id:750442), fatigue, and the brittle-ductile transition, and how it couples seamlessly with thermal, chemical, and electrical fields. Finally, **Hands-On Practices** will provide a series of guided problems designed to solidify your understanding of the core concepts and build practical skills in their numerical implementation.

## Principles and Mechanisms

The classical theory of [linear elastic fracture mechanics](@entry_id:172400) (LEFM) provides a powerful framework for predicting [crack propagation](@entry_id:160116) in brittle materials, centered on the concept of the [stress intensity factor](@entry_id:157604). However, its reliance on a pre-existing crack and its limited applicability to complex geometries, branching, and initiation from smooth surfaces motivate a more general and flexible approach. This chapter delves into the principles of **[variational fracture mechanics](@entry_id:196925)**, which recasts fracture as an [energy minimization](@entry_id:147698) problem, and explores its most powerful numerical implementation: the **[phase-field method](@entry_id:191689)**. This perspective treats [crack nucleation](@entry_id:748035) and propagation not as a special condition to be checked, but as an intrinsic part of the system's evolution, naturally emerging from the competition between stored elastic energy and fracture energy.

### The Energetic Principle of Brittle Fracture

The foundational idea of [variational fracture mechanics](@entry_id:196925), first proposed by A. A. Griffith, is that a crack extends only if the extension process results in a net decrease in the total energy of the system. The total energy is composed of two competing terms: the stored [elastic potential energy](@entry_id:164278) within the body and the [surface energy](@entry_id:161228) required to create new crack faces. A crack grows when the amount of elastic energy released is sufficient to overcome the material's [intrinsic resistance](@entry_id:166682) to fracture.

Let us formalize this for a simple, yet illustrative, case. Consider an infinite, linear elastic plate containing a central through-thickness crack of length $2a$, subjected to a uniform remote tensile stress $\sigma$. The total potential energy of this system, $\Pi$, is the sum of the stored [elastic strain energy](@entry_id:202243), $U$, and the potential of the external loads. For a [quasi-static process](@entry_id:151741), crack advance occurs when the **energy release rate**, $G$, which is the energy made available per unit of new crack area, reaches a critical value, $G_c$. The value $G_c$ is a material property known as the **[fracture energy](@entry_id:174458)** or **critical energy release rate**. The condition for fracture is thus:

$G = G_c$

The energy release rate is formally defined as the negative rate of change of the total potential energy with respect to the crack area, $\mathcal{A}$. For a crack of length $2a$ in a plate of unit thickness, the area is $2a$, so we can write:

$G = -\frac{1}{2}\frac{d\Pi}{da}$

From [elasticity theory](@entry_id:203053), the introduction of a crack of length $2a$ into the infinite plate reduces the potential energy by an amount $\frac{\pi\sigma^2 a^2}{E}$ for plane stress conditions, where $E$ is Young's modulus. The total potential energy can thus be written as $\Pi(a) = \Pi_{\text{uncracked}} - \frac{\pi\sigma^2 a^2}{E}$, where the first term is a constant. Differentiating with respect to $a$ gives the [energy release rate](@entry_id:158357):

$G = -\frac{1}{2} \frac{d}{da} \left( \Pi_{\text{uncracked}} - \frac{\pi\sigma^2 a^2}{E} \right) = \frac{\pi\sigma^2 a}{E}$

At the onset of fracture, we set $G = G_c$. This allows us to solve for the critical stress, $\sigma_c$, at which the crack will propagate [@problem_id:2929085]:

$\sigma_c = \sqrt{\frac{E G_c}{\pi a}}$

This is the celebrated Griffith criterion. Its derivation from a global [energy balance](@entry_id:150831) principle is the cornerstone of [variational fracture mechanics](@entry_id:196925). It transforms fracture from a problem of singular stresses at a [crack tip](@entry_id:182807) into a problem of energy competition, paving the way for more powerful generalizations.

### The Francfort-Marigo Variational Framework

While Griffith's theory is profoundly insightful, it is restricted to the propagation of a single, straight crack. In the late 1990s, G. A. Francfort and J.-J. Marigo proposed a comprehensive variational theory for quasi-static [brittle fracture](@entry_id:158949) that can handle arbitrary crack initiation and complex crack paths.

Their framework considers the total energy of a body occupying a domain $\Omega$ with a crack set $\Gamma$ as:

$\Phi(u, \Gamma) = \int_{\Omega \setminus \Gamma} \psi(\boldsymbol{\varepsilon}(u)) \, \mathrm{d}x - \mathcal{W}_{\text{ext}}(u) + G_c \mathcal{H}^{d-1}(\Gamma)$

Here, $u$ is the displacement field, $\boldsymbol{\varepsilon}(u)$ is the [strain tensor](@entry_id:193332), and $\psi(\boldsymbol{\varepsilon})$ is the elastic energy density. $\mathcal{W}_{\text{ext}}(u)$ represents the work done by external loads. The crucial new term is the surface energy, $G_c \mathcal{H}^{d-1}(\Gamma)$, where $\mathcal{H}^{d-1}$ is the $(d-1)$-dimensional Hausdorff measure of the crack set $\Gamma$ (i.e., its length in 2D or area in 3D).

The evolution of the system $(u(t), \Gamma(t))$ is governed by two fundamental principles [@problem_id:2929143]:

1.  **Irreversibility**: Cracks can only grow; they cannot heal. Mathematically, for any two times $s \le t$, the crack set must satisfy $\Gamma(s) \subseteq \Gamma(t)$. This implies that the total crack area, $a(t) = \mathcal{H}^{d-1}(\Gamma(t))$, is a [non-decreasing function](@entry_id:202520) of time: $\dot{a}(t) \ge 0$.

2.  **Global Stability**: At any given time $t$, the current configuration $(u(t), \Gamma(t))$ must be stable. This means the total energy cannot be lowered by any further crack growth. In other words, the partial derivative of the total energy with respect to the crack area $a$ must be non-negative.

From these principles, we can derive the conditions that govern crack evolution. If we define the mechanical [energy release rate](@entry_id:158357) $G(t)$ as the rate of decrease of the elastic and load potential energy with respect to crack area, the stability condition implies that the driving force cannot exceed the material resistance:

$G(t) \le G_c$

Furthermore, for a rate-independent process, crack growth ($\dot{a}(t) > 0$) can only occur when the system is at the critical limit, i.e., when $G(t) = G_c$. If the system is strictly stable ($G(t)  G_c$), no crack growth can occur ($\dot{a}(t) = 0$). These conditions can be elegantly summarized in a set of Karush-Kuhn-Tucker (KKT) conditions:

-   $G(t) \le G_c$ (Stability)
-   $\dot{a}(t) \ge 0$ (Irreversibility)
-   $(G_c - G(t))\dot{a}(t) = 0$ (Complementarity)

This variational framework is extremely powerful, but it presents a formidable computational challenge: one must find the optimal crack path $\Gamma$ among all possible sets within the body, a task involving the minimization of a non-convex functional over a complex space of geometric objects.

### Phase-Field Regularization of Fracture

The [phase-field method](@entry_id:191689) circumvents the difficulties of tracking sharp, evolving crack geometries by regularizing the problem. The core idea is to approximate the lower-dimensional crack set $\Gamma$ with a continuous [scalar field](@entry_id:154310) $d(\boldsymbol{x}, t)$, called the **phase-field** or **damage field**. This field varies smoothly from an "intact" state (e.g., $d=0$) to a "fully broken" state (e.g., $d=1$) over a narrow transition zone whose width is controlled by a small length-scale parameter, $\ell$.

The discontinuous jump in displacement across a sharp crack is thus replaced by a smooth but rapid variation of the displacement field within this transition zone. Most importantly, the surface energy term $G_c \mathcal{H}^{d-1}(\Gamma)$ is replaced by a volume integral that depends on the phase-field and its gradient. This is known as the **Ambrosio-Tortorelli approximation**. The total [energy functional](@entry_id:170311) becomes a function of the continuous fields $u$ and $d$:

$\Pi[u,d] = \int_{\Omega} g(d) \psi_e(\boldsymbol{\varepsilon}(u)) \, \mathrm{d}x + G_c \int_{\Omega} \gamma_\ell(d, \nabla d) \, \mathrm{d}x - \mathcal{W}_{\text{ext}}(u)$

Here, $g(d)$ is a **degradation function** that reduces the [material stiffness](@entry_id:158390) as damage evolves, and $\gamma_\ell(d, \nabla d)$ is the **crack [surface density](@entry_id:161889) functional**. This formulation transforms the geometrically complex problem of finding an optimal crack path into a standard, albeit coupled, system of [partial differential equations](@entry_id:143134) for the fields $u$ and $d$, which can be solved with standard numerical methods like the Finite Element Method (FEM).

To see how this works, consider a simple 1D bar under a prescribed end displacement $\bar{U}$ [@problem_id:2929105]. In the discrete Griffith model, the energy of the intact state is purely elastic, $E_{\text{intact}} = \frac{EA\bar{U}^2}{2L}$, while the energy of the broken state (with zero elastic energy) is the fracture energy, $E_{\text{broken}} = G_c A$. Equating these gives the critical displacement for fracture: $\bar{U}_c = \sqrt{\frac{2LG_c}{E}}$. The [phase-field model](@entry_id:178606) is constructed to replicate this global energy balance. The energy of the intact state ($d \equiv 0$) is identical. The energy of the broken state is given by the [fracture energy](@entry_id:174458) integral, which, by careful construction of $\gamma_\ell$, evaluates to $G_c A$. Thus, the [phase-field model](@entry_id:178606) yields the exact same critical displacement $\bar{U}_c$, demonstrating that it correctly approximates the global energy of the discrete crack system.

### Key Mechanisms of Phase-Field Modeling

The success of the [phase-field method](@entry_id:191689) hinges on the careful definition of its core components: the crack [surface density](@entry_id:161889) and the degradation function.

#### The Crack Surface Density Functional

The crack [surface density](@entry_id:161889) functional, $\gamma_\ell(d, \nabla d)$, is designed such that its volume integral approximates the [surface energy](@entry_id:161228) $G_c \times \text{Area}(\Gamma)$. A common form, known as the AT2 model, is:

$\gamma_\ell(d, \nabla d) = \frac{1}{2\ell} d^2 + \frac{\ell}{2} |\nabla d|^2$

where $d=1$ represents a fully broken state. Another common formulation (often called AT1-style) uses a field $\alpha \in [0,1]$ where $\alpha=0$ is broken and $\alpha=1$ is intact, with a functional like [@problem_id:2929081]:

$\Gamma_\ell[\alpha] = \int_\Omega \left( \frac{1}{4\ell}(1-\alpha)^2 + \ell |\nabla \alpha|^2 \right) \, \mathrm{d}x$

The first term in these functionals penalizes states that are not purely intact or broken, effectively forcing the phase-field to be close to 0 or 1 [almost everywhere](@entry_id:146631). The second term penalizes sharp gradients, thus regularizing the transition and giving the crack its characteristic width, which is proportional to $\ell$.

A fundamental property of these functionals is that when minimized, they yield a total energy that is independent of the regularization length $\ell$. To see this, consider the 1D case of a crack at $x=0$. The governing Euler-Lagrange equation for the phase-field profile can be derived and solved. For the AT2 model with boundary conditions $d(0)=1$ and $d(|x| \to \infty) \to 0$, the optimal profile is an [exponential decay](@entry_id:136762) [@problem_id:2929106]:

$d(x) = \exp(-|x|/\ell)$

Substituting this optimal profile back into the fracture energy integral, $\int_{-\infty}^\infty ( \frac{1}{2\ell} d^2 + \frac{\ell}{2} (d')^2 ) \, dx$, one finds that it evaluates to exactly 1 [@problem_id:2929105, @problem_id:2929106]. Thus, the total [fracture energy](@entry_id:174458) contributed by this term is $G_c \times 1 = G_c$ (per unit area), demonstrating that the model is correctly calibrated and the physics is independent of the non-physical regularization parameter $\ell$. This independence is a crucial property, confirming the method's consistency.

Different choices for the [potential function](@entry_id:268662) within the functional, such as the AT1 model ($w(d)=d$) versus the AT2 model ($w(d)=d^2$), lead to different optimal profiles and regularized energies, but the fundamental principle of $\ell$-independence holds. For instance, the minimized energy of the AT1 model is $4/3$ times that of the AT2 model for the same boundary conditions [@problem_id:2929129], highlighting the importance of correct calibration for each specific model choice.

#### Coupling Elasticity and Damage: Degradation and Asymmetry

The phase-field couples to the mechanical behavior through the **degradation function**, $g(d)$. The elastic energy density $\psi_e$ is degraded by this function, typically as $g(d) \psi_e$. A common choice is a quadratic function $g(d) = (1-d)^2 + \kappa$, where $d=0$ is intact and $d=1$ is broken [@problem_id:2929106, @problem_id:2929127]. Here $g(0)=1$, leaving the intact material's stiffness unchanged, while $g(1)=\kappa$, where $\kappa$ is a small positive constant (e.g., $\kappa = 10^{-6}$) that acts as a **residual stiffness**. This small stiffness prevents the governing equations from becoming singular when a region is fully broken, which aids [numerical stability](@entry_id:146550).

A critical physical consideration is that cracks in most materials are driven by tension, not compression. A material under hydrostatic compression should not fracture. A naive degradation of the total elastic energy would incorrectly predict damage growth under compressive states. To remedy this, the elastic energy density $\psi_e$ is split into a tensile part, $\psi_+$, and a compressive part, $\psi_-$. Only the tensile part is degraded by the phase-field:

$\psi_{\text{degraded}} = g(d)\psi_+ + \psi_-$

Several methods exist to perform this split. A common and robust approach is the **spectral decomposition** of the [strain tensor](@entry_id:193332) $\boldsymbol{\varepsilon}$ [@problem_id:2929056]. First, the [principal strains](@entry_id:197797) $\varepsilon_i$ and corresponding principal directions $\boldsymbol{n}_i$ are found by solving the eigenvalue problem for $\boldsymbol{\varepsilon}$. The [strain tensor](@entry_id:193332) can then be additively decomposed into its tensile and compressive parts:

$\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_+ + \boldsymbol{\varepsilon}_-$ where $\boldsymbol{\varepsilon}_+ = \sum_{i=1}^3 \langle \varepsilon_i \rangle_+ \boldsymbol{n}_i \otimes \boldsymbol{n}_i$

Here, $\langle x \rangle_+ = \max(x, 0)$ is the Macaulay bracket, which isolates the positive (tensile) [principal strains](@entry_id:197797). The tensile energy density $\psi_+$ is then simply the elastic energy evaluated using the tensile [strain tensor](@entry_id:193332), $\psi_+ = \psi_e(\boldsymbol{\varepsilon}_+)$. For an [isotropic material](@entry_id:204616) with Lamé parameters $\lambda$ and $\mu$, this is:

$\psi_+(\boldsymbol{\varepsilon}) = \frac{1}{2} \lambda (\text{tr}(\boldsymbol{\varepsilon}_+))^2 + \mu \, \boldsymbol{\varepsilon}_+ : \boldsymbol{\varepsilon}_+$

For example, given a plane-strain state with [principal strains](@entry_id:197797) $\varepsilon_1 = 0.002$ (tensile) and $\varepsilon_2 = -0.001$ (compressive), the tensile [strain tensor](@entry_id:193332) $\boldsymbol{\varepsilon}_+$ would only contain the component associated with $\varepsilon_1$. The energy density $\psi_+$ would be computed from this tensor and then degraded by $g(d)$ to find the crack-driving energy [@problem_id:2929056]. This procedure ensures that cracks remain closed and do not propagate under compression.

### Governing Equations and Solution Strategies

#### Derivation of the Coupled System

The equilibrium state of the system at any given moment is found by minimizing the [total potential energy](@entry_id:185512) functional $\Pi[u,d]$ with respect to both the displacement field $u$ and the phase-field $d$. This is a standard procedure in the calculus of variations. Taking the [first variation](@entry_id:174697) $\delta\Pi$ and setting it to zero for all admissible variations $\delta u$ and $\delta d$ yields the coupled system of Euler-Lagrange equations.

The variation with respect to displacement, $\delta u$, leads to the **weak form of the momentum balance** equation [@problem_id:2929106]:

$\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\delta u) \, \mathrm{d}x = \int_{\Omega} \boldsymbol{b} \cdot \delta u \, \mathrm{d}x + \int_{\partial\Omega} \boldsymbol{t} \cdot \delta u \, \mathrm{d}S$

where the stress is now a function of damage, $\boldsymbol{\sigma} = \frac{\partial \psi_{\text{degraded}}}{\partial \boldsymbol{\varepsilon}} = g(d) \frac{\partial \psi_+}{\partial \boldsymbol{\varepsilon}} + \frac{\partial \psi_-}{\partial \boldsymbol{\varepsilon}}$. The corresponding strong form is the familiar [equilibrium equation](@entry_id:749057), $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \mathbf{0}$.

The variation with respect to the phase-field, $\delta d$, yields the **[weak form](@entry_id:137295) of the phase-field evolution equation**. After [integration by parts](@entry_id:136350), it leads to the strong form [@problem_id:2929106]:

$-G_c \ell \Delta d + \frac{G_c}{\ell}d - 2(1-d)\psi_+ = 0$

This is for the AT2 model with $g(d)=(1-d)^2$. This equation shows a beautiful balance: the first two terms represent the internal "restoring force" of the phase-field, resisting changes. The last term, $-2(1-d)\psi_+$, is the [thermodynamic driving force for damage](@entry_id:182386), which is proportional to the tensile elastic energy. When $\psi_+$ is large enough, it overcomes the resistance, and the damage field $d$ evolves (increases).

#### Enforcing Irreversibility in Numerical Solutions

When solving the problem incrementally in time, the physical constraint of damage irreversibility, $\dot{d} \ge 0$, must be strictly enforced. If a material is loaded, damaged, and then unloaded, the damage must not "heal". Two primary, thermodynamically consistent strategies are used in numerical implementations [@problem_id:2929139]:

1.  **Monolithic Approach with Inequality Constraints**: At each time step $n$, the condition is enforced directly by requiring $d^n(\boldsymbol{x}) \ge d^{n-1}(\boldsymbol{x})$ for all $\boldsymbol{x}$. The coupled system for $(u^n, d^n)$ is solved simultaneously, subject to this inequality constraint. This transforms the minimization problem into a **[variational inequality](@entry_id:172788)**, which is computationally demanding but robust and [unconditionally stable](@entry_id:146281).

2.  **Staggered Approach with a History Variable**: An alternative is to solve for $u$ and $d$ sequentially in an iterative loop. To enforce [irreversibility](@entry_id:140985) in this scheme, the instantaneous crack-driving energy $\psi_+$ is replaced by a **history variable** $H(\boldsymbol{x}, t)$, defined as the maximum tensile energy experienced at that point up to the current time:

    $H(\boldsymbol{x}, t) = \max_{s \in [0, t]} \psi_+(\boldsymbol{\varepsilon}(\boldsymbol{u}(\boldsymbol{x}, s)))$

    At each time step, one first solves the mechanical problem for $u^n$ and updates the history field: $H^n = \max(H^{n-1}, \psi_+(u^n))$. Then, one solves the phase-field equation using $H^n$ as the driver. Since $H^n$ is by definition non-decreasing, the resulting damage field $d^n$ will also be non-decreasing, thus elegantly satisfying [irreversibility](@entry_id:140985) without an explicit inequality constraint.

Other approaches, such as using [penalty methods](@entry_id:636090) to approximate the inequality or defining history variables based on time integrals of energy, are generally not used as they can violate the [thermodynamic principles](@entry_id:142232) or the rate-independent nature of [brittle fracture](@entry_id:158949) [@problem_id:2929139].

#### Solution Schemes: Monolithic vs. Staggered

The two strategies for enforcing irreversibility correspond to two main classes of numerical solution algorithms.

-   **Monolithic solvers** tackle the full, coupled system of equations for $(u, d)$ at once, typically using a Newton-Raphson method to solve the [nonlinear system](@entry_id:162704) arising from the [variational inequality](@entry_id:172788). This approach is robust and often requires fewer iterations overall, but each iteration is computationally expensive as it involves solving a large, [ill-conditioned matrix](@entry_id:147408) system.

-   **Staggered solvers**, also known as alternate minimization or block Gauss-Seidel schemes, are simpler to implement. At each time step, one iterates between solving the linear elasticity problem for $u$ (with $d$ fixed) and the nonlinear phase-field problem for $d$ (with $u$ fixed and using the history field $H$). The convergence of this iterative scheme depends on the properties of the system. For the simplified 1D model, one can analyze the convergence by calculating the spectral radius $\rho$ of the Gauss-Seidel iteration matrix. The [spectral radius](@entry_id:138984) depends on the [coupling strength](@entry_id:275517) between the $u$ and $d$ fields and is given by an expression of the form [@problem_id:2929127]:

    $\rho = \frac{b^2}{ac} = \frac{4 E u^{2} (1-d)^{2}}{\left((1-d)^{2} + \kappa\right) \left(E u^{2} + \frac{L^{2} G_{c}}{\ell}\right)}$

    where $a, b, c$ are the entries of the system's Hessian matrix. For the iteration to converge, it is necessary that $\rho  1$. This analysis shows that convergence can be slow or may fail when the coupling is strong, for instance, just before crack initiation when the elastic energy $u^2$ is high.

#### Discretization, Regularization, and Convergence

A final, crucial aspect of practical implementation is the interplay between the [finite element mesh](@entry_id:174862) size, $h$, and the phase-field regularization length, $\ell$. For the numerical solution to be accurate, the mesh must be fine enough to resolve the smooth but rapid variation of the phase-field profile over the width $\ell$. A common rule of thumb is to have at least a few elements across the crack width, which implies that the ratio $\ell/h$ must be greater than some value, for instance, $\ell/h > 2$.

A more rigorous analysis can quantify the [numerical error](@entry_id:147272) introduced by the discretization. Using a piecewise-linear finite element interpolation of the exact 1D exponential crack profile, one can compute the discretized fracture energy. This discrete energy is always an overestimation of the true continuum energy. The [relative error](@entry_id:147538) can be found via an [asymptotic expansion](@entry_id:149302) for small mesh sizes [@problem_id:2929090]. For the AT2 model, this relative overestimation is, to leading order:

$E_{\text{rel}} = \frac{\Psi_h - G_c}{G_c} \approx \frac{1}{24} \left(\frac{h}{\ell}\right)^2$

This result is highly significant. It shows that the [numerical error](@entry_id:147272) is directly controlled by the ratio of the mesh size to the regularization length. If a user desires to keep this error below a certain tolerance $\varepsilon$, this formula provides a direct requirement on the mesh design [@problem_id:2929090]:

$\frac{\ell}{h} \ge \frac{1}{\sqrt{24\varepsilon}} = \frac{1}{2\sqrt{6\varepsilon}}$

This establishes a quantitative link between the phase-field parameter $\ell$, which controls the "diffuseness" of the crack, and the computational cost, dictated by the mesh size $h$. A smaller, more physically realistic $\ell$ necessitates a finer mesh and a higher computational cost to maintain accuracy. This trade-off is at the heart of all practical [phase-field fracture](@entry_id:178059) simulations.