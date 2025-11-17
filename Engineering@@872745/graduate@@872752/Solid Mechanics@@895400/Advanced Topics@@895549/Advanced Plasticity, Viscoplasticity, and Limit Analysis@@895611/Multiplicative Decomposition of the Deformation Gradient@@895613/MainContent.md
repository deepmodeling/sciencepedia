## Introduction
In the realm of [solid mechanics](@entry_id:164042), describing materials that undergo large, permanent deformations—a behavior known as [finite strain](@entry_id:749398) [elastoplasticity](@entry_id:193198)—presents a significant theoretical challenge. While [infinitesimal strain](@entry_id:197162) theories can rely on a simple additive split of strain into elastic and plastic parts, this approach breaks down when rotations and geometric non-linearities are large. The solution lies in a more profound and physically grounded framework: the [multiplicative decomposition](@entry_id:199514) of the deformation gradient. This powerful concept, which posits that the total deformation gradient $\boldsymbol{F}$ can be factored into an elastic part $\boldsymbol{F}_{\mathrm{e}}$ and a plastic part $\boldsymbol{F}_{\mathrm{p}}$, forms the bedrock of modern continuum [plasticity theory](@entry_id:177023).

This article provides a graduate-level exploration of this fundamental principle. It addresses the crucial need for a constitutively sound method to separate recoverable and dissipative deformation mechanisms at [finite strain](@entry_id:749398). Across three chapters, you will gain a deep understanding of this essential tool. The first chapter, "Principles and Mechanisms," establishes the theoretical foundation, distinguishing the multiplicative postulate from the kinematic polar decomposition and exploring its thermodynamic consequences. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the framework's immense utility in diverse fields, from [metal forming](@entry_id:188560) and materials science to [computational mechanics](@entry_id:174464) and [biomechanics](@entry_id:153973). Finally, "Hands-On Practices" offers a series of guided problems to solidify your comprehension and apply the theory to concrete examples.

## Principles and Mechanisms

This chapter delves into the theoretical underpinnings of [finite strain](@entry_id:749398) [elastoplasticity](@entry_id:193198), focusing on the central concept of the [multiplicative decomposition](@entry_id:199514) of the deformation gradient. We will begin by reviewing the purely kinematic separation of motion into stretch and rotation, and then introduce the constitutive postulate that separates deformation into elastic and plastic parts. This framework allows us to construct thermodynamically consistent models that correctly account for the distinct physical mechanisms of recoverable [elastic strain](@entry_id:189634) and permanent [plastic flow](@entry_id:201346).

### The Kinematic Foundation: Polar Decomposition

Any description of [finite deformation](@entry_id:172086) begins with the **deformation gradient**, $\boldsymbol{F}$, which serves as the [local linear approximation](@entry_id:263289) of the deformation mapping $\boldsymbol{\varphi}(\mathbf{X},t)$. It maps an infinitesimal material line element $d\mathbf{X}$ from the reference configuration to its counterpart $d\mathbf{x}$ in the current configuration:

$$
d\mathbf{x} = \boldsymbol{F} d\mathbf{X}
$$

The condition $\det \boldsymbol{F} > 0$ is assumed throughout, ensuring that the mapping is locally invertible and preserves the orientation of material elements [@problem_id:2663646]. From a purely geometric perspective, the [deformation gradient tensor](@entry_id:150370) $\boldsymbol{F}$ encapsulates the complete local information about how the material is stretched and rotated. The powerful **[polar decomposition theorem](@entry_id:753554)** provides a unique way to disentangle these two effects. For any invertible $\boldsymbol{F}$, it can be factored as:

$$
\boldsymbol{F} = \boldsymbol{R} \boldsymbol{U} = \boldsymbol{V} \boldsymbol{R}
$$

Here, $\boldsymbol{R}$ is a proper orthogonal tensor ($\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R} = \boldsymbol{I}$ and $\det \boldsymbol{R} = +1$), representing a pure **rigid rotation**. The tensors $\boldsymbol{U}$ and $\boldsymbol{V}$ are symmetric and positive-definite, known as the **[right stretch tensor](@entry_id:193756)** and **[left stretch tensor](@entry_id:197330)**, respectively. This decomposition is purely mathematical and kinematic, holding for any deformation without reference to the material's constitution [@problem_id:2663676].

