## Introduction
Modeling the complex mechanical behavior of [geomaterials](@entry_id:749838), which exhibit both elastic (recoverable) and plastic (irrecoverable) deformation, is a central challenge in [computational geomechanics](@entry_id:747617). To accurately simulate problems such as [foundation settlement](@entry_id:749535), [slope stability](@entry_id:190607), or tunneling, a robust mathematical framework is required to link the material's stress state to its deformation. This article addresses the critical knowledge gap between abstract constitutive theory and its concrete implementation in numerical solvers by focusing on the derivation and application of the elastoplastic [constitutive matrix](@entry_id:164908), or tangent modulus.

This article will guide you through the theoretical underpinnings and practical significance of this essential component. The journey is structured into three parts:
*   **Principles and Mechanisms** delves into the first principles of [rate-independent plasticity](@entry_id:754082) to derive the [continuum tangent modulus](@entry_id:201751) and, most importantly, the algorithmic or [consistent tangent modulus](@entry_id:168075) required for numerically accurate and efficient simulations.
*   **Applications and Interdisciplinary Connections** explores how this general framework is applied to classic [constitutive models](@entry_id:174726) like von Mises, Drucker-Prager, and Modified Cam-Clay, and discusses its role in advanced topics such as [poromechanics](@entry_id:175398), [material stability](@entry_id:183933), and [finite strain](@entry_id:749398) analysis.
*   **Hands-On Practices** provides a set of practical exercises to solidify understanding, from benchmarking convergence rates to deriving and verifying the tangent for a foundational plasticity model.

## Principles and Mechanisms

The behavior of [geomaterials](@entry_id:749838) under complex loading paths often involves both recoverable (elastic) and irrecoverable (plastic) deformations. Capturing this behavior in a computational model requires a robust mathematical framework that relates stress to strain. This chapter delves into the principles and mechanisms of elastoplastic [constitutive models](@entry_id:174726), focusing on the formulation of the tangent modulus, a critical component for the numerical solution of [boundary value problems](@entry_id:137204) in [geomechanics](@entry_id:175967). We will begin with the fundamental rate form of the constitutive law, derive the [continuum tangent modulus](@entry_id:201751), and then transition to the discrete algorithmic form required for computational simulations, culminating in the concept of the [consistent tangent modulus](@entry_id:168075).

### The Elastoplastic Constitutive Law in Rate Form

The foundation of rate-independent [elastoplasticity](@entry_id:193198) rests on three key postulates: an additive decomposition of strain rates, a yield criterion defining the limit of elastic behavior, and a [flow rule](@entry_id:177163) governing the evolution of plastic strain.

The total strain rate, denoted by $\dot{\boldsymbol{\varepsilon}}$, is assumed to be additively composed of an elastic part, $\dot{\boldsymbol{\varepsilon}}^e$, and a plastic part, $\dot{\boldsymbol{\varepsilon}}^p$:
$$ \dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^e + \dot{\boldsymbol{\varepsilon}}^p $$
The elastic strain rate is related to the stress rate $\dot{\boldsymbol{\sigma}}$ through a linear elastic law, governed by the fourth-order [elastic stiffness tensor](@entry_id:196425), $\boldsymbol{D}^e$:
$$ \dot{\boldsymbol{\sigma}} = \boldsymbol{D}^e : \dot{\boldsymbol{\varepsilon}}^e $$
This relationship implies that the stress rate is determined by the elastic portion of the deformation.

Plastic deformation is initiated when the stress state reaches a critical boundary, defined by a **yield function**, $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}) \le 0$, where $\boldsymbol{\alpha}$ represents a set of [internal state variables](@entry_id:750754) (e.g., hardening parameters). The region in [stress space](@entry_id:199156) where $f  0$ is the elastic domain. Plastic loading can only occur when the stress state is on the yield surface, i.e., $f=0$.

The evolution of plastic strain is described by a **[flow rule](@entry_id:177163)**, which specifies the direction of plastic straining. For many materials, this is given by:
$$ \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}} $$
Here, $g(\boldsymbol{\sigma}, \boldsymbol{\alpha})$ is the **plastic potential function**, and $\dot{\lambda}$ is the scalar **[plastic multiplier](@entry_id:753519) rate**. If the [plastic potential](@entry_id:164680) is identical to the yield function ($g=f$), the flow is termed **associative**; otherwise, it is **non-associated**. The direction of [plastic flow](@entry_id:201346) is then given by the tensor $\boldsymbol{M} = \partial g / \partial \boldsymbol{\sigma}$.

