## Introduction
Stress and strain tensors are the foundational language of [continuum mechanics](@entry_id:155125), providing the essential framework for describing how materials deform under applied forces. For scientists and engineers, particularly in fields like geophysics and materials science, mastering these concepts is not merely an academic exercise; it is the key to building realistic models of complex mechanical behavior, from the slow creep of [tectonic plates](@entry_id:755829) to the failure of engineered materials. However, students and researchers often face a significant hurdle: bridging the gap between the abstract mathematical formalism of tensors and their practical application in solving tangible problems. This article is designed to cross that bridge, offering a comprehensive and structured exploration of stress and strain.

The journey begins in the first chapter, **Principles and Mechanisms**, where we will lay the theoretical groundwork. We will start with the fundamental [continuum hypothesis](@entry_id:154179), explore the different mathematical measures of strain for both small and large deformations, and define the various stress tensors used to characterize internal forces. Following this, the second chapter, **Applications and Interdisciplinary Connections**, will showcase these concepts in action, with a particular focus on their use in the earth sciences. We will see how stress and strain analysis is used to model large-scale geodynamics, understand [earthquake physics](@entry_id:748780), and formulate advanced constitutive laws for complex geological materials. Finally, **Hands-On Practices** will offer a chance to solidify your understanding by tackling practical problems central to [computational mechanics](@entry_id:174464) and [geophysics](@entry_id:147342). By moving from core theory to practical application, this article provides the tools needed to confidently apply the principles of continuum mechanics to cutting-edge scientific and engineering research.

## Principles and Mechanisms

### The Continuum Hypothesis

The foundation of [continuum mechanics](@entry_id:155125), and by extension its application to [computational geophysics](@entry_id:747618), rests upon the **[continuum hypothesis](@entry_id:154179)**. This principle allows us to model materials like rock, soil, and mantle fluids, which are microscopically composed of discrete grains, crystals, or molecules, as a continuous medium. The validity of this assumption hinges on the principle of **[scale separation](@entry_id:152215)**. We postulate that there exists a characteristic length scale, often called a **Representative Elementary Volume (REV)**, which is simultaneously much larger than the microstructural scale (e.g., [grain size](@entry_id:161460)) and much smaller than the macroscopic scale of the problem domain.

Within this REV, the statistical fluctuations of microscopic properties average out, allowing us to define smooth, continuous field quantities such as density $\rho(\boldsymbol{x}, t)$, velocity $\boldsymbol{v}(\boldsymbol{x}, t)$, and stress $\boldsymbol{\sigma}(\boldsymbol{x}, t)$ at a mathematical point $\boldsymbol{x}$. For this to be valid, a clear separation of scales must exist. Let $a$ be the characteristic microstructural length (e.g., grain diameter), $L$ be the macroscopic length scale of the entire domain, and $\ell_c$ be the [correlation length](@entry_id:143364) of microscopic fluctuations (such as [force chains](@entry_id:199587) or porosity variations). A valid continuum model requires the existence of an REV of size $\ell_{\mathrm{REV}}$ such that $a \ll \ell_{\mathrm{REV}} \ll L$. Furthermore, for the REV to be statistically representative, it must be larger than the a [correlation length](@entry_id:143364), i.e., $\ell_{\mathrm{REV}} \gtrsim \ell_c$.

In computational practice, the size of a numerical grid cell, $\Delta x$, must itself be a valid REV. Therefore, the condition becomes $a \ll \ell_c \lesssim \Delta x \ll L$. If, for instance, a model of a fault gouge has a mean grain size of $a = 5 \times 10^{-4}\ \mathrm{m}$, a macroscopic domain length of $L = 10\ \mathrm{m}$, and a [correlation length](@entry_id:143364) of [force chains](@entry_id:199587) of $\ell_c = 5 \times 10^{-2}\ \mathrm{m}$, then a proposed grid spacing of $\Delta x = 1 \times 10^{-2}\ \mathrm{m}$ would be inconsistent with the [continuum hypothesis](@entry_id:154179). This is because the grid cell is smaller than the [correlation length](@entry_id:143364) ($\Delta x  \ell_c$), meaning it cannot contain a statistically [representative sample](@entry_id:201715) of the [microstructure](@entry_id:148601), and the continuum fields of stress and strain would not be well-defined at that resolution . When such [scale separation](@entry_id:152215) is absent, a discrete approach, such as the Discrete Element Method (DEM), becomes necessary.

