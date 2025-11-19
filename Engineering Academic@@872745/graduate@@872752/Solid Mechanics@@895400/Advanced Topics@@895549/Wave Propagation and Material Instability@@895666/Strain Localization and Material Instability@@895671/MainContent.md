## Introduction
The transition from a state of smooth, uniform deformation to one characterized by intense, localized strain is a defining moment in the life of a solid material. This phenomenon, known as [strain localization](@entry_id:176973), marks the onset of failure modes like necking in ductile metals and shear banding in soils and rocks. Understanding this critical juncture is not merely an academic exercise; it is fundamental to predicting material failure, ensuring [structural integrity](@entry_id:165319), and optimizing advanced engineering processes. The central challenge lies in identifying the precise conditions under which a material loses its ability to deform homogeneously, a problem that bridges physical mechanisms with the mathematical structure of continuum mechanics.

This article provides a comprehensive exploration of the principles governing [material instability](@entry_id:172649) and [strain localization](@entry_id:176973). We will demystify the transition from stable to unstable behavior by examining it from multiple perspectives. The journey is structured into three distinct parts:

First, we will delve into the **Principles and Mechanisms** that form the theoretical bedrock of the topic. This section will build from the intuitive, macroscopic Considère criterion for tensile necking to the powerful and general framework of loss of ellipticity, which provides a universal condition for the formation of [shear bands](@entry_id:183352).

Next, we will explore the theory's vast reach in **Applications and Interdisciplinary Connections**. We will see how these fundamental principles manifest across diverse fields, explaining geological fault formation in geomechanics, predicting [adiabatic shear bands](@entry_id:162684) in high-speed manufacturing, and even describing [pattern formation](@entry_id:139998) in soft biological tissues.

Finally, the **Hands-On Practices** section provides an opportunity to solidify this knowledge. Through a series of guided problems, you will engage directly with the concepts of [ellipticity](@entry_id:199972), energy non-[convexity](@entry_id:138568), and [numerical stability analysis](@entry_id:201462), bridging the gap between abstract theory and practical application. Our exploration begins with the core principles that dictate when and why materials break.

## Principles and Mechanisms

The onset of [material instability](@entry_id:172649), where a previously uniform deformation gives way to a spatially localized pattern such as necking or shear banding, represents a critical juncture in the mechanical response of a solid. This transition from a stable to an unstable state is not merely a geometric curiosity; it is fundamentally linked to the loss of well-posedness of the governing equations of continuum mechanics. Understanding the principles that dictate this transition and the material mechanisms that drive it is paramount for predicting [material failure](@entry_id:160997), designing robust structures, and developing predictive computational models. This chapter elucidates these core principles and mechanisms, beginning with macroscopic instabilities and progressing to the general continuum theory of [strain localization](@entry_id:176973).

### Conditions for Material Instability

The transition from stable, homogeneous deformation to localized instability can be diagnosed by examining the response of the material system to infinitesimal perturbations. If a kinematically admissible mode of non-uniform deformation can occur with less energy or a lower driving force than the corresponding uniform deformation, the homogeneous state is considered unstable. This general principle manifests in different forms depending on the geometry, loading, and constitutive nature of the material.

#### Macroscopic Instability: The Considère Criterion for Necking

A classic and intuitive example of [material instability](@entry_id:172649) is the phenomenon of **necking** in a ductile bar under [uniaxial tension](@entry_id:188287). Consider a [prismatic bar](@entry_id:190143) of initial length $L_0$ and cross-sectional area $A_0$ subjected to a tensile force $F$. For a material whose response can be described by a true stress-true strain curve, $\sigma = \sigma(\epsilon)$, the instability condition can be derived from a simple force-balance argument [@problem_id:2689959].

The [true stress](@entry_id:190985) $\sigma$ is defined as the force per unit of current area, $\sigma = F/A$. The true strain (or [logarithmic strain](@entry_id:751438)) $\epsilon$ is defined as $\epsilon = \ln(L/L_0)$, where $L$ is the current length. A key assumption for [plastic deformation in metals](@entry_id:180560) is the [conservation of volume](@entry_id:276587), which implies $AL = A_0 L_0$. Using these definitions, we can express the current area $A$ in terms of the true strain:
$L = L_0 \exp(\epsilon)$, so $A = A_0 L_0 / L = A_0 \exp(-\epsilon)$.

