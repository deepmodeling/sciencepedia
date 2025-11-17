## Introduction
Hyperelastic materials, such as rubber and biological soft tissues, are defined by their remarkable ability to undergo immense, reversible deformations, a behavior that classical linear elasticity fails to describe. To accurately predict and engineer with these materials, we must turn to the nonlinear framework of continuum mechanics. Among the most foundational and widely used theories in this domain are the Neo-Hookean and Mooney-Rivlin models. These [constitutive models](@entry_id:174726) provide a powerful yet accessible entry point into the mechanics of soft matter by linking macroscopic mechanical response to a stored [strain energy function](@entry_id:170590). This article serves as a comprehensive guide to understanding these two pivotal models, addressing the gap between abstract theory and practical application.

Over the next three sections, you will embark on a structured journey through the world of [hyperelasticity](@entry_id:168357). We will begin in "Principles and Mechanisms," where we lay the theoretical groundwork, starting from the kinematics of [large deformations](@entry_id:167243) and proceeding to the thermodynamic derivation of the stress from a [strain energy potential](@entry_id:755493). Next, in "Applications and Interdisciplinary Connections," we will apply these models to predict material behavior in common scenarios like [uniaxial tension](@entry_id:188287) and membrane inflation, exploring their relevance in engineering, [biomechanics](@entry_id:153973), and material characterization. Finally, "Hands-On Practices" will provide you with the opportunity to actively engage with the material through guided problems, solidifying your understanding from theoretical derivation to computational implementation.

## Principles and Mechanisms

The behavior of [hyperelastic materials](@entry_id:190241), such as rubber and other elastomers, is characterized by their ability to undergo large, reversible deformations. Unlike linearly elastic materials, their constitutive response is inherently nonlinear. The Neo-Hookean and Mooney-Rivlin models represent foundational frameworks for describing this behavior. This chapter elucidates the fundamental principles that govern these models, from the kinematic description of large deformations to the thermodynamic basis for their [constitutive laws](@entry_id:178936).

### Kinematic Foundations: From Deformation to Invariants

To describe the mechanics of [finite deformation](@entry_id:172086), we must first establish a robust kinematic framework. The motion of a material body is described by a mapping that takes each point $\mathbf{X}$ in the reference (undeformed) configuration to a point $\mathbf{x}$ in the current (deformed) configuration. The local deformation is quantified by the **[deformation gradient](@entry_id:163749)** tensor, $\mathbf{F}$, defined as:
$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}
$$
The tensor $\mathbf{F}$ maps infinitesimal vectors from the reference configuration to the current configuration. It contains information about both local stretching and rotation. The determinant of the [deformation gradient](@entry_id:163749), $J = \det \mathbf{F}$, represents the ratio of a volume element in the current configuration to its corresponding volume in the reference configuration. Thus, $J$ measures the local change in volume.

While $\mathbf{F}$ completely describes the local deformation, it is not an objective measure of strain, as it changes with a [rigid body rotation](@entry_id:167024) of the observer. To formulate constitutive laws that are independent of the observer (a principle known as **[material objectivity](@entry_id:177919)** or [frame-indifference](@entry_id:197245)), we must work with quantities that depend only on the stretching of the material. The primary tensors used for this purpose are the right and left Cauchy-Green deformation tensors.

The **right Cauchy-Green tensor**, $\mathbf{C}$, is a symmetric tensor defined in the reference configuration:
$$
\mathbf{C} = \mathbf{F}^{T}\mathbf{F}
$$
The **left Cauchy-Green tensor**, $\mathbf{B}$, is a [symmetric tensor](@entry_id:144567) defined in the current configuration:
$$
\mathbf{B} = \mathbf{F}\mathbf{F}^{T}
$$
Both $\mathbf{C}$ and $\mathbf{B}$ are pure measures of strain, as they are unaffected by superposed rigid body rotations. They share the same [principal invariants](@entry_id:193522) and their eigenvalues are the squares of the **[principal stretches](@entry_id:194664)**, denoted $(\lambda_1, \lambda_2, \lambda_3)$. The [principal stretches](@entry_id:194664) represent the ratios of the lengths of infinitesimal line elements along three mutually orthogonal principal directions after deformation to their initial lengths.

