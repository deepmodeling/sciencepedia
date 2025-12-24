## Introduction
The ability to accurately predict [material failure](@entry_id:160997) and fracture is a cornerstone of modern engineering and materials science. While classical theories provide a powerful foundation, they often fall short when confronted with the complex process of [damage evolution](@entry_id:184965) and [crack propagation](@entry_id:160116) in many materials. The straightforward application of classical continuum mechanics to materials that soften under load leads to mathematical and numerical pathologies, yielding results that depend on the computational grid rather than intrinsic material properties. This represents a significant knowledge gap that has driven the development of more advanced theoretical frameworks.

This article provides a comprehensive exploration of nonlocal and regularized modeling methods designed to overcome these limitations. It charts a course from the fundamental energetic principles of fracture to the sophisticated continuum theories that govern modern simulations. Across the following chapters, you will gain a robust understanding of this critical field.

*   **Principles and Mechanisms** will first establish why local models fail, introducing the concept of [pathological mesh dependence](@entry_id:183356). It will then systematically detail a range of regularized methods, including Cohesive Zone Models, integral nonlocal theories, Phase-Field models, and Peridynamics, explaining how each introduces an intrinsic length scale to restore physical realism.

*   **Applications and Interdisciplinary Connections** will demonstrate the practical utility of these theories. We will explore their use in engineering [structural integrity](@entry_id:165319), multiscale modeling of [heterogeneous materials](@entry_id:196262), and their surprising application in diverse fields such as [geosciences](@entry_id:749876) and ecology, highlighting the unifying power of nonlocal concepts.

*   **Hands-On Practices** will solidify your understanding through a series of conceptual problems. These exercises are designed to connect the abstract theories to concrete calculations, bridging the gap between microscale physics, continuum-level parameters, and model predictions.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanisms underpinning modern nonlocal and fracture modeling methods. We begin by establishing the classical energetic criterion for fracture, then demonstrate the inherent limitations of local [continuum models](@entry_id:190374) in describing failure, thereby motivating the introduction of nonlocal theories. Subsequently, we will systematically explore a range of regularized methods, including [cohesive zone models](@entry_id:194108), integral-type [nonlocal models](@entry_id:175315), phase-field models, and [peridynamics](@entry_id:191791), each offering a distinct strategy for incorporating a [material length scale](@entry_id:197771) to ensure physically realistic and numerically robust simulations of fracture.

### The Energetic Basis of Fracture: Griffith's Theory

The modern understanding of fracture mechanics begins with the seminal work of A.A. Griffith, who posited that the propagation of a crack is governed by a balance of energy. Specifically, for a crack to extend, the energy released from the elastic body must be sufficient to supply the energy required to create new crack surfaces. This principle can be formalized by considering the **[total potential energy](@entry_id:185512)** of a body-loads system, denoted by $\Pi$.

For a linear elastic body, the total potential energy is defined as the difference between the stored [elastic strain energy](@entry_id:202243), $U$, and the work done by external forces, $W$:
$$
\Pi = U - W
$$
Consider a body containing a pre-existing crack of length $a$. During a quasi-static crack extension of an infinitesimal amount $da$, the total potential energy of the system will change. The **[energy release rate](@entry_id:158357)**, $G$, is defined as the rate of decrease of the [total potential energy](@entry_id:185512) with respect to an increase in crack area. For a two-dimensional body of unit thickness, this is expressed as:
$$
G = - \frac{\partial \Pi}{\partial a}
$$
This derivative is evaluated while holding the externally prescribed boundary conditions fixed (i.e., fixed applied loads or fixed prescribed displacements). The negative sign indicates that energy is *released* as the potential of the system *decreases*. This released energy becomes available to drive the fracture process.

The material's resistance to fracture is quantified by the **critical [energy release rate](@entry_id:158357)**, or **[fracture energy](@entry_id:174458)**, $G_c$. This is a material property representing the energy required to create a unit area of new crack surface. Griffith's criterion for [brittle fracture](@entry_id:158949) states that [crack propagation](@entry_id:160116) occurs when the available [energy release rate](@entry_id:158357) equals the material's [fracture resistance](@entry_id:197108) :
$$
G = G_c
$$
If $G  G_c$, the crack will not grow. This elegant energy balance forms the bedrock of Linear Elastic Fracture Mechanics (LEFM).

