## Introduction
Modeling the initiation and growth of cracks is a fundamental challenge in solid mechanics, critical for ensuring the safety and reliability of engineering structures. Classical fracture mechanics excels at predicting the behavior of pre-existing, well-defined cracks but struggles with complex scenarios involving the nucleation of new cracks, branching, and [coalescence](@entry_id:147963). The [phase-field method](@entry_id:191689) addresses this gap by recasting the sharp, discontinuous problem of fracture into a continuous one, governed by a unified [variational principle](@entry_id:145218) of energy minimization. This approach provides a powerful and versatile framework for simulating complex fracture patterns without ad-hoc criteria.

This article provides a comprehensive overview of [phase-field fracture modeling](@entry_id:193245), guiding the reader from foundational theory to practical application. The first chapter, **Principles and Mechanisms**, deconstructs the core energy functional, explaining how stored elastic energy and [fracture energy](@entry_id:174458) are modeled, and derives the critical criteria for [crack nucleation](@entry_id:748035) and propagation. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the framework's adaptability by exploring extensions to [ductile fracture](@entry_id:161045), [anisotropic materials](@entry_id:184874), and [coupled multiphysics](@entry_id:747969) problems. Finally, the **Hands-On Practices** chapter provides concrete exercises to solidify the theoretical concepts and bridge the gap to numerical implementation. We will begin by exploring the [variational formulation](@entry_id:166033) that lies at the heart of this elegant and powerful theory.

## Principles and Mechanisms

The phase-field approach to fracture mechanics recasts the complex problem of evolving discontinuities into a more tractable continuum problem governed by a [variational principle](@entry_id:145218). At its core, the method posits that the total energy of a body containing cracks is minimized at every stage of its quasi-static evolution. This total [energy functional](@entry_id:170311), $\Psi$, is the central object of the theory, and its careful construction dictates the model's physical and mathematical behavior. This chapter will deconstruct this functional, explaining the principles behind each of its components and the mechanisms that govern [crack nucleation](@entry_id:748035) and propagation.

### The Variational Formulation of Fracture

The total energy of a system comprising an elastic body in domain $\Omega$ is expressed as a functional of the displacement field $\boldsymbol{u}$ and a scalar phase-field variable $d$. This phase-field, $d(\boldsymbol{x}, t)$, is a continuous field defined over the body, where $\boldsymbol{x}$ is a point in the material and $t$ is time. It serves as an order parameter describing the integrity of the material: $d=0$ represents the pristine, undamaged state, while $d=1$ signifies a fully fractured state. Intermediate values $d \in (0,1)$ represent partial damage.

The total energy $\Psi$ is composed of two primary contributions: the stored elastic energy within the bulk of the material and the energy dissipated in the creation of new fracture surfaces. The general form is:

$$
\Psi[\boldsymbol{u}, d] = \int_{\Omega} \psi_e(\boldsymbol{\varepsilon}(\boldsymbol{u}), d) \, \mathrm{d}V + \int_{\Omega} \psi_f(d, \nabla d) \, \mathrm{d}V
$$

Here, $\psi_e$ is the elastic strain energy density, which is degraded by the presence of damage, and $\psi_f$ is the fracture energy density, which penalizes the formation of cracks. The strain tensor is the standard [small-strain tensor](@entry_id:754968) $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top})$. The following sections detail the physical principles underpinning the specific forms of $\psi_e$ and $\psi_f$.

### Modeling Stored Energy: Degradation and Asymmetry

The presence of damage, such as micro-cracks and voids, reduces a material's ability to store elastic energy. The [phase-field model](@entry_id:178606) captures this by degrading the elastic energy density of the pristine material, $\psi_0(\boldsymbol{\varepsilon})$, through a **degradation function**, $g(d)$.

#### The Degradation Function