Constitutive models for [isotropic materials](@entry_id:170678) are typically formulated in terms of the **[principal invariants](@entry_id:193522)** of $\mathbf{C}$ (or $\mathbf{B}$). These invariants are scalar quantities that are independent of the choice of coordinate system. For a tensor $\mathbf{C}$, they are defined as:
$$
I_1 = \mathrm{tr}(\mathbf{C})
$$
$$
I_2 = \frac{1}{2} [(\mathrm{tr}(\mathbf{C}))^2 - \mathrm{tr}(\mathbf{C}^2)]
$$
$$
I_3 = \det(\mathbf{C})
$$
These abstract definitions can be given a more direct physical interpretation by expressing them in terms of the [principal stretches](@entry_id:194664). By considering a coordinate system aligned with the principal directions of stretch, the tensor $\mathbf{C}$ becomes a [diagonal matrix](@entry_id:637782) with components $\lambda_1^2, \lambda_2^2, \lambda_3^2$. A direct calculation then reveals the fundamental relationship between the invariants and the [principal stretches](@entry_id:194664) [@problem_id:2664630]:
$$
I_1 = \lambda_1^2 + \lambda_2^2 + \lambda_3^2
$$
$$
I_2 = \lambda_1^2\lambda_2^2 + \lambda_2^2\lambda_3^2 + \lambda_3^2\lambda_1^2
$$
$$
I_3 = \lambda_1^2\lambda_2^2\lambda_3^2
$$
Furthermore, we can see that $I_3 = (\lambda_1\lambda_2\lambda_3)^2 = (\det \mathbf{F})^2 = J^2$. This directly links the third invariant to the volumetric change.

### The Axiomatic Basis of Isotropic Hyperelasticity

Hyperelastic materials are, by definition, materials for which the stress tensor is derivable from a scalar [potential function](@entry_id:268662) known as the **[strain energy density function](@entry_id:199500)**, $W$. This function represents the elastic energy stored in the material per unit of reference volume. The specific form of $W$ for a given material is constrained by fundamental physical principles.

First, the principle of **[material objectivity](@entry_id:177919)** (or [frame-indifference](@entry_id:197245)) requires that the stored energy must be independent of any [rigid body rotation](@entry_id:167024) applied to the deformed body. This means that if we replace $\mathbf{F}$ with $\mathbf{R}\mathbf{F}$, where $\mathbf{R}$ is a proper orthogonal tensor, the energy must not change: $W(\mathbf{R}\mathbf{F}) = W(\mathbf{F})$. Using the [polar decomposition theorem](@entry_id:753554), which states that $\mathbf{F} = \mathbf{R}_p \mathbf{U}$ where $\mathbf{R}_p$ is a rotation and $\mathbf{U}$ is the symmetric, positive-definite [right stretch tensor](@entry_id:193756), objectivity can be shown to reduce the dependency of $W$ from the full [deformation gradient](@entry_id:163749) $\mathbf{F}$ to the [right stretch tensor](@entry_id:193756) $\mathbf{U}$ only. Since $\mathbf{C} = \mathbf{U}^2$ and there is a one-to-one correspondence between $\mathbf{U}$ and $\mathbf{C}$, this is equivalent to stating that the [strain energy](@entry_id:162699) can be expressed as a function of the right Cauchy-Green tensor, $W = \widehat{W}(\mathbf{C})$ [@problem_id:2664596].

Second, for an **isotropic** material, the constitutive response must be independent of the orientation of the material itself. This means that rotating the reference configuration before deforming the material should not alter the stored energy. Mathematically, this translates to the condition $\widehat{W}(\mathbf{C}) = \widehat{W}(\mathbf{Q}^{T}\mathbf{C}\mathbf{Q})$ for all proper orthogonal tensors $\mathbf{Q}$. A function with this property is known as an isotropic scalar-valued function of a symmetric tensor. A central result from representation theory states that any such function can be expressed as a function of the [principal invariants](@entry_id:193522) of its tensor argument. Therefore, for an isotropic [hyperelastic material](@entry_id:195319), the [strain energy function](@entry_id:170590) must take the general form [@problem_id:2664596]:
$$
W = \bar{W}(I_1, I_2, I_3)
$$
Equivalently, because the invariants are the [elementary symmetric polynomials](@entry_id:152224) of the squared [principal stretches](@entry_id:194664), this implies that $W$ can also be expressed as a symmetric function of the [principal stretches](@entry_id:194664), $W = \phi(\lambda_1, \lambda_2, \lambda_3)$ [@problem_id:2664596].

### Constitutive Relations: From Energy to Stress

