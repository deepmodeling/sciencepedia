## Introduction
In the realm of solid mechanics, describing materials that undergo large, permanent deformations—a behavior known as finite strain elastoplasticity—presents a significant theoretical challenge. While infinitesimal strain theories can rely on a simple additive split of strain into elastic and plastic parts, this approach breaks down when rotations and geometric non-linearities are large. The solution lies in a more profound and physically grounded framework: the multiplicative decomposition of the deformation gradient. This powerful concept, which posits that the total deformation gradient $\boldsymbol{F}$ can be factored into an elastic part $\boldsymbol{F}_{\mathrm{e}}$ and a plastic part $\boldsymbol{F}_{\mathrm{p}}$, forms the bedrock of modern continuum plasticity theory.

This article provides a graduate-level exploration of this fundamental principle. It addresses the crucial need for a constitutively sound method to separate recoverable and dissipative deformation mechanisms at finite strain. Across three chapters, you will gain a deep understanding of this essential tool. The first chapter, "Principles and Mechanisms," establishes the theoretical foundation, distinguishing the multiplicative postulate from the kinematic polar decomposition and exploring its thermodynamic consequences. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the framework's immense utility in diverse fields, from metal forming and materials science to computational mechanics and biomechanics. Finally, "Hands-On Practices" offers a series of guided problems to solidify your comprehension and apply the theory to concrete examples.

## Principles and Mechanisms

This chapter delves into the theoretical underpinnings of finite strain elastoplasticity, focusing on the central concept of the multiplicative decomposition of the deformation gradient. We will begin by reviewing the purely kinematic separation of motion into stretch and rotation, and then introduce the constitutive postulate that separates deformation into elastic and plastic parts. This framework allows us to construct thermodynamically consistent models that correctly account for the distinct physical mechanisms of recoverable elastic strain and permanent plastic flow.

### The Kinematic Foundation: Polar Decomposition

Any description of finite deformation begins with the **deformation gradient**, $\boldsymbol{F}$, which serves as the local linear approximation of the deformation mapping $\boldsymbol{\varphi}(\mathbf{X},t)$. It maps an infinitesimal material line element $d\mathbf{X}$ from the reference configuration to its counterpart $d\mathbf{x}$ in the current configuration:

$$
d\mathbf{x} = \boldsymbol{F} d\mathbf{X}
$$

The condition $\det \boldsymbol{F} > 0$ is assumed throughout, ensuring that the mapping is locally invertible and preserves the orientation of material elements [@problem_id:2663646]. From a purely geometric perspective, the deformation gradient tensor $\boldsymbol{F}$ encapsulates the complete local information about how the material is stretched and rotated. The powerful **polar decomposition theorem** provides a unique way to disentangle these two effects. For any invertible $\boldsymbol{F}$, it can be factored as:

$$
\boldsymbol{F} = \boldsymbol{R} \boldsymbol{U} = \boldsymbol{V} \boldsymbol{R}
$$

Here, $\boldsymbol{R}$ is a proper orthogonal tensor ($\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R} = \boldsymbol{I}$ and $\det \boldsymbol{R} = +1$), representing a pure **rigid rotation**. The tensors $\boldsymbol{U}$ and $\boldsymbol{V}$ are symmetric and positive-definite, known as the **right stretch tensor** and **left stretch tensor**, respectively. This decomposition is purely mathematical and kinematic, holding for any deformation without reference to the material's constitution [@problem_id:2663676].

The physical interpretation is direct: the right decomposition $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ can be seen as a sequence where a material element is first stretched and sheared by $\boldsymbol{U}$ in the reference configuration, and then rigidly rotated by $\boldsymbol{R}$ into its final orientation. The left decomposition $\boldsymbol{F} = \boldsymbol{V}\boldsymbol{R}$ reverses this sequence.

The change in length of a material element is governed by the stretch tensors. The squared length of the deformed element $d\mathbf{x}$ is:

$$
|d\mathbf{x}|^2 = d\mathbf{x} \cdot d\mathbf{x} = (\boldsymbol{F}d\mathbf{X}) \cdot (\boldsymbol{F}d\mathbf{X}) = d\mathbf{X} \cdot (\boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} d\mathbf{X})
$$

This defines the **right Cauchy-Green deformation tensor**, $\boldsymbol{C} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F}$. Substituting the polar decomposition, we find $\boldsymbol{C} = (\boldsymbol{R}\boldsymbol{U})^{\mathsf{T}}(\boldsymbol{R}\boldsymbol{U}) = \boldsymbol{U}^{\mathsf{T}}\boldsymbol{R}^{\mathsf{T}}\boldsymbol{R}\boldsymbol{U} = \boldsymbol{U}^2$. Thus, the right stretch tensor $\boldsymbol{U}$ is the unique symmetric positive-definite square root of $\boldsymbol{C}$. Similarly, the **left Cauchy-Green tensor** (or **Finger tensor**), $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathsf{T}}$, is related to the left stretch tensor by $\boldsymbol{B} = \boldsymbol{V}^2$. The eigenvalues of $\boldsymbol{C}$ and $\boldsymbol{B}$ are identical and equal to the squares of the **principal stretches**, $\lambda_i^2$, which quantify the amount of stretching along principal axes. The orthonormal eigenvectors of $\boldsymbol{C}$ define these principal directions in the reference configuration [@problem_id:2663646].

An essential property of these kinematic quantities relates to the principle of material frame-indifference (objectivity). If the current configuration undergoes a superposed rigid rotation $\boldsymbol{Q}$, the deformation gradient transforms to $\tilde{\boldsymbol{F}} = \boldsymbol{Q}\boldsymbol{F}$. The new right Cauchy-Green tensor is $\tilde{\boldsymbol{C}} = \tilde{\boldsymbol{F}}^{\mathsf{T}}\tilde{\boldsymbol{F}} = (\boldsymbol{Q}\boldsymbol{F})^{\mathsf{T}}(\boldsymbol{Q}\boldsymbol{F}) = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F} = \boldsymbol{F}^{\mathsf{T}}\boldsymbol{F} = \boldsymbol{C}$. Since $\boldsymbol{C}$ is unchanged, its square root $\boldsymbol{U}$ is also unchanged. The right stretch tensor is therefore an **objective** measure of deformation. The rotation tensor, however, transforms as $\tilde{\boldsymbol{R}} = \boldsymbol{Q}\boldsymbol{R}$ and is not objective [@problem_id:2663646].

### The Constitutive Postulate: Multiplicative Decomposition

While the polar decomposition provides profound geometric insight, it is insufficient for building constitutive models of materials that exhibit permanent, or **inelastic**, deformation. The tensors $\boldsymbol{U}$ and $\boldsymbol{R}$ mix the effects of recoverable elastic deformation and permanent plastic flow. To model these distinct physical phenomena, we need a decomposition founded on constitutive principles.

For infinitesimal strains, this is achieved through the additive decomposition of the strain tensor, $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_{\mathrm{e}} + \boldsymbol{\varepsilon}_{\mathrm{p}}$. This simple addition is invalid for finite deformations where large rotations and geometric nonlinearities are present. The kinematics of sequential deformations are inherently multiplicative, as dictated by the chain rule for composite maps [@problem_id:2663674]. This leads to the central postulate of finite strain plasticity, the **multiplicative decomposition** of the deformation gradient, first proposed by E. H. Lee:

$$
\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}
$$

Here, $\boldsymbol{F}_{\mathrm{p}}$ is the **plastic deformation gradient** and $\boldsymbol{F}_{\mathrm{e}}$ is the **elastic deformation gradient**.

#### The Concept of the Intermediate Configuration

This factorization introduces the concept of a local, stress-free **intermediate configuration**. The decomposition is interpreted as a sequence of two distinct mappings [@problem_id:2663674]:

1.  A mapping from the reference configuration to the intermediate configuration, characterized by $\boldsymbol{F}_{\mathrm{p}}$. This mapping represents the permanent, dissipative rearrangement of the material's microstructure, such as dislocation slip in a crystal.

