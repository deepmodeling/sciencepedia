## Introduction
The transition of [geomaterials](@entry_id:749838) from elastic deformation to irreversible plastic failure is a fundamental process in [geomechanics](@entry_id:175967), critical to the design and safety of nearly every geotechnical structure, from foundations and slopes to tunnels and dams. Predicting when and how a material will yield under complex stress states requires a robust mathematical framework. This article addresses this need by providing a comprehensive overview of classical [yield criteria](@entry_id:178101), which form the bedrock of modern [plasticity theory](@entry_id:177023) for [geomaterials](@entry_id:749838). By bridging theoretical concepts with practical applications, this article will equip you with the knowledge to model and predict [material failure](@entry_id:160997).

The journey begins in "Principles and Mechanisms," where we establish the mathematical language of plasticity, starting with coordinate-independent [stress invariants](@entry_id:170526). We will then explore a hierarchy of [yield criteria](@entry_id:178101)—from the pressure-independent Tresca and von Mises models to the pressure-dependent Mohr-Coulomb, Drucker-Prager, and Hoek-Brown criteria—and introduce the [flow rule](@entry_id:177163) that governs the direction of plastic deformation. Next, "Applications and Interdisciplinary Connections" demonstrates how these theories are applied in engineering analysis, parameter characterization, and advanced [computational geomechanics](@entry_id:747617), highlighting their role in finite element simulations and connections to fields like experimental mechanics and [numerical analysis](@entry_id:142637). Finally, "Hands-On Practices" will solidify your understanding through guided problems that apply the core concepts, such as calculating [stress invariants](@entry_id:170526) and implementing a basic [return-mapping algorithm](@entry_id:168456).

## Principles and Mechanisms

The transition from purely [elastic deformation](@entry_id:161971) to permanent, inelastic behavior is a defining characteristic of [geomaterials](@entry_id:749838) under load. This transition, known as yielding, marks the onset of plasticity. To mathematically describe and predict this behavior, a rigorous theoretical framework is required. This section establishes the fundamental principles and mechanisms governing [classical plasticity theory](@entry_id:167389) as applied to [geomaterials](@entry_id:749838). We will first introduce the invariant language used to describe complex stress states, then explore a hierarchy of [yield criteria](@entry_id:178101), and finally, detail the rules that govern the evolution of [plastic deformation](@entry_id:139726) once yielding has begun.

### A Coordinate-Independent Description of Stress: Invariants

The state of stress at a point is described by the Cauchy stress tensor, $\boldsymbol{\sigma}$, a second-order symmetric tensor. While its components depend on the chosen coordinate system, the physical state of stress does not. Therefore, to formulate material laws that are objective and independent of the observer's reference frame, we describe stress using scalar quantities that are invariant under [coordinate transformations](@entry_id:172727). These are known as **[stress invariants](@entry_id:170526)**.

For an isotropic material, the material response depends only on these invariants. The most fundamental decomposition of stress separates its volume-changing (hydrostatic) and shape-changing (deviatoric) components. The stress tensor $\boldsymbol{\sigma}$ is additively decomposed as:

$\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}$

Here, $p$ is the **[mean stress](@entry_id:751819)** (or hydrostatic stress), which represents the average normal stress across any three mutually orthogonal planes. In geomechanics, it is conventional to consider compressive stresses as positive. The [mean stress](@entry_id:751819) is defined as one-third of the trace of the stress tensor:

$p = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})$

where $\sigma_{ii}$ are the diagonal components of the tensor. In a [principal stress](@entry_id:204375) frame, this simplifies to $p = \frac{1}{3}(\sigma_1 + \sigma_2 + \sigma_3)$, where $\sigma_1, \sigma_2, \sigma_3$ are the [principal stresses](@entry_id:176761).

The tensor $\boldsymbol{s}$ is the **[deviatoric stress tensor](@entry_id:267642)**, representing the portion of the stress that causes distortion or shear. By definition, it is traceless, $\mathrm{tr}(\boldsymbol{s}) = 0$. The tensor $\boldsymbol{I}$ is the second-order identity tensor.

While $p$ is the first invariant of $\boldsymbol{\sigma}$, the behavior of many [geomaterials](@entry_id:749838), particularly their failure, is governed by the invariants of the [deviatoric stress tensor](@entry_id:267642), commonly denoted $J_2$ and $J_3$. The **second deviatoric stress invariant**, $J_2$, is a measure of the magnitude of the [deviatoric stress](@entry_id:163323), related to the elastic shear [strain energy density](@entry_id:200085). It is defined as:

$J_2 = \frac{1}{2} \boldsymbol{s}:\boldsymbol{s} = \frac{1}{2} s_{ij}s_{ij}$

In terms of principal deviatoric stresses ($s_i = \sigma_i - p$), this becomes $J_2 = \frac{1}{2}(s_1^2 + s_2^2 + s_3^2)$. It is often convenient to work with a related quantity, the **equivalent shear stress** or **deviatoric stress magnitude**, $q$, defined as:

$q = \sqrt{3J_2} = \sqrt{\frac{1}{2}[(\sigma_1 - \sigma_2)^2 + (\sigma_2 - \sigma_3)^2 + (\sigma_3 - \sigma_1)^2]}$

The **third deviatoric stress invariant**, $J_3$, relates to the skewness of the stress state and distinguishes between different types of shear. It is defined as the determinant of the [deviatoric stress tensor](@entry_id:267642):

$J_3 = \det(\boldsymbol{s}) = s_1 s_2 s_3$

The invariants $p$, $J_2$, and $J_3$ provide a complete, coordinate-independent description of the stress state. The state of stress can be visualized as a point in a three-dimensional space defined by these invariants. A particularly useful visualization is the **deviatoric plane**, which is a plane in [principal stress space](@entry_id:184388) perpendicular to the hydrostatic axis ($\sigma_1 = \sigma_2 = \sigma_3$). On this plane, $p$ is constant, and the stress state is defined by $J_2$ and a third quantity, the **Lode angle**, $\theta$. The Lode angle describes the [angular position](@entry_id:174053) on a circle of constant $J_2$ and thus characterizes the influence of the intermediate [principal stress](@entry_id:204375), $\sigma_2$. One common definition relates the Lode angle to the invariants $J_2$ and $J_3$ [@problem_id:3506654]:

$\cos(3\theta) = \frac{3\sqrt{3}}{2} \frac{J_3}{J_2^{3/2}}$

Different conventions exist for the range and definition of $\theta$. A convention often used in [computational plasticity](@entry_id:171377) defines the range such that specific physical states correspond to particular angles. For instance, **axisymmetric (or triaxial) compression** ($\sigma_1 > \sigma_2 = \sigma_3$) and **axisymmetric (or triaxial) extension** ($\sigma_1 = \sigma_2 > \sigma_3$) represent fundamental loading paths. These states correspond to vertices of the [yield surface](@entry_id:175331) in the deviatoric plane. A state of **pure shear** occurs when one of the principal deviatoric stresses is zero. For example, if $s_2=0$, then $J_3=0$, which implies $\cos(3\theta) = 0$ and gives $\theta = \pi/6$ rad. [@problem_id:3506654] [@problem_id:3506643]

To illustrate, consider a principal stress state of $\boldsymbol{\sigma} = \mathrm{diag}(100, 50, 0)$ MPa.
The [mean stress](@entry_id:751819) is $p = \frac{1}{3}(100+50+0) = 50$ MPa.
The principal deviatoric stresses are $s_1 = 100 - 50 = 50$ MPa, $s_2 = 50 - 50 = 0$ MPa, and $s_3 = 0 - 50 = -50$ MPa.
The invariants are $J_2 = \frac{1}{2}(50^2 + 0^2 + (-50)^2) = 2500$ MPa$^2$ and $J_3 = (50)(0)(-50) = 0$ MPa$^3$.
The deviatoric stress magnitude is $q = \sqrt{3 \times 2500} = 50\sqrt{3}$ MPa.
Since $J_3=0$, this represents a pure shear state, and the Lode angle calculation yields $\theta = \pi/6$ rad. [@problem_id:3506654]

### The Yield Criterion: A Boundary for Elasticity

The **[yield criterion](@entry_id:193897)** defines the limit of elastic behavior. It is represented by a surface in [stress space](@entry_id:199156), described by a **yield function**, $f(\boldsymbol{\sigma}, \boldsymbol{\kappa}) = 0$, where $\boldsymbol{\kappa}$ represents a set of [internal state variables](@entry_id:750754) (e.g., hardening parameters). A stress state is considered elastic if $f  0$, and [plastic deformation](@entry_id:139726) may occur if $f = 0$. Stress states where $f > 0$ are inadmissible. The shape of this surface reflects the physical mechanisms that govern material failure.