The degradation function $g(d)$ modulates the stiffness of the material. For a well-posed and physically realistic model, $g(d)$ must satisfy a set of essential mathematical and physical constraints [@problem_id:3587475]:

1.  **Normalization:** At the undamaged state ($d=0$), the material must possess its full stiffness. Thus, $g(0) = 1$.
2.  **Residual Stiffness:** At the fully broken state ($d=1$), the material should have negligible or zero stiffness. To avoid numerical issues like ill-conditioning of the [stiffness matrix](@entry_id:178659), it is common to retain a small residual stiffness, controlled by a parameter $\kappa \ll 1$. This condition is expressed as $g(1) = \kappa$. If $\kappa=0$, the material loses all load-[bearing capacity](@entry_id:746747).
3.  **Monotonic Degradation:** As damage increases, stiffness should not increase. This requires the function to be monotonically decreasing: $g'(d) \le 0$ for all $d \in [0,1]$.
4.  **Convexity:** For stable material behavior and well-posedness of the governing equations, the degradation should not occur too abruptly. A common requirement is that the degradation curve be convex, meaning $g''(d) \ge 0$. This ensures that the energy landscape does not contain features that promote unstable, mesh-dependent solutions.
5.  **Consistent Nucleation:** To ensure that there is a driving force for damage to initiate from the pristine state ($d=0$) under tensile loading, the slope of the degradation function at the origin must be strictly negative, i.e., $g'(0) \lt 0$.

A function that satisfies all these criteria is the quadratic form, widely used in fracture modeling:

$$
g(d) = (1-d)^2(1-\kappa) + \kappa
$$

When $\kappa$ is taken to be zero for simplicity, this reduces to $g(d) = (1-d)^2$. This quadratic form is convex and satisfies all the necessary conditions for a stable model. Other choices, such as a linear function $g(d) = (1-d)(1-\kappa) + \kappa$, also satisfy these conditions, but the quadratic form is often favored for its smooth degradation behavior. Functions that are not convex, such as $g(d) = \kappa + (1-\kappa)(1-d^2)$, can lead to instabilities and are generally avoided [@problem_id:3587475].

#### Tension-Compression Asymmetry

A crucial physical observation for brittle materials like rock or ceramics is that they fail primarily under tension, while they can withstand large compressive stresses. A simple [isotropic damage](@entry_id:750875) model, where the total elastic energy $\psi_0$ is degraded, would predict spurious damage accumulation under high hydrostatic compression. This is unphysical.

To address this, the elastic energy density is split into a **tensile part**, $\psi^+$, and a **compressive part**, $\psi^-$, such that $\psi_0 = \psi^+ + \psi^-$. Only the tensile part, which is responsible for crack opening and growth, is degraded by the phase field. The stored energy density is then written as:

$$
\psi_e(\boldsymbol{\varepsilon}, d) = g(d) \psi^+(\boldsymbol{\varepsilon}) + \psi^-(\boldsymbol{\varepsilon})
$$

A common and effective method to perform this split is through a **[spectral decomposition](@entry_id:148809)** of the [strain tensor](@entry_id:193332) $\boldsymbol{\varepsilon}$ [@problem_id:3587585]. The strain tensor is diagonalized to find its [principal strains](@entry_id:197797) $\varepsilon_i$ and [principal directions](@entry_id:276187) $\boldsymbol{n}_i$. The tensile and compressive parts of the strain tensor, $\boldsymbol{\varepsilon}^+$ and $\boldsymbol{\varepsilon}^-$, are then constructed using the Macaulay bracket notation $\langle x \rangle_+ = \max(x, 0)$ and $\langle x \rangle_- = \min(x, 0)$:

$$
\boldsymbol{\varepsilon}^+ = \sum_{i=1}^{3} \langle \varepsilon_i \rangle_+ \boldsymbol{n}_i \otimes \boldsymbol{n}_i \quad \text{and} \quad \boldsymbol{\varepsilon}^- = \sum_{i=1}^{3} \langle \varepsilon_i \rangle_- \boldsymbol{n}_i \otimes \boldsymbol{n}_i
$$