2.  A mapping from the intermediate configuration to the current, deformed configuration, characterized by $\boldsymbol{F}_{\mathrm{e}}$. This mapping represents the recoverable, elastic distortion of the material (e.g., the crystal lattice) that generates the observed stress.

The intermediate configuration is physically understood as the state that would be reached if a small material element were hypothetically excised from the body and elastically unloaded, allowing it to relax to a state of zero stress. The deformation remaining in this relaxed state is the plastic deformation, $\boldsymbol{F}_{\mathrm{p}}$. The subsequent elastic deformation, $\boldsymbol{F}_{\mathrm{e}}$, is then what is required to stretch and rotate this relaxed element to fit into its actual, stressed position in the current body [@problem_id:2663648]. This conceptual framework is the key to separating recoverable and permanent deformations at finite strain.

#### Distinguishing Kinematic and Constitutive Decompositions

It is crucial to distinguish the multiplicative decomposition $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}$ from the polar decomposition $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$ [@problem_id:2663676].

*   **Nature**: Polar decomposition is purely kinematic and unique. It applies to any invertible tensor and carries no information about the material's properties. The multiplicative decomposition is a **constitutive postulate**. It is not a general mathematical theorem but a physical hypothesis about material behavior. Its factors, $\boldsymbol{F}_{\mathrm{e}}$ and $\boldsymbol{F}_{\mathrm{p}}$, are internal state variables whose evolution must be described by constitutive laws (a flow rule for $\boldsymbol{F}_{\mathrm{p}}$ and an elastic law for $\boldsymbol{F}_{\mathrm{e}}$).

*   **Uniqueness**: The polar decomposition is unique. The multiplicative decomposition is inherently non-unique, a point we will elaborate on shortly.

*   **Interpretation**: In polar decomposition, $\boldsymbol{R}$ is a pure rotation and $\boldsymbol{U}$ is a pure stretch. In the multiplicative split, $\boldsymbol{F}_{\mathrm{e}}$ and $\boldsymbol{F}_{\mathrm{p}}$ are general tensors, each containing both stretch and rotation. For instance, the physically motivated case for many metals involves large plastic shearing and rotation ($\boldsymbol{F}_{\mathrm{p}}$) but small elastic strains, allowing the multiplicative framework to model phenomena far beyond the reach of linearized, additive strain theories [@problem_id:2663648]. Equating the factors of the two decompositions (e.g., $\boldsymbol{F}_{\mathrm{e}} = \boldsymbol{R}$, $\boldsymbol{F}_{\mathrm{p}} = \boldsymbol{U}$) is physically nonsensical, as it would imply that elastic response is purely rotational (zero stiffness) and plastic response is purely stretching.

### Fundamental Properties of the Multiplicative Decomposition

#### Volumetric and Isochoric Decomposition

The multiplicative property of the determinant applies directly to the decomposition: $J = \det(\boldsymbol{F}) = \det(\boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}) = \det(\boldsymbol{F}_{\mathrm{e}})\det(\boldsymbol{F}_{\mathrm{p}})$. Letting $J_{\mathrm{e}} = \det(\boldsymbol{F}_{\mathrm{e}})$ and $J_{\mathrm{p}} = \det(\boldsymbol{F}_{\mathrm{p}})$, we have:

$$
J = J_{\mathrm{e}} J_{\mathrm{p}}
$$

This elegantly separates the total volume change ratio $J$ into elastic and plastic contributions. For many crystalline metals, plastic deformation occurs primarily through dislocation slip, which is a shear mechanism that conserves volume. This is modeled by the common assumption of **plastic incompressibility**, or isochoric plastic flow:

$$
J_{\mathrm{p}} = \det(\boldsymbol{F}_{\mathrm{p}}) = 1
$$

Under this widely used assumption, the Jacobian relation simplifies to $J = J_{\mathrm{e}}$. This implies that any change in the material's volume is accommodated entirely by the elastic deformation, i.e., by the compression or expansion of the atomic lattice [@problem_id:2663674].

#### Incompatibility, the Intermediate Configuration, and Dislocations