The relationship between loading and plastic flow is governed by the **Karush-Kuhn-Tucker (KKT) conditions** [@problem_id:3522245], which state that:
$$ f \le 0, \quad \dot{\lambda} \ge 0, \quad \dot{\lambda} f = 0 $$
These conditions elegantly encapsulate the physics: plastic flow ($\dot{\lambda}0$) can only occur when the stress state is on the yield surface ($f=0$), and the stress state cannot lie outside the yield surface ($f0$ is inadmissible). During [plastic loading](@entry_id:753518), the stress state must remain on the [yield surface](@entry_id:175331). This imposes an additional constraint known as the **[consistency condition](@entry_id:198045)**:
$$ \dot{f} = 0 $$

### The Continuum Elastoplastic Tangent Modulus

The [consistency condition](@entry_id:198045) is the key to deriving a direct relationship between the total [strain rate](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}$ and the stress rate $\dot{\boldsymbol{\sigma}}$. For a model with hardening, the [yield function](@entry_id:167970) depends on both stress $\boldsymbol{\sigma}$ and internal variables $\boldsymbol{\alpha}$. Its rate of change is found using the chain rule:
$$ \dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} = 0 $$
Let's denote the normal to the [yield surface](@entry_id:175331) as $\boldsymbol{N} = \partial f / \partial \boldsymbol{\sigma}$. The evolution of the internal variables is typically linked to the [plastic multiplier](@entry_id:753519), for instance, through a hardening modulus $H$ such that $\frac{\partial f}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} = -H \dot{\lambda}$. The consistency condition becomes:
$$ \boldsymbol{N} : \dot{\boldsymbol{\sigma}} - H \dot{\lambda} = 0 $$

We can now solve for the [plastic multiplier](@entry_id:753519) rate $\dot{\lambda}$ [@problem_id:3522245]. By substituting the elastic law $\dot{\boldsymbol{\sigma}} = \boldsymbol{D}^e : (\dot{\boldsymbol{\varepsilon}} - \dot{\boldsymbol{\varepsilon}}^p)$ and the [flow rule](@entry_id:177163) $\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \boldsymbol{M}$ into the consistency condition, we obtain:
$$ \boldsymbol{N} : \left[ \boldsymbol{D}^e : (\dot{\boldsymbol{\varepsilon}} - \dot{\lambda} \boldsymbol{M}) \right] - H \dot{\lambda} = 0 $$
Distributing the terms and solving for $\dot{\lambda}$ yields:
$$ \dot{\lambda} = \frac{\boldsymbol{N} : \boldsymbol{D}^e : \dot{\boldsymbol{\varepsilon}}}{H + \boldsymbol{N} : \boldsymbol{D}^e : \boldsymbol{M}} $$
This expression is valid during [plastic loading](@entry_id:753518), which occurs if the numerator, representing the elastic trial stress rate projected onto the [yield surface](@entry_id:175331) normal, is positive. Otherwise, the process is elastic ($\dot{\lambda}=0$).

By substituting this expression for $\dot{\lambda}$ back into the stress [rate equation](@entry_id:203049), we arrive at the final rate-form [constitutive law](@entry_id:167255) that incorporates both elastic and plastic effects:
$$ \dot{\boldsymbol{\sigma}} = \boldsymbol{D}^e : (\dot{\boldsymbol{\varepsilon}} - \dot{\lambda} \boldsymbol{M}) = \left[ \boldsymbol{D}^e - \frac{(\boldsymbol{D}^e : \boldsymbol{M}) \otimes (\boldsymbol{N} : \boldsymbol{D}^e)}{H + \boldsymbol{N} : \boldsymbol{D}^e : \boldsymbol{M}} \right] : \dot{\boldsymbol{\varepsilon}} $$
The term in the square brackets is the **continuum [elastoplastic tangent modulus](@entry_id:189492)**, denoted $\boldsymbol{D}^{ep}_{cont}$. It provides the instantaneous relationship between the total [strain rate](@entry_id:154778) and the stress rate for a material at a plastic state. This is the tangent modulus referred to as the **continuum tangent** [@problem_id:3522256], as it is derived purely from the continuum-level [constitutive equations](@entry_id:138559), independent of any specific [numerical time integration](@entry_id:752837) scheme.