The tensile force $F$ can now be written as a function of the true strain $\epsilon$:
$F(\epsilon) = \sigma(\epsilon) A(\epsilon) = \sigma(\epsilon) A_0 \exp(-\epsilon)$.

During uniform elongation, the force $F$ increases with strain as the material work-hardens. However, the cross-sectional area $A$ simultaneously decreases. Necking instability commences at the point of maximum force, beyond which the decrease in area overcomes the increase in stress from hardening. At this point, any local imperfection will lead to a runaway reduction in area, as a smaller force is required to continue the deformation. Mathematically, this corresponds to the point where the force becomes stationary with respect to strain, i.e., $dF/d\epsilon = 0$. Applying the [product rule](@entry_id:144424):
$$ \frac{dF}{d\epsilon} = A_0 \left( \frac{d\sigma}{d\epsilon}\exp(-\epsilon) - \sigma(\epsilon)\exp(-\epsilon) \right) = 0 $$
Since $A_0$ and $\exp(-\epsilon)$ are non-zero, this simplifies to the celebrated **Considère criterion**:
$$ \frac{d\sigma}{d\epsilon} = \sigma $$
This elegant result states that [tensile instability](@entry_id:163505) begins when the slope of the true stress-true strain curve—the instantaneous **hardening rate**—becomes equal to the magnitude of the true stress itself.

For many metals, the plastic portion of the [true stress-strain curve](@entry_id:184799) can be approximated by the **Hollomon power law**, $\sigma = K \epsilon^n$, where $K$ is the strength coefficient and $n$ is the strain-hardening exponent. For such a material, the hardening rate is $d\sigma/d\epsilon = K n \epsilon^{n-1}$. Applying the Considère criterion, we find the critical strain $\epsilon_c$ for the onset of necking:
$$ K n \epsilon_c^{n-1} = K \epsilon_c^n $$
This simplifies to a remarkably simple result: $\epsilon_c = n$. Thus, for a power-law hardening material, the uniform true strain that can be sustained before necking is numerically equal to its strain-hardening exponent [@problem_id:2689959].

#### General Criterion for Strain Localization: Loss of Ellipticity

While the Considère criterion provides a powerful tool for a specific geometry, a more general theory is needed to describe localization in complex stress states, such as the formation of **[shear bands](@entry_id:183352)**. The modern framework for analyzing this phenomenon, pioneered by Hadamard, Hill, and Rudnicki and Rice, recasts the problem as a question of the [well-posedness](@entry_id:148590) of the governing [partial differential equations](@entry_id:143134) (PDEs) of equilibrium [@problem_id:2689893] [@problem_id:2689964].

Consider a homogeneous body in a state of uniform [stress and strain](@entry_id:137374). We investigate the possibility of a discontinuous deformation mode, specifically the formation of a narrow band across which the [displacement gradient](@entry_id:165352) suffers a jump. This is known as a **Hadamard rank-1 discontinuity**. Let the band be represented by a surface with [unit normal vector](@entry_id:178851) $\boldsymbol{n}$. The jump in the [velocity gradient](@entry_id:261686) across this surface is given by Maxwell's [compatibility condition](@entry_id:171102):
$$ \llbracket \nabla\dot{\boldsymbol{u}} \rrbracket = \boldsymbol{g} \otimes \boldsymbol{n} $$
where $\boldsymbol{g}$ is the jump amplitude vector, and $\llbracket \cdot \rrbracket$ denotes the jump in a quantity across the band. The corresponding jump in the [strain rate tensor](@entry_id:198281) $\dot{\boldsymbol{\varepsilon}}$ is the symmetric part of this expression:
$$ \llbracket \dot{\boldsymbol{\varepsilon}} \rrbracket = \frac{1}{2} (\boldsymbol{g} \otimes \boldsymbol{n} + \boldsymbol{n} \otimes \boldsymbol{g}) $$