A profound consequence of the multiplicative framework arises from the nature of plastic deformation. In a crystalline solid, plastic flow is mediated by the motion of defects known as **dislocations**. If there is a non-uniform distribution of dislocations, the material lattice becomes curved. This means that after plastic deformation, the local neighborhoods no longer fit together perfectly to form a continuous body. The plastic deformation field $\boldsymbol{F}_{\mathrm{p}}(\mathbf{X})$ cannot be described as the gradient of a single, continuous placement map.

Mathematically, a tensor field can be expressed as the gradient of a vector field only if its curl is zero. The presence of a net dislocation density, referred to as **Geometrically Necessary Dislocations (GNDs)**, results in a non-zero curl of the plastic deformation gradient:

$$
\operatorname{Curl} \boldsymbol{F}_{\mathrm{p}} \neq \mathbf{0}
$$

This property is known as **incompatibility**. The tensor $\boldsymbol{\alpha} = -J_{\mathrm{p}}^{-1} \boldsymbol{F}_{\mathrm{p}} (\operatorname{Curl} \boldsymbol{F}_{\mathrm{p}})$ is commonly defined as the GND density tensor in the intermediate configuration [@problem_id:2663666]. Because $\boldsymbol{F}_{\mathrm{p}}$ is incompatible, the intermediate configuration is often described as "fictitious" or "local." It cannot be realized globally in Euclidean space without introducing cuts or overlaps. Nevertheless, the field $\boldsymbol{F}_{\mathrm{p}}(\mathbf{X})$ is well-defined at every material point and provides a valid local description of the permanent deformation, forming a sound basis for constitutive modeling [@problem_id:2663674].

#### Rotational Indeterminacy and Constitutive Objectivity

The intermediate configuration is defined as being locally stress-free, but its orientation is arbitrary. This leads to a fundamental non-uniqueness, or **gauge freedom**, in the multiplicative decomposition. For any arbitrary time-dependent rotation tensor $\boldsymbol{Q}(t) \in \mathrm{SO}(3)$, we can define a new pair of elastic and plastic deformations:

$$
\boldsymbol{F}_{\mathrm{e}}^{\star} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{Q}^{\mathsf{T}} \quad \text{and} \quad \boldsymbol{F}_{\mathrm{p}}^{\star} = \boldsymbol{Q} \boldsymbol{F}_{\mathrm{p}}
$$

This new pair still yields the same total deformation gradient, since $\boldsymbol{F}_{\mathrm{e}}^{\star}\boldsymbol{F}_{\mathrm{p}}^{\star} = (\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}})(\boldsymbol{Q}\boldsymbol{F}_{\mathrm{p}}) = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}} = \boldsymbol{F}$ [@problem_id:2663647]. This transformation corresponds to applying an arbitrary rigid rotation to the intermediate configuration.

Physical laws must be independent of this arbitrary choice of gauge. This has important consequences for constitutive modeling:

*   **Isotropic Materials**: For an isotropic material, the stored energy function must be independent of the orientation of the intermediate state. Let us examine the transformation of the elastic Cauchy-Green tensors. The left tensor $\boldsymbol{b}_{\mathrm{e}} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}$ is invariant: $\boldsymbol{b}_{\mathrm{e}}^{\star} = (\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}})(\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}})^{\mathsf{T}} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}\boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}} = \boldsymbol{b}_{\mathrm{e}}$. The right tensor $\boldsymbol{C}_{\mathrm{e}} = \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}\boldsymbol{F}_{\mathrm{e}}$ transforms by rotation: $\boldsymbol{C}_{\mathrm{e}}^{\star} = (\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}})^{\mathsf{T}}(\boldsymbol{F}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}}) = \boldsymbol{Q}\boldsymbol{C}_{\mathrm{e}}\boldsymbol{Q}^{\mathsf{T}}$. An isotropic free energy function $\psi$ depends only on the scalar invariants of its strain-like argument. Since the invariants of $\boldsymbol{C}_{\mathrm{e}}$ are unaffected by rotation (i.e., $I_k(\boldsymbol{C}_{\mathrm{e}}^{\star})=I_k(\boldsymbol{C}_{\mathrm{e}})$), formulating the energy as $\psi = \hat{\psi}(I_1(\boldsymbol{C}_{\mathrm{e}}), I_2(\boldsymbol{C}_{\mathrm{e}}), I_3(\boldsymbol{C}_{\mathrm{e}}))$ ensures that the model is automatically invariant to the choice of $\boldsymbol{Q}$. Similarly, any function of the invariant tensor $\boldsymbol{b}_{\mathrm{e}}$ will also satisfy this requirement.

