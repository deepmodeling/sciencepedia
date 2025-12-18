## Introduction
Predicting the initiation and propagation of fractures is a central challenge in [computational mechanics](@entry_id:174464), particularly in fields like [geomechanics](@entry_id:175967) where complex crack networks govern [material failure](@entry_id:160997). Traditional methods struggle with the geometric complexity of tracking sharp, evolving discontinuities. The [phase-field method](@entry_id:191689) offers an elegant and powerful alternative by reformulating the fracture problem within a continuous variational framework, treating cracks as diffuse damage zones. This approach circumvents the need for explicit crack tracking, allowing for the natural simulation of [crack nucleation](@entry_id:748035), branching, and coalescence. This article provides a comprehensive overview of the [phase-field method](@entry_id:191689) for fracture. We will begin in **Principles and Mechanisms** by constructing the model from its energetic foundations in Griffith's theory and exploring its core constitutive components. Next, in **Applications and Interdisciplinary Connections**, we will demonstrate its utility by examining its role in solving complex geomechanical problems like [hydraulic fracturing](@entry_id:750442) and its coupling with other physical phenomena. Finally, the **Hands-On Practices** section will offer opportunities to solidify theoretical understanding through targeted analytical and computational exercises.

## Principles and Mechanisms

This chapter details the foundational principles and constitutive mechanisms that underpin the [phase-field modeling](@entry_id:169811) of fracture. We begin by revisiting the classical energetic theory of [brittle fracture](@entry_id:158949), which [phase-field methods](@entry_id:753383) aim to regularize. We then construct the [phase-field model](@entry_id:178606) from its core components, explore significant variations and their physical implications, and conclude with a discussion of the critical numerical principles required for a robust and objective computational implementation.

### The Variational Basis: From Griffith's Theory to Phase-Field Regularization

The modern [variational approach to fracture](@entry_id:203472) is rooted in the seminal work of Griffith, who reformulated the problem of [crack propagation](@entry_id:160116) not as a local stress condition, but as a global competition between two forms of energy. For a brittle elastic body occupying a domain $\Omega$, the **Griffith [energetic formulation](@entry_id:199250)** posits that the state of the system—defined by the displacement field $\boldsymbol{u}$ and the crack set $\Gamma$—is one that minimizes the [total potential energy](@entry_id:185512) of the system . This total energy, $\Psi(\boldsymbol{u}, \Gamma)$, is the sum of the stored [elastic strain energy](@entry_id:202243) and the energy required to create the crack surfaces:

$$
\Psi(\boldsymbol{u}, \Gamma) = \int_{\Omega \setminus \Gamma} \psi_e(\boldsymbol{\varepsilon}(\boldsymbol{u})) \, d\mathbf{x} + \int_{\Gamma} G_c \, dS
$$

Here, $\psi_e(\boldsymbol{\varepsilon}(\boldsymbol{u}))$ is the [elastic strain energy](@entry_id:202243) density, a function of the small strain tensor $\boldsymbol{\varepsilon}(\boldsymbol{u})$. The second term represents the fracture energy, where $G_c$ is the **critical [energy release rate](@entry_id:158357)** or **[fracture toughness](@entry_id:157609)**, a material constant with units of energy per unit area, and the integral is taken over the $(n-1)$-dimensional crack surface $\Gamma$. A crack propagates when the release of stored elastic energy from an incremental crack advance is sufficient to pay the energetic price $G_c$ for the newly created surface area.

This formulation is powerful but presents formidable challenges for both analytical and computational treatments. The crack set $\Gamma$ is a geometric object of lower dimension than the domain, a sharp discontinuity whose location is not known *a priori*. Tracking its complex evolution, including initiation, branching, and merging, within a standard [continuum mechanics](@entry_id:155125) framework is exceptionally difficult.

The [phase-field method](@entry_id:191689) circumvents this difficulty by regularizing the sharp crack topology. Instead of representing the crack as a discrete surface, it is described by a continuous [scalar field](@entry_id:154310), $d(\mathbf{x})$, often called the **phase field** or **damage field**. This field varies smoothly from $d=0$ in the intact material to $d=1$ in the fully fractured regions. The sharp geometric discontinuity is thus replaced by a diffuse transition zone of finite width, rendering the problem amenable to standard numerical methods like the Finite Element Method.

