## Introduction
The concepts of stress and strain are the cornerstones of mechanics, providing the essential language to describe how materials respond to external forces. For graduate students in [nanomechanics](@entry_id:185346) and surface science, a deep understanding of their tensor formalism is not just academic—it is the bedrock upon which the analysis of nanoscale systems is built. However, a significant challenge lies in bridging the elegant, scale-free framework of classical continuum mechanics with the complex, discrete, and surface-dominated world of the nanoscale. This article is structured to guide you through this journey. The first chapter, **Principles and Mechanisms**, lays out the rigorous mathematical foundation of stress and strain tensors, from [kinematics](@entry_id:173318) to [constitutive laws](@entry_id:178936). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the power of this framework in solving real-world problems in materials science, thermodynamics, and [nanomechanics](@entry_id:185346). Finally, the **Hands-On Practices** chapter offers a chance to apply these theories to challenging problems. We begin by establishing the fundamental principles and mechanisms that govern deformation and internal force.

## Principles and Mechanisms

The analysis of how nanoscale materials deform and sustain loads rests upon the mathematical framework of stress and strain. These concepts, formalized as second-order tensors, provide a complete local description of a material's deformation and its internal force state. This chapter lays out the fundamental principles and mechanisms governing stress and strain, beginning with the purely geometric description of deformation (kinematics), followed by the description of [internal forces](@entry_id:167605) (kinetics), the material-specific laws that connect them ([constitutive relations](@entry_id:186508)), and finally, a discussion of how these continuum concepts are rooted in and extended for the nanometer scale.

### Kinematics of Deformation: The Language of Strain

Kinematics is the branch of mechanics concerned with the motion of points and bodies without considering the forces that cause them to move. In continuum mechanics, this involves describing the mapping of a body from an initial, undeformed state to a final, deformed state.

#### Finite Deformation

To describe a deformation rigorously, we consider a body occupying a **reference configuration**, denoted by $\Omega_0$, at an initial time. Each material point in this body is identified by its [position vector](@entry_id:168381) $\mathbf{X}$ in a fixed coordinate system. After deformation, at a time $t$, the body occupies a **current configuration**, $\Omega_t$, and the same material point has moved to a new position $\mathbf{x}$. The **deformation map** $\varphi$ provides the relationship between these positions:

$$
\mathbf{x} = \varphi(\mathbf{X}, t)
$$

For a physically realistic deformation, this map must be continuous, one-to-one (preventing material interpenetration), and orientation-preserving. Such a map is a time-dependent diffeomorphism. A physical quantity expressed as a function of $\mathbf{X}$ is said to be in a **referential (or Lagrangian) description**, while a quantity expressed as a function of $\mathbf{x}$ is in a **spatial (or Eulerian) description** [@problem_id:2788083].

The local behavior of the deformation is captured by the **[deformation gradient tensor](@entry_id:150370)**, $\mathbf{F}$, defined as the gradient of the deformation map with respect to the material coordinate $\mathbf{X}$:

$$
\mathbf{F} = \nabla_{\mathbf{X}} \varphi = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}
$$

In component form, this is $F_{ij} = \partial x_i / \partial X_j$. The deformation gradient is a fundamental measure that describes how infinitesimal line elements are transformed. An infinitesimal material vector $d\mathbf{X}$ in the reference configuration is mapped to a spatial vector $d\mathbf{x}$ in the current configuration via the [linear transformation](@entry_id:143080) $d\mathbf{x} = \mathbf{F} d\mathbf{X}$ [@problem_id:2788083]. The determinant of the deformation gradient, $J = \det(\mathbf{F})$, represents the local change in volume, with $dv = J dV$. The condition of being orientation-preserving implies $J > 0$.

The **displacement** of a material point is the vector connecting its initial position to its current position. In the referential description, the displacement field $\mathbf{u}$ is given by:

$$
\mathbf{u}(\mathbf{X}, t) = \varphi(\mathbf{X}, t) - \mathbf{X}
$$

The gradient of this field with respect to the material coordinates gives the **material [displacement gradient](@entry_id:165352)**, which is directly related to $\mathbf{F}$:

$$
\nabla_{\mathbf{X}} \mathbf{u} = \nabla_{\mathbf{X}} (\varphi(\mathbf{X}) - \mathbf{X}) = \mathbf{F} - \mathbf{I}
$$

where $\mathbf{I}$ is the second-order identity tensor [@problem_id:2788083].

While $\mathbf{F}$ fully characterizes the local deformation, it is not an ideal measure of *strain* because it includes local rigid-body rotations. A pure strain measure should be zero for any rigid rotation. To construct such a measure, we examine how the squared length of a material line element $d\mathbf{X}$ changes upon deformation. The squared length in the current configuration is:

$$
|d\mathbf{x}|^2 = d\mathbf{x} \cdot d\mathbf{x} = (\mathbf{F} d\mathbf{X}) \cdot (\mathbf{F} d\mathbf{X}) = d\mathbf{X} \cdot (\mathbf{F}^{\mathsf{T}} \mathbf{F}) d\mathbf{X}
$$

The tensor that governs this change in squared length is the **right Cauchy-Green deformation tensor**, $\mathbf{C}$:

$$
\mathbf{C} = \mathbf{F}^{\mathsf{T}} \mathbf{F}
$$

The tensor $\mathbf{C}$ is symmetric and [positive definite](@entry_id:149459). Since a [rigid-body rotation](@entry_id:268623) corresponds to an orthogonal tensor $\mathbf{Q}$ (where $\mathbf{Q}^{\mathsf{T}}\mathbf{Q} = \mathbf{I}$), if the deformation is a pure rotation, $\mathbf{F} = \mathbf{Q}$, then $\mathbf{C} = \mathbf{Q}^{\mathsf{T}}\mathbf{Q} = \mathbf{I}$. This suggests that the deviation of $\mathbf{C}$ from the identity tensor $\mathbf{I}$ is a pure measure of strain. This leads to the definition of the **Green-Lagrange [strain tensor](@entry_id:193332)**, $\mathbf{E}$:

$$
\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I}) = \frac{1}{2}(\mathbf{F}^{\mathsf{T}} \mathbf{F} - \mathbf{I})
$$

The Green-Lagrange strain tensor is a referential measure that is zero if and only if the deformation is a [rigid-body motion](@entry_id:265795).

To illustrate these concepts, consider the homogeneous deformation of **simple shear** in a crystalline monolayer, described by the map $\varphi(X) = (X_1 + k X_2, X_2, X_3)$, where $k$ is the amount of shear [@problem_id:2788087]. The [deformation gradient](@entry_id:163749) $\mathbf{F}$ is:
$$
\mathbf{F} = \begin{pmatrix} 1  k  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix}
$$
From this, we can compute the right Cauchy-Green tensor $\mathbf{C} = \mathbf{F}^{\mathsf{T}}\mathbf{F}$:
$$
\mathbf{C} = \begin{pmatrix} 1  0  0 \\ k  1  0 \\ 0  0  1 \end{pmatrix} \begin{pmatrix} 1  k  0 \\ 0  1  0 \\ 0  0  1 \end{pmatrix} = \begin{pmatrix} 1  k  0 \\ k  k^2+1  0 \\ 0  0  1 \end{pmatrix}
$$
The Green-Lagrange strain tensor $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$ is then:
$$
\mathbf{E} = \frac{1}{2} \begin{pmatrix} 0  k  0 \\ k  k^2  0 \\ 0  0  0 \end{pmatrix} = \begin{pmatrix} 0  k/2  0 \\ k/2  k^2/2  0 \\ 0  0  0 \end{pmatrix}
$$
This example demonstrates that even for a simple deformation, the relationship between displacement and [finite strain](@entry_id:749398) can be nonlinear (note the $k^2$ term).

#### Infinitesimal Deformation (Small Strain Theory)

In many engineering and physics applications, particularly in the study of stiff materials like crystalline solids, deformations are very small. This allows for a significant simplification of the kinematic framework. The **[small strain approximation](@entry_id:754971)** assumes that the displacement gradients are much smaller than unity, i.e., $|\nabla_{\mathbf{X}} \mathbf{u}| \ll 1$.