For a [quasi-static process](@entry_id:151741) (neglecting inertia), the [balance of linear momentum](@entry_id:193575) requires that the traction rate vector $\dot{\boldsymbol{t}} = \dot{\boldsymbol{\sigma}}\cdot\boldsymbol{n}$ be continuous across the band. This implies:
$$ \llbracket \dot{\boldsymbol{\sigma}} \rrbracket \cdot \boldsymbol{n} = \boldsymbol{0} $$
The incremental constitutive law relates the stress rate to the [strain rate](@entry_id:154778) via the fourth-order **tangent stiffness tensor** $\mathbb{C}$: $\dot{\boldsymbol{\sigma}} = \mathbb{C} : \dot{\boldsymbol{\varepsilon}}$. Since the material is homogeneous, the jump in stress rate is $\llbracket \dot{\boldsymbol{\sigma}} \rrbracket = \mathbb{C} : \llbracket \dot{\boldsymbol{\varepsilon}} \rrbracket$. Substituting these relations yields:
$$ (\mathbb{C} : [ \frac{1}{2} (\boldsymbol{g} \otimes \boldsymbol{n} + \boldsymbol{n} \otimes \boldsymbol{g}) ]) \cdot \boldsymbol{n} = \boldsymbol{0} $$
Using the minor symmetries of the stiffness tensor ($C_{ijkl} = C_{ijlk}$), this simplifies to a set of linear algebraic equations for the jump vector $\boldsymbol{g}$:
$$ (\boldsymbol{n} \cdot \mathbb{C} \cdot \boldsymbol{n}) \cdot \boldsymbol{g} = \boldsymbol{0} $$
Here, we have introduced the second-order **[acoustic tensor](@entry_id:200089)** $\boldsymbol{Q}(\boldsymbol{n})$, defined in component form as $Q_{ik}(\boldsymbol{n}) = n_j C_{ijkl} n_l$. The condition for localization becomes:
$$ \boldsymbol{Q}(\boldsymbol{n}) \cdot \boldsymbol{g} = \boldsymbol{0} $$
A non-[trivial solution](@entry_id:155162) for $\boldsymbol{g}$ (i.e., the formation of a localization band) is possible only if the [acoustic tensor](@entry_id:200089) is singular. Therefore, the necessary condition for the onset of [strain localization](@entry_id:176973) is the existence of a direction $\boldsymbol{n}$ for which:
$$ \det(\boldsymbol{Q}(\boldsymbol{n})) = 0 $$
This condition signals the **loss of ellipticity** of the governing static PDEs.

#### The Acoustic Tensor and PDE Classification

The connection between the [acoustic tensor](@entry_id:200089) and the type of the governing PDE system provides the mathematical foundation for the localization criterion [@problem_id:2689979]. The incremental [equilibrium equations](@entry_id:172166) for a homogeneous solid can be written as $C_{ijkl} u_{k,lj} = 0$. The character of this system of second-order PDEs is determined by its **[principal symbol](@entry_id:190703)**, which is obtained by replacing each partial derivative $\partial/\partial x_j$ with a component $\xi_j$ of a real covector $\boldsymbol{\xi}$. This procedure yields the matrix with components $\mathcal{P}_{ik}(\boldsymbol{\xi}) = C_{ijkl} \xi_j \xi_l$. This is precisely the [acoustic tensor](@entry_id:200089), with the wave normal $\boldsymbol{n}$ replaced by the [covector](@entry_id:150263) $\boldsymbol{\xi}$.

The classification of the PDE system is as follows:
-   **Elliptic**: The system is elliptic if $\det(\boldsymbol{Q}(\boldsymbol{\xi})) \neq 0$ for all non-zero real $\boldsymbol{\xi}$. In this case, solutions are smooth and the [boundary value problem](@entry_id:138753) is well-posed. This corresponds to stable material behavior.
-   **Parabolic**: The system becomes parabolic at the instant when $\det(\boldsymbol{Q}(\boldsymbol{\xi})) = 0$ for some specific direction $\boldsymbol{\xi}$. This marks the loss of [ellipticity](@entry_id:199972) and the onset of instability, allowing for the formation of [shear bands](@entry_id:183352).
-   **Hyperbolic**: The system is hyperbolic if the [acoustic tensor](@entry_id:200089) has real eigenvalues, which relates to wave propagation in dynamic problems. Loss of [hyperbolicity](@entry_id:262766) (imaginary wave speeds) occurs if $\boldsymbol{Q}(\boldsymbol{\xi})$ ceases to be [positive semi-definite](@entry_id:262808).