### The Breakdown of Local Continuum Models for Softening Materials

While Griffith's theory provides a powerful criterion for a single, discrete crack, practical engineering analysis often requires modeling the process of material degradation and failure within a continuum framework. In such models, failure is often represented by a gradual loss of stiffness, a phenomenon known as **[strain softening](@entry_id:185019)**. A common approach is to introduce a scalar **[damage variable](@entry_id:197066)**, $d \in [0,1]$, where $d=0$ represents the intact material and $d=1$ represents the fully failed state. The stress, $\sigma$, is then related to strain, $\epsilon$, through a degraded elastic modulus, for instance, $\sigma = (1-d)E\epsilon$, where $E$ is the Young's modulus of the intact material.

This seemingly straightforward approach, when implemented within a purely **local constitutive framework** (where the material response at a point depends only on variables at that same point), leads to profound theoretical and numerical difficulties. The core issue is the pathological dependence of the results on the discretization, typically a [finite element mesh](@entry_id:174862).

To understand this, consider a simple one-dimensional bar in tension, modeled with a local [strain-softening](@entry_id:755491) damage law. As the bar is stretched, the strain will not remain uniform. Due to inherent instabilities in the softening regime, any small perturbation will cause strain and damage to concentrate, or **localize**, into a narrow band. In a local continuum model that lacks any [intrinsic length scale](@entry_id:750789), the governing equations permit this localization band to become infinitesimally thin.

When this problem is solved numerically using finite elements of size $h$, the localization band inevitably collapses to the smallest possible width the mesh can resolve: the width of a single element. Thus, the width of the [fracture process zone](@entry_id:749561) becomes $w_{loc} \approx h$.

From a thermodynamic perspective, the total energy dissipated per unit volume, $g_f$, to completely damage a material point is a finite material property. The total energy dissipated by the structure to form a complete crack, $W_{diss}$, is the integral of $g_f$ over the volume of the localization zone, $V_{loc} = A \cdot w_{loc}$, where $A$ is the cross-sectional area. This gives:
$$
W_{diss} = g_f \cdot A \cdot w_{loc} \approx g_f \cdot A \cdot h
$$
This result is physically untenable. It predicts that the energy required to fracture the specimen is proportional to the mesh size $h$. As the mesh is refined ($h \to 0$), the predicted [fracture energy](@entry_id:174458) spuriously vanishes ($W_{diss} \to 0$) . This pathological **[mesh dependence](@entry_id:174253)** renders the predictions of local softening models meaningless, as the structural response depends on the arbitrary choice of discretization rather than the intrinsic properties of the material.

### Regularization through an Intrinsic Material Length Scale

The remedy for this pathological behavior is to enrich the continuum description with an **[intrinsic material length scale](@entry_id:197348)**, typically denoted by $\ell$. This length scale is not an arbitrary numerical parameter but a material property that reflects the finite size of the [fracture process zone](@entry_id:749561), which is dictated by the material's microstructure (e.g., [grain size](@entry_id:161460), aggregate size) or the physical mechanisms of decohesion.

This length scale, $\ell$, represents the characteristic distance over which nonlocal interactions or micromechanical processes occur. Its magnitude can be estimated from fundamental material properties. The classical LEFM stress field near a crack tip is singular, scaling as $\sigma \sim K_{Ic}/\sqrt{r}$, where $K_{Ic}$ is the [fracture toughness](@entry_id:157609) and $r$ is the distance from the tip. This singularity is unphysical and must be truncated at some small scale. If we posit that this truncation occurs when the elastic stress reaches the material's intrinsic tensile strength, $\sigma_c$, we can define the process zone size $\ell$ by the relation :
$$
\sigma_c \sim \frac{K_{Ic}}{\sqrt{\ell}} \implies \ell \sim \left(\frac{K_{Ic}}{\sigma_c}\right)^2
$$
Using the fundamental relationship from LEFM, $K_{Ic}^2 = E' G_c$ (where $E'$ is the plane-strain or plane-stress modulus), we arrive at a crucial scaling law for the intrinsic length:
$$
\ell \sim \frac{E' G_c}{\sigma_c^2}
$$
This relationship shows that the length scale of the [fracture process zone](@entry_id:749561) is determined by the interplay between the material's toughness ($G_c$), stiffness ($E'$), and strength ($\sigma_c$). Incorporating such a length scale into the continuum model is the key to restoring objectivity and obtaining physically meaningful predictions of fracture.