### Measures of Strain

Assuming a body behaves as a continuum, we can describe its deformation by a **motion map** $\boldsymbol{\varphi}$, which maps each material point from its position $\boldsymbol{X}$ in a reference configuration to its position $\boldsymbol{x}$ in the current configuration: $\boldsymbol{x} = \boldsymbol{\varphi}(\boldsymbol{X})$. The local deformation is entirely characterized by the **[deformation gradient tensor](@entry_id:150370)**, $\boldsymbol{F}$, defined as the gradient of the motion with respect to the reference position:

$$
\boldsymbol{F} = \frac{\partial \boldsymbol{\varphi}}{\partial \boldsymbol{X}} = \frac{\partial \boldsymbol{x}}{\partial \boldsymbol{X}}
$$

The deformation gradient maps a differential [line element](@entry_id:196833) $\mathrm{d}\boldsymbol{X}$ in the reference configuration to its corresponding element $\mathrm{d}\boldsymbol{x}$ in the current configuration: $\mathrm{d}\boldsymbol{x} = \boldsymbol{F} \mathrm{d}\boldsymbol{X}$. While $\boldsymbol{F}$ contains all information about the local deformation, it also includes [rigid body rotation](@entry_id:167024). To quantify deformation (stretching and shearing) independently of rotation, we define strain tensors.

#### Finite Strain Tensors

For [large deformations](@entry_id:167243), several [strain measures](@entry_id:755495) exist, each with a distinct physical interpretation. Two of the most fundamental are the Green-Lagrange and Euler-Almansi strain tensors.

The **Green–Lagrange strain tensor**, $\boldsymbol{E}$, measures the change in squared length of a material line element relative to its original length. It is defined as:

$$
\mathrm{d}s^2 - \mathrm{d}S^2 = (\mathrm{d}\boldsymbol{x})^T(\mathrm{d}\boldsymbol{x}) - (\mathrm{d}\boldsymbol{X})^T(\mathrm{d}\boldsymbol{X}) = (\boldsymbol{F}\mathrm{d}\boldsymbol{X})^T(\boldsymbol{F}\mathrm{d}\boldsymbol{X}) - (\mathrm{d}\boldsymbol{X})^T(\mathrm{d}\boldsymbol{X}) = (\mathrm{d}\boldsymbol{X})^T (\boldsymbol{F}^T\boldsymbol{F} - \boldsymbol{I}) \mathrm{d}\boldsymbol{X}
$$

where $\mathrm{d}s$ and $\mathrm{d}S$ are the lengths of the [line element](@entry_id:196833) in the current and reference configurations, respectively, and $\boldsymbol{I}$ is the identity tensor. This gives rise to the definition of $\boldsymbol{E}$ through the relation $\mathrm{d}s^2 - \mathrm{d}S^2 = 2 (\mathrm{d}\boldsymbol{X})^T \boldsymbol{E} \mathrm{d}\boldsymbol{X}$, leading to:

$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^T\boldsymbol{F} - \boldsymbol{I})
$$

Since $\boldsymbol{E}$ is defined with respect to the reference configuration, it is a **Lagrangian** quantity .

Conversely, the **Euler–Almansi [strain tensor](@entry_id:193332)**, $\boldsymbol{e}$, measures the same change in squared length but refers it to the [line element](@entry_id:196833) in the current configuration. Using $\mathrm{d}\boldsymbol{X} = \boldsymbol{F}^{-1}\mathrm{d}\boldsymbol{x}$, we have:

$$
\mathrm{d}s^2 - \mathrm{d}S^2 = (\mathrm{d}\boldsymbol{x})^T \boldsymbol{I} \mathrm{d}\boldsymbol{x} - (\boldsymbol{F}^{-1}\mathrm{d}\boldsymbol{x})^T(\boldsymbol{F}^{-1}\mathrm{d}\boldsymbol{x}) = (\mathrm{d}\boldsymbol{x})^T (\boldsymbol{I} - \boldsymbol{F}^{-T}\boldsymbol{F}^{-1}) \mathrm{d}\boldsymbol{x}
$$