### The Ambrosio–Tortorelli Approximation of Fracture Energy

The mathematical heart of the [phase-field fracture](@entry_id:178059) model is the approximation of the Griffith surface [energy integral](@entry_id:166228), $G_c \mathcal{H}^{n-1}(\Gamma)$ (where $\mathcal{H}^{n-1}$ is the Hausdorff measure), with a volume integral involving the phase field $d$ and its gradient. This is achieved using a functional of the type proposed by Ambrosio and Tortorelli in the context of [image segmentation](@entry_id:263141). The fracture energy functional, $\Psi_c$, takes the form:

$$
\Psi_c(d) = G_c \int_{\Omega} \gamma_\ell(d, \nabla d) \, d\mathbf{x}
$$

where $\gamma_\ell(d, \nabla d)$ is the crack [surface density](@entry_id:161889) functional. A widely used and variationally consistent form is given by :

$$
\gamma_\ell(d, \nabla d) = \frac{1}{c_w} \left( \frac{w(d)}{\ell} + \ell |\nabla d|^2 \right)
$$

This functional contains several key components:
- The **length scale parameter** $\ell$ is a positive constant with dimensions of length. It is a model parameter, not a numerical one, that dictates the width of the regularized crack band. As we will see, the crack profile typically decays over a characteristic length proportional to $\ell$ .
- The **gradient energy term**, $\ell |\nabla d|^2$, penalizes spatial variations in the phase field. This term ensures that the transition from intact ($d=0$) to broken ($d=1$) remains localized within a narrow band, preventing damage from diffusing non-physically throughout the domain.
- The **local energy term**, $w(d)/\ell$, penalizes states of partial damage ($0  d  1$). The function $w(d)$ is a potential, typically satisfying $w(0)=0$ and $w(d) > 0$ for $d>0$.
- The **normalization constant** $c_w$ is crucial for ensuring the energetic consistency of the approximation. The phase-field energy $\Psi_c(d)$ must converge to the Griffith energy $G_c \mathcal{H}^{n-1}(\Gamma)$ in the sharp-interface limit, i.e., as $\ell \to 0$. This property, known as **$\Gamma$-convergence**, is guaranteed only if the energy of a one-dimensional optimal transition profile is correctly calibrated. This calibration yields $c_w = 2 \int_0^1 \sqrt{w(s)} \, ds$. For a common choice $w(d) = d^2$, this gives $c_w=1$ .

### The Coupled System: Degrading Elastic Energy

To complete the model, the phase field must be coupled to the mechanical deformation. This is achieved by making the elastic strain energy dependent on the damage state. The elastic energy of the damaged material, $\Psi_e$, is written as:

$$
\Psi_e(\boldsymbol{u}, d) = \int_\Omega \psi_e(\boldsymbol{\varepsilon}(\boldsymbol{u}), d) \, d\mathbf{x} = \int_\Omega g(d) \psi_0(\boldsymbol{\varepsilon}(\boldsymbol{u})) \, d\mathbf{x}
$$

where $\psi_0(\boldsymbol{\varepsilon})$ is the [strain energy density](@entry_id:200085) of the pristine, undamaged material. The **degradation function**, $g(d)$, models the loss of stiffness as the material cracks. It is a monotonically decreasing function satisfying $g(0)=1$ (undamaged stiffness) and $g(1)=0$ (no stiffness). A common choice is a quadratic function, e.g., $g(d)=(1-d)^2$.

In practice, setting $g(1)=0$ would cause the [stiffness matrix](@entry_id:178659) in a numerical simulation to become singular in fully cracked regions, leading to ill-conditioning and solver failure. To prevent this, a small **residual stiffness**, $\kappa \ll 1$, is introduced, such that $g(d) = (1-d)^2 + \kappa$ or similar forms with $g(1)=\kappa > 0$. This ensures the problem remains numerically well-posed without significantly affecting the physical response .

The [total potential energy](@entry_id:185512) of the phase-field system is the sum of the degraded elastic energy and the regularized [fracture energy](@entry_id:174458):

$$
\Psi(\boldsymbol{u}, d) = \int_\Omega \left( g(d) \psi_0(\boldsymbol{\varepsilon}(\boldsymbol{u})) + G_c \gamma_\ell(d, \nabla d) \right) \, d\mathbf{x}
$$

