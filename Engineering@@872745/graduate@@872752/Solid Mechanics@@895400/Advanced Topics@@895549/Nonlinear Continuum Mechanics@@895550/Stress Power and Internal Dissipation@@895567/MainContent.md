## Introduction
Understanding how materials respond to external forces is a central goal of [solid mechanics](@entry_id:164042). This response is not purely mechanical; it is governed by the fundamental laws of thermodynamics, which dictate how energy is stored and dissipated. At the heart of this interplay lie two critical concepts: **[stress power](@entry_id:182907)**, the rate at which mechanical work is done on a material, and **internal dissipation**, the portion of that work irreversibly lost as heat. The key challenge for engineers and scientists is to develop predictive models that can accurately account for this energy partitioning. Without a rigorous framework for dissipation, it is impossible to model crucial real-world behaviors such as plastic deformation, material damping, or fracture.

This article provides a comprehensive overview of this thermodynamic framework. The first chapter, **Principles and Mechanisms**, establishes the foundational definitions of [stress power](@entry_id:182907) and internal dissipation from first principles of continuum mechanics and thermodynamics. The second chapter, **Applications and Interdisciplinary Connections**, explores how these concepts are applied to model complex material behaviors across a wide range of fields, from [viscoelasticity](@entry_id:148045) to [computational mechanics](@entry_id:174464). Finally, the **Hands-On Practices** chapter offers a series of guided problems to solidify theoretical understanding through practical calculation and computational analysis.

## Principles and Mechanisms

The behavior of materials under load is fundamentally governed by the interplay of mechanics and thermodynamics. Central to this interplay are the concepts of **[stress power](@entry_id:182907)**—the rate at which stresses perform work on a deforming material—and **internal dissipation**, the portion of this work that is irreversibly converted into other energy forms, typically heat. This chapter elucidates the principles defining these quantities and explores the mechanisms through which they govern material response, from simple elasticity to complex, inelastic phenomena.

### The Mechanical Definition of Stress Power

The concept of [stress power](@entry_id:182907) arises directly from the balance of [mechanical energy](@entry_id:162989) within a continuum. Consider an arbitrary sub-region of a deformable body. The total power supplied to this region is the sum of the work done by body forces acting throughout its volume and [surface tractions](@entry_id:169207) acting on its boundary. By applying Cauchy's formula for the [traction vector](@entry_id:189429) and the [divergence theorem](@entry_id:145271), and accounting for the rate of change of kinetic energy, we can isolate the rate at which work is done internally by the stress field. This quantity, expressed per unit of current volume, is the **stress power density**, denoted as $p$.

For a general continuum described by a Cauchy stress tensor $\boldsymbol{\sigma}$ and a velocity field $\mathbf{v}$, the stress [power density](@entry_id:194407) is given by the double contraction of the stress and the [velocity gradient](@entry_id:261686), $\nabla\mathbf{v}$:

$p = \boldsymbol{\sigma} : \nabla\mathbf{v}$

Here, the double contraction $\mathbf{A} : \mathbf{B}$ is defined as the trace of the matrix product $\mathbf{A}^{\mathsf{T}}\mathbf{B}$. This expression represents the total rate of mechanical work per unit volume performed by the stresses on the material element [@problem_id:2691165].

#### Kinematic Decomposition and the Role of Stress Symmetry

To understand the physical nature of [stress power](@entry_id:182907), it is essential to decompose the [velocity gradient tensor](@entry_id:270928), $\nabla\mathbf{v}$, into its symmetric and antisymmetric parts. This unique decomposition yields two fundamental kinematic quantities:

1.  The **[rate-of-deformation tensor](@entry_id:184787)**, $\mathbf{D} = \frac{1}{2}\left(\nabla\mathbf{v} + (\nabla\mathbf{v})^{\mathsf{T}}\right)$, which is symmetric ($\mathbf{D} = \mathbf{D}^{\mathsf{T}}$). This tensor describes the rate at which the material element is stretching and shearing, i.e., changing its shape. Its trace, $\mathrm{tr}(\mathbf{D})$, represents the rate of [volumetric expansion](@entry_id:144241) or compression.

2.  The **[spin tensor](@entry_id:187346)**, $\mathbf{W} = \frac{1}{2}\left(\nabla\mathbf{v} - (\nabla\mathbf{v})^{\mathsf{T}}\right)$, which is skew-symmetric ($\mathbf{W} = -\mathbf{W}^{\mathsf{T}}$). This tensor describes the rate of [rigid-body rotation](@entry_id:268623), or spin, of the material element [@problem_id:2691168].