This defines $\boldsymbol{e}$ through $\mathrm{d}s^2 - \mathrm{d}S^2 = 2 (\mathrm{d}\boldsymbol{x})^T \boldsymbol{e} \mathrm{d}\boldsymbol{x}$, giving:

$$
\boldsymbol{e} = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{F}^{-T}\boldsymbol{F}^{-1}) = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{B}^{-1})
$$

where $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^T$ is the left Cauchy-Green tensor. As $\boldsymbol{e}$ is defined with respect to the current configuration, it is an **Eulerian** quantity . A crucial property of any valid strain measure is that it must be zero for a pure [rigid body motion](@entry_id:144691) ([rotation and translation](@entry_id:175994)). For a [rigid body motion](@entry_id:144691), $\boldsymbol{F}$ is a proper orthogonal tensor $\boldsymbol{Q}$, satisfying $\boldsymbol{Q}^T\boldsymbol{Q} = \boldsymbol{I}$ and $\boldsymbol{Q}\boldsymbol{Q}^T = \boldsymbol{I}$. It is easily verified that for such an $\boldsymbol{F}$, both $\boldsymbol{E}$ and $\boldsymbol{e}$ vanish .

Another important [finite strain](@entry_id:749398) measure, particularly useful in certain [constitutive models](@entry_id:174726), is the **Hencky strain** or **[logarithmic strain](@entry_id:751438)**, $\boldsymbol{H}$. It is defined via the [polar decomposition](@entry_id:149541) of the deformation gradient, $\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U}$, where $\boldsymbol{R}$ is the [rotation tensor](@entry_id:191990) and $\boldsymbol{U}$ is the symmetric, positive-definite [right stretch tensor](@entry_id:193756). The Hencky strain is the tensor logarithm of $\boldsymbol{U}$:

$$
\boldsymbol{H} = \ln(\boldsymbol{U})
$$

The Hencky strain is advantageous because it is additive for coaxial stretches, a property not shared by $\boldsymbol{E}$ or $\boldsymbol{e}$. However, its computation is more intensive as it requires [spectral decomposition](@entry_id:148809) of $\boldsymbol{U}$. Its use in hyperelastic models provides an alternative to models based on $\boldsymbol{E}$, often yielding more physically plausible responses under extreme compression .

#### The Small-Strain Approximation

In many geophysical applications where deformations are small, it is computationally advantageous to linearize the [kinematics](@entry_id:173318). If the **[displacement field](@entry_id:141476)** is $\boldsymbol{u}(\boldsymbol{X}) = \boldsymbol{x} - \boldsymbol{X}$, then the deformation gradient is $\boldsymbol{F} = \boldsymbol{I} + \nabla \boldsymbol{u}$, where $\nabla \boldsymbol{u} = \partial \boldsymbol{u} / \partial \boldsymbol{X}$. Under the assumption that the displacement gradients are small, i.e., $\|\nabla \boldsymbol{u}\| \ll 1$, we can simplify the [finite strain measures](@entry_id:185716).

Substituting $\boldsymbol{F} = \boldsymbol{I} + \nabla \boldsymbol{u}$ into the definition of the Green-Lagrange strain tensor $\boldsymbol{E}$ gives:

$$
\boldsymbol{E} = \frac{1}{2}((\boldsymbol{I} + \nabla \boldsymbol{u})^T(\boldsymbol{I} + \nabla \boldsymbol{u}) - \boldsymbol{I}) = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^T + (\nabla \boldsymbol{u})^T \nabla \boldsymbol{u})
$$

When $\|\nabla \boldsymbol{u}\|$ is small, the quadratic term $(\nabla \boldsymbol{u})^T \nabla \boldsymbol{u}$ is of a higher order of smallness and can be neglected. This leads to the **[infinitesimal strain tensor](@entry_id:167211)**, $\boldsymbol{\varepsilon}$:

$$
\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^T)
$$