### A Survey of Nonlocal and Regularized Fracture Models

Several classes of models have been developed to introduce an intrinsic length scale and regularize the problem of [strain softening](@entry_id:185019). These models differ in their formulation but share the common goal of ensuring that the simulated fracture process dissipates a finite, mesh-independent amount of energy.

#### Cohesive Zone Models (CZM)

Cohesive Zone Models (CZMs) regularize fracture by replacing the singular crack tip of LEFM with a **[fracture process zone](@entry_id:749561)** of finite length. Within this zone, the crack faces are not traction-free but are bridged by [cohesive forces](@entry_id:274824). The behavior of this zone is described by a **[traction-separation law](@entry_id:170931) (TSL)**, which defines the cohesive traction, $T$, as a function of the crack opening displacement, $\delta$.

A typical TSL, for example a bilinear law, has the following key features :
1.  An initial stiffness, where traction increases with separation.
2.  A peak traction, $T_{max}$, which represents the [cohesive strength](@entry_id:194858) of the material.
3.  A softening branch, where traction decreases as the separation continues to increase.
4.  A critical separation, $\delta_c$, at which the traction vanishes, signifying complete decohesion and the formation of a true, traction-free crack.

Critically, the TSL must be energetically consistent with Griffith's theory. The [irreversible work](@entry_id:1126749) of separation per unit area required to create a new crack surface must be equal to the material's [fracture energy](@entry_id:174458), $G_c$. This imposes a direct constraint on the TSL parameters: the area under the traction-separation curve must equal $G_c$.
$$
\int_0^{\delta_c} T(\delta) \, \mathrm{d}\delta = G_c
$$
For the bilinear law, this yields the simple relation $G_c = \frac{1}{2} T_{max} \delta_c$. By introducing the parameters $T_{max}$ and $G_c$ (which implicitly define $\delta_c$), the CZM framework effectively embeds a length scale into the problem, regularizing the singularity and ensuring that [fracture energy](@entry_id:174458) is dissipated correctly.

#### Framework of Nonlocal Continuum Mechanics

A broader class of models introduces nonlocality directly into the bulk [constitutive equations](@entry_id:138559), while retaining the classical, local form of the balance laws. The fundamental premise is that the [balance of linear momentum](@entry_id:193575), derived from Newton's laws and the [divergence theorem](@entry_id:145271), remains a local differential statement :
$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \rho \ddot{\mathbf{u}}
$$
This holds true as long as the [internal forces](@entry_id:167605) can be represented by a Cauchy stress tensor $\boldsymbol{\sigma}$. The nonlocality is introduced in the **[constitutive law](@entry_id:167255)**, which defines how $\boldsymbol{\sigma}$ at a point $\mathbf{x}$ is related to the deformation field. Instead of depending solely on the strain at $\mathbf{x}$, the stress becomes a functional of the strain field in a neighborhood of $\mathbf{x}$.

This conceptual separation is crucial: the fundamental balance principles remain local, while the material's behavior is described nonlocally. This framework forms the basis for integral-type and gradient-type [nonlocal models](@entry_id:175315).

#### Integral-Type Nonlocal Models

In integral-type [nonlocal models](@entry_id:175315), a state variable at a point is replaced by its weighted average over a finite neighborhood. For instance, in a [nonlocal damage model](@entry_id:181532), the evolution of damage might be driven not by the local strain, but by a nonlocal equivalent strain, $\bar{\varepsilon}(\mathbf{x})$ :
$$
\bar{\varepsilon}(\mathbf{x}) = \int_{\Omega} \omega(\mathbf{x}-\boldsymbol{\xi}) \, \varepsilon_{\text{eq}}(\boldsymbol{\xi}) \, \mathrm{d}\boldsymbol{\xi}
$$
Here, $\varepsilon_{\text{eq}}$ is a local measure of strain, and $\omega$ is a **nonlocal weighting kernel** or **[influence function](@entry_id:168646)**. This kernel is the heart of the model, and it must satisfy several key properties to ensure physical and mathematical consistency :