With this decomposition, $\nabla\mathbf{v} = \mathbf{D} + \mathbf{W}$, the stress power density can be written as:

$p = \boldsymbol{\sigma} : (\mathbf{D} + \mathbf{W}) = \boldsymbol{\sigma} : \mathbf{D} + \boldsymbol{\sigma} : \mathbf{W}$

For a **classical Cauchy continuum**, where body couples are assumed to be absent, the [balance of angular momentum](@entry_id:181848) requires the Cauchy stress tensor $\boldsymbol{\sigma}$ to be symmetric ($\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$). In this ubiquitous and fundamentally important case, the second term in the power expression vanishes identically. This is because the double contraction of any [symmetric tensor](@entry_id:144567) with any [skew-symmetric tensor](@entry_id:199349) is always zero.

Proof: $\boldsymbol{\sigma} : \mathbf{W} = \sigma_{ij} W_{ij}$. Due to symmetry of $\boldsymbol{\sigma}$ and skew-symmetry of $\mathbf{W}$, we have $\sigma_{ij} = \sigma_{ji}$ and $W_{ij} = -W_{ji}$. Thus, $\sigma_{ij} W_{ij} = \sigma_{ji} (-W_{ji}) = -\sigma_{ji} W_{ji}$. By relabeling the indices, this is equivalent to $-\sigma_{ij} W_{ij}$. The only scalar that equals its own negative is zero.

Therefore, for the vast majority of engineering materials modeled within the classical framework, the stress power density simplifies to:

$p = \boldsymbol{\sigma} : \mathbf{D}$

This is a profound result: in a classical continuum, **stresses do work only on the deformational part of the motion, not on the rotational part** [@problem_id:2691165]. This is intuitively clear when considering a pure [rigid-body motion](@entry_id:265795). In such a motion, the body translates and rotates without any change in shape, meaning the [rate-of-deformation tensor](@entry_id:184787) is zero, $\mathbf{D} = \mathbf{0}$. Consequently, the internal stress power density is zero, $p = \boldsymbol{\sigma} : \mathbf{0} = 0$, regardless of the stress state or the rate of rotation. No internal work is done if there is no deformation [@problem_id:2691193].

In more advanced theories for materials with internal [microstructure](@entry_id:148601), such as **Cosserat (or micropolar) media**, the stress tensor $\boldsymbol{\sigma}$ is not necessarily symmetric. In these cases, the term $\boldsymbol{\sigma} : \mathbf{W}$ can be non-zero, representing work done by moments associated with micro-rotations [@problem_id:2691165]. This extension will be discussed in a later section.

### The Thermodynamic Framework: Stored Energy and Dissipation

While the [stress power](@entry_id:182907) $p = \boldsymbol{\sigma} : \mathbf{D}$ represents the total [mechanical power](@entry_id:163535) input to the material's internal structure, thermodynamics dictates how this power is allocated. The First and Second Laws of Thermodynamics provide a rigorous framework for partitioning this power into a recoverable (stored) part and an irrecoverable (dissipated) part.

For an [isothermal process](@entry_id:143096), the key [thermodynamic potential](@entry_id:143115) is the **Helmholtz free energy** per unit mass, $\psi$. The quantity $\rho \psi$, where $\rho$ is the mass density, represents the stored energy density of the system. The Second Law of Thermodynamics, in the form of the **Clausius-Duhem inequality**, provides the fundamental constraint on material behavior. For isothermal processes, this inequality can be written in spatial form as [@problem_id:2887014]:

$\mathcal{D}_{\text{int}} = \boldsymbol{\sigma} : \mathbf{D} - \rho \dot{\psi} \geq 0$

Here, $\dot{\psi}$ is the [material time derivative](@entry_id:190892) of the specific Helmholtz free energy. This inequality provides a clear and powerful interpretation of the [stress power](@entry_id:182907):

*   $\boldsymbol{\sigma} : \mathbf{D}$ is the total [mechanical power](@entry_id:163535) density supplied by the stresses.
*   $\rho \dot{\psi}$ is the rate of change of the stored energy density. This is the portion of the power that is stored in a recoverable manner, for instance, as [elastic strain energy](@entry_id:202243).
*   $\mathcal{D}_{\text{int}}$ is the **internal [dissipation rate](@entry_id:748577)**, which must be non-negative. It represents the portion of the [stress power](@entry_id:182907) that is irreversibly converted, typically into heat, due to phenomena like viscosity or plasticity.