The error incurred by this approximation, $\boldsymbol{E} - \boldsymbol{\varepsilon}$, is precisely the neglected quadratic term, $\frac{1}{2}(\nabla \boldsymbol{u})^T \nabla \boldsymbol{u}$. The magnitude of this error therefore scales as $O(\|\nabla \boldsymbol{u}\|^2)$. This quadratic scaling provides the formal justification for the small-strain approximation: for sufficiently small displacement gradients, the linear measure $\boldsymbol{\varepsilon}$ is an excellent approximation of the true [finite strain](@entry_id:749398) . A similar analysis shows that the Euler-Almansi strain $\boldsymbol{e}$ also reduces to $\boldsymbol{\varepsilon}$ in this limit .

### The Concept of Stress

Stress describes the [internal forces](@entry_id:167605) that particles of a continuum exert on each other. The **[traction vector](@entry_id:189429)** $\boldsymbol{t}$ is defined as the force per unit area acting on a surface. The **Cauchy stress tensor** $\boldsymbol{\sigma}$ relates the traction vector to the orientation of the surface, given by its [unit normal vector](@entry_id:178851) $\boldsymbol{n}$, through **Cauchy's relation**:

$$
\boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n}
$$

The Cauchy stress is the "true," physically measurable stress, defined in the current, deformed configuration. For a standard (non-polar) continuum, where there are no internal body couples or couple stresses, the **[balance of angular momentum](@entry_id:181848)** requires the Cauchy stress tensor to be symmetric:

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^T
$$

This fundamental symmetry holds regardless of the material's constitutive response (e.g., [isotropy](@entry_id:159159) or anisotropy) or the magnitude of the strain .

#### Volumetric and Deviatoric Stress

It is often useful to decompose the stress tensor into two parts that correspond to distinct types of deformation: a part that causes volume change and a part that causes shape change (distortion). This is the **[volumetric-deviatoric decomposition](@entry_id:183756)**. Any stress tensor $\boldsymbol{\sigma}$ can be uniquely written as:

$$
\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}
$$

Here, $p$ is the **[mean stress](@entry_id:751819)** or **[hydrostatic stress](@entry_id:186327)**, defined as one-third of the trace of the stress tensor:

$$
p = \frac{1}{3} \mathrm{tr}(\boldsymbol{\sigma}) = \frac{1}{3}(\sigma_{11} + \sigma_{22} + \sigma_{33})
$$

The term $p\boldsymbol{I}$ is the **isotropic** part of the stress. The remaining part, $\boldsymbol{s} = \boldsymbol{\sigma} - p\boldsymbol{I}$, is the **[deviatoric stress tensor](@entry_id:267642)**. By its construction, the [deviatoric stress](@entry_id:163323) is always trace-free, $\mathrm{tr}(\boldsymbol{s}) = 0$. This decomposition is fundamental in the theory of plasticity and geomechanical [failure criteria](@entry_id:195168), where [hydrostatic pressure](@entry_id:141627) often influences material strength and the deviatoric stress drives shear failure . For example, for a stress state given by $\boldsymbol{\sigma} = \begin{pmatrix} 120  30  -10 \\ 30  80  20 \\ -10  20  100 \end{pmatrix}\ \mathrm{MPa}$, the [mean stress](@entry_id:751819) is $p = \frac{1}{3}(120+80+100) = 100\ \mathrm{MPa}$. The [deviatoric stress](@entry_id:163323) is then $\boldsymbol{s} = \boldsymbol{\sigma} - 100\boldsymbol{I} = \begin{pmatrix} 20  30  -10 \\ 30  -20  20 \\ -10  20  0 \end{pmatrix}\ \mathrm{MPa}$.

### Stress Measures in Finite Deformation

When dealing with [large strains](@entry_id:751152), the fact that Cauchy stress $\boldsymbol{\sigma}$ is defined on the deformed geometry can be inconvenient for formulating [constitutive laws](@entry_id:178936), which are more naturally expressed relative to the material's undeformed state. This gives rise to alternative, material-based [stress measures](@entry_id:198799).

The **First Piola-Kirchhoff stress tensor** $\boldsymbol{P}$ is a "nominal" stress that relates the force in the current configuration to an area in the *reference* configuration. It is related to the Cauchy stress by:

$$
\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$