The physical interpretation is direct: the right decomposition $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ can be seen as a sequence where a material element is first stretched and sheared by $\boldsymbol{U}$ in the reference configuration, and then rigidly rotated by $\boldsymbol{R}$ into its final orientation. The left decomposition $\boldsymbol{F} = \boldsymbol{V}\boldsymbol{R}$ reverses this sequence.

The change in length of a material element is governed by the stretch tensors. The squared length of the deformed element $d\mathbf{x}$ is:

$$
|d\mathbf{x}|^2 = d\mathbf{x} \cdot d\mathbf{x} = (\boldsymbol{F}d\mathbf{X}) \cdot (\boldsymbol{F}d\mathbf{X}) = d\mathbf{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} d\mathbf{X})
$$

This defines the **right Cauchy-Green deformation tensor**, $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$. Substituting the [polar decomposition](@entry_id:149541), we find $\boldsymbol{C} = (\boldsymbol{R}\boldsymbol{U})^{\mathsf{T}}(\boldsymbol{R}\boldsymbol{U}) = \boldsymbol{U}^{\mathsf{T}}\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}\boldsymbol{U} = \boldsymbol{U}^2$. Thus, the [right stretch tensor](@entry_id:193756) $\boldsymbol{U}$ is the unique [symmetric positive-definite](@entry_id:145886) square root of $\boldsymbol{C}$. Similarly, the **left Cauchy-Green tensor** (or **Finger tensor**), $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}$, is related to the [left stretch tensor](@entry_id:197330) by $\boldsymbol{B} = \boldsymbol{V}^2$. The eigenvalues of $\boldsymbol{C}$ and $\boldsymbol{B}$ are identical and equal to the squares of the **[principal stretches](@entry_id:194664)**, $\lambda_i^2$, which quantify the amount of stretching along principal axes. The orthonormal eigenvectors of $\boldsymbol{C}$ define these [principal directions](@entry_id:276187) in the reference configuration [@problem_id:2663646].

An essential property of these kinematic quantities relates to the [principle of material frame-indifference](@entry_id:188488) (objectivity). If the current configuration undergoes a superposed rigid rotation $\boldsymbol{Q}$, the [deformation gradient](@entry_id:163749) transforms to $\tilde{\boldsymbol{F}} = \boldsymbol{Q}\boldsymbol{F}$. The new right Cauchy-Green tensor is $\tilde{\boldsymbol{C}} = \tilde{\boldsymbol{F}}^{\mathsf{T}}\tilde{\boldsymbol{F}} = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{C}$. Since $\boldsymbol{C}$ is unchanged, its square root $\boldsymbol{U}$ is also unchanged. The [right stretch tensor](@entry_id:193756) is therefore an **objective** measure of deformation. The [rotation tensor](@entry_id:191990), however, transforms as $\tilde{\boldsymbol{R}} = \boldsymbol{Q}\boldsymbol{R}$ and is not objective [@problem_id:2663646].

### The Constitutive Postulate: Multiplicative Decomposition

While the polar decomposition provides profound geometric insight, it is insufficient for building [constitutive models](@entry_id:174726) of materials that exhibit permanent, or **inelastic**, deformation. The tensors $\boldsymbol{U}$ and $\boldsymbol{R}$ mix the effects of recoverable [elastic deformation](@entry_id:161971) and permanent plastic flow. To model these distinct physical phenomena, we need a decomposition founded on constitutive principles.

For infinitesimal strains, this is achieved through the additive decomposition of the [strain tensor](@entry_id:193332), $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_{\mathrm{e}} + \boldsymbol{\varepsilon}_{\mathrm{p}}$. This simple addition is invalid for finite deformations where [large rotations](@entry_id:751151) and geometric nonlinearities are present. The kinematics of sequential deformations are inherently multiplicative, as dictated by the [chain rule](@entry_id:147422) for composite maps [@problem_id:2663674]. This leads to the central postulate of [finite strain plasticity](@entry_id:175182), the **[multiplicative decomposition](@entry_id:199514)** of the [deformation gradient](@entry_id:163749), first proposed by E. H. Lee:

$$
\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}
$$

Here, $\boldsymbol{F}_{\mathrm{p}}$ is the **[plastic deformation gradient](@entry_id:188153)** and $\boldsymbol{F}_{\mathrm{e}}$ is the **elastic [deformation gradient](@entry_id:163749)**.

#### The Concept of the Intermediate Configuration