### Matrix Representation of the Elastic Response

For implementation in numerical software, such as a Finite Element Method (FEM) code, tensor equations must be translated into matrix-vector form. This is accomplished using **Voigt notation**, which maps symmetric second-order tensors (like stress and strain) to six-component vectors and fourth-order tensors (like stiffness) to $6 \times 6$ matrices.

A subtlety arises in this mapping regarding the definition of shear strains. To preserve the equivalence between the tensor double-dot product for power density ($\dot{W} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}$) and the vector dot product ($\dot{W} = \boldsymbol{\sigma}_v^T \dot{\boldsymbol{\varepsilon}}_v$), a specific convention must be adopted. The common **engineering strain** convention defines the shear components of the strain vector as $\gamma_{ij} = 2\varepsilon_{ij}$ for $i \neq j$. If this convention is used for the strain vector while the stress vector contains the [true stress](@entry_id:190985) components $\sigma_{ij}$, the work-conjugacy is preserved [@problem_id:3522254]. This choice affects the components of the stiffness and compliance matrices.

For an isotropic linear elastic material characterized by its bulk modulus $K$ and [shear modulus](@entry_id:167228) $G$, the relationship $\boldsymbol{\sigma} = 3K \boldsymbol{\varepsilon}^{\text{vol}} + 2G \boldsymbol{\varepsilon}^{\text{dev}}$ can be written in $6 \times 6$ matrix form, $\boldsymbol{\sigma}_v = \boldsymbol{D}^e \boldsymbol{\varepsilon}_v$, using the engineering strain convention [@problem_id:3522303]. The stiffness matrix $\boldsymbol{D}^e$ is given by:
$$
\boldsymbol{D}^e = \begin{pmatrix}
K + \frac{4G}{3}   K - \frac{2G}{3}   K - \frac{2G}{3}   0   0   0 \\
K - \frac{2G}{3}   K + \frac{4G}{3}   K - \frac{2G}{3}   0   0   0 \\
K - \frac{2G}{3}   K - \frac{2G}{3}   K + \frac{4G}{3}   0   0   0 \\
0   0   0   G   0   0 \\
0   0   0   0   G   0 \\
0   0   0   0   0   G
\end{pmatrix}
$$
This matrix can be spectrally decomposed using volumetric and deviatoric projector matrices, $\boldsymbol{P}^{\text{vol}}$ and $\boldsymbol{P}^{\text{dev}}$, as $\boldsymbol{D}^e = 3K \boldsymbol{P}^{\text{vol}} + 2G \boldsymbol{P}^{\text{dev}}$ [@problem_id:3522303]. This decomposition is particularly useful for models whose responses are naturally split into volumetric and deviatoric parts.

The inverse of the [stiffness matrix](@entry_id:178659) is the **[compliance matrix](@entry_id:185679)**, $\boldsymbol{C}^e = (\boldsymbol{D}^e)^{-1}$, which maps stress to strain. For the material to be physically stable, the [strain energy](@entry_id:162699) must be positive, which requires the stiffness matrix $\boldsymbol{D}^e$ (and [compliance matrix](@entry_id:185679) $\boldsymbol{C}^e$) to be [positive definite](@entry_id:149459). This translates to the physical constraints that both the bulk modulus and the [shear modulus](@entry_id:167228) must be positive: $K  0$ and $G  0$ [@problem_id:3522218].

### The Algorithmic (Consistent) Tangent Modulus

In [computational mechanics](@entry_id:174464), [boundary value problems](@entry_id:137204) are solved incrementally. A typical quasi-[static analysis](@entry_id:755368) involves applying loads or displacements in a series of small steps. Within each step, an iterative scheme, most commonly the **Newton-Raphson method**, is used to solve the nonlinear system of algebraic equations that arise from the FEM discretization.