#### Pressure-Independent Criteria: Tresca and von Mises

For materials whose yield strength is largely unaffected by hydrostatic pressure, such as metals, the [yield criteria](@entry_id:178101) are functions of the deviatoric stress only.

The **Tresca criterion** postulates that yielding occurs when the maximum shear stress, $\tau_{max}$, at a point reaches a critical value, the material's [shear strength](@entry_id:754762) $k$. In a 3D stress state, the maximum shear stress is half the difference between the largest and smallest principal stresses ($\sigma_1 \ge \sigma_2 \ge \sigma_3$):

$\tau_{max} = \frac{\sigma_1 - \sigma_3}{2}$

The [yield function](@entry_id:167970) is therefore $f = \frac{\sigma_1 - \sigma_3}{2} - k$. For example, given a stress state $\boldsymbol{\sigma} = \mathrm{diag}(80, 20, -10)$ MPa and a shear strength $k=30$ MPa, the maximum shear stress is $\tau_{max} = \frac{80 - (-10)}{2} = 45$ MPa. The [yield function](@entry_id:167970) evaluates to $f = 45 - 30 = 15$ MPa. Since $f > 0$, the material has yielded. [@problem_id:3506610]. In the deviatoric plane, the Tresca criterion plots as an irregular hexagon.

The **von Mises criterion** proposes that yielding begins when the second deviatoric stress invariant, $J_2$, reaches a critical value. It is often called a $J_2$-plasticity model. The [yield function](@entry_id:167970) is:

$f = \sqrt{J_2} - k$

Expressed in terms of the [deviatoric stress](@entry_id:163323) magnitude $q$, this becomes $f = q/\sqrt{3} - k = 0$. Unlike Tresca, the von Mises criterion is a smooth function and plots as a circle in the deviatoric plane. This circular shape means that the predicted yield strength is independent of the Lode angle $\theta$, implying no sensitivity to the intermediate principal stress. [@problem_id:3506665]

#### Pressure-Dependent Criteria: Mohr-Coulomb, Drucker-Prager, and Hoek-Brown

The strength of most [geomaterials](@entry_id:749838), such as soils and rocks, is highly dependent on confining pressure; they become stronger under compression. This behavior necessitates the use of [pressure-dependent yield criteria](@entry_id:197002).

The **Mohr-Coulomb criterion** is a cornerstone of [soil mechanics](@entry_id:180264). It extends the concept of [sliding friction](@entry_id:167677) to a continuum, stating that failure occurs on a plane when the shear stress $\tau$ on that plane satisfies a [linear relationship](@entry_id:267880) with the [normal stress](@entry_id:184326) $\sigma_n$ (compression positive):

$\tau = c + \sigma_n \tan\phi$

where $c$ is the **cohesion** and $\phi$ is the **[angle of internal friction](@entry_id:197521)**. In terms of principal stresses, this criterion becomes $\sigma_1(1-\sin\phi) = \sigma_3(1+\sin\phi) + 2c\cos\phi$. Because it depends on $\sigma_1$ and $\sigma_3$, it is sensitive to the Lode angle. In the deviatoric plane, it plots as an irregular hexagon, similar to Tresca, but its size increases with mean pressure $p$.

This Lode angle dependence results in different strengths for different stress paths. For a fixed mean pressure $p$, the strength $q$ is highest in triaxial compression ($\theta$ at one extreme of its range) and lowest in triaxial extension ($\theta$ at the other extreme). For example, under triaxial compression ($\sigma_1 > \sigma_2 = \sigma_3$), the criterion can be written as $q = M_c p + k_c$, while for triaxial extension ($\sigma_1 = \sigma_2 > \sigma_3$), it is $q = M_e p + k_e$, where the slope $M$ and intercept $k$ are functions of $c$ and $\phi$. Specifically, $M_c = \frac{6\sin\phi}{3-\sin\phi}$ and $M_e = \frac{6\sin\phi}{3+\sin\phi}$. Since $\sin\phi > 0$ for a frictional material, it is clear that $M_c > M_e$, meaning the material is stronger in triaxial compression. [@problem_id:3506651] [@problem_id:3506665]