This factorization introduces the concept of a local, stress-free **intermediate configuration**. The decomposition is interpreted as a sequence of two distinct mappings [@problem_id:2663674]:

1.  A mapping from the reference configuration to the intermediate configuration, characterized by $\boldsymbol{F}_{\mathrm{p}}$. This mapping represents the permanent, dissipative rearrangement of the material's microstructure, such as dislocation slip in a crystal.

2.  A mapping from the intermediate configuration to the current, deformed configuration, characterized by $\boldsymbol{F}_{\mathrm{e}}$. This mapping represents the recoverable, elastic distortion of the material (e.g., the crystal lattice) that generates the observed stress.

The intermediate configuration is physically understood as the state that would be reached if a small material element were hypothetically excised from the body and elastically unloaded, allowing it to relax to a state of zero stress. The deformation remaining in this relaxed state is the [plastic deformation](@entry_id:139726), $\boldsymbol{F}_{\mathrm{p}}$. The subsequent [elastic deformation](@entry_id:161971), $\boldsymbol{F}_{\mathrm{e}}$, is then what is required to stretch and rotate this relaxed element to fit into its actual, stressed position in the current body [@problem_id:2663648]. This conceptual framework is the key to separating recoverable and permanent deformations at [finite strain](@entry_id:749398).

#### Distinguishing Kinematic and Constitutive Decompositions

It is crucial to distinguish the [multiplicative decomposition](@entry_id:199514) $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}$ from the [polar decomposition](@entry_id:149541) $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ [@problem_id:2663676].

*   **Nature**: Polar decomposition is purely kinematic and unique. It applies to any invertible tensor and carries no information about the material's properties. The [multiplicative decomposition](@entry_id:199514) is a **constitutive postulate**. It is not a general mathematical theorem but a physical hypothesis about material behavior. Its factors, $\boldsymbol{F}_{\mathrm{e}}$ and $\boldsymbol{F}_{\mathrm{p}}$, are [internal state variables](@entry_id:750754) whose evolution must be described by constitutive laws (a [flow rule](@entry_id:177163) for $\boldsymbol{F}_{\mathrm{p}}$ and an elastic law for $\boldsymbol{F}_{\mathrm{e}}$).

*   **Uniqueness**: The polar decomposition is unique. The [multiplicative decomposition](@entry_id:199514) is inherently non-unique, a point we will elaborate on shortly.

*   **Interpretation**: In polar decomposition, $\boldsymbol{R}$ is a pure rotation and $\boldsymbol{U}$ is a pure stretch. In the multiplicative split, $\boldsymbol{F}_{\mathrm{e}}$ and $\boldsymbol{F}_{\mathrm{p}}$ are general tensors, each containing both stretch and rotation. For instance, the physically motivated case for many metals involves large plastic shearing and rotation ($\boldsymbol{F}_{\mathrm{p}}$) but small elastic strains, allowing the multiplicative framework to model phenomena far beyond the reach of linearized, additive strain theories [@problem_id:2663648]. Equating the factors of the two decompositions (e.g., $\boldsymbol{F}_{\mathrm{e}} = \boldsymbol{R}$, $\boldsymbol{F}_{\mathrm{p}} = \boldsymbol{U}$) is physically nonsensical, as it would imply that elastic response is purely rotational (zero stiffness) and plastic response is purely stretching.

### Fundamental Properties of the Multiplicative Decomposition

#### Volumetric and Isochoric Decomposition

The multiplicative property of the determinant applies directly to the decomposition: $J = \det(\boldsymbol{F}) = \det(\boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}) = \det(\boldsymbol{F}_{\mathrm{e}})\det(\boldsymbol{F}_{\mathrm{p}})$. Letting $J_{\mathrm{e}} = \det(\boldsymbol{F}_{\mathrm{e}})$ and $J_{\mathrm{p}} = \det(\boldsymbol{F}_{\mathrm{p}})$, we have:

$$
J = J_{\mathrm{e}} J_{\mathrm{p}}
$$

This elegantly separates the total volume change ratio $J$ into elastic and plastic contributions. For many crystalline metals, [plastic deformation](@entry_id:139726) occurs primarily through dislocation slip, which is a shear mechanism that conserves volume. This is modeled by the common assumption of **[plastic incompressibility](@entry_id:183440)**, or isochoric [plastic flow](@entry_id:201346):