The discrete form of the [principle of virtual work](@entry_id:138749) leads to a system of equations expressed in terms of a **residual vector**, $\boldsymbol{R}(\boldsymbol{u})$, which must be zero at equilibrium [@problem_id:3522208]. The residual is the difference between the internal forces, which depend on the stress state, and the external applied forces. The Newton-Raphson method finds the [displacement vector](@entry_id:262782) $\boldsymbol{u}$ that solves $\boldsymbol{R}(\boldsymbol{u}) = \boldsymbol{0}$ by iteratively solving a linearized system:
$$ \boldsymbol{K}_T (\boldsymbol{u}_k) \Delta \boldsymbol{u}_{k+1} = - \boldsymbol{R}(\boldsymbol{u}_k) $$
where $\boldsymbol{u}_k$ is the displacement at iteration $k$, $\Delta \boldsymbol{u}_{k+1}$ is the correction, and $\boldsymbol{K}_T$ is the global tangent stiffness matrix, which is the Jacobian of the residual: $\boldsymbol{K}_T = \partial \boldsymbol{R} / \partial \boldsymbol{u}$. The structure of this global matrix is an assembly of element contributions:
$$ \boldsymbol{K}_T = \int_\Omega \boldsymbol{B}^T \frac{\mathrm{d}\boldsymbol{\sigma}}{\mathrm{d}\boldsymbol{\varepsilon}} \boldsymbol{B} \, \mathrm{d}\Omega $$
where $\boldsymbol{B}$ is the [strain-displacement matrix](@entry_id:163451).

The crucial term is $\mathrm{d}\boldsymbol{\sigma} / \mathrm{d}\boldsymbol{\varepsilon}$, the tangent modulus at the material point. A key insight in [computational plasticity](@entry_id:171377) is that for the Newton-Raphson method to achieve its characteristic **quadratic rate of convergence**, this tangent modulus must be the *exact* [linearization](@entry_id:267670) of the numerical algorithm used to update the stress over a finite increment [@problem_id:3522256], [@problem_id:3522208]. This specific tangent is called the **[algorithmic tangent modulus](@entry_id:199979)** or **[consistent tangent modulus](@entry_id:168075)**, denoted $\boldsymbol{D}^{alg}$.

At the end of a load step from time $n$ to $n+1$, the stress $\boldsymbol{\sigma}_{n+1}$ is computed via a discrete update rule, often a **[return mapping algorithm](@entry_id:173819)**, which can be schematically written as $\boldsymbol{\sigma}_{n+1} = \mathcal{G}(\boldsymbol{\varepsilon}_{n+1}, \text{state}_n)$. The consistent tangent is precisely the derivative of this function:
$$ \boldsymbol{D}^{alg} = \frac{\mathrm{d}\boldsymbol{\sigma}_{n+1}}{\mathrm{d}\boldsymbol{\varepsilon}_{n+1}} = \frac{\mathrm{d}\mathcal{G}}{\mathrm{d}\boldsymbol{\varepsilon}_{n+1}} $$
Using the continuum tangent $\boldsymbol{D}^{ep}_{cont}$ in place of $\boldsymbol{D}^{alg}$ results in an approximate Jacobian. While this may still lead to a solution, the [rate of convergence](@entry_id:146534) degrades from quadratic to linear, requiring significantly more iterations. For purely elastic steps, $\boldsymbol{D}^{alg}$ coincides with $\boldsymbol{D}^e$ and $\boldsymbol{D}^{ep}_{cont}$, but they differ during [plastic loading](@entry_id:753518) for any finite step size [@problem_id:3522256].

### Derivation of the Consistent Tangent: J2 Plasticity

To make the abstract concept of the consistent tangent concrete, we will derive it for a widely used model: von Mises (or J2) plasticity with associative flow and linear [isotropic hardening](@entry_id:164486) [@problem_id:3522257]. This model is governed by a [yield function](@entry_id:167970) $f(\boldsymbol{s}, \kappa) = \sqrt{\frac{3}{2}} \|\boldsymbol{s}\| - (\sigma_{y0} + H\kappa)$, where $\boldsymbol{s}$ is the [deviatoric stress](@entry_id:163323), $\kappa$ is the equivalent plastic strain, $\sigma_{y0}$ is the initial yield stress, and $H$ is the hardening modulus.