Under this assumption, the distinction between the [material and spatial coordinates](@entry_id:751726) becomes negligible ($\mathbf{x} \approx \mathbf{X}$), and we can express all gradients with respect to a single coordinate system. The Green-Lagrange [strain tensor](@entry_id:193332) $\mathbf{E}$ can be linearized. Substituting $\mathbf{F} = \mathbf{I} + \nabla \mathbf{u}$:
$$
\mathbf{E} = \frac{1}{2}((\mathbf{I} + (\nabla \mathbf{u})^{\mathsf{T}})(\mathbf{I} + \nabla \mathbf{u}) - \mathbf{I}) = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\mathsf{T}} + (\nabla \mathbf{u})^{\mathsf{T}} \nabla \mathbf{u})
$$
When gradients are small, the quadratic term $(\nabla \mathbf{u})^{\mathsf{T}} \nabla \mathbf{u}$ is negligible compared to the linear terms. This leaves us with the **[infinitesimal strain tensor](@entry_id:167211)** (also known as the small strain or Cauchy strain tensor), $\boldsymbol{\varepsilon}$:

$$
\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + (\nabla \mathbf{u})^{\mathsf{T}})
$$

By definition, $\boldsymbol{\varepsilon}$ is the symmetric part of the [displacement gradient](@entry_id:165352). The skew-symmetric part is the **[infinitesimal rotation tensor](@entry_id:192754)**, $\boldsymbol{\omega}$:

$$
\boldsymbol{\omega} = \frac{1}{2}(\nabla \mathbf{u} - (\nabla \mathbf{u})^{\mathsf{T}})
$$

Thus, the [displacement gradient](@entry_id:165352) is additively decomposed into a strain and a rotation: $\nabla \mathbf{u} = \boldsymbol{\varepsilon} + \boldsymbol{\omega}$. This powerful decomposition separates the local deformation (change in shape and size), captured by $\boldsymbol{\varepsilon}$, from the local [rigid-body rotation](@entry_id:268623), captured by $\boldsymbol{\omega}$ [@problem_id:2788100].

A key property of the [infinitesimal strain tensor](@entry_id:167211) is its invariance to small rigid-body motions, a property known as **linearized objectivity**. Superimposing a small rigid rotation onto an existing [displacement field](@entry_id:141476) does not change the strain tensor, because the gradient of a rigid-body displacement is purely skew-symmetric, which vanishes upon symmetrization [@problem_id:2788100]. This confirms that $\boldsymbol{\varepsilon}$ is a true measure of deformation.

### Kinetics of Internal Forces: The Concept of Stress

While strain describes the geometry of deformation, stress describes the [internal forces](@entry_id:167605) that material particles exert on one another.

#### The Cauchy Stress Tensor and Traction

Imagine an internal surface within a deformed body, defined by its [unit normal vector](@entry_id:178851) $\mathbf{n}$. The material on one side of the surface exerts a force on the material on the other side. The **traction vector**, $\mathbf{t}(\mathbf{n})$, is defined as this force per unit of current area. In general, $\mathbf{t}$ depends on the location $\mathbf{x}$ and the orientation of the surface $\mathbf{n}$.

A fundamental result of continuum mechanics, **Cauchy's Stress Theorem**, states that the [traction vector](@entry_id:189429) is a linear function of the [normal vector](@entry_id:264185). This linear relationship is defined by the **Cauchy stress tensor**, $\boldsymbol{\sigma}$:

$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}
$$

The Cauchy stress tensor $\boldsymbol{\sigma}$ is a second-order tensor field that completely characterizes the state of stress at a point in the material. Its component $\sigma_{ij}$ represents the $i$-th component of the [traction vector](@entry_id:189429) acting on a surface whose normal points in the $j$-th direction. The [balance of angular momentum](@entry_id:181848), in the absence of body couples, requires the Cauchy stress tensor to be symmetric, i.e., $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$.