$$
J_{\mathrm{p}} = \det(\boldsymbol{F}_{\mathrm{p}}) = 1
$$

Under this widely used assumption, the Jacobian relation simplifies to $J = J_{\mathrm{e}}$. This implies that any change in the material's volume is accommodated entirely by the elastic deformation, i.e., by the compression or expansion of the atomic lattice [@problem_id:2663674].

#### Incompatibility, the Intermediate Configuration, and Dislocations

A profound consequence of the multiplicative framework arises from the nature of [plastic deformation](@entry_id:139726). In a crystalline solid, [plastic flow](@entry_id:201346) is mediated by the motion of defects known as **dislocations**. If there is a non-uniform distribution of dislocations, the material lattice becomes curved. This means that after plastic deformation, the local neighborhoods no longer fit together perfectly to form a continuous body. The [plastic deformation](@entry_id:139726) field $\boldsymbol{F}_{\mathrm{p}}(\mathbf{X})$ cannot be described as the gradient of a single, continuous placement map.

Mathematically, a [tensor field](@entry_id:266532) can be expressed as the [gradient of a vector](@entry_id:188005) field only if its curl is zero. The presence of a net dislocation density, referred to as **Geometrically Necessary Dislocations (GNDs)**, results in a non-zero curl of the [plastic deformation gradient](@entry_id:188153):

$$
\operatorname{Curl} \boldsymbol{F}_{\mathrm{p}} \neq \mathbf{0}
$$

This property is known as **incompatibility**. The tensor $\boldsymbol{\alpha} = -J_{\mathrm{p}}^{-1} \boldsymbol{F}_{\mathrm{p}} (\operatorname{Curl} \boldsymbol{F}_{\mathrm{p}})$ is commonly defined as the GND density tensor in the intermediate configuration [@problem_id:2663666]. Because $\boldsymbol{F}_{\mathrm{p}}$ is incompatible, the intermediate configuration is often described as "fictitious" or "local." It cannot be realized globally in Euclidean space without introducing cuts or overlaps. Nevertheless, the field $\boldsymbol{F}_{\mathrm{p}}(\mathbf{X})$ is well-defined at every material point and provides a valid local description of the permanent deformation, forming a sound basis for [constitutive modeling](@entry_id:183370) [@problem_id:2663674].

#### Rotational Indeterminacy and Constitutive Objectivity

The intermediate configuration is defined as being locally stress-free, but its orientation is arbitrary. This leads to a fundamental non-uniqueness, or **[gauge freedom](@entry_id:160491)**, in the [multiplicative decomposition](@entry_id:199514). For any arbitrary time-dependent [rotation tensor](@entry_id:191990) $\boldsymbol{Q}(t) \in \mathrm{SO}(3)$, we can define a new pair of elastic and plastic deformations:

$$
\boldsymbol{F}_{\mathrm{e}}^{\star} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{Q}^{\mathsf{T}} \quad \text{and} \quad \boldsymbol{F}_{\mathrm{p}}^{\star} = \boldsymbol{Q} \boldsymbol{F}_{\mathrm{p}}
$$

This new pair still yields the same total deformation gradient, since $\boldsymbol{F}_{\mathrm{e}}^{\star}\boldsymbol{F}_{\mathrm{p}}^{\star} = (\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}})(\boldsymbol{Q}\boldsymbol{F}_{\mathrm{p}}) = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}} = \boldsymbol{F}$ [@problem_id:2663647]. This transformation corresponds to applying an arbitrary rigid rotation to the intermediate configuration.

Physical laws must be independent of this arbitrary choice of gauge. This has important consequences for [constitutive modeling](@entry_id:183370):