The relationship between the stored energy $W$ and the stress is not an arbitrary postulate but a direct consequence of the Second Law of Thermodynamics. For an [isothermal process](@entry_id:143096) in a material with no internal dissipative mechanisms, the **Clausius-Duhem inequality** requires that the rate of mechanical work done on the material cannot be less than the rate of increase of its stored (free) energy. For a [hyperelastic material](@entry_id:195319), these two rates must be exactly equal, implying zero dissipation.

By expressing the [stress power](@entry_id:182907) in terms of a [work-conjugate stress](@entry_id:182069)-strain pair and equating it to the rate of change of the stored energy, $\dot{W}$, we can derive the constitutive law. This procedure, known as the Coleman-Noll procedure, leads to a fundamental expression for the symmetric **Second Piola-Kirchhoff (PK2) stress tensor**, $\mathbf{S}$, which is work-conjugate to the rate of the Green-Lagrange strain tensor $\mathbf{E} = \frac{1}{2}(\mathbf{C}-\mathbf{I})$:
$$
\mathbf{S} = 2 \frac{\partial W}{\partial \mathbf{C}}
$$
The PK2 stress $\mathbf{S}$ is a [nominal stress](@entry_id:201335) measure referred to the reference configuration. In experimental and engineering practice, we are often more interested in the **Cauchy stress tensor**, $\mathbf{\sigma}$, which is the true stress acting on the current, deformed configuration. The Cauchy stress can be obtained from the PK2 stress via a "push-forward" transformation. This transformation yields the general [constitutive equation](@entry_id:267976) for the Cauchy stress of a compressible [hyperelastic material](@entry_id:195319) [@problem_id:2664664]:
$$
\mathbf{\sigma} = \frac{1}{J} \mathbf{F} \mathbf{S} \mathbf{F}^{T} = \frac{2}{J} \mathbf{F} \frac{\partial W}{\partial \mathbf{C}} \mathbf{F}^{T}
$$
This equation is the cornerstone of hyperelastic [constitutive modeling](@entry_id:183370), providing the explicit link from any given [strain energy function](@entry_id:170590) $W$ to the physically relevant Cauchy stress.

### Modeling Incompressibility

Many rubber-like materials are [nearly incompressible](@entry_id:752387), meaning their volume remains almost constant even under [large deformations](@entry_id:167243). Modeling such materials as perfectly incompressible simplifies the theory and is often an excellent approximation. The kinematic constraint for [incompressibility](@entry_id:274914) is:
$$
J = \det \mathbf{F} = 1
$$
This constraint implies that the third invariant is fixed, $I_3 = J^2 = 1$. Consequently, for an [incompressible material](@entry_id:159741), the [strain energy function](@entry_id:170590) depends at most on the first two invariants, $W = W(I_1, I_2)$ [@problem_id:2664596].

The incompressibility constraint cannot be satisfied for arbitrary deformations; rather, it imposes a constraint on the possible deformation fields. In the constitutive framework, this is handled by introducing a **Lagrange multiplier field**, $p$. This field has the physical interpretation of a hydrostatic pressure, which is an unknown reaction pressure that develops within the material to enforce the volume-preserving constraint. A crucial point is that this pressure $p$ is **not a material parameter** determined by the [constitutive law](@entry_id:167255). Instead, it is an independent field variable that must be solved for as part of the overall [boundary value problem](@entry_id:138753), alongside the deformation field. Its value is determined by the need to satisfy the [equations of equilibrium](@entry_id:193797) and the boundary conditions simultaneously with the constraint $J=1$ [@problem_id:2664634].

For purely displacement-prescribed boundary conditions, the field $p$ is only determined up to an arbitrary additive constant, as adding a constant to the pressure field does not alter the [equilibrium equations](@entry_id:172166) [@problem_id:2664634]. An absolute value for $p$ can only be fixed if a traction or pressure value is specified somewhere on the boundary.

With the inclusion of the Lagrange multiplier, the general expression for the Cauchy stress of an incompressible, isotropic [hyperelastic material](@entry_id:195319) becomes:
$$
\mathbf{\sigma} = -p\mathbf{I} + 2 \frac{\partial W}{\partial I_1} \mathbf{B} - 2 \frac{\partial W}{\partial I_2} \mathbf{B}^{-1}
$$
Here, the dependence on the second invariant $I_2$ is often expressed via the inverse of the left Cauchy-Green tensor, $\mathbf{B}^{-1}$, which is valid for [incompressible materials](@entry_id:175963) since $\mathbf{B}^{-1}$ can be related to $\mathbf{B}^2$ through the Cayley-Hamilton theorem when $\det \mathbf{B} = 1$.