The integration of the [constitutive law](@entry_id:167255) over an increment $\Delta\boldsymbol{\varepsilon}$ is performed using a [return mapping algorithm](@entry_id:173819):
1.  **Elastic Trial Step:** First, assume the entire increment is elastic. The trial stress state $(\boldsymbol{p}^{\text{tr}}, \boldsymbol{s}^{\text{tr}})$ is computed:
    $$ p^{\text{tr}} = p_n + K \mathrm{tr}(\Delta\boldsymbol{\varepsilon}) \quad \text{and} \quad \boldsymbol{s}^{\text{tr}} = \boldsymbol{s}_n + 2G \mathrm{dev}(\Delta\boldsymbol{\varepsilon}) $$
2.  **Yield Check:** Evaluate the [yield function](@entry_id:167970) at the trial state: $f^{\text{tr}} = \sqrt{\frac{3}{2}} \|\boldsymbol{s}^{\text{tr}}\| - (\sigma_{y0} + H\kappa_n)$. If $f^{\text{tr}} \le 0$, the step is elastic, and the final state is the trial state.
3.  **Plastic Corrector (Return Mapping):** If $f^{\text{tr}}  0$, [plastic deformation](@entry_id:139726) occurs. The stress must be "returned" to the [yield surface](@entry_id:175331). For J2 plasticity, this return is radial in deviatoric stress space. The updated stress $\boldsymbol{s}_{n+1}$ is found by solving a system of equations comprising the discrete [flow rule](@entry_id:177163) and the final yield condition $f(\boldsymbol{s}_{n+1}, \kappa_{n+1}) = 0$. This leads to an explicit solution for the discrete [plastic multiplier](@entry_id:753519) increment $\Delta\lambda$:
    $$ \Delta\lambda = \frac{f^{\text{tr}}}{3G + H} $$
    The final [deviatoric stress](@entry_id:163323) is then updated as:
    $$ \boldsymbol{s}_{n+1} = \boldsymbol{s}^{\text{tr}} - 2G \Delta\lambda \sqrt{\frac{3}{2}} \boldsymbol{n}^{\text{tr}} = \left(1 - \frac{3G \Delta\lambda}{\sigma_{\mathrm{eq}}^{\text{tr}}}\right) \boldsymbol{s}^{\text{tr}} $$
    where $\boldsymbol{n}^{\text{tr}} = \boldsymbol{s}^{\text{tr}} / \|\boldsymbol{s}^{\text{tr}}\|$ is the unit direction of the trial [deviatoric stress](@entry_id:163323) and $\sigma_{\mathrm{eq}}^{\text{tr}} = \sqrt{\frac{3}{2}}\|\boldsymbol{s}^{\text{tr}}\|$. The pressure update remains purely elastic, $p_{n+1} = p^{\text{tr}}$.

4.  **Consistent Tangent Derivation:** The [consistent tangent modulus](@entry_id:168075) $\boldsymbol{D}^{alg} = \mathrm{d}\boldsymbol{\sigma}_{n+1} / \mathrm{d}\boldsymbol{\varepsilon}$ is found by differentiating the final stress expressions with respect to the total strain $\boldsymbol{\varepsilon}_{n+1}$. This requires careful application of the chain rule, as $\boldsymbol{s}_{n+1}$ depends on $\boldsymbol{s}^{\text{tr}}$ and $\Delta\lambda$, both of which are functions of $\boldsymbol{\varepsilon}_{n+1}$. The differentiation yields:
    $$ \boldsymbol{D}^{alg} = K \boldsymbol{I} \otimes \boldsymbol{I} + 2G \beta_1 \left( \boldsymbol{I}^{\text{dev}} - \boldsymbol{n}^{\text{tr}} \otimes \boldsymbol{n}^{\text{tr}} \right) + 2G \beta_2 (\boldsymbol{n}^{\text{tr}} \otimes \boldsymbol{n}^{\text{tr}}) $$
    where $\boldsymbol{I}^{\text{dev}}$ is the fourth-order deviatoric identity tensor, and the scalars $\beta_1$ and $\beta_2$ are functions of the material properties and the trial state:
    $$ \beta_1 = 1 - \frac{3G \Delta\lambda}{\sigma_{\mathrm{eq}}^{\text{tr}}} \quad \text{and} \quad \beta_2 = \frac{\beta_1}{1 + H/(3G)} $$
    This expression for $\boldsymbol{D}^{alg}$ is the correct tangent to use in the [global stiffness matrix](@entry_id:138630) to ensure [quadratic convergence](@entry_id:142552) for simulations using the J2 plasticity model.