*   **Anisotropic Materials**: For anisotropic materials, such as single crystals or composites with preferred fiber directions, the free energy $\psi$ may depend on $\boldsymbol{C}_{\mathrm{e}}$ and one or more structural tensors (e.g., $\boldsymbol{M}$) that define the material's anisotropy in the intermediate configuration. To maintain invariance under the gauge transformation, these structural tensors must co-transform with the configuration, i.e., $\boldsymbol{M}^{\star} = \boldsymbol{Q}\boldsymbol{M}\boldsymbol{Q}^{\mathsf{T}}$. This ensures that the physical description remains unchanged regardless of the chosen orientation for the intermediate state [@problem_id:2663647].

### Thermodynamic Framework and Stress Measures

The true power of the multiplicative decomposition is realized when it is integrated into a thermodynamic framework, allowing for the formulation of stress-strain relations and evolution equations for plastic flow.

#### The Locus of Stored Energy

A cornerstone of elastoplasticity theory is that plastic deformation is a dissipative process, whereas elastic deformation is recoverable and stores energy. This is formally expressed by postulating that the Helmholtz free energy per unit reference volume, $\Psi$, is a function only of the elastic part of the deformation. To satisfy the principle of material frame-indifference, $\Psi$ must depend on a pure measure of elastic strain, not the full elastic deformation tensor $\boldsymbol{F}_{\mathrm{e}}$ (which includes rotation). The standard choice is the elastic right Cauchy-Green tensor $\boldsymbol{C}_{\mathrm{e}} = \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}\boldsymbol{F}_{\mathrm{e}}$ [@problem_id:2663676]:

$$
\Psi(\boldsymbol{F}, \boldsymbol{F}_{\mathrm{p}}) = \psi(\boldsymbol{C}_{\mathrm{e}})
$$

This formulation ensures that the stored energy is independent of any rigid-body rotation of the observer (acting on $\boldsymbol{F}_{\mathrm{e}}$ from the left) and, for isotropic materials, independent of the rotational gauge of the intermediate configuration (acting on $\boldsymbol{C}_{\mathrm{e}}$ via a similarity transform).

#### Definitions of Stress

With the free energy function defined, the various stress measures can be derived. The fundamental stress measure conjugate to the elastic strain $\boldsymbol{C}_{\mathrm{e}}$ is the **elastic Second Piola-Kirchhoff (PK2) stress**, defined on the intermediate configuration:

$$
\boldsymbol{S}_{\mathrm{e}} = 2 \frac{\partial \psi}{\partial \boldsymbol{C}_{\mathrm{e}}}
$$

This symmetric tensor represents the stress in the conceptual unloaded state. The physically observable stresses in the current configuration are obtained by "pushing forward" this stress with the elastic deformation $\boldsymbol{F}_{\mathrm{e}}$. The symmetric **Kirchhoff stress** $\boldsymbol{\tau}$ is given by:

$$
\boldsymbol{\tau} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}
$$

The **Cauchy stress** $\boldsymbol{\sigma}$, or "true stress," is then found by accounting for the total volume change:

$$
\boldsymbol{\sigma} = J^{-1} \boldsymbol{\tau}
$$

Finally, the **First Piola-Kirchhoff (PK1) stress** $\boldsymbol{P}$, which relates forces in the current configuration to areas in the reference configuration, can be derived through standard transformations as $\boldsymbol{P} = \boldsymbol{\tau} \boldsymbol{F}^{-\mathsf{T}}$. Substituting the above relations yields:

$$
\boldsymbol{P} = (\boldsymbol{F}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}) (\boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}})^{-\mathsf{T}} = \boldsymbol{F}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{p}}^{-\mathsf{T}}
$$

These relationships form the constitutive core of any finite strain elastoplasticity model [@problem_id:2663649].

#### The Driving Force for Plasticity: The Mandel Stress

To develop an evolution equation for the plastic deformation $\boldsymbol{F}_{\mathrm{p}}$ (a **flow rule**), we must identify the thermodynamic force that drives plasticity. This is found by examining the mechanical dissipation, which, by the Second Law of Thermodynamics (Clausius-Duhem inequality), must be non-negative. For an isothermal process, the dissipation rate per unit reference volume, $\mathcal{D}$, is the total stress power minus the rate of change of stored energy: $\mathcal{D} = \boldsymbol{P}:\dot{\boldsymbol{F}} - \dot{\Psi} \ge 0$.

Since $\Psi$ depends only on the elastic state, the stored energy term cancels the elastic part of the stress power, leaving only the plastic dissipation. A rigorous derivation shows that this plastic dissipation can be expressed as a product of a stress-like quantity and a rate-of-deformation-like quantity, both defined in the intermediate configuration [@problem_id:2663673]:

$$
\mathcal{D}_{\mathrm{p}} = (\boldsymbol{C}_{\mathrm{e}} \boldsymbol{S}_{\mathrm{e}}):\boldsymbol{L}_{\mathrm{p}}
$$

where $\boldsymbol{L}_{\mathrm{p}} = \dot{\boldsymbol{F}}_{\mathrm{p}}\boldsymbol{F}_{\mathrm{p}}^{-1}$ is the plastic velocity gradient. The tensor $\boldsymbol{M} = \boldsymbol{C}_{\mathrm{e}}\boldsymbol{S}_{\mathrm{e}}$ is known as the **Mandel stress**. If $\boldsymbol{M}$ is symmetric (which is true for isotropic elasticity), the dissipation reduces further to $\mathcal{D}_{\mathrm{p}} = \boldsymbol{M}:\boldsymbol{D}_{\mathrm{p}}$, where $\boldsymbol{D}_{\mathrm{p}}$ is the symmetric plastic rate of deformation.

This result is fundamental: the Mandel stress $\boldsymbol{M}$ is the stress measure in the intermediate configuration that is work-conjugate to the plastic rate of deformation. It is therefore the appropriate **thermodynamic driving force** for plastic flow. Plastic flow rules are consequently formulated as relationships between $\boldsymbol{D}_{\mathrm{p}}$ (or $\boldsymbol{L}_{\mathrm{p}}$) and $\boldsymbol{M}$.

### The Kinematics of Flow

The static decomposition $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}$ provides the framework, but plasticity is a dynamic process of flow. The kinematics of this flow are described by the rates of the deformation tensors.

#### Additive Decomposition of Velocity Gradients

Taking the material time derivative of $\boldsymbol{F} = \boldsymbol{F}_{\mathrm{e}}\boldsymbol{F}_{\mathrm{p}}$ and performing some algebra leads to an additive decomposition of the **spatial velocity gradient** $\boldsymbol{L} = \dot{\boldsymbol{F}}\boldsymbol{F}^{-1}$. Defining the elastic and plastic velocity gradients as $\boldsymbol{L}_{\mathrm{e}} = \dot{\boldsymbol{F}}_{\mathrm{e}} \boldsymbol{F}_{\mathrm{e}}^{-1}$ and $\boldsymbol{L}_{\mathrm{p}} = \dot{\boldsymbol{F}}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{p}}^{-1}$, respectively, we obtain:

$$
\boldsymbol{L} = \boldsymbol{L}_{\mathrm{e}} + \boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1}
$$

This crucial relation states that the spatial velocity gradient is the sum of the elastic velocity gradient and the "push-forward" of the plastic velocity gradient from the intermediate to the current configuration [@problem_id:2649689].