The corners of the Mohr-Coulomb hexagon introduce mathematical singularities, which pose challenges for numerical algorithms. The **Drucker-Prager criterion** provides a smooth, conical approximation to the Mohr-Coulomb pyramid. Its [yield function](@entry_id:167970) is linear in $p$ and depends on $\sqrt{J_2}$:

$f = \alpha p + \sqrt{J_2} - k = 0$

This criterion plots as a circle in the deviatoric plane, meaning it is insensitive to the Lode angle. The parameters $\alpha$ and $k$ can be calibrated to match the Mohr-Coulomb criterion along specific stress paths, for instance, by making the Drucker-Prager circle circumscribe the Mohr-Coulomb hexagon, matching it at the triaxial compression vertices. This provides a computationally robust alternative, albeit at the cost of ignoring the experimentally observed difference in strength between compression and extension. [@problem_id:3506635] [@problem_id:3506665]

For rock masses, which are characterized by the presence of discontinuities, the empirical **Hoek-Brown criterion** is widely used. The generalized version relates the major and minor [principal stresses](@entry_id:176761) at failure:

$\sigma_1 = \sigma_3 + \sigma_{ci} \left( m_b \frac{\sigma_3}{\sigma_{ci}} + s \right)^a$

The parameters have clear physical interpretations: $\sigma_{ci}$ is the uniaxial compressive strength of the intact rock; $m_b$ is a material constant that is reduced from its intact value by jointing; $s$ is a structural parameter that ranges from $s=1$ for intact rock to $s=0$ for a completely fractured or disaggregated rock mass; and $a$ is an exponent that controls the curvature of the failure envelope. [@problem_id:3506648] This criterion is inherently non-linear and, in its generalized 3D form, depends on the Lode angle, creating a smoothed triangular shape in the deviatoric plane that fits experimental data for rocks better than the Mohr-Coulomb hexagon.

### The Flow Rule: Governing the Direction of Plastic Strain

Once the stress state reaches the [yield surface](@entry_id:175331), [plastic deformation](@entry_id:139726) begins. The [yield criterion](@entry_id:193897) tells us *if* yielding occurs, but it does not specify the *nature* of the ensuing plastic strain. This is the role of the **[flow rule](@entry_id:177163)**, which dictates the direction of the plastic [strain rate tensor](@entry_id:198281), $\dot{\boldsymbol{\varepsilon}}^p$.

In [rate-independent plasticity](@entry_id:754082), the [flow rule](@entry_id:177163) is given by:

$\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}$

Here, $\dot{\lambda}$ is the **[plastic multiplier](@entry_id:753519)**, a non-negative scalar that determines the magnitude of plastic flow, and $g(\boldsymbol{\sigma})$ is a scalar function of stress known as the **[plastic potential](@entry_id:164680)**. The gradient $\frac{\partial g}{\partial \boldsymbol{\sigma}}$ defines the direction of [plastic flow](@entry_id:201346) in the nine-dimensional [stress space](@entry_id:199156). Geometrically, this direction is normal to the [level surfaces](@entry_id:196027) of the plastic [potential function](@entry_id:268662) $g$.

A critical distinction is made based on the choice of $g$:
1.  **Associated Flow Rule**: If the [plastic potential](@entry_id:164680) is chosen to be the same as the yield function ($g = f$), the flow is said to be associated. In this case, the plastic strain rate is normal to the [yield surface](@entry_id:175331) itself. This is a common assumption for metals.
2.  **Non-Associated Flow Rule**: If the [plastic potential](@entry_id:164680) differs from the yield function ($g \neq f$), the flow is non-associated. The plastic [strain rate](@entry_id:154778) is normal to the [plastic potential](@entry_id:164680) surface, which is generally not aligned with the normal to the yield surface. [@problem_id:3506592]

For pressure-dependent materials like soils and rocks, an [associated flow rule](@entry_id:201731) ($g=f$) for a criterion like Mohr-Coulomb or Drucker-Prager predicts a large amount of plastic volume increase ([dilatancy](@entry_id:201001)) upon shearing, because the yield surfaces are inclined with respect to the deviatoric plane. Experimental observations often show that the actual dilatancy is significantly less than predicted by an associated rule. This discrepancy motivates the use of a [non-associated flow rule](@entry_id:172454), where a separate [plastic potential](@entry_id:164680) $g$ is chosen to better capture the observed volumetric behavior. For instance, a Drucker-Prager model might use a yield function $f = \alpha p + \sqrt{J_2} - k$ but a [plastic potential](@entry_id:164680) $g = \alpha_g p + \sqrt{J_2}$ with a [dilatancy](@entry_id:201001) parameter $\alpha_g  \alpha$. This reduces the predicted plastic [volumetric strain rate](@entry_id:272471) for a given amount of shear. [@problem_id:3506592]