### Advanced Topics and Structural Properties

The structure and properties of the [elastoplastic tangent modulus](@entry_id:189492) are deeply connected to the physical assumptions of the underlying [constitutive model](@entry_id:747751).

#### Symmetry and Non-Associated Flow

For an [associative flow rule](@entry_id:163391) ($g=f$), the continuum tangent $\boldsymbol{D}^{ep}_{cont}$ and the consistent tangent $\boldsymbol{D}^{alg}$ are symmetric. This has significant computational benefits, as symmetric solvers can be used for the global system of equations. However, many [geomaterials](@entry_id:749838), particularly frictional soils and rocks, exhibit **[non-associated flow](@entry_id:202786)**. A common example is a material following a pressure-sensitive Drucker-Prager [yield criterion](@entry_id:193897) but with a different [dilatancy angle](@entry_id:748435) in the [plastic potential](@entry_id:164680) [@problem_id:3522233]. For such a non-associated model, the tangent modulus becomes **non-symmetric**. This asymmetry arises from the difference between the [yield surface](@entry_id:175331) normal $\boldsymbol{N}$ and the [plastic flow](@entry_id:201346) direction $\boldsymbol{M}$, leading to a non-symmetric [rank-one update](@entry_id:137543) to the elastic stiffness matrix. This non-symmetry reflects physical phenomena like shear-induced dilation or [compaction](@entry_id:267261) and has major implications for the stability of the material and the choice of [numerical solvers](@entry_id:634411).

#### Non-Smooth Yield Surfaces

Many classical [yield criteria](@entry_id:178101) for [geomaterials](@entry_id:749838), such as the Mohr-Coulomb and Drucker-Prager models, feature sharp **corners or edges** in [stress space](@entry_id:199156). At these non-smooth locations, the gradient of the yield function, $\partial f / \partial \boldsymbol{\sigma}$, is not uniquely defined [@problem_id:3522276]. This poses a significant theoretical and algorithmic challenge. The direction of [plastic flow](@entry_id:201346) is no longer a single vector but lies within a cone of possible directions, mathematically described by the **[subdifferential](@entry_id:175641)** of the yield function.
To formulate a robust [return mapping algorithm](@entry_id:173819) and a consistent tangent, special techniques are required. These include [regularization methods](@entry_id:150559) that smooth the corners, or more complex multi-surface plasticity algorithms that treat the state as being on multiple yield surfaces simultaneously. Without such treatment, the consistent tangent is not uniquely defined, and the quadratic convergence of the Newton-Raphson method is lost.

#### Frame Indifference and Finite Strain

The discussion thus far has been within a small-strain framework. When deformations become large, the principle of **[material frame indifference](@entry_id:166014) (objectivity)** must be explicitly considered [@problem_id:3522226]. This principle states that the constitutive response must be independent of the observer's reference frame (i.e., superposed [rigid body motions](@entry_id:200666)). In a small-strain formulation, this is implicitly satisfied because rigid body rotations do not contribute to the strain measure.

In a finite-strain formulation, however, the [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$, is not an objective quantity. To formulate an objective [constitutive law](@entry_id:167255), one must use an **[objective stress rate](@entry_id:168809)**, such as the Jaumann or Truesdell rate, which accounts for the spin of the material. The [constitutive law](@entry_id:167255) takes the form $\overset{\triangledown}{\boldsymbol{\sigma}} = \boldsymbol{D}^{ep} : \boldsymbol{d}$, where $\overset{\triangledown}{\boldsymbol{\sigma}}$ is the objective rate and $\boldsymbol{d}$ is the [rate of deformation tensor](@entry_id:182598). The choice of objective rate introduces additional terms into the tangent modulus that depend on the current stress state, further complicating its derivation. The most rigorous approach involves formulating the [constitutive law](@entry_id:167255) in a material setting using [work-conjugate stress](@entry_id:182069) and [strain measures](@entry_id:755495) (e.g., the second Piola-Kirchhoff stress and Green-Lagrange strain) and then transforming the resulting tangent modulus to the spatial configuration [@problem_id:3522226].