The energy parts $\psi^+$ and $\psi^-$ are then defined based on these tensors. For an isotropic material with Lamé parameters $\lambda$ and $\mu$, a standard split is:

$$
\psi^+(\boldsymbol{\varepsilon}) = \frac{1}{2}\lambda \langle \mathrm{tr}(\boldsymbol{\varepsilon}) \rangle_+^2 + \mu \boldsymbol{\varepsilon}^+ : \boldsymbol{\varepsilon}^+
$$

$$
\psi^-(\boldsymbol{\varepsilon}) = \psi_0(\boldsymbol{\varepsilon}) - \psi^+(\boldsymbol{\varepsilon})
$$

With this formulation, under a state of pure hydrostatic compression (where all $\varepsilon_i \lt 0$), both $\langle \mathrm{tr}(\boldsymbol{\varepsilon}) \rangle_+$ and $\boldsymbol{\varepsilon}^+$ are zero. This results in $\psi^+ = 0$. Since the driving force for damage is derived from $\psi^+$, no damage will nucleate or grow, correctly capturing the material's behavior. Conversely, under pure shear (e.g., $\varepsilon_1 > 0$, $\varepsilon_2  0$, $\varepsilon_3 = 0$), the tensile [principal strain](@entry_id:184539) ensures that $\psi^+  0$, providing a driving force for fracture, which is also physically correct [@problem_id:3587585].

### Modeling Fracture Energy: Regularization and the Length Scale

In his seminal work, Griffith postulated that creating a new fracture surface requires a specific amount of energy, characterized by the material's toughness, or critical energy release rate, $G_c$. For a sharp crack with surface $\Gamma$, the total [fracture energy](@entry_id:174458) is $W_f = \int_{\Gamma} G_c \, \mathrm{d}A$. Modeling the evolution of this sharp, lower-dimensional surface within a 3D continuum presents significant computational challenges.

The [phase-field method](@entry_id:191689) circumvents this by regularizing the sharp crack energy. The [surface integral](@entry_id:275394) is approximated by a volume integral over a diffuse crack band. This is achieved using a **crack [surface density](@entry_id:161889) functional**, $\gamma(d, \nabla d)$, which depends on both the phase-field value and its gradient. The total fracture energy is then:

$$
\Psi_f[d] = \int_{\Omega} G_c \, \gamma(d, \nabla d) \, \mathrm{d}V
$$

The functional $\gamma$ is carefully constructed to converge to the true surface area as the width of the diffuse band shrinks to zero. A widely-used form is the **Ambrosio–Tortorelli (AT) functional**. For the so-called AT2 model, it is given by:

$$
\gamma(d, \nabla d) = \frac{d^2}{2l} + \frac{l}{2}|\nabla d|^2
$$

This functional introduces a new, crucial parameter: $l$, the **internal length scale**. This parameter dictates the width of the region over which the phase-field transitions from $0$ to $1$. By solving the Euler-Lagrange equation for the 1D fracture [energy functional](@entry_id:170311), one can find the optimal profile of a stationary crack. For the AT2 functional, this profile is an exponential decay [@problem_id:3587565]:

$$
d(x) = \exp(-|x|/l)
$$

This shows that $l$ is the characteristic length of the damage zone. The total [fracture energy](@entry_id:174458) dissipated per unit area for this profile can be calculated by integrating $G_c \gamma(d, \nabla d)$ across the 1D profile, and it can be proven that this integral evaluates to exactly $G_c$ [@problem_id:3587457]. This is a remarkable property: the length scale $l$ controls the width of the smeared crack but not the total energy dissipated, which is solely determined by the material parameter $G_c$.