### The Integrated Framework for Elastoplasticity

To create a complete and computationally tractable model, the concepts of yielding and flow must be integrated within a consistent mathematical framework. This framework is built upon three pillars: the yield condition, the [flow rule](@entry_id:177163), and the loading/unloading conditions.

#### Loading-Unloading Conditions and Consistency

The transition between elastic and plastic states is governed by a set of criteria known as the **Karush-Kuhn-Tucker (KKT) conditions**. For a yield function $f(\boldsymbol{\sigma}, \kappa) \le 0$ and [plastic multiplier](@entry_id:753519) $\dot{\lambda}$, these are:

1.  **Admissibility**: $f \le 0$ (The stress state must be inside or on the [yield surface](@entry_id:175331)).
2.  **Non-negative Dissipation**: $\dot{\lambda} \ge 0$ (Plastic flow is irreversible).
3.  **Complementarity**: $\dot{\lambda} f = 0$ (Plastic flow occurs only when the stress state is on the yield surface).

These three conditions mathematically define all possible scenarios:
- **Elastic state**: $f  0$, which requires $\dot{\lambda} = 0$.
- **Plastic loading**: $f = 0$ and $\dot{\lambda} > 0$.
- **Elastic unloading**: $f = 0$ initially, but the load increment causes the stress state to move into the elastic domain ($f  0$), so $\dot{\lambda} = 0$. [@problem_id:3506593]

During [plastic loading](@entry_id:753518), the stress state must remain on the yield surface. This imposes an additional constraint known as the **consistency condition**:

$\dot{f} = 0$

This condition states that the rate of change of the yield function must be zero during plastic flow. It is crucial for determining the value of the [plastic multiplier](@entry_id:753519) $\dot{\lambda}$. These conditions hold true regardless of whether the [flow rule](@entry_id:177163) is associated or non-associated. The yield function $f$ always defines the elastic domain, while the [plastic potential](@entry_id:164680) $g$ only dictates the flow direction. This is a critical point in the numerical implementation of plasticity models, such as in **return-mapping algorithms**, where the final stress state is projected back onto the [yield surface](@entry_id:175331) $f=0$ along a direction determined by $g$. [@problem_id:3506592] [@problem_id:3506593]

#### Thermodynamic Admissibility

A final, overarching principle is that any [constitutive model](@entry_id:747751) must be consistent with the laws of thermodynamics. For plasticity, the second law requires that the rate of **[plastic dissipation](@entry_id:201273)**, $\mathcal{D}$, must be non-negative for any admissible process. The dissipation rate is the work done by the stresses over the plastic strain rates:

$\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p \ge 0$

For an [associated flow rule](@entry_id:201731) ($g=f$), where the yield surface is convex, this condition is automatically satisfied. However, for a [non-associated flow rule](@entry_id:172454), this is not guaranteed and imposes constraints on the choice of the [plastic potential](@entry_id:164680) $g$.

Consider the non-associated Drucker-Prager model with [yield function](@entry_id:167970) $f = \sqrt{J_2} + \alpha_f p - k$ and [plastic potential](@entry_id:164680) $g = \sqrt{J_2} + \alpha_g p$. The [dissipation rate](@entry_id:748577) for a stress state on the yield surface can be derived as $\mathcal{D} = \dot{\lambda}(k + (\alpha_g - \alpha_f)p)$. For this to be non-negative for all possible pressures $p$ on the [yield surface](@entry_id:175331) (which can be very large in tension, i.e., $p \to -\infty$), it can be shown that the parameters must satisfy $0 \le \alpha_g \le \alpha_f$. This ensures that the model is thermodynamically admissible and does not spuriously generate energy. Under these constraints, the minimum possible dissipation rate occurs at the apex of the yield cone and is found to be $\mathcal{D}_{min} = \dot{\lambda} \frac{k \alpha_g}{\alpha_f}$. [@problem_id:3506633] This highlights how fundamental physical principles place rigorous mathematical constraints on the formulation of advanced [constitutive models](@entry_id:174726).