### Canonical Models: Neo-Hookean and Mooney-Rivlin

The general form $W(I_1, I_2)$ provides a template for developing specific material models. The Neo-Hookean and Mooney-Rivlin models are the simplest and most widely used examples.

#### The Incompressible Neo-Hookean Model
The **Neo-Hookean model** is the simplest model for isotropic [hyperelasticity](@entry_id:168357). It is motivated by the statistical mechanics of ideal polymer chains and postulates that the [strain energy](@entry_id:162699) is a linear function of only the first invariant, $I_1$. Its [strain energy density](@entry_id:200085) is given by:
$$
W = C_{10}(I_1 - 3) = \frac{\mu}{2}(I_1 - 3)
$$
where $C_{10}$ is a material constant, and $\mu = 2C_{10}$ is the initial shear modulus. The constant term $-3$ ensures that the energy is zero in the undeformed state where $I_1=3$. Since $W$ has no dependence on $I_2$, the term $\partial W/\partial I_2$ is zero. The [constitutive law](@entry_id:167255) for the Cauchy stress simplifies considerably [@problem_id:2664598]:
$$
\mathbf{\sigma} = \mu \mathbf{B} - p\mathbf{I}
$$

#### The Incompressible Mooney-Rivlin Model
The Neo-Hookean model provides a good approximation for some rubbers but fails to capture the behavior of others, even at moderate strains. The **Mooney-Rivlin model** is a phenomenological extension that adds a linear dependence on the second invariant, $I_2$:
$$
W = C_{10}(I_1 - 3) + C_{01}(I_2 - 3)
$$
Here, $C_{10}$ and $C_{01}$ are material constants. The initial shear modulus for this model is $\mu = 2(C_{10} + C_{01})$. The Neo-Hookean model is a special case of the Mooney-Rivlin model where $C_{01}=0$. The Cauchy stress for a Mooney-Rivlin material is:
$$
\mathbf{\sigma} = -p\mathbf{I} + 2C_{10}\mathbf{B} - 2C_{01}\mathbf{B}^{-1}
$$
The inclusion of the $C_{01}$ term provides an additional degree of freedom to fit experimental data. A classic demonstration of its effect is in uniaxial extension. For the same small-strain [shear modulus](@entry_id:167228) $\mu$, the [nominal stress](@entry_id:201335)-stretch response of the Mooney-Rivlin model with $C_{01} > 0$ has a lower tangent modulus at large stretches compared to the Neo-Hookean model. This often leads to a better fit for the S-shaped curves typical of many elastomers in tension [@problem_id:2664626]. Specifically, the [nominal stress](@entry_id:201335) $P_{11}$ relations are:
$$
P_{11}^{\mathrm{NH}}(\lambda) = \mu(\lambda - \lambda^{-2})
$$
$$
P_{11}^{\mathrm{MR}}(\lambda) = 2C_{10}(\lambda - \lambda^{-2}) + 2C_{01}(1 - \lambda^{-3})
$$
The Mooney-Rivlin model's asymptotic tangent modulus is $2C_{10}$, whereas the Neo-Hookean model's is $\mu$. Since $\mu = 2C_{10} + 2C_{01}$, a positive $C_{01}$ reduces the large-strain stiffness, often improving agreement with experimental results [@problem_id:2664626].

### Extension to Compressible Models: The Isochoric-Volumetric Split

While many rubbers are [nearly incompressible](@entry_id:752387), in some applications or for certain materials (like foams), [compressibility](@entry_id:144559) is significant. A naive application of a model like $W=W(I_1, I_2)$ to a compressible material would lead to unphysical coupling between shear and volumetric responses. For example, a pure dilation could generate deviatoric (shear) stresses.