Because $\boldsymbol{\sigma}$ is a real, symmetric tensor, the [spectral theorem](@entry_id:136620) guarantees that it has three real eigenvalues and a corresponding set of three mutually [orthogonal eigenvectors](@entry_id:155522). The eigenvalues are known as the **principal stresses** ($\sigma_1, \sigma_2, \sigma_3$), and the eigenvectors are the **principal directions** ($\mathbf{n}_1, \mathbf{n}_2, \mathbf{n}_3$). In the coordinate system aligned with these [principal directions](@entry_id:276187), the stress tensor is diagonal. This is the state of **principal stress**, where no shear stresses exist on the faces of an elemental cube aligned with the principal axes. The stress tensor can be expressed via its **[spectral decomposition](@entry_id:148809)**:

$$
\boldsymbol{\sigma} = \sum_{i=1}^{3} \sigma_i (\mathbf{n}_i \otimes \mathbf{n}_i)
$$

where $\otimes$ denotes the [tensor product](@entry_id:140694) [@problem_id:2788091]. Using this representation, the traction on any plane with normal $\mathbf{n}$ can be elegantly computed. Expressing $\mathbf{n}$ in the principal basis, $\mathbf{n} = \sum c_i \mathbf{n}_i$ (where $c_i = \mathbf{n} \cdot \mathbf{n}_i$ are the [direction cosines](@entry_id:170591)), the [traction vector](@entry_id:189429) becomes:

$$
\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n} = \left( \sum_{i=1}^{3} \sigma_i \mathbf{n}_i \otimes \mathbf{n}_i \right) \left( \sum_{j=1}^{3} c_j \mathbf{n}_j \right) = \sum_{i=1}^{3} \sigma_i c_i \mathbf{n}_i
$$

For example, consider a point in a cubic nanofilm where the [principal stresses](@entry_id:176761) are $\sigma_1 = 1.8$ GPa, $\sigma_2 = 0.6$ GPa, and $\sigma_3 = -0.4$ GPa along the $[100]$, $[010]$, and $[001]$ axes, respectively. To find the magnitude of the traction on a plane with Miller indices $(1,2,2)$, we first find its [unit normal vector](@entry_id:178851) $\mathbf{n} = \frac{1}{3}[1, 2, 2]$. The [direction cosines](@entry_id:170591) are $c_1=1/3, c_2=2/3, c_3=2/3$. The [traction vector](@entry_id:189429) is $\mathbf{t} = 1.8(\frac{1}{3})\mathbf{n}_1 + 0.6(\frac{2}{3})\mathbf{n}_2 - 0.4(\frac{2}{3})\mathbf{n}_3$. Its magnitude is $\sqrt{ (0.6)^2 + (0.4)^2 + (-0.8/3)^2 } \approx 0.7688$ GPa [@problem_id:2788091].

#### Stress Power and Work Conjugacy

Stress and strain are energetically connected. The rate at which [internal forces](@entry_id:167605) do work during deformation is the **stress [power density](@entry_id:194407)**, $P$. This power is the product of stress and the [rate of strain](@entry_id:267998). The [velocity gradient tensor](@entry_id:270928), $\mathbf{L} = \nabla \mathbf{v}$, can be decomposed into its symmetric part, the **[rate of deformation tensor](@entry_id:182598)** $\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathsf{T}}) = \dot{\boldsymbol{\varepsilon}}$, and its skew-symmetric part, the **[spin tensor](@entry_id:187346)** $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathsf{T}}) = \dot{\boldsymbol{\omega}}$. The stress [power density](@entry_id:194407) is given by the double contraction:

$$
P = \boldsymbol{\sigma} : \mathbf{L} = \boldsymbol{\sigma} : (\mathbf{D} + \mathbf{W}) = \boldsymbol{\sigma} : \mathbf{D} + \boldsymbol{\sigma} : \mathbf{W}
$$

Because the Cauchy stress tensor $\boldsymbol{\sigma}$ is symmetric and the [spin tensor](@entry_id:187346) $\mathbf{W}$ is skew-symmetric, their double contraction is identically zero ($\boldsymbol{\sigma} : \mathbf{W} = \sigma_{ij}W_{ij} = 0$). Therefore, the stress [power density](@entry_id:194407) simplifies to:

$$
P = \boldsymbol{\sigma} : \mathbf{D}
$$

This crucial result shows that only the rate of deformation ([strain rate](@entry_id:154778)) contributes to the internal power; [rigid-body rotation](@entry_id:268623) does no work with the Cauchy stress [@problem_id:2788100]. This establishes that stress $\boldsymbol{\sigma}$ and strain rate $\mathbf{D}$ (or, in a virtual work context, stress and virtual strain $\delta\boldsymbol{\varepsilon}$) are **work-conjugate pairs**. This relationship is the thermodynamic foundation for deriving constitutive laws from energy potentials.

### Constitutive Laws: Linking Stress and Strain

Constitutive laws are mathematical models that describe the material-specific relationship between [stress and strain](@entry_id:137374). For elastic materials, this relationship is reversible.

#### Linear Elasticity and the Stiffness Tensor

For many materials under small strains, the relationship between [stress and strain](@entry_id:137374) is approximately linear. This is the domain of **linear elasticity**. If the material is also **hyperelastic**, its response can be derived from a **[strain energy density function](@entry_id:199500)**, $W(\boldsymbol{\varepsilon})$, which represents the elastic energy stored per unit reference volume. The stress tensor is then obtained by differentiating $W$ with respect to the [strain tensor](@entry_id:193332):

$$
\sigma_{ij} = \frac{\partial W}{\partial \varepsilon_{ij}}
$$

For a linear elastic material, $W$ must be a quadratic function of the strain components. The stress is then a linear function of strain, a relationship known as the generalized Hooke's Law:

$$
\sigma_{ij} = C_{ijkl} \varepsilon_{kl}
$$

The **stiffness tensor**, $C_{ijkl}$, is a fourth-order tensor containing the elastic constants of the material. By differentiating the stress-strain relation, we see that it is also the second derivative of the [strain energy density](@entry_id:200085):

$$
C_{ijkl} = \frac{\partial \sigma_{ij}}{\partial \varepsilon_{kl}} = \frac{\partial^2 W}{\partial \varepsilon_{ij} \partial \varepsilon_{kl}}
$$

This definition, combined with the symmetry of the stress and strain tensors, imposes [fundamental symmetries](@entry_id:161256) on the [stiffness tensor](@entry_id:176588) [@problem_id:2788099]:
1.  **Minor Symmetries**: $C_{ijkl} = C_{jikl}$ (from $\sigma_{ij}=\sigma_{ji}$) and $C_{ijkl} = C_{ijlk}$ (from $\varepsilon_{kl}=\varepsilon_{lk}$).
2.  **Major Symmetry**: $C_{ijkl} = C_{klij}$ (from the existence of $W$, allowing the order of differentiation to be swapped).

These symmetries reduce the number of independent components in the most general anisotropic [stiffness tensor](@entry_id:176588) from $3^4 = 81$ to just 21.

#### Isotropic Elasticity and Material Stability

Material properties are often independent of direction, a property known as **isotropy**. For a linearly elastic isotropic material, the [stiffness tensor](@entry_id:176588) must be constructed from the only available [isotropic tensors](@entry_id:195105) (the identity tensor $\mathbf{I}$ and its products). The most general form satisfying all symmetries is:

$$
C_{ijkl} = \lambda \delta_{ij} \delta_{kl} + \mu (\delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk})
$$

Here, $\lambda$ and $\mu$ are the two independent **Lamé parameters**. The parameter $\mu$ is also known as the [shear modulus](@entry_id:167228). Substituting this into Hooke's Law yields the stress-strain relation for [isotropic linear elasticity](@entry_id:185899):

$$
\boldsymbol{\sigma} = 2\mu \boldsymbol{\varepsilon} + \lambda \mathrm{tr}(\boldsymbol{\varepsilon}) \mathbf{I}
$$

Material symmetry further reduces the number of independent constants. For instance, a material with cubic crystal symmetry has 3 independent constants, while a transversely isotropic material has 5 [@problem_id:2788099].