This single inequality is the cornerstone of modern [constitutive modeling](@entry_id:183370), as any valid material model must ensure that $\mathcal{D}_{\text{int}} \ge 0$ for all possible deformation processes.

A simple illustration is a material under **hydrostatic stress**, $\boldsymbol{\sigma} = -p\mathbf{I}$, where $p$ is the pressure and $\mathbf{I}$ is the identity tensor. The [stress power](@entry_id:182907) becomes $p = (-p\mathbf{I}) : \mathbf{D} = -p\,\mathrm{tr}(\mathbf{D})$. Since $\mathrm{tr}(\mathbf{D})$ is the rate of [volumetric expansion](@entry_id:144241), we see that for compression ($\mathrm{tr}(\mathbf{D})  0$), the pressure does positive work on the body, and for expansion ($\mathrm{tr}(\mathbf{D}) > 0$), the pressure does negative work [@problem_id:2691168]. Whether this work is stored or dissipated depends on the material's constitutive nature.

### Applications in Constitutive Modeling

The decomposition of [stress power](@entry_id:182907) into stored and dissipated parts provides the primary means of classifying and constructing material models.

#### Hyperelasticity versus Inelasticity

A material is defined as **hyperelastic** if its [stress response](@entry_id:168351) can be derived solely from a stored energy potential (the Helmholtz free energy, in this context). In this case, the [stress power](@entry_id:182907) is always exactly equal to the rate of change of stored energy, $\boldsymbol{\sigma} : \mathbf{D} = \rho \dot{\psi}$. Consequently, the internal dissipation is identically zero, $\mathcal{D}_{\text{int}} = 0$. A key consequence is that the work done by the stresses over any closed deformation cycle is zero. The material response is path-independent.

In contrast, **inelastic materials**, which include viscoelastic and plastic materials, exhibit dissipation ($\mathcal{D}_{\text{int}} > 0$). This positive dissipation is fundamentally linked to path-dependence and energy loss. A simple model that illustrates this is the one-dimensional Kelvin-Voigt solid [@problem_id:2691192], whose [constitutive law](@entry_id:167255) is given by $\sigma = E\varepsilon + \eta\dot{\varepsilon}$. For this material, the Helmholtz free energy can be identified with the elastic stored energy, $\psi = \frac{1}{2} E \varepsilon^2 / \rho$. The rate of change of stored energy density is $\rho\dot{\psi} = E\varepsilon\dot{\varepsilon}$. The [stress power](@entry_id:182907) is $\sigma\dot{\varepsilon} = (E\varepsilon + \eta\dot{\varepsilon})\dot{\varepsilon} = E\varepsilon\dot{\varepsilon} + \eta\dot{\varepsilon}^2$. Applying the Clausius-Duhem inequality, the dissipation is:

$\mathcal{D}_{\text{int}} = \sigma\dot{\varepsilon} - \rho\dot{\psi} = (E\varepsilon\dot{\varepsilon} + \eta\dot{\varepsilon}^2) - E\varepsilon\dot{\varepsilon} = \eta\dot{\varepsilon}^2 \ge 0$

Since the viscosity $\eta$ is positive, the dissipation is always non-negative. The net work done over a closed strain cycle is not zero but is equal to the total dissipated energy $\oint \mathcal{D}_{\text{int}} dt > 0$. This positive work over a cycle is the hallmark of an inelastic material and is the reason the [stress-strain curve](@entry_id:159459) for a [cyclic process](@entry_id:146195) forms a [hysteresis loop](@entry_id:160173).

#### Objectivity in Rate-Dependent Models

When extending [constitutive modeling](@entry_id:183370) to finite strains, the concept of [work conjugacy](@entry_id:194957) becomes crucial. For rate-type constitutive laws, which relate a rate of stress to the rate of deformation (e.g., $\text{(rate of }\boldsymbol{\tau}) = \mathbb{C}:\mathbf{D}$), the choice of stress rate is critical. The **Principle of Material Frame-Indifference (Objectivity)** demands that the [constitutive law](@entry_id:167255) must be independent of the observer.