To address this, a common and physically motivated approach is to decompose the [strain energy](@entry_id:162699) into a part that governs volume changes (volumetric) and a part that governs shape changes (isochoric or deviatoric) [@problem_id:2664691]. This is achieved by a [multiplicative decomposition](@entry_id:199514) of the [deformation gradient](@entry_id:163749) into a volumetric part and an isochoric part: $\mathbf{F} = J^{1/3}\bar{\mathbf{F}}$, where $\det \bar{\mathbf{F}} = 1$. This leads to a modified, or isochoric, right Cauchy-Green tensor:
$$
\bar{\mathbf{C}} = J^{-2/3}\mathbf{C}
$$
By construction, $\det \bar{\mathbf{C}} = 1$. The isochoric invariants $\bar{I}_1 = \mathrm{tr}(\bar{\mathbf{C}})$ and $\bar{I}_2 = \frac{1}{2} [(\mathrm{tr}(\bar{\mathbf{C}}))^2 - \mathrm{tr}(\bar{\mathbf{C}}^2)]$ now measure purely distortional deformation. The strain energy is then additively split:
$$
W = W_{\text{iso}}(\bar{I}_1, \bar{I}_2) + U(J)
$$
Here, $W_{\text{iso}}$ is the isochoric (shear) energy, and $U(J)$ is the volumetric energy, which penalizes changes in volume from $J=1$. This form ensures that pure volumetric deformations (where $\bar{\mathbf{C}}=\mathbf{I}$) do not generate [deviatoric stress](@entry_id:163323), and pure isochoric deformations do not generate hydrostatic stress in a stress-free reference state [@problem_id:2664691].

A **compressible Mooney-Rivlin model** can be formulated using this split [@problem_id:2582958]:
$$
W = C_1(\bar{I}_1 - 3) + C_2(\bar{I}_2 - 3) + U(J)
$$
In this form, the parameters $C_1$ and $C_2$ exclusively control the material's resistance to shape change. The linearized, small-strain shear modulus is given by $\mu_0 = 2(C_1 + C_2)$ and is independent of the volumetric part. The volumetric behavior, including the [bulk modulus](@entry_id:160069) $K_0 = U''(1)$, is determined solely by the function $U(J)$.

### Limitations and Advanced Concepts

While the Neo-Hookean and Mooney-Rivlin models are cornerstones of rubber elasticity, they have well-understood limitations that motivate the development of more advanced models.

#### Strain Stiffening
At very large stretches, the polymer chains within a rubber network approach their maximum possible extension. This leads to a dramatic, abrupt increase in stiffness, a phenomenon known as **[strain stiffening](@entry_id:198587)** or "locking". The polynomial-based forms of the Neo-Hookean and Mooney-Rivlin models cannot capture this behavior. Their stress-stretch curves, being [rational functions](@entry_id:154279) of stretch, grow polynomially and do not exhibit the required vertical asymptote at a finite limiting stretch [@problem_id:2664604]. To model this, one must use [strain energy](@entry_id:162699) functions that incorporate a singularity. A classic example is the **Gent model**, which has a logarithmic form:
$$
W = -\frac{\mu J_m}{2} \ln \left(1 - \frac{I_1-3}{J_m}\right)
$$
This function becomes singular as $I_1$ approaches a limiting value $I_{1,\max} = 3+J_m$, where $J_m$ is a material parameter related to the limiting chain extensibility. This singularity in energy translates directly to a divergence in stress at a finite limiting stretch, accurately capturing the strain-stiffening phenomenon [@problem_id:2664604].

#### Inelastic Effects: Hysteresis and the Mullins Effect
Real elastomers are not perfectly elastic. When subjected to cyclic loading, they exhibit [energy dissipation](@entry_id:147406), which manifests as a **hysteresis loop** in the stress-strain diagram. Furthermore, upon reloading, the material is often significantly softer than it was during its initial loading, a phenomenon known as the **Mullins effect**.

Hyperelastic models like the Neo-Hookean and Mooney-Rivlin are, by definition, conservative and history-independent. The stress is a unique function of the current deformation. This means the work done over any closed deformation cycle is zero, and the material has no "memory" of its past loading history. Consequently, these models can capture neither [hysteresis](@entry_id:268538) nor the Mullins effect [@problem_id:2664635].

To model these inelastic phenomena, the constitutive framework must be extended to include **internal variables** and a mechanism for [energy dissipation](@entry_id:147406) consistent with the Second Law of Thermodynamics. Hysteresis is typically captured using a **viscoelastic** framework, where internal variables represent the state of dissipative dashpots in a network model. The Mullins effect is commonly modeled using **pseudo-elasticity** or [continuum damage mechanics](@entry_id:177438), where a damage-like internal variable tracks the maximum previously experienced strain and softens the elastic response accordingly [@problem_id:2664635]. These advanced topics extend beyond the scope of pure [hyperelasticity](@entry_id:168357) but are essential for the [predictive modeling](@entry_id:166398) of real elastomeric components.