*   **Isotropic Materials**: For an isotropic material, the [stored energy function](@entry_id:166355) must be independent of the orientation of the intermediate state. Let us examine the transformation of the elastic Cauchy-Green tensors. The left tensor $\boldsymbol{b}_{\mathrm{e}} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}$ is invariant: $\boldsymbol{b}_{\mathrm{e}}^{\star} = (\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}})(\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}})^{\mathsf{T}} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}} = \boldsymbol{b}_{\mathrm{e}}$. The right tensor $\boldsymbol{C}_{\mathrm{e}} = \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}\boldsymbol{F}_{\mathrm{e}}$ transforms by rotation: $\boldsymbol{C}_{\mathrm{e}}^{\star} = (\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}})^{\mathsf{T}}(\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}}) = \boldsymbol{Q}\boldsymbol{C}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}}$. An isotropic free energy function $\psi$ depends only on the [scalar invariants](@entry_id:193787) of its strain-like argument. Since the invariants of $\boldsymbol{C}_{\mathrm{e}}$ are unaffected by rotation (i.e., $I_k(\boldsymbol{C}_{\mathrm{e}}^{\star})=I_k(\boldsymbol{C}_{\mathrm{e}})$), formulating the energy as $\psi = \hat{\psi}(I_1(\boldsymbol{C}_{\mathrm{e}}), I_2(\boldsymbol{C}_{\mathrm{e}}), I_3(\boldsymbol{C}_{\mathrm{e}}))$ ensures that the model is automatically invariant to the choice of $\boldsymbol{Q}$. Similarly, any function of the [invariant tensor](@entry_id:188619) $\boldsymbol{b}_{\mathrm{e}}$ will also satisfy this requirement.

*   **Anisotropic Materials**: For [anisotropic materials](@entry_id:184874), such as single crystals or [composites](@entry_id:150827) with preferred fiber directions, the free energy $\psi$ may depend on $\boldsymbol{C}_{\mathrm{e}}$ and one or more structural tensors (e.g., $\boldsymbol{M}$) that define the material's anisotropy in the intermediate configuration. To maintain invariance under the [gauge transformation](@entry_id:141321), these structural tensors must co-transform with the configuration, i.e., $\boldsymbol{M}^{\star} = \boldsymbol{Q}\boldsymbol{M}\boldsymbol{Q}^{\mathsf{T}}$. This ensures that the physical description remains unchanged regardless of the chosen orientation for the intermediate state [@problem_id:2663647].

### Thermodynamic Framework and Stress Measures

The true power of the [multiplicative decomposition](@entry_id:199514) is realized when it is integrated into a thermodynamic framework, allowing for the formulation of stress-strain relations and [evolution equations](@entry_id:268137) for plastic flow.

#### The Locus of Stored Energy

A cornerstone of [elastoplasticity](@entry_id:193198) theory is that [plastic deformation](@entry_id:139726) is a dissipative process, whereas [elastic deformation](@entry_id:161971) is recoverable and stores energy. This is formally expressed by postulating that the Helmholtz free energy per unit reference volume, $\Psi$, is a function only of the elastic part of the deformation. To satisfy the [principle of material frame-indifference](@entry_id:188488), $\Psi$ must depend on a pure measure of [elastic strain](@entry_id:189634), not the full [elastic deformation](@entry_id:161971) tensor $\boldsymbol{F}_{\mathrm{e}}$ (which includes rotation). The standard choice is the elastic right Cauchy-Green tensor $\boldsymbol{C}_{\mathrm{e}} = \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}\boldsymbol{F}_{\mathrm{e}}$ [@problem_id:2663676]:

$$
\Psi(\boldsymbol{F}, \boldsymbol{F}_{\mathrm{p}}) = \psi(\boldsymbol{C}_{\mathrm{e}})
$$

This formulation ensures that the stored energy is independent of any [rigid-body rotation](@entry_id:268623) of the observer (acting on $\boldsymbol{F}_{\mathrm{e}}$ from the left) and, for [isotropic materials](@entry_id:170678), independent of the rotational gauge of the intermediate configuration (acting on $\boldsymbol{C}_{\mathrm{e}}$ via a similarity transform).

#### Definitions of Stress

With the free energy function defined, the various [stress measures](@entry_id:198799) can be derived. The fundamental stress measure conjugate to the elastic strain $\boldsymbol{C}_{\mathrm{e}}$ is the **elastic Second Piola-Kirchhoff (PK2) stress**, defined on the intermediate configuration:

$$
\boldsymbol{S}_{\mathrm{e}} = 2 \frac{\partial \psi}{\partial \boldsymbol{C}_{\mathrm{e}}}
$$

This symmetric tensor represents the stress in the conceptual unloaded state. The physically observable stresses in the current configuration are obtained by "pushing forward" this stress with the elastic deformation $\boldsymbol{F}_{\mathrm{e}}$. The symmetric **Kirchhoff stress** $\boldsymbol{\tau}$ is given by:

$$
\boldsymbol{\tau} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}
$$

The **Cauchy stress** $\boldsymbol{\sigma}$, or "[true stress](@entry_id:190985)," is then found by accounting for the total volume change:

$$
\boldsymbol{\sigma} = J^{-1} \boldsymbol{\tau}
$$

Finally, the **First Piola-Kirchhoff (PK1) stress** $\boldsymbol{P}$, which relates forces in the current configuration to areas in the reference configuration, can be derived through standard transformations as $\boldsymbol{P} = \boldsymbol{\tau} \boldsymbol{F}^{-\mathsf{T}}$. Substituting the above relations yields:

$$
\boldsymbol{P} = (\boldsymbol{F}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}) (\boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}})^{-\mathsf{T}} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}^{-\mathsf{T}}
$$

These relationships form the constitutive core of any [finite strain](@entry_id:749398) [elastoplasticity](@entry_id:193198) model [@problem_id:2663649].

#### The Driving Force for Plasticity: The Mandel Stress

To develop an evolution equation for the plastic deformation $\boldsymbol{F}_{\mathrm{p}}$ (a **[flow rule](@entry_id:177163)**), we must identify the [thermodynamic force](@entry_id:755913) that drives plasticity. This is found by examining the [mechanical dissipation](@entry_id:169843), which, by the Second Law of Thermodynamics (Clausius-Duhem inequality), must be non-negative. For an [isothermal process](@entry_id:143096), the dissipation rate per unit reference volume, $\mathcal{D}$, is the total [stress power](@entry_id:182907) minus the rate of change of stored energy: $\mathcal{D} = \boldsymbol{P}:\dot{\boldsymbol{F}} - \dot{\Psi} \ge 0$.

Since $\Psi$ depends only on the elastic state, the stored energy term cancels the elastic part of the [stress power](@entry_id:182907), leaving only the [plastic dissipation](@entry_id:201273). A rigorous derivation shows that this [plastic dissipation](@entry_id:201273) can be expressed as a product of a stress-like quantity and a rate-of-deformation-like quantity, both defined in the intermediate configuration [@problem_id:2663673]:

$$
\mathcal{D}_{\mathrm{p}} = (\boldsymbol{C}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}}):\boldsymbol{L}_{\mathrm{p}}
$$

where $\boldsymbol{L}_{\mathrm{p}} = \dot{\boldsymbol{F}}_{\mathrm{p}}\boldsymbol{F}_{\mathrm{p}}^{-1}$ is the plastic [velocity gradient](@entry_id:261686). The tensor $\boldsymbol{M} = \boldsymbol{C}_{\mathrm{e}}\boldsymbol{S}_{\mathrm{e}}$ is known as the **Mandel stress**. If $\boldsymbol{M}$ is symmetric (which is true for [isotropic elasticity](@entry_id:203237)), the dissipation reduces further to $\mathcal{D}_{\mathrm{p}} = \boldsymbol{M}:\boldsymbol{D}_{\mathrm{p}}$, where $\boldsymbol{D}_{\mathrm{p}}$ is the symmetric plastic rate of deformation.

This result is fundamental: the Mandel stress $\boldsymbol{M}$ is the stress measure in the intermediate configuration that is work-conjugate to the plastic rate of deformation. It is therefore the appropriate **thermodynamic driving force** for [plastic flow](@entry_id:201346). Plastic flow rules are consequently formulated as relationships between $\boldsymbol{D}_{\mathrm{p}}$ (or $\boldsymbol{L}_{\mathrm{p}}$) and $\boldsymbol{M}$.

### The Kinematics of Flow

The static decomposition $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}$ provides the framework, but plasticity is a dynamic process of flow. The [kinematics](@entry_id:173318) of this flow are described by the rates of the deformation tensors.

#### Additive Decomposition of Velocity Gradients

Taking the [material time derivative](@entry_id:190892) of $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}$ and performing some algebra leads to an additive decomposition of the **[spatial velocity gradient](@entry_id:187198)** $\boldsymbol{L} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}$. Defining the elastic and plastic velocity gradients as $\boldsymbol{L}_{\mathrm{e}} = \dot{\boldsymbol{F}}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{e}}^{-1}$ and $\boldsymbol{L}_{\mathrm{p}} = \dot{\boldsymbol{F}}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{p}}^{-1}$, respectively, we obtain:

$$
\boldsymbol{L} = \boldsymbol{L}_{\mathrm{e}} + \boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1}
$$