For a linear [isotropic material](@entry_id:204616) with tangent Lamé parameters $\lambda_t$ and $\mu_t$, the [acoustic tensor](@entry_id:200089) is $\boldsymbol{Q}(\boldsymbol{\xi}) = (\lambda_t + \mu_t)\boldsymbol{\xi} \otimes \boldsymbol{\xi} + \mu_t |\boldsymbol{\xi}|^2 \boldsymbol{I}$. Its determinant can be shown to be $\det(\boldsymbol{Q}(\boldsymbol{\xi})) = \mu_t (\lambda_t + 2\mu_t) (|\boldsymbol{\xi}|^2)^2$ [@problem_id:2689979]. For a standard elastic solid, where the shear modulus $\mu > 0$ and the P-wave modulus $\lambda + 2\mu > 0$, the [acoustic tensor](@entry_id:200089) is positive definite for all directions, meaning $\det(\boldsymbol{Q}(\boldsymbol{n})) > 0$. Such a material cannot localize in the Hadamard sense under quasi-static loading [@problem_id:2689893]. Localization requires the tangent stiffness to degrade, typically through [plastic deformation](@entry_id:139726) or damage, such that either the tangent [shear modulus](@entry_id:167228) or the tangent [bulk modulus](@entry_id:160069) vanishes, causing the determinant to become zero.

### Stability, Ellipticity, and Constitutive Behavior

The [acoustic tensor](@entry_id:200089) criterion provides a universal diagnostic for localization, but the onset of instability is ultimately dictated by the evolution of the material's constitutive response. The key lies in understanding how plasticity, damage, and other inelastic phenomena degrade the [tangent stiffness](@entry_id:166213) tensor $\mathbb{C}$ to the point where ellipticity is lost.

#### Strong Ellipticity vs. Positive Definiteness