The evolution of the system is found by seeking [stationary points](@entry_id:136617) of this functional with respect to both the displacement field $\boldsymbol{u}$ and the phase field $d$.

### Constitutive Choices: AT1 and AT2 Models and Emergent Strength

The choice of the local potential $w(d)$ in the crack [surface density](@entry_id:161889) has profound consequences for the model's behavior, particularly concerning the initiation of damage. The two most common choices are known as the AT2 and AT1 models.

- The **AT2 model** uses a quadratic potential, $w(d) = d^2$. Since $w'(0)=0$, an analysis of the local [energy balance](@entry_id:150831) shows that there is no positive energy threshold for damage to initiate. Any amount of [elastic strain energy](@entry_id:202243) will cause a small amount of damage to develop. The potential is strictly convex, leading to a gradual onset of fracture .

- The **AT1 model** uses a [linear potential](@entry_id:160860), $w(d) = d$. In this case, $w'(0)=1$, which results in a positive [damage initiation](@entry_id:748159) threshold. The material behaves elastically up to a critical [strain energy density](@entry_id:200085), beyond which damage initiates abruptly. This corresponds to a model with a finite tensile strength and is often considered more representative of brittle behavior. The potential is convex but not strictly convex .

The connection between the abstract model parameters ($E, G_c, \ell$) and a material's measurable tensile strength can be made explicit by analyzing a 1D stationary profile. By solving the Euler-Lagrange equations for the [phase-field model](@entry_id:178606) under uniform tension, one can derive the cohesive law—the relationship between traction and opening displacement—that is implicitly encoded in the formulation. This analysis reveals that the peak traction, or tensile strength $t_{max}$, is an emergent property of the model, typically scaling as $t_{max} \propto \sqrt{EG_c/\ell}$. For the same material properties ($E, G_c$), the AT1 and AT2 models predict different strengths, and thus require different length scale parameters ($\ell$) to match a measured tensile strength of a real material like rock .

### Application to Geomaterials: Energy Splitting and Mixed-Mode Fracture

Geomaterials typically exhibit starkly different behavior in tension and compression. Cracks open and propagate under tension, but close and can transmit compressive stresses. A model that degrades the total elastic energy indiscriminately would incorrectly predict [stiffness degradation](@entry_id:202277) and [damage evolution](@entry_id:184965) under pure hydrostatic compression, a state that should not cause fracture.

To model this **unilateral behavior**, the elastic strain energy density, $\psi_0$, is split into a **tensile part**, $\psi_0^+$, and a **compressive part**, $\psi_0^-$. Only the tensile part, which is responsible for driving cracks, is degraded by the phase field:

$$
\psi_e(\boldsymbol{\varepsilon}, d) = g(d)\psi_0^+(\boldsymbol{\varepsilon}) + \psi_0^-(\boldsymbol{\varepsilon})
$$

Several strategies exist for this decomposition :
- A **spectral split** decomposes the [strain tensor](@entry_id:193332) $\boldsymbol{\varepsilon}$ into its principal components and defines $\psi_0^+$ based on the energy contribution from positive (tensile) [principal strains](@entry_id:197797). This method can predict fracture under uniaxial compression due to lateral expansion (positive transverse strains).
- A **volumetric-deviatoric split** decomposes the strain into its volumetric (dilatational) and deviatoric (shear) parts. A common approach for [brittle fracture](@entry_id:158949) is to degrade the deviatoric energy and the tensile part of the volumetric energy.

This concept of [energy splitting](@entry_id:193178) is the gateway to modeling **[mixed-mode fracture](@entry_id:182261)**. Fracture modes II (in-plane shear) and III (out-of-plane tearing) are driven by shear stresses. To capture these phenomena, the model must allow for the degradation of shear stiffness. Degrading the deviatoric part of the elastic energy naturally achieves this. The model's response to mixed-mode loading can be further refined by making the [fracture toughness](@entry_id:157609) $G_c$ a function of the **mode-mixity angle** $\psi$, a measure of the ratio of shear to opening energy release rates, e.g., $\psi = \arctan\left(\sqrt{(G_{II}+G_{III})/G_{I}}\right)$. This allows the model to capture the experimental observation that many materials are tougher in shear than in tension . For problems involving fracture under confinement, a further refinement is to introduce frictional dissipation on the regularized crack surfaces.