This property is what grants [phase-field models](@entry_id:202885) **mesh objectivity**. In contrast, simpler local smeared damage models, which lack a gradient term and an internal length scale, suffer from spurious [mesh dependency](@entry_id:198563). In such models, the [fracture energy](@entry_id:174458) localizes to the smallest possible width allowed by the [discretization](@entry_id:145012)—a single row of elements. The total dissipated energy thus becomes proportional to the element size $h$, vanishing as the mesh is refined. To achieve objective results, these local models require ad-hoc regularization, such as scaling the material's softening law by $1/h$ (the [crack band model](@entry_id:748034)) [@problem_id:3587584]. Phase-field models, by incorporating the length scale $l$ directly into the continuum theory, provide a more elegant and robust solution to this problem. For numerical accuracy, the [finite element mesh](@entry_id:174862) size $h$ must be fine enough to resolve the damage profile, typically requiring $h \lesssim l/3$ [@problem_id:3587565].

### Nucleation Criteria: The Onset of Damage

Crack [nucleation](@entry_id:140577) is the process by which damage initiates from a previously intact state. In the phase-field framework, this corresponds to the transition of the phase-field $d$ from $0$ to a positive value. This transition is governed by an energetic criterion derived from the stability of the undamaged state.

The evolution of damage is driven by the release of stored elastic energy. We can define a **local thermodynamic driving force** for damage, $Y$, as the energetic conjugate to the [damage variable](@entry_id:197066) $d$, arising from the degradation of elastic energy:

$$
Y = -\frac{\partial (g(d)\psi^+)}{\partial d}
$$

For the standard choice $g(d)=(1-d)^2$, this yields $Y = 2(1-d)\psi^+$ [@problem_id:3587503]. At the onset of damage from a pristine state ($d=0$), the driving force is simply $Y(0) = 2\psi^+$.

Damage will nucleate if this driving force can overcome the resistance posed by the fracture energy term. The nature of this resistance at $d=0$ depends critically on the choice of the crack [surface density](@entry_id:161889) functional $\gamma(d, \nabla d)$. This leads to different nucleation behaviors for different models [@problem_id:3587477] [@problem_id:3587571]:

-   **AT2 Model:** For $\gamma(d, \nabla d) = \frac{d^2}{2l} + \frac{l}{2}|\nabla d|^2$, the resistance term arising from $\partial \gamma / \partial d$ is $d/l$, which is zero at $d=0$. Consequently, the condition for the loss of stability is simply $Y(0)  0$, or $\psi^+  0$. This implies that any amount of tensile elastic energy creates a driving force for damage. This does not mean the material has zero strength; the gradient term $|\nabla d|^2$ penalizes the formation of damage, and the actual [nucleation](@entry_id:140577) at a structural level occurs at a finite load.

-   **AT1 Model:** An alternative is the AT1 model, where $\gamma(d, \nabla d) = \frac{d}{l} + l|\nabla d|^2$. Here, the resistance term $\partial \gamma / \partial d$ is $1/l$, which is constant and non-zero. The stability criterion becomes a competition between the driving force and this initial resistance: $2\psi^+ \ge G_c/l$. This establishes a clear, finite energy threshold for damage nucleation.

This nucleation threshold can be translated into a critical stress, representing the material's **tensile strength**. For models exhibiting a finite nucleation threshold, a scaling analysis reveals the relationship between strength and the fundamental material parameters. For many standard models, including AT1 and even the regularized behavior of AT2 at a structural level, the critical nucleation stress $\sigma_c$ follows the [scaling law](@entry_id:266186) [@problem_id:3587565] [@problem_id:3587584]:

$$
\sigma_c \propto \sqrt{\frac{E G_c}{l}}
$$

This relationship highlights the dual role of the model parameters. The [fracture toughness](@entry_id:157609) $G_c$ governs the energy required for a crack to *propagate*, while the combination of Young's modulus $E$, toughness $G_c$, and length scale $l$ governs the stress required for a crack to *nucleate*. A tougher material (higher $G_c$) or a material with a smaller [intrinsic length scale](@entry_id:750789) (allowing for sharper cracks) will exhibit a higher tensile strength.