A finer distinction must be made between [material stability](@entry_id:183933) in an energetic sense and the [well-posedness](@entry_id:148590) of the field equations. A material is said to be stable if its tangent stiffness tensor $\mathbb{C}$ is **[positive definite](@entry_id:149459)**, meaning the incremental work $\frac{1}{2} \dot{\boldsymbol{\varepsilon}} : \mathbb{C} : \dot{\boldsymbol{\varepsilon}}$ is positive for any non-zero [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$. This guarantees uniqueness of solution in static [boundary value problems](@entry_id:137204).

However, the condition for the [well-posedness](@entry_id:148590) of the PDE system is the slightly weaker **[strong ellipticity](@entry_id:755529) condition**, also known as the Legendre-Hadamard condition [@problem_id:2689924]. This requires the [acoustic tensor](@entry_id:200089) $\boldsymbol{Q}(\boldsymbol{n})$ to be positive definite for all unit vectors $\boldsymbol{n}$. This is equivalent to the inequality $\boldsymbol{g} \cdot \boldsymbol{Q}(\boldsymbol{n}) \cdot \boldsymbol{g} = C_{ijkl} g_i n_j g_k n_l > 0$ for all non-zero vectors $\boldsymbol{g}$ and $\boldsymbol{n}$.

Positive definiteness of $\mathbb{C}$ implies [strong ellipticity](@entry_id:755529), but the converse is not true. A material can be strongly elliptic yet fail to be positive definite. For instance, an isotropic material with shear modulus $\mu=1$ and Lamé parameter $\lambda=-0.8$ is strongly elliptic because $\mu > 0$ and $\lambda+2\mu=1.2 > 0$. However, its [bulk modulus](@entry_id:160069) $K = \lambda + 2/3\mu = -0.8 + 2/3  0$, so the [stiffness tensor](@entry_id:176588) is not [positive definite](@entry_id:149459); the material would be unstable under hydrostatic loading. Yet, it remains stable against the formation of [shear bands](@entry_id:183352). Loss of [strong ellipticity](@entry_id:755529)—when $\det(\boldsymbol{Q}(\boldsymbol{n}))=0$ for some $\boldsymbol{n}$—is the direct precursor to [strain localization](@entry_id:176973) [@problem_id:2689924].

#### The Elastoplastic Tangent Modulus

To analyze localization in ductile materials, the [acoustic tensor](@entry_id:200089) must be constructed using the **[elastoplastic tangent modulus](@entry_id:189492)**, $\mathbb{C}^{ep}$. This operator relates the total [strain rate](@entry_id:154778) to the stress rate during [plastic flow](@entry_id:201346), $\dot{\boldsymbol{\sigma}} = \mathbb{C}^{ep} : \dot{\boldsymbol{\varepsilon}}$. Its derivation is a cornerstone of [plasticity theory](@entry_id:177023) [@problem_id:2689940].

For a general [rate-independent plasticity](@entry_id:754082) model with a yield function $f(\boldsymbol{\sigma}, \kappa)$, a [plastic potential](@entry_id:164680) $g(\boldsymbol{\sigma}, \kappa)$, and a hardening modulus $H$, the [elastoplastic tangent modulus](@entry_id:189492) is given by:
$$ \mathbb{C}^{ep} = \mathbb{C}^{e} - \frac{(\mathbb{C}^{e} : \boldsymbol{m}) \otimes (\mathbb{C}^{e} : \boldsymbol{n})}{H + \boldsymbol{n} : \mathbb{C}^{e} : \boldsymbol{m}} $$
Here, $\mathbb{C}^e$ is the [elastic stiffness tensor](@entry_id:196425), $\boldsymbol{n} = \partial f / \partial \boldsymbol{\sigma}$ is the normal to the yield surface, and $\boldsymbol{m} = \partial g / \partial \boldsymbol{\sigma}$ is the plastic flow direction. If the flow is **associated**, the [plastic potential](@entry_id:164680) is the same as the yield function ($g=f$), which means $\boldsymbol{m}=\boldsymbol{n}$. In this case, the tangent modulus $\mathbb{C}^{ep}$ possesses [major symmetry](@entry_id:198487). If the flow is **non-associated** ($g \neq f$), as is common for frictional materials like soils and rocks, then $\boldsymbol{m} \neq \boldsymbol{n}$, and $\mathbb{C}^{ep}$ is non-symmetric. This lack of symmetry has profound consequences for stability.

#### Drucker's Postulate and Material Stability

An alternative, energy-based perspective on [material stability](@entry_id:183933) is provided by **Drucker's stability postulate** [@problem_id:2689930]. In its incremental form, it states that for any infinitesimal [plastic loading](@entry_id:753518) process, the incremental plastic work must be non-negative:
$$ \dot{W}^p = \dot{\boldsymbol{\sigma}} : \dot{\boldsymbol{\varepsilon}}^p \ge 0 $$
This postulate ensures a basic level of stability, precluding behaviors where the material could spontaneously release energy under an applied stress. For an [associated flow rule](@entry_id:201731) ($ \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \boldsymbol{n}$) and a [convex yield surface](@entry_id:203690), the postulate is satisfied as long as the material does not exhibit softening ($H \ge 0$). Softening, by its nature, violates the postulate and is a direct cause of instability.

#### The Role of Non-Associativity and Softening

The connection between Drucker's postulate and localization becomes critical in non-associated materials. With non-[associativity](@entry_id:147258) ($\boldsymbol{m} \neq \boldsymbol{n}$), it is possible for Drucker's postulate to be violated even while the material is hardening in a conventional sense (e.g., $H>0$) [@problem_id:2689930] [@problem_id:2689944]. This is because the stress rate vector $\dot{\boldsymbol{\sigma}}$ is constrained by the [consistency condition](@entry_id:198045) to be nearly orthogonal to the yield surface normal $\boldsymbol{n}$, but it may form an obtuse angle with the flow direction $\boldsymbol{m}$. In such a case, $\dot{\boldsymbol{\sigma}} : \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} (\dot{\boldsymbol{\sigma}} : \boldsymbol{m})  0$.

This violation of Drucker's postulate indicates an intrinsic [material instability](@entry_id:172649). It leads to a non-symmetric [elastoplastic tangent modulus](@entry_id:189492) $\mathbb{C}^{ep}$ whose symmetric part can lose positive definiteness. This, in turn, is sufficient to cause a loss of [strong ellipticity](@entry_id:755529), allowing the localization condition $\det(\boldsymbol{Q}_s(\boldsymbol{n})) = 0$ (where $\boldsymbol{Q}_s$ is the symmetric part of the [acoustic tensor](@entry_id:200089)) to be met while the material is still macroscopically hardening. This is a crucial mechanism for [shear band formation](@entry_id:754755) in geological and [granular materials](@entry_id:750005), which are known to exhibit [non-associated flow](@entry_id:202786) ([dilatancy](@entry_id:201001) being different from friction). Furthermore, non-associativity affects the predicted orientation of [shear bands](@entry_id:183352); the band angle depends on both the friction angle (related to $f$) and the [dilatancy angle](@entry_id:748435) (related to $g$) [@problem_id:2689944].