The simple [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\tau}}$, is *not* an objective rate. A law formulated using $\dot{\boldsymbol{\tau}}$ would incorrectly predict stress changes for a body undergoing a pure [rigid-body rotation](@entry_id:268623), during which $\mathbf{D}=\mathbf{0}$ but the stress tensor components should rotate with the body [@problem_id:2691194]. To remedy this, **[objective stress rates](@entry_id:199282)** (such as the Jaumann, Green-Naghdi, or Truesdell rates) are constructed. These rates are designed to be frame-indifferent and to vanish during pure rigid rotations. Using an [objective stress rate](@entry_id:168809) ensures that the constitutive law correctly predicts zero stress change (in the material's rotating frame) when there is no deformation ($\mathbf{D}=\mathbf{0}$), thus preserving the fundamental principle that [stress power](@entry_id:182907) is only generated by deformation.

#### Advanced Thermodynamic Frameworks for Inelasticity

Modern constitutive theories leverage the dissipation principle within more abstract and powerful frameworks.

The theory of **Generalized Standard Materials (GSM)** provides a systematic way to construct thermodynamically consistent models [@problem_id:2691184]. It postulates a Helmholtz free energy $\psi$ that depends on both observable strains $\boldsymbol{\varepsilon}$ and a set of [internal state variables](@entry_id:750754) $\boldsymbol{\alpha}$, and a **dissipation potential** $\phi$ that depends on the rate of the internal variables $\dot{\boldsymbol{\alpha}}$. By defining the stresses and thermodynamic forces conjugate to these variables, the evolution laws are derived such that the Clausius-Duhem inequality is automatically satisfied. Within this framework, the convexity of the energy potential $\psi$ is crucial for ensuring the stability of the material and the [well-posedness](@entry_id:148590) of [boundary value problems](@entry_id:137204), while the [convexity](@entry_id:138568) of the dissipation potential $\phi$ guarantees positive dissipation and a unique evolution path for the internal variables.

For [finite strain plasticity](@entry_id:175182), often described by the [multiplicative decomposition](@entry_id:199514) of the [deformation gradient](@entry_id:163749) $\mathbf{F} = \mathbf{F}^{\mathrm{e}}\mathbf{F}^{\mathrm{p}}$, the dissipation principle guides the identification of correct [stress and strain](@entry_id:137374)-rate measures in the abstract "intermediate configuration" [@problem_id:2691156]. It leads to the identification of the **Mandel stress tensor** as the work-conjugate measure to the plastic rate of deformation, ensuring that the formulation is independent of both the observer and arbitrary rotations of the intermediate reference frame.

In the limit of rate-independent processes like fracture or [perfect plasticity](@entry_id:753335), an **[energetic formulation](@entry_id:199250)** provides a global-in-time perspective [@problem_id:2691154]. This framework is built upon two core principles: a **stability condition**, which states that the current state is stable if the dissipative cost to reach any other state is greater than or equal to the potential energy release, and a global **[energy balance](@entry_id:150831)**, which is an integrated form of the First Law stating that initial energy plus work from external loads equals final energy plus total accumulated dissipation.

### Extension to Micropolar Continua

The principles of [stress power](@entry_id:182907) and objectivity find elegant application in theories beyond the classical continuum. In a **Cosserat (or micropolar) continuum**, each material point possesses independent [rotational degrees of freedom](@entry_id:141502), described by a [microrotation](@entry_id:184355) vector $\boldsymbol{\varphi}$ and its rate, the microspin $\boldsymbol{\omega}$ [@problem_id:2691161]. This richer kinematics requires an expanded set of stresses and strain rates.

In this theory, the Cauchy stress $\boldsymbol{\sigma}$ is generally non-symmetric, and a **[couple-stress](@entry_id:747952) tensor** $\boldsymbol{\mu}$ emerges, which is conjugate to the gradient of the microspin, $\nabla\boldsymbol{\omega}$. To ensure objectivity, the classical strain-rate measure $\nabla\mathbf{v}$ is replaced by a relative measure that accounts for the [microstructure](@entry_id:148601)'s own rotation, $\boldsymbol{\gamma} = \nabla\mathbf{v} - \mathbf{W}(\boldsymbol{\omega})$, where $\mathbf{W}(\boldsymbol{\omega})$ is the [skew-symmetric tensor](@entry_id:199349) associated with the microspin vector $\boldsymbol{\omega}$. The objective internal [power density](@entry_id:194407) becomes:

$p_{\text{int}} = \boldsymbol{\sigma} : \big(\nabla \boldsymbol{v} - \boldsymbol{W}(\boldsymbol{\omega})\big) + \boldsymbol{\mu} : \nabla \boldsymbol{\omega}$

This expression reveals the new work-conjugate pairs: the force-stress $\boldsymbol{\sigma}$ does work on the relative deformation rate, while the [couple-stress](@entry_id:747952) $\boldsymbol{\mu}$ does work on the gradient of the microspin. This demonstrates the power and generality of the concept of [stress power](@entry_id:182907), which provides a systematic path for extending mechanical and thermodynamic principles to more complex material behaviors.