### Propagation Criteria: The Growth of Cracks

Once a crack has nucleated, its subsequent growth is governed by the propagation criterion. This criterion must account for the fundamental physical constraint that fracture is an irreversible, dissipative process.

#### Irreversibility and the History Field

The governing equations for $d$ are derived from the minimization of the energy functional $\Psi$. If the evolution were solely driven by the instantaneous strain energy $\psi^+$, a reduction in load (and thus a decrease in $\psi^+$) could lead to a decrease in $d$ to re-minimize the total energy. This would correspond to unphysical crack healing.

To enforce the **irreversibility constraint**, $\dot{d}(x,t) \ge 0$, the driving force for damage must not decrease upon unloading. This is achieved by replacing the instantaneous tensile energy $\psi^+$ in the evolution law with a non-decreasing **history field**, $H(\boldsymbol{x}, t)$ [@problem_id:3587519]:

$$
H(\boldsymbol{x}, t) = \max_{s \le t} \psi^+(\boldsymbol{\varepsilon}(\boldsymbol{x}, s))
$$

The history field $H$ stores the maximum tensile energy density that a material point has ever experienced. By driving damage with $H$, we ensure that once a certain level of damage has been created by a given load, it remains even if the load is subsequently removed.

#### The KKT Conditions for Evolution

With the introduction of the history field, the complete, rate-independent evolution law for damage is formulated as a [variational inequality](@entry_id:172788). This is most elegantly expressed using the **Karush-Kuhn-Tucker (KKT) conditions**. These conditions state that at any point in the material, the system must satisfy a set of loading-unloading, [irreversibility](@entry_id:140985), and consistency constraints [@problem_id:3587457].

Let the driving force be $Y = 2(1-d)(1-\kappa)H$ (using the more general degradation function) and the resistance operator be $\mathcal{L}d = \frac{d}{l} - l \Delta d$. The KKT conditions are:

1.  **Loading-Unloading:** $Y - G_c \mathcal{L}d \le 0$
2.  **Irreversibility:** $\dot{d} \ge 0$
3.  **Complementary Slackness:** $(Y - G_c \mathcal{L}d) \dot{d} = 0$

These three conditions fully define the propagation criterion. The first states that the net driving force for damage cannot be positive. The third, the complementary condition, is the key: it dictates that damage can only increase ($\dot{d}  0$) at points where the driving force exactly balances the material's resistance ($Y = G_c \mathcal{L}d$). At all other points, either the driving force is less than the resistance and damage is arrested ($\dot{d}=0$), or the point is unloading and damage is also arrested.

### Connection to Classical Fracture Mechanics

A robust [phase-field model](@entry_id:178606) must be consistent with the established theories of Linear Elastic Fracture Mechanics (LEFM) in the appropriate limit. The model is constructed such that in the limit of the internal length scale approaching zero, $l \to 0$, the diffuse phase-field solution $\Gamma$-converges to the sharp-crack solution of Griffith's theory [@problem_id:3587526].

A practical consequence of this convergence is the recovery of classical propagation criteria. For a steadily advancing crack in a phase-field simulation, the macroscopic [energy release rate](@entry_id:158357), $G$, which can be computed using the path-independent **$J$-integral**, will be equal to the material's [fracture toughness](@entry_id:157609), $G_c$. That is, the model satisfies the Griffith criterion $G = G_c$ [@problem_id:3587457]. The $J$-integral itself is a measure of the [configurational force](@entry_id:187765) acting on the crack tip, derived from the Eshelby energy-momentum tensor. The fact that the phase-field formulation recovers this classical result provides a powerful validation of the theory and a bridge between the continuum damage approach and the classical energetic arguments of fracture mechanics [@problem_id:3587526].