### The Irreversibility of Fracture

A fundamental physical principle is that fracture is an irreversible, dissipative process: once formed, a crack cannot heal. The variational framework based on simple [energy minimization](@entry_id:147698) does not inherently enforce this. If the load were reduced, a simple minimization of the total energy might predict a decrease in $d$, corresponding to unphysical healing. Therefore, the **[irreversibility](@entry_id:140985) constraint**, $\dot{d}(\mathbf{x}, t) \ge 0$ (or its time-discrete counterpart $d_n \ge d_{n-1}$), must be explicitly enforced in any quasi-static simulation.

Three common strategies for enforcing this constraint are :
1.  **History Field**: This elegant and robust approach redefines the driving force for damage. Instead of the current [strain energy](@entry_id:162699) $\psi_0^+$, the evolution of $d$ is driven by a history field $\mathcal{H}(\mathbf{x},t) = \max_{s \le t} \psi_0^+(\mathbf{x}, s)$, which stores the maximum driving energy ever experienced at a point. Since $\mathcal{H}$ is non-decreasing by definition, damage is automatically irreversible. This method avoids explicit constraints in the numerical solver.
2.  **Lagrange Multipliers**: This method enforces the inequality constraint $d_n - d_{n-1} \ge 0$ exactly by introducing a Lagrange multiplier field. It is variationally exact and energetically consistent but transforms the minimization problem into a more complex [saddle-point problem](@entry_id:178398), requiring specialized solvers (e.g., [active-set methods](@entry_id:746235)).
3.  **Penalization**: This technique adds a penalty term to the energy functional that penalizes violations of the constraint (e.g., a term proportional to $\langle d_{n-1} - d_n \rangle_+^2$). It is simpler to implement than the Lagrange multiplier method but enforces the constraint only approximately and can lead to severe [ill-conditioning](@entry_id:138674) of the numerical system as the penalty parameter is increased.

### From Continuous Model to Discrete Computation: Objectivity and Convergence

A correct computational implementation of the [phase-field model](@entry_id:178606) must yield results that are independent of the arbitrary choices of the [numerical discretization](@entry_id:752782), a property known as **mesh objectivity**. The key to achieving this lies in understanding the distinct roles of the physical length scale $\ell$ and the numerical mesh size $h$ .

- The internal length $\ell$ is a parameter of the physical model. It sets the width of the [fracture process zone](@entry_id:749561). Changing $\ell$ changes the model and its predictions (e.g., the emergent tensile strength).
- The mesh size $h$ is a parameter of the [numerical discretization](@entry_id:752782). It controls the resolution of the approximation. Changing $h$ should, for a convergent scheme, lead to a more accurate solution of the *same* physical problem defined by $\ell$.

For the numerical solution to be objective, the mesh must be fine enough to resolve the physical features of the model. Since the phase field varies over a characteristic length $\ell$, this imposes a critical resolution requirement: **the mesh size $h$ must be significantly smaller than the length scale $\ell$**. In the limit of [mesh refinement](@entry_id:168565), this is expressed as $h/\ell \to 0$ . Schemes that violate this, for instance by coupling the parameters (e.g., setting $h=\ell$), reintroduce the [pathological mesh dependence](@entry_id:183356) that variational [phase-field methods](@entry_id:753383) were designed to eliminate.

The full power of the [phase-field method](@entry_id:191689) is realized through a two-step convergence process, which is formalized by the mathematical theory of $\Gamma$-convergence :
1.  **Convergence to the Regularized Solution**: For a *fixed* length scale $\ell  0$, refining the mesh such that $h \to 0$ causes the discrete numerical solution to converge to the exact solution of the continuous regularized phase-field problem. The computed crack will have a width of order $\mathcal{O}(\ell)$.
2.  **Convergence to the Sharp-Crack Solution**: As the length scale is made progressively smaller, $\ell \to 0$, *while simultaneously refining the mesh to maintain the resolution condition* $h/\ell \to 0$, the solution of the regularized problem converges to the solution of the original, sharp-interface Griffith fracture problem.

This dual-limit process ensures that [phase-field models](@entry_id:202885) provide a robust, objective, and physically consistent framework for simulating the complex evolution of fractures in [geomaterials](@entry_id:749838) and other brittle solids.