where $J = \det(\boldsymbol{F})$ is the volumetric ratio. Because $\boldsymbol{P}$ maps a vector in the reference frame (a normal to a reference area) to a vector in the current frame (a force vector), it is a **two-point tensor**. A direct consequence is that, in general, $\boldsymbol{P}$ is **non-symmetric**, even though $\boldsymbol{\sigma}$ is symmetric .

The **Second Piola-Kirchhoff stress tensor** $\boldsymbol{S}$ is a fully Lagrangian measure. It is related to $\boldsymbol{P}$ via a [pull-back operation](@entry_id:753859) by $\boldsymbol{F}^{-1}$:

$$
\boldsymbol{S} = \boldsymbol{F}^{-1}\boldsymbol{P} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-T}
$$

This tensor relates a "pseudo-force" in the reference frame to an area in the reference frame. A key property of $\boldsymbol{S}$ is that it is **symmetric** as a direct consequence of the symmetry of $\boldsymbol{\sigma}$. Another crucial property is that it is work-conjugate to the rate of the Green-Lagrange strain tensor, $\dot{\boldsymbol{E}}$. That is, the [stress power](@entry_id:182907) per unit reference volume is given by $\dot{W} = \boldsymbol{S} : \dot{\boldsymbol{E}}$. This makes $\boldsymbol{S}$ the natural stress measure for hyperelastic [constitutive models](@entry_id:174726) based on the Green-Lagrange strain, such as the Saint Venant-Kirchhoff model .

As a concrete example, consider a material with deformation gradient $\boldsymbol{F} = \mathrm{diag}(1.2, 0.8, 1.0)$ and a resulting Cauchy stress $\boldsymbol{\sigma} = \mathrm{diag}(100, 50, 25)\ \mathrm{MPa}$. The Jacobian is $J = 1.2 \times 0.8 \times 1.0 = 0.96$. Using the transformation laws, one can compute the corresponding material stress tensors as $\boldsymbol{P} = \mathrm{diag}(80, 60, 24)\ \mathrm{MPa}$ and $\boldsymbol{S} = \mathrm{diag}(66.67, 75, 24)\ \mathrm{MPa}$ . This example highlights that even for a purely diagonal (coaxial) deformation, the numerical values of the principal components of the three stress tensors differ significantly.

### Constitutive Modeling: Linking Stress and Strain

The [equations of motion](@entry_id:170720) and definitions of [stress and strain](@entry_id:137374) are universal. What distinguishes one material from another is its **constitutive law**, the relationship between stress and strain.

#### Isotropic Materials and Stress Invariants

For an **isotropic** material, the constitutive response must be independent of the orientation of the coordinate system. This means that any scalar function of the stress tensor, such as a [yield criterion](@entry_id:193897) or a [strain energy potential](@entry_id:755493), must depend only on quantities that are invariant under coordinate rotations. These quantities are the **[stress invariants](@entry_id:170526)**. A common and complete set of invariants for a symmetric tensor $\boldsymbol{\sigma}$ is:

1.  **First invariant, $I_1$**: Related to the [mean stress](@entry_id:751819). $I_1 = \mathrm{tr}(\boldsymbol{\sigma})$.
2.  **Second invariant of the [deviatoric stress](@entry_id:163323), $J_2$**: Related to the magnitude of shear. $J_2 = \frac{1}{2} \boldsymbol{s} : \boldsymbol{s} = \frac{1}{2}\mathrm{tr}(\boldsymbol{s}^T\boldsymbol{s})$.
3.  **Third invariant of the [deviatoric stress](@entry_id:163323), $J_3$**: Related to the "type" of shear state (the Lode angle). $J_3 = \det(\boldsymbol{s})$.

An alternative set, often used, is $(I_1, J_2, I_3 = \det(\boldsymbol{\sigma}))$. Any isotropic scalar function $f(\boldsymbol{\sigma})$ can be expressed as a function $\hat{f}(I_1, J_2, J_3)$. For example, many [pressure-sensitive yield criteria](@entry_id:195835) used in [geomechanics](@entry_id:175967), such as the **Drucker-Prager criterion**, are formulated to be insensitive to the Lode angle and thus depend only on $I_1$ and $J_2$:

$$
f(I_1, J_2) = \sqrt{J_2} + \alpha I_1 - k = 0
$$

Here, the dependence on $I_1$ captures the sensitivity of [material strength](@entry_id:136917) to [hydrostatic pressure](@entry_id:141627), while the dependence on $J_2$ captures the role of shear stress in causing failure .

#### Anisotropic Elasticity

Many geological materials, such as shales, schists, or layered evaporites, exhibit significant **anisotropy**. Their elastic properties depend on direction. The general linear elastic relationship $\sigma_{ij} = C_{ijkl}\varepsilon_{kl}$ involves a fourth-order [stiffness tensor](@entry_id:176588) $\mathbb{C}$. For a general anisotropic material, $\mathbb{C}$ has 21 independent components. For materials with certain symmetries, this number is reduced.

A common case in [geophysics](@entry_id:147342) is **[transverse isotropy](@entry_id:756140)**, which describes materials with a single axis of rotational symmetry and a plane of [isotropy](@entry_id:159159) perpendicular to it (e.g., horizontally bedded shales). If the [axis of symmetry](@entry_id:177299) is the $x_3$-axis, [material symmetry](@entry_id:173835) constraints reduce the number of [independent elastic constants](@entry_id:203649) to five. In Voigt matrix notation, where stress and strain are represented as 6-component vectors, the stiffness matrix $\mathbf{C}^V$ takes the form:

$$
\mathbf{C}^{V} = \begin{pmatrix}
C_{11}  C_{11} - 2C_{66}  C_{13}  0  0  0 \\
C_{11} - 2C_{66}  C_{11}  C_{13}  0  0  0 \\
C_{13}  C_{13}  C_{33}  0  0  0 \\
0  0  0  C_{44}  0  0 \\
0  0  0  0  C_{44}  0 \\
0  0  0  0  0  C_{66}
\end{pmatrix}
$$

The five independent constants are $C_{11}, C_{33}, C_{13}, C_{44}, C_{66}$. The relation $C_{12} = C_{11} - 2C_{66}$ is a direct consequence of [isotropy](@entry_id:159159) in the $x_1-x_2$ plane .

### Advanced Topic: Objective Stress Rates in Rate-Type Models

For rate-dependent materials like [viscoelastic fluids](@entry_id:198948) (relevant for [mantle convection](@entry_id:203493)) or viscoplastic solids, the constitutive law relates a rate of stress to a [rate of strain](@entry_id:267998). When working in a [finite deformation](@entry_id:172086), Eulerian setting, a complication arises: the simple [material time derivative](@entry_id:190892) of the Cauchy stress, $\dot{\boldsymbol{\sigma}}$, is **not objective**. This means it is not frame-indifferent; an observer undergoing rigid rotation relative to the material would measure a different stress rate, leading to spurious stress changes.

To formulate valid [constitutive laws](@entry_id:178936), we must use an **[objective stress rate](@entry_id:168809)**, which is constructed to be independent of the observer's rotation. These rates typically involve correcting $\dot{\boldsymbol{\sigma}}$ for the rotation of the material, which is quantified by the **[spin tensor](@entry_id:187346)** $\boldsymbol{W} = \frac{1}{2}(\nabla\boldsymbol{v} - (\nabla\boldsymbol{v})^T)$.

One common objective rate is the **Jaumann stress rate**, a [corotational rate](@entry_id:193173) defined as:

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\boldsymbol{W}
$$

Another widely used rate is the **Oldroyd upper-convected stress rate**, defined in terms of the full velocity gradient $\boldsymbol{L} = \nabla \boldsymbol{v}$:

$$
\overset{\triangledown}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \boldsymbol{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\boldsymbol{L}^{T}
$$

Both of these rates can be shown to vanish for a pure [rigid body rotation](@entry_id:167024) (where the rate of deformation $\boldsymbol{D}=\boldsymbol{0}$), confirming their objectivity and making them suitable for use in [constitutive equations](@entry_id:138559) for materials undergoing large-strain flow . The choice between different [objective rates](@entry_id:198692) is a complex topic, as they can lead to different predictions in large-strain shear flows, but their use is essential for the physical and mathematical consistency of computational models.