1.  **Compact Support:** The kernel is non-zero only within a finite radius, $\ell$ or $\delta$, known as the **horizon**. $\omega(\mathbf{r}) = 0$ for $\|\mathbf{r}\| > \ell$. This enforces a finite interaction range, determined by the material's intrinsic length scale.
2.  **Symmetry:** The kernel is symmetric, $\omega(\mathbf{r}) = \omega(-\mathbf{r})$. For [isotropic materials](@entry_id:170678), it is typically radial, $\omega(\mathbf{r}) = \hat{\omega}(\|\mathbf{r}\|)$. This property ensures the reciprocity of interactions (action-reaction) and leads to a [self-adjoint operator](@entry_id:149601), guaranteeing [conservation of linear momentum](@entry_id:165717).
3.  **Non-negativity:** The kernel is non-negative, $\omega(\mathbf{r}) \ge 0$. This ensures that the averaging process is a smoothing operation and prevents non-physical cancellations, leading to a stable material response.
4.  **Normalization:** The kernel integrates to unity, $\int \omega(\mathbf{r}) \, \mathrm{d}\mathbf{r} = 1$. This ensures that a uniform strain field remains unchanged after averaging, preserving consistency. Near boundaries, the kernel must be re-normalized to account for the truncated domain.

By averaging the strain field, this formulation smears out sharp strain localizations. The width of the localization band is no longer tied to the mesh size $h$, but is instead controlled by the nonlocal interaction radius $\ell$. This renders the dissipated [fracture energy](@entry_id:174458) objective with respect to mesh refinement, resolving the pathology of local models .

#### Gradient-Enhanced (Phase-Field) Models

An alternative to integral averaging is to introduce the length scale through spatial gradients of an internal variable. **Phase-field models** of fracture are a prominent example of this approach. In these models, the sharp geometry of a crack is regularized by a continuous [scalar field](@entry_id:154310) $d(\mathbf{x})$, often called the phase field or integrity field, which varies smoothly from an "intact" state (e.g., $d=1$) to a "fully broken" state (e.g., $d=0$) over a narrow transition zone.

The total energy of the system includes a regularized surface energy functional, which penalizes both the existence of the broken phase and spatial gradients of the phase field. A common form is the Ambrosio-Tortorelli functional :
$$
\Gamma_{\ell}(d) = \int_{\Omega} \left( \frac{(1-d)^2}{4\ell} + \ell |\nabla d|^2 \right) \mathrm{d}\mathbf{x}
$$
Here, the term $\ell |\nabla d|^2$ penalizes sharp transitions, enforcing a smooth profile, while the potential term $\frac{(1-d)^2}{4\ell}$ penalizes deviations from the intact state $d=1$. The parameter $\ell$ is an intrinsic length scale that controls the balance between these two terms and, consequently, governs the width of the diffuse crack interface, which scales as $\mathcal{O}(\ell)$.

A remarkable property of this functional, established through the mathematical theory of **$\Gamma$-convergence**, is that as the length scale $\ell \to 0$, the energy $\Gamma_{\ell}(d)$ converges to the surface energy of a sharp crack. For the specific normalization given above, this limit is:
$$
\lim_{\ell \to 0} \Gamma_{\ell}(d) = \frac{1}{2} \mathcal{H}^{n-1}(\Gamma)
$$
where $\Gamma$ is the sharp crack set and $\mathcal{H}^{n-1}$ is its $(n-1)$-dimensional area. By scaling this functional with $2G_c$, the model's total dissipated energy rigorously converges to the Griffith [fracture energy](@entry_id:174458) in the [sharp-interface limit](@entry_id:1131545), providing a powerful and thermodynamically consistent framework for simulating complex crack initiation and propagation.

#### Peridynamics: A Reformulation of Continuum Mechanics

Peridynamics represents a more radical departure from classical mechanics. Instead of regularizing a local theory, it reformulates the fundamental laws of motion from the ground up, abandoning the concept of stress and its divergence altogether. This is necessary when internal forces cannot be idealized as contact forces acting on surfaces, as assumed by the Cauchy stress principle .