This crucial relation states that the [spatial velocity gradient](@entry_id:187198) is the sum of the elastic velocity gradient and the "push-forward" of the plastic velocity gradient from the intermediate to the current configuration [@problem_id:2649689].

The velocity gradient $\boldsymbol{L}$ is decomposed into its symmetric part, the **rate of deformation** $\boldsymbol{D} = \operatorname{sym}(\boldsymbol{L})$, and its skew-symmetric part, the **spin** $\boldsymbol{W} = \operatorname{skew}(\boldsymbol{L})$. Applying these operators to the additive decomposition gives:

$$
\boldsymbol{D} = \boldsymbol{D}_{\mathrm{e}} + \operatorname{sym}(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1})
$$

$$
\boldsymbol{W} = \boldsymbol{W}_{\mathrm{e}} + \operatorname{skew}(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1})
$$

It is important to note that the push-forward operation does not distribute over the symmetric and skew parts. That is, $\operatorname{sym}(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1})$ is not, in general, equal to $\boldsymbol{F}_{\mathrm{e}} \boldsymbol{D}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1}$. The simplification only holds in the special case where the [elastic deformation](@entry_id:161971) is a pure rotation ($\boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}\boldsymbol{F}_{\mathrm{e}}=\boldsymbol{I}$) [@problem_id:2649689]. Finally, the assumption of [plastic incompressibility](@entry_id:183440) ($J_{\mathrm{p}}=1$) implies that the trace of the plastic velocity gradient is zero, which means the plastic flow is volume-preserving at the rate level: $\operatorname{tr}(\boldsymbol{D}_{\mathrm{p}}) = 0$.

#### The Physical Meaning of Elastic and Plastic Spin

The spin tensors in the [kinematic decomposition](@entry_id:751020) have precise physical interpretations that are critical in fields like [crystal plasticity](@entry_id:141273). The orientation of the material's underlying microstructure (e.g., the crystal lattice) is determined by the rotational part of the *elastic* deformation tensor, $\boldsymbol{F}_{\mathrm{e}}$. Using a [polar decomposition](@entry_id:149541) on the elastic part, $\boldsymbol{F}_{\mathrm{e}} = \boldsymbol{R}_{\mathrm{e}} \boldsymbol{U}_{\mathrm{e}}$, the tensor $\boldsymbol{R}_{\mathrm{e}}$ represents the **lattice orientation**.

The rate of change of this orientation, or the **[lattice spin](@entry_id:198780)**, is given by the [skew-symmetric tensor](@entry_id:199349) $\dot{\boldsymbol{R}}_{\mathrm{e}}\boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}}$. A careful kinematic derivation reveals its relation to the elastic spin $\boldsymbol{W}_{\mathrm{e}}$ [@problem_id:2663660]:

$$
\dot{\boldsymbol{R}}_{\mathrm{e}}\boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}} = \boldsymbol{W}_{\mathrm{e}} - \operatorname{skew}(\boldsymbol{R}_{\mathrm{e}} \dot{\boldsymbol{U}}_{\mathrm{e}} \boldsymbol{U}_{\mathrm{e}}^{-1} \boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}})
$$

This equation delivers a subtle but essential insight: the rate of rotation of the lattice is not equal to the elastic spin $\boldsymbol{W}_{\mathrm{e}}$. It differs by a term that is non-zero if the principal axes of elastic stretch do not coincide with the principal axes of the rate of elastic stretch. In many metals, elastic strains are small and this term is often negligible, leading to the common approximation $\dot{\boldsymbol{R}}_{\mathrm{e}}\boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}} \approx \boldsymbol{W}_{\mathrm{e}}$.

Most importantly, the **[plastic spin](@entry_id:188692)** $\boldsymbol{W}_{\mathrm{p}}$ does not appear in the equation for the lattice rotation rate. This means that [plastic spin](@entry_id:188692), which arises from the plastic [velocity gradient](@entry_id:261686) in the intermediate configuration, does not directly cause the crystal lattice to rotate. The [plastic spin](@entry_id:188692)'s effect is on the overall spatial spin $\boldsymbol{W}$, but the physical rotation of the material's internal structure is governed entirely by the [kinematics](@entry_id:173318) of the [elastic deformation](@entry_id:161971). This distinction is fundamental to correctly modeling [texture evolution](@entry_id:194385) and anisotropy in [polycrystalline materials](@entry_id:158956).