The velocity gradient $\boldsymbol{L}$ is decomposed into its symmetric part, the **rate of deformation** $\boldsymbol{D} = \operatorname{sym}(\boldsymbol{L})$, and its skew-symmetric part, the **spin** $\boldsymbol{W} = \operatorname{skew}(\boldsymbol{L})$. Applying these operators to the additive decomposition gives:

$$
\boldsymbol{D} = \boldsymbol{D}_{\mathrm{e}} + \operatorname{sym}(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1})
$$

$$
\boldsymbol{W} = \boldsymbol{W}_{\mathrm{e}} + \operatorname{skew}(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1})
$$

It is important to note that the push-forward operation does not distribute over the symmetric and skew parts. That is, $\operatorname{sym}(\boldsymbol{F}_{\mathrm{e}} \boldsymbol{L}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1})$ is not, in general, equal to $\boldsymbol{F}_{\mathrm{e}} \boldsymbol{D}_{\mathrm{p}} \boldsymbol{F}_{\mathrm{e}}^{-1}$. The simplification only holds in the special case where the elastic deformation is a pure rotation ($\boldsymbol{F}_{\mathrm{e}}^{\mathsf{T}}\boldsymbol{F}_{\mathrm{e}}=\boldsymbol{I}$) [@problem_id:2649689]. Finally, the assumption of plastic incompressibility ($J_{\mathrm{p}}=1$) implies that the trace of the plastic velocity gradient is zero, which means the plastic flow is volume-preserving at the rate level: $\operatorname{tr}(\boldsymbol{D}_{\mathrm{p}}) = 0$.

#### The Physical Meaning of Elastic and Plastic Spin

The spin tensors in the kinematic decomposition have precise physical interpretations that are critical in fields like crystal plasticity. The orientation of the material's underlying microstructure (e.g., the crystal lattice) is determined by the rotational part of the *elastic* deformation tensor, $\boldsymbol{F}_{\mathrm{e}}$. Using a polar decomposition on the elastic part, $\boldsymbol{F}_{\mathrm{e}} = \boldsymbol{R}_{\mathrm{e}} \boldsymbol{U}_{\mathrm{e}}$, the tensor $\boldsymbol{R}_{\mathrm{e}}$ represents the **lattice orientation**.

The rate of change of this orientation, or the **lattice spin**, is given by the skew-symmetric tensor $\dot{\boldsymbol{R}}_{\mathrm{e}}\boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}}$. A careful kinematic derivation reveals its relation to the elastic spin $\boldsymbol{W}_{\mathrm{e}}$ [@problem_id:2663660]:

$$
\dot{\boldsymbol{R}}_{\mathrm{e}}\boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}} = \boldsymbol{W}_{\mathrm{e}} - \operatorname{skew}(\boldsymbol{R}_{\mathrm{e}} \dot{\boldsymbol{U}}_{\mathrm{e}} \boldsymbol{U}_{\mathrm{e}}^{-1} \boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}})
$$

This equation delivers a subtle but essential insight: the rate of rotation of the lattice is not equal to the elastic spin $\boldsymbol{W}_{\mathrm{e}}$. It differs by a term that is non-zero if the principal axes of elastic stretch do not coincide with the principal axes of the rate of elastic stretch. In many metals, elastic strains are small and this term is often negligible, leading to the common approximation $\dot{\boldsymbol{R}}_{\mathrm{e}}\boldsymbol{R}_{\mathrm{e}}^{\mathsf{T}} \approx \boldsymbol{W}_{\mathrm{e}}$.

Most importantly, the **plastic spin** $\boldsymbol{W}_{\mathrm{p}}$ does not appear in the equation for the lattice rotation rate. This means that plastic spin, which arises from the plastic velocity gradient in the intermediate configuration, does not directly cause the crystal lattice to rotate. The plastic spin's effect is on the overall spatial spin $\boldsymbol{W}$, but the physical rotation of the material's internal structure is governed entirely by the kinematics of the elastic deformation. This distinction is fundamental to correctly modeling texture evolution and anisotropy in polycrystalline materials.