In the **bond-based peridynamic** framework, material points interact directly with other points within a finite horizon $\delta$ through pairwise "bond" forces. The [balance of linear momentum](@entry_id:193575) is written directly in its integral form :
$$
\rho(\mathbf{x}) \ddot{\mathbf{u}}(\mathbf{x}, t) = \int_{H_\delta(\mathbf{x})} \mathbf{f}\big(\mathbf{u}(\boldsymbol{\xi}, t) - \mathbf{u}(\mathbf{x}, t), \boldsymbol{\xi}-\mathbf{x}\big) \, \mathrm{d}\boldsymbol{\xi} + \mathbf{b}(\mathbf{x}, t)
$$
Here, $\mathbf{f}$ is the pairwise force function that depends on the relative displacement of two points. The most significant feature of this equation is the absence of any [spatial derivatives](@entry_id:1132036) of the [displacement field](@entry_id:141476) $\mathbf{u}$. Since the governing equation is an integro-differential equation, it remains well-defined even when the [displacement field](@entry_id:141476) is discontinuous, as it is across a crack. This allows [peridynamics](@entry_id:191791) to naturally model crack initiation and propagation without special numerical treatments.

However, the original bond-based formulation has a significant limitation. The assumption of [central forces](@entry_id:267832) (forces acting along the line connecting two points) imposes a constraint on the elastic properties of the material. By comparing the [strain energy](@entry_id:162699) of a bond-based model under homogeneous deformation to that of classical elasticity, it can be shown that this assumption forces the Lamé parameters to be equal, $\lambda = \mu$. In three dimensions, this constrains the material's **Poisson's ratio** to a fixed value of $\nu = 1/4$ .

To overcome this, **[state-based peridynamics](@entry_id:190841)** was developed. In this more general formulation, the force in a bond is allowed to depend on the collective deformation of all bonds in the neighborhood (the "state"). This allows for the construction of constitutive models that can independently represent volumetric and shear responses, thereby accommodating any admissible Poisson's ratio and modeling a general isotropic elastic material.

### Numerical Treatment of Discontinuities: The Extended Finite Element Method (XFEM)

While [nonlocal models](@entry_id:175315) regularize the problem at the continuum level, an alternative approach is to retain the local continuum description (e.g., LEFM) and enhance the numerical method to handle the solution's known features. The **Extended Finite Element Method (XFEM)** is a powerful technique for modeling discrete cracks without the need for the [computational mesh](@entry_id:168560) to conform to the crack geometry.

XFEM is based on the **[partition of unity method](@entry_id:170899)**, which enriches the standard [finite element approximation](@entry_id:166278) with [special functions](@entry_id:143234) that capture the behavior of the solution near the crack. The approximation for the displacement field $\mathbf{u}(\mathbf{x})$ is constructed as :
$$
\mathbf{u}(\mathbf{x}) = \underbrace{\sum_{i \in \mathcal{N}} N_i(\mathbf{x})\,\mathbf{u}_i}_{\text{Standard FEM}} \;+\; \underbrace{\sum_{j \in \mathcal{N}_H} N_j(\mathbf{x})\,\mathbf{a}_j\left[H(\phi(\mathbf{x})) - H(\phi(\mathbf{x}_j))\right]}_{\text{Heaviside Enrichment}} \;+\; \underbrace{\sum_{k \in \mathcal{N}_T} N_k(\mathbf{x}) \sum_{m=1}^4 \mathbf{b}_k^m\left[F_m(r,\theta) - F_m(r_k,\theta_k)\right]}_{\text{Tip Enrichment}}
$$
This approximation consists of three parts:
1.  **Standard Part:** The classical [finite element approximation](@entry_id:166278) using [shape functions](@entry_id:141015) $N_i$ and nodal degrees of freedom $\mathbf{u}_i$.
2.  **Heaviside Enrichment:** For nodes whose support is cut by the crack, the approximation is enriched with a discontinuous **Heaviside function**, $H(\phi(\mathbf{x}))$, which models the displacement jump across the crack faces.
3.  **Tip Enrichment:** For nodes near the crack tip, the approximation is further enriched with a set of asymptotic **branch functions**, $\{F_m(r, \theta)\}$, which accurately capture the $\sqrt{r}$ singularity of the LEFM solution.

The [enrichment functions](@entry_id:163895) are multiplied by the standard [shape functions](@entry_id:141015), localizing their effect. The "shifted" form, where the nodal value of the enrichment function is subtracted, is employed to preserve the physical interpretation of the standard nodal DOFs $\mathbf{u}_i$ and improve the conditioning of the system matrix. XFEM provides a highly accurate and efficient way to solve LEFM problems, serving as a powerful alternative to continuum-based [nonlocal models](@entry_id:175315), especially when the physics of a single, sharp crack is the primary interest.