### Localization in Numerical Simulations: Ill-Posedness and Regularization

The onset of [strain localization](@entry_id:176973) presents a profound challenge for numerical methods like the Finite Element Method (FEM). The mathematical [ill-posedness](@entry_id:635673) of the underlying problem manifests as severe artifacts in the numerical solution.

#### The Pathology of Local Softening Models

When a [constitutive model](@entry_id:747751) exhibits **[strain softening](@entry_id:185019)** (i.e., a decreasing stress with increasing strain) and is purely **local** (the stress at a point depends only on the history at that same point), the material's tangent modulus becomes negative. As discussed, this leads to a loss of [ellipticity](@entry_id:199972) of the governing PDEs [@problem_id:2689932].

A local model has no inherent **internal length scale**. Consequently, when the continuum problem becomes ill-posed, there is no material property to dictate the width of the localization band. In a finite element simulation, the only available length scale is the element size, $h$. As a result, the numerical solution will always concentrate the entire softening deformation into the smallest possible region—a single row of elements. The width of the computed localization band will thus shrink with the mesh size.

This leads to a **[pathological mesh dependence](@entry_id:183356)**. The total energy dissipated in the formation of the failure surface, which should be a material property (the fracture energy), is calculated by integrating the dissipated energy density over the volume of the localization band. Since the band volume shrinks to zero as $h \to 0$, the computed energy dissipation spuriously vanishes. The global structural response (e.g., the force-displacement curve) also fails to converge as the mesh is refined, rendering the simulation results meaningless.

#### Regularization via Internal Length Scales

The remedy for this [pathology](@entry_id:193640) is **regularization**: enriching the [constitutive model](@entry_id:747751) to restore [well-posedness](@entry_id:148590) to the [boundary value problem](@entry_id:138753). The key is to introduce a physical internal length scale, $\ell$, into the continuum description. This ensures that the localization band has a finite, mesh-independent width.

Various [regularization techniques](@entry_id:261393) exist, including nonlocal models, rate-dependent (viscoplastic) models, and [gradient-enhanced models](@entry_id:162584). They all share the common feature of introducing non-locality in space or time, which prevents strain from collapsing onto a surface of zero thickness.

#### Gradient-Enhanced Models: A Case Study

A particularly elegant approach is the use of **[gradient-enhanced models](@entry_id:162584)** [@problem_id:2689962]. In these models, the material's free energy or [yield function](@entry_id:167970) is made to depend not only on the local strain or [damage variable](@entry_id:197066) $\alpha$, but also on its spatial gradient, $\nabla\alpha$. A simple form for the incremental energy functional in a softening material includes a [gradient penalty](@entry_id:635835):
$$ \Delta \Pi[\alpha] = \int_V \left( \frac{1}{2} h \alpha^2 + \frac{1}{2} c \ell^2 |\nabla\alpha|^2 \right) dV $$
Here, $h0$ represents the local softening, while the gradient term, with constants $c0$ and $\ell0$, penalizes sharp spatial variations of $\alpha$. The parameter $\ell$ explicitly introduces an internal length scale.

A [linear stability analysis](@entry_id:154985) of a homogeneous state shows the effect of this term. A perturbation of the form $\alpha(x) = A \cos(kx)$ changes the system's energy by an amount proportional to $(h + c \ell^2 k^2)$. Since $h0$, modes with small wavenumbers $k$ can lower the energy and are thus unstable. However, the gradient term $c \ell^2 k^2$ stabilizes high-[wavenumber](@entry_id:172452) modes. The competition between these two effects results in a **cutoff [wavenumber](@entry_id:172452)**, $k_c = \sqrt{|h|/(c\ell^2)}$. Only modes with $k  k_c$ can grow.

This regularization completely changes the nature of the instability. It suppresses infinitely sharp localization and selects a characteristic pattern with a finite width, $w$, that scales with the internal length: $w \sim 1/k_c \sim \ell \sqrt{c/|h|}$. By setting a minimum width for the shear band, the [gradient-enhanced model](@entry_id:749989) ensures that the boundary value problem remains well-posed. As a result, numerical simulations produce results that are objective with respect to [mesh refinement](@entry_id:168565), with the total dissipated energy converging to a finite, non-zero value, provided the mesh is fine enough to resolve the [characteristic length](@entry_id:265857) $\ell$ [@problem_id:2689932].