For a material to be physically stable, the strain energy stored must be positive for any non-zero strain state. This means the [strain energy density](@entry_id:200085) $W = \frac{1}{2} \boldsymbol{\varepsilon} : \boldsymbol{\sigma} = \frac{1}{2} C_{ijkl} \varepsilon_{ij} \varepsilon_{kl}$ must be a [positive definite](@entry_id:149459) quadratic form. For an isotropic material, we can express $W$ in terms of the deviatoric and volumetric parts of the strain. This decomposition reveals that [thermodynamic stability](@entry_id:142877) requires strict positivity of the energetic contributions from both pure shear and pure volumetric deformation [@problem_id:2788105]. This leads to the following [necessary and sufficient conditions](@entry_id:635428) on the Lamé parameters for a 3D bulk material:
$$
\mu > 0 \quad \text{and} \quad 3\lambda + 2\mu > 0
$$
The first condition ensures stability against shear, while the second (related to the bulk modulus $K = \lambda + \frac{2}{3}\mu$) ensures stability against volume changes.

### Stress and Strain at the Nanoscale: Bridging Length Scales

Classical continuum mechanics assumes materials are homogeneous. At the nanoscale, the discrete atomic nature of matter and the high [surface-to-volume ratio](@entry_id:177477) introduce new phenomena that require extensions to the classical theory.

#### Surface Stress and Surface Elasticity

The atoms at a surface or interface are in a different environment than those in the bulk, leading to distinct [mechanical properties](@entry_id:201145). The work required to create new surface area is the **[surface free energy](@entry_id:159200)**, $\gamma$. For a solid, this scalar quantity is generally not equivalent to the **[surface stress](@entry_id:191241)**, $\boldsymbol{\tau}_s$, which is a second-order tensor describing the in-plane forces within the surface.

The relationship between them is given by the **Shuttleworth equation**. This can be derived by considering the virtual work done in deforming a surface. The variation in total [surface free energy](@entry_id:159200), $\delta F_s = \delta \int \gamma \, da$, has contributions from both the change in area ($\delta(da)$) and the change in [surface energy](@entry_id:161228) density with strain ($\delta\gamma$). By equating this to the work done by the surface stress, $\delta F_s = \int \boldsymbol{\tau}_s : \delta\boldsymbol{\varepsilon}_s \, da$, we find [@problem_id:2788080]:

$$
\boldsymbol{\tau}_s = \gamma \mathbf{I}_s + \frac{\partial \gamma}{\partial \boldsymbol{\varepsilon}_s}
$$

Here, $\mathbf{I}_s$ is the in-surface identity tensor and $\boldsymbol{\varepsilon}_s$ is the in-surface strain tensor. This equation reveals a crucial distinction: surface stress includes a term related to the resistance of the surface to elastic stretching ($\partial\gamma/\partial\boldsymbol{\varepsilon}_s$), which is absent for liquids. For an isotropic liquid interface, $\gamma$ is constant with respect to strain, so the derivative term vanishes, and the [surface stress](@entry_id:191241) tensor becomes isotropic: $\boldsymbol{\tau}_s = \gamma \mathbf{I}_s$. In this special case, the scalar surface tension is equivalent to the magnitude of the [surface stress](@entry_id:191241) [@problem_id:2788080].

Just as for bulk materials, [thermodynamic stability](@entry_id:142877) requires the surface elastic energy to be [positive definite](@entry_id:149459). For a 2D isotropic surface described by surface Lamé parameters $\lambda_s$ and $\mu_s$, this leads to the stability conditions [@problem_id:2788105]:
$$
\mu_s > 0 \quad \text{and} \quad \lambda_s + \mu_s > 0
$$

#### From Atoms to Continuum: The Cauchy-Born Rule and Virial Stress

The elastic properties of a crystalline solid ultimately arise from its [interatomic potentials](@entry_id:177673). A key multiscale hypothesis that connects the atomistic and continuum scales is the **Cauchy-Born rule**. It states that for a deformation that is slowly varying on the scale of the lattice, the crystal lattice deforms locally according to the macroscopic [deformation gradient](@entry_id:163749) $\mathbf{F}$. That is, the [lattice vectors](@entry_id:161583) $\mathbf{a}_i$ in the reference state deform to $\mathbf{a}'_i = \mathbf{F} \mathbf{a}_i$ [@problem_id:2788123].

This rule allows one to derive the continuum [strain energy density](@entry_id:200085) $W$ directly from the atomistic potential energy. For a given $\mathbf{F}$, one can calculate the deformed bond lengths and angles, compute the [total potential energy](@entry_id:185512) per unit volume of the deformed lattice, and identify this as $W(\mathbf{F})$. For example, for a 2D square lattice with nearest-neighbor harmonic bonds, applying the Cauchy-Born rule yields a [strain energy density](@entry_id:200085) that depends on the diagonal components of the right Cauchy-Green tensor, $W = \frac{k}{2} [ (\sqrt{C_{11}} - 1)^2 + (\sqrt{C_{22}} - 1)^2 ]$ [@problem_id:2788123].

An alternative, purely microscopic definition of stress comes from statistical mechanics. The **virial stress** is a measure of the momentum flux across a given volume. It consists of two parts: a **kinetic contribution** arising from the transport of momentum by particles moving across the volume's boundaries, and a **configurational contribution** arising from the interatomic forces acting between particles [@problem_id:2788129].

The virial stress is a microscopic quantity, while the Cauchy stress is a continuum one. The connection between them is subtle. The virial stress, if computed using the absolute velocities of particles in the [lab frame](@entry_id:181186), includes a convective term related to the [bulk flow](@entry_id:149773) of the material and is not Galilean invariant. To recover the true Cauchy stress, which represents [momentum flux](@entry_id:199796) in the co-[moving frame](@entry_id:274518) of the material, one must compute the virial using the **peculiar velocities** of particles (their velocity relative to the local streaming velocity) and perform a [coarse-graining](@entry_id:141933) average over a representative volume. When this is done, the averaged microscopic stress coincides with the continuum Cauchy stress that enters the momentum balance equation [@problem_id:2788129].

#### Generalized Continuum Theories for Nanomechanics

At the nanoscale, the [characteristic length](@entry_id:265857) of the microstructure (e.g., grain size) can be comparable to the length scale of the [deformation gradient](@entry_id:163749). In such cases, classical continuum theory, which is scale-free, can fail to predict phenomena like size-dependent hardening. **Generalized continuum theories** have been developed to address this by incorporating internal length scales into the constitutive framework.

Two prominent examples are [micropolar elasticity](@entry_id:190542) and [strain-gradient elasticity](@entry_id:197079) [@problem_id:2788112]:
*   **Micropolar (Cosserat) Elasticity** enriches the continuum by assigning independent [rotational degrees of freedom](@entry_id:141502), the **[microrotation](@entry_id:184355) field** $\boldsymbol{\varphi}$, to each material point, in addition to the standard displacement $\mathbf{u}$. This is suitable for materials with granular or cellular microstructures. The key kinematic measures are a non-symmetric distortion tensor and a curvature tensor (gradient of [microrotation](@entry_id:184355)). The work-conjugate stresses are a generally **non-symmetric force-stress tensor** $\boldsymbol{\sigma}$ and a **[couple-stress](@entry_id:747952) tensor** $\boldsymbol{\mu}$, which represents the torque per unit area.

*   **Strain-Gradient Elasticity** extends the classical theory by assuming the [strain energy density](@entry_id:200085) depends not only on the strain $\boldsymbol{\varepsilon}$ but also on its gradient, $\nabla\boldsymbol{\varepsilon}$. This approach does not introduce new kinematic fields, relying only on the displacement $\mathbf{u}$. The [work-conjugate stress](@entry_id:182069) measures are the standard (symmetric) Cauchy stress $\boldsymbol{\sigma}$ and a **[higher-order stress](@entry_id:186008) tensor** $\boldsymbol{\tau}$ that is conjugate to the [strain gradient](@entry_id:204192).

These advanced theories provide a richer description of material behavior, enabling the modeling of [size effects](@entry_id:153734) and complex responses observed in [nanomechanics](@entry_id:185346) and [metamaterials](@entry_id:276826).