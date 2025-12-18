## Introduction
Linear elasticity is a cornerstone theory of solid mechanics, providing the fundamental framework for understanding how materials deform under external loads. Its central premise—a linear relationship between stress and strain—offers a powerful yet elegant approximation for the mechanical response of most solids undergoing small deformations. This theory is not only indispensable for the design and analysis of engineered structures, from bridges to microelectronic components, but also serves as the essential continuum model in advanced multiscale simulations that connect atomic-level physics to macroscopic behavior. This article addresses the need for a coherent exposition of linear elasticity, bridging its rigorous mathematical underpinnings with its diverse and modern applications.

Over the following chapters, you will embark on a structured exploration of this vital topic. The journey begins in the **Principles and Mechanisms** chapter, where we will rigorously define the concepts of strain and stress, derive the generalized Hooke's Law from [thermodynamic principles](@entry_id:142232), and explore how [material symmetry](@entry_id:173835) dictates the [elastic constants](@entry_id:146207). Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the theory's predictive power by solving classic engineering problems and showing how it enables multiscale modeling of [heterogeneous materials](@entry_id:196262) and provides insights into fields like biomechanics and geomechanics. Finally, the **Hands-On Practices** section will offer an opportunity to solidify your understanding by applying these concepts to solve concrete problems. We begin by laying the theoretical groundwork, starting with the [kinematics of deformation](@entry_id:189142).

## Principles and Mechanisms

The theory of linear elasticity provides the fundamental framework for describing the mechanical response of solid materials to small deformations. It represents a cornerstone of solid mechanics and serves as the coarse-scale continuum model in many multiscale simulation methodologies. This chapter elucidates the core principles and mechanisms of [linear elasticity](@entry_id:166983), building from the [kinematics of deformation](@entry_id:189142) and the concept of stress to the [constitutive laws](@entry_id:178936) that connect them, their thermodynamic underpinnings, and the formulation of [boundary value problems](@entry_id:137204) for computational analysis.

### The Kinematics of Deformation: Measuring Strain

To quantify how a body deforms, we must first describe its motion. We consider a body occupying a reference configuration, where the position of any material point is denoted by the vector $\boldsymbol{X}$. After deformation, the body occupies a current configuration, and the same material point moves to a new position $\boldsymbol{x}$. The mapping from the reference to the current configuration is given by the motion $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X})$. The displacement of the point is the vector $\boldsymbol{u}(\boldsymbol{X}) = \boldsymbol{x} - \boldsymbol{X}$.

The local deformation is characterized by the **[deformation gradient tensor](@entry_id:150370)**, $\boldsymbol{F}$, defined as the gradient of the motion with respect to the reference coordinates:
$$ \boldsymbol{F} = \nabla_{\boldsymbol{X}} \boldsymbol{\chi} = \boldsymbol{I} + \nabla_{\boldsymbol{X}} \boldsymbol{u} $$
where $\boldsymbol{I}$ is the second-order identity tensor and $\nabla_{\boldsymbol{X}} \boldsymbol{u}$ is the **[displacement gradient tensor](@entry_id:748571)**. The tensor $\boldsymbol{F}$ maps an infinitesimal vector $d\boldsymbol{X}$ in the reference configuration to its corresponding vector $d\boldsymbol{x}$ in the current configuration: $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$.

A central challenge in mechanics is to define a measure of "strain" that quantifies deformation but is insensitive to rigid-body motions (translations and rotations), as these do not induce any [internal forces](@entry_id:167605). A pure [rigid-body rotation](@entry_id:268623) is described by a [deformation gradient](@entry_id:163749) $\boldsymbol{F} = \boldsymbol{R}$, where $\boldsymbol{R}$ is a proper orthogonal tensor satisfying $\boldsymbol{R}^{\top}\boldsymbol{R} = \boldsymbol{I}$. A robust measure of strain must be zero for such a transformation. The **Green-Lagrange [finite strain](@entry_id:749398) tensor**, $\boldsymbol{E}$, achieves this by measuring the change in the squared length of material vectors:
$$ |d\boldsymbol{x}|^2 - |d\boldsymbol{X}|^2 = (d\boldsymbol{X})^{\top} \boldsymbol{F}^{\top}\boldsymbol{F} d\boldsymbol{X} - (d\boldsymbol{X})^{\top}\boldsymbol{I} d\boldsymbol{X} = 2 (d\boldsymbol{X})^{\top} \boldsymbol{E} d\boldsymbol{X} $$
This defines $\boldsymbol{E}$ as:
$$ \boldsymbol{E} = \frac{1}{2} (\boldsymbol{F}^{\top}\boldsymbol{F} - \boldsymbol{I}) $$
For a pure rotation $\boldsymbol{F}=\boldsymbol{R}$, $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{R}^{\top}\boldsymbol{R} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{I} - \boldsymbol{I}) = \mathbf{0}$. Therefore, the Green-Lagrange strain is **objective**, or frame-indifferent .

Linear elasticity is built upon the assumption of **small deformations**, where the displacement gradients are small compared to unity, i.e., $\|\nabla_{\boldsymbol{X}} \boldsymbol{u}\| \ll 1$. Under this condition, we can linearize the Green-Lagrange strain. Substituting $\boldsymbol{F} = \boldsymbol{I} + \nabla \boldsymbol{u}$ (we drop the subscript $\boldsymbol{X}$ for brevity) into the definition of $\boldsymbol{E}$:
$$ \boldsymbol{E} = \frac{1}{2} ((\boldsymbol{I} + \nabla \boldsymbol{u})^{\top}(\boldsymbol{I} + \nabla \boldsymbol{u}) - \boldsymbol{I}) = \frac{1}{2} (\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top} + (\nabla \boldsymbol{u})^{\top}\nabla \boldsymbol{u}) $$
The **[infinitesimal strain tensor](@entry_id:167211)**, or [small-strain tensor](@entry_id:754968), $\boldsymbol{\varepsilon}$, is defined by neglecting the second-order term $(\nabla \boldsymbol{u})^{\top}\nabla \boldsymbol{u}$:
$$ \boldsymbol{\varepsilon} = \frac{1}{2} ((\nabla \boldsymbol{u}) + (\nabla \boldsymbol{u})^{\top}) $$
The approximation $\boldsymbol{E} \approx \boldsymbol{\varepsilon}$ is thus valid to first order, with a leading-order error of $\mathcal{O}(\|\nabla \boldsymbol{u}\|^2)$ .

This definition reveals a fundamental decomposition of the [displacement gradient](@entry_id:165352). Any second-order tensor can be uniquely decomposed into a symmetric part and a skew-symmetric part. For $\nabla \boldsymbol{u}$, this decomposition is:
$$ \nabla \boldsymbol{u} = \boldsymbol{\varepsilon} + \boldsymbol{\omega} $$
where $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top})$ is the symmetric strain tensor and $\boldsymbol{\omega} = \frac{1}{2}(\nabla \boldsymbol{u} - (\nabla \boldsymbol{u})^{\top})$ is the skew-symmetric **[infinitesimal rotation tensor](@entry_id:192754)**. The geometric interpretation is that $\boldsymbol{\varepsilon}$ describes the actual change in shape and size (stretching and shearing) of a material element, while $\boldsymbol{\omega}$ describes its local [rigid-body rotation](@entry_id:268623) . For an infinitesimal [rigid-body motion](@entry_id:265795) of the form $\boldsymbol{u}(\boldsymbol{x}) = \boldsymbol{W}\boldsymbol{x} + \boldsymbol{c}$, where $\boldsymbol{W}$ is a constant [skew-symmetric tensor](@entry_id:199349) and $\boldsymbol{c}$ is a constant translation vector, the [displacement gradient](@entry_id:165352) is $\nabla \boldsymbol{u} = \boldsymbol{W}$. The resulting strain is $\boldsymbol{\varepsilon} = \frac{1}{2}(\boldsymbol{W} + \boldsymbol{W}^{\top}) = \frac{1}{2}(\boldsymbol{W} - \boldsymbol{W}) = \mathbf{0}$. This confirms that infinitesimal [rigid motions](@entry_id:170523) produce zero strain, a crucial consistency requirement. Superposing such a motion onto an existing [displacement field](@entry_id:141476) does not alter the resulting [infinitesimal strain](@entry_id:197162) .

However, this property comes at a cost. While the [finite strain](@entry_id:749398) $\boldsymbol{E}$ is fully objective, the [infinitesimal strain](@entry_id:197162) $\boldsymbol{\varepsilon}$ is not. For a finite rotation represented by $\boldsymbol{F}=\boldsymbol{R}$, the corresponding $\boldsymbol{\varepsilon}$ is non-zero. Only for small rotations, where the rotation angle $\theta$ is small, is $\boldsymbol{\varepsilon}$ approximately objective, with a fictitious strain that scales as $\mathcal{O}(\theta^2)$ . This limitation defines the domain of validity for [linear elasticity](@entry_id:166983): it is restricted to scenarios involving both small strains and small rotations.

### The Concept of Stress: Forces within a Continuum

When a body is subjected to external forces, [internal forces](@entry_id:167605) develop to maintain equilibrium. These internal forces, distributed over internal surfaces, are quantified by the concept of **stress**. Consider an imaginary plane with [unit normal vector](@entry_id:178851) $\boldsymbol{n}$ passing through a point in the deformed body. The force per unit area exerted by the material on one side of the plane upon the other is called the **[traction vector](@entry_id:189429)**, $\boldsymbol{t}$.

A fundamental result, derived from the [balance of linear momentum](@entry_id:193575), is **Cauchy's Stress Theorem**. It states that the [traction vector](@entry_id:189429) $\boldsymbol{t}$ is a linear function of the [normal vector](@entry_id:264185) $\boldsymbol{n}$, mediated by a second-order tensor known as the **Cauchy stress tensor**, $\boldsymbol{\sigma}$:
$$ \boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n} $$
The Cauchy stress, often called the "[true stress](@entry_id:190985)," is a measure of force per unit area in the *current*, deformed configuration. For a classical (non-polar) continuum, the [balance of angular momentum](@entry_id:181848) further requires the Cauchy stress tensor to be symmetric, i.e., $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\top}$ .

In computational and theoretical mechanics, especially in the context of finite deformations, it is often more convenient to relate forces to the *reference* configuration. This gives rise to other [stress measures](@entry_id:198799) :
- The **First Piola-Kirchhoff (PK1) stress tensor**, $\boldsymbol{P}$, relates the force in the current configuration to the area in the reference configuration. The nominal traction $\boldsymbol{T}$ (force per unit reference area) is given by $\boldsymbol{T} = \boldsymbol{P}\boldsymbol{N}$, where $\boldsymbol{N}$ is the normal in the reference configuration. $\boldsymbol{P}$ is generally not symmetric and is related to Cauchy stress by $\boldsymbol{P} = J \boldsymbol{\sigma} \boldsymbol{F}^{-\top}$, where $J = \det(\boldsymbol{F})$.
- The **Second Piola-Kirchhoff (PK2) stress tensor**, $\boldsymbol{S}$, is a [symmetric tensor](@entry_id:144567) that is work-conjugate to the Green-Lagrange strain $\boldsymbol{E}$. It is related to $\boldsymbol{P}$ by $\boldsymbol{P} = \boldsymbol{F}\boldsymbol{S}$ and to $\boldsymbol{\sigma}$ by $\boldsymbol{S} = J \boldsymbol{F}^{-1} \boldsymbol{\sigma} \boldsymbol{F}^{-\top}$.

A key justification for the simplified framework of linear elasticity is that in the limit of small deformations, these different [stress measures](@entry_id:198799) converge. When $\|\nabla \boldsymbol{u}\| \ll 1$, the deformation gradient $\boldsymbol{F} \approx \boldsymbol{I}$ and the volume ratio $J \approx 1$. Consequently, the relations between the stress tensors simplify, and we find that $\boldsymbol{\sigma} \approx \boldsymbol{P} \approx \boldsymbol{S}$. Thus, within linear elasticity, we can work exclusively with the symmetric Cauchy stress tensor $\boldsymbol{\sigma}$ without ambiguity .

### The Constitutive Relation: Hooke's Law and the Elasticity Tensor

The constitutive law is the mathematical model that describes the material's specific mechanical behavior, connecting the kinematic measure of deformation (strain) to the kinetic measure of internal forces (stress). For a linearly elastic solid, this relationship is the **generalized Hooke's Law**, which postulates a linear mapping between the [stress and strain](@entry_id:137374) tensors:
$$ \sigma_{ij} = C_{ijkl} \varepsilon_{kl} $$
In this [index notation](@entry_id:191923) (with summation over repeated indices implied), $\boldsymbol{C}$ is the fourth-order **[elasticity tensor](@entry_id:170728)** (or [stiffness tensor](@entry_id:176588)). This tensor encapsulates the material's stiffness properties.

This linear law is not merely an ad-hoc assumption; it has a deep thermodynamic foundation. For a **hyperelastic** material, the mechanical response is derivable from a [scalar potential](@entry_id:276177), the **[strain energy density function](@entry_id:199500)**, $\psi(\boldsymbol{\varepsilon})$. For an isothermal, reversible process, the principles of thermodynamics, specifically the Clausius-Duhem inequality, show that the stress tensor must be the derivative of the Helmholtz free energy density (which for isothermal processes is the strain energy density) with respect to the [strain tensor](@entry_id:193332) :
$$ \boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} $$
Linear elasticity arises from approximating the strain energy density as a quadratic function of strain, which is valid for small strains about an unstressed reference state:
$$ \psi(\boldsymbol{\varepsilon}) = \frac{1}{2} \boldsymbol{\varepsilon} : \boldsymbol{C} : \boldsymbol{\varepsilon} = \frac{1}{2} C_{ijkl} \varepsilon_{ij} \varepsilon_{kl} $$
Taking the derivative of this quadratic potential directly yields Hooke's Law, $\sigma_{ij} = C_{ijkl}\varepsilon_{kl}$ .

The existence of this energy potential imposes crucial symmetries on the [elasticity tensor](@entry_id:170728) $\boldsymbol{C}$  :
1.  **Minor Symmetries**: The symmetry of the stress tensor ($\sigma_{ij} = \sigma_{ji}$) and the [strain tensor](@entry_id:193332) ($\varepsilon_{kl} = \varepsilon_{lk}$) allows us to assume, without loss of generality, that the [elasticity tensor](@entry_id:170728) is symmetric with respect to its first two and last two indices: $C_{ijkl} = C_{jikl}$ and $C_{ijkl} = C_{ijlk}$. These symmetries reduce the number of independent components of $\boldsymbol{C}$ in three dimensions from $3^4=81$ to $36$.
2.  **Major Symmetry**: The fact that $\boldsymbol{C}$ is the second derivative of the scalar potential $\psi$ ($C_{ijkl} = \frac{\partial^2 \psi}{\partial \varepsilon_{ij} \partial \varepsilon_{kl}}$) means that, by the equality of [mixed partial derivatives](@entry_id:139334) (Schwarz's theorem), it must also possess [major symmetry](@entry_id:198487): $C_{ijkl} = C_{klij}$. This additional symmetry reduces the number of [independent elastic constants](@entry_id:203649) from $36$ to $21$ for a general anisotropic material.

Furthermore, for the undeformed state to be thermodynamically stable, the strain energy must be positive for any non-zero deformation. This requires the quadratic form $\psi(\boldsymbol{\varepsilon})$ to be [positive definite](@entry_id:149459), which in turn means the [elasticity tensor](@entry_id:170728) $\boldsymbol{C}$ must be a **[positive definite](@entry_id:149459)** tensor on the space of symmetric second-order tensors .

The convex conjugate of the strain energy density is the **[complementary energy](@entry_id:192009) density**, $\phi(\boldsymbol{\sigma}) = \sup_{\boldsymbol{\varepsilon}} (\boldsymbol{\sigma}:\boldsymbol{\varepsilon} - \psi(\boldsymbol{\varepsilon}))$. For a linear elastic material, this evaluates to a quadratic function of stress:
$$ \phi(\boldsymbol{\sigma}) = \frac{1}{2} \boldsymbol{\sigma} : \boldsymbol{S} : \boldsymbol{\sigma} $$
where $\boldsymbol{S} = \boldsymbol{C}^{-1}$ is the fourth-order **compliance tensor** .

### Material Symmetry and Anisotropy

The 21 [independent elastic constants](@entry_id:203649) characterize a fully anisotropic material, belonging to the **triclinic** crystal system, which has the lowest degree of symmetry. For materials with higher symmetry, the [elasticity tensor](@entry_id:170728) $\boldsymbol{C}$ must be invariant under the [symmetry operations](@entry_id:143398) (e.g., rotations, reflections) of the material's [point group](@entry_id:145002). Each symmetry operation imposes additional constraints on the components of $\boldsymbol{C}$, further reducing the number of independent constants .

The hierarchy of elastic constants for various [crystal systems](@entry_id:137271) is a fundamental concept in materials science. A standard sequence, from lowest to highest symmetry, is as follows :
- **Triclinic**: 21 independent constants.
- **Monoclinic** (one 2-fold axis or [mirror plane](@entry_id:148117)): 13 constants.
- **Orthorhombic** (three orthogonal 2-fold axes or mirror planes): 9 constants.
- **Tetragonal** (one 4-fold axis): 7 or 6 constants, depending on the specific [point group](@entry_id:145002).
- **Trigonal** (one 3-fold axis): 7 or 6 constants, depending on the specific [point group](@entry_id:145002).
- **Hexagonal** (one 6-fold axis): 5 constants.
- **Cubic** (four 3-fold axes): 3 constants ($C_{11}$, $C_{12}$, $C_{44}$ in Voigt notation).
- **Isotropic** (infinite symmetry axes): 2 constants.

Understanding this hierarchy is critical in multiscale modeling, as the macroscopic elastic behavior of a material is dictated by its underlying crystal structure or, in the case of aggregates, the statistical distribution of orientations.

### Isotropic Linear Elasticity

The case of **isotropic** materials, which exhibit the same mechanical properties in all directions, is of paramount importance in engineering and science. For an isotropic material, the [elasticity tensor](@entry_id:170728) must be invariant under all orthogonal transformations. This constraint reduces the [elasticity tensor](@entry_id:170728) to a form expressible with just two independent constants :
$$ C_{ijkl} = \lambda \delta_{ij} \delta_{kl} + \mu (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) $$
The constants $\lambda$ and $\mu$ are known as the **Lamé parameters**. The parameter $\mu$ is also the **[shear modulus](@entry_id:167228)**, often denoted by $G$. Substituting this form into the generalized Hooke's Law gives the familiar stress-strain relation for [isotropic materials](@entry_id:170678):
$$ \boldsymbol{\sigma} = \lambda (\text{tr}(\boldsymbol{\varepsilon})) \boldsymbol{I} + 2\mu \boldsymbol{\varepsilon} $$
where $\text{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk}$ is the [volumetric strain](@entry_id:267252).

While $\lambda$ and $\mu$ are mathematically convenient, engineers and material scientists often use other moduli defined by specific, idealized mechanical tests. These are all interrelated  .
- **Young's Modulus ($E$)** and **Poisson's Ratio ($\nu$)**: Defined from a uniaxial stress test. They relate to the Lamé parameters as:
  $$ E = \frac{\mu(3\lambda + 2\mu)}{\lambda + \mu}, \quad \nu = \frac{\lambda}{2(\lambda + \mu)} $$
- **Bulk Modulus ($K$)**: Defined from a hydrostatic pressure test as the resistance to volume change. It relates as:
  $$ K = \lambda + \frac{2}{3}\mu $$
- **Longitudinal or P-wave Modulus ($M$)**: Represents stiffness in [uniaxial strain](@entry_id:1133592) conditions (e.g., in a longitudinal wave). It is defined as:
  $$ M = K + \frac{4}{3}G = \lambda + 2\mu $$

These relationships can be inverted to express all moduli in terms of any pair, most commonly ($E, \nu$). The key conversion formulas are :
$$ \mu = G = \frac{E}{2(1+\nu)} $$
$$ K = \frac{E}{3(1-2\nu)} $$
$$ \lambda = \frac{E\nu}{(1+\nu)(1-2\nu)} $$
$$ M = \frac{E(1-\nu)}{(1+\nu)(1-2\nu)} $$

The [thermodynamic stability](@entry_id:142877) condition that $\boldsymbol{C}$ be [positive definite](@entry_id:149459) translates into simple constraints on these moduli. The [strain energy](@entry_id:162699) can be decomposed into volumetric and deviatoric (shear) parts, $W = \frac{1}{2}K(\text{tr}(\boldsymbol{\varepsilon}))^2 + G \boldsymbol{\varepsilon}'_{ij}\boldsymbol{\varepsilon}'_{ij}$, where $\boldsymbol{\varepsilon}'$ is the [deviatoric strain](@entry_id:201263). Stability requires the coefficients to be positive:
$$ K > 0 \quad \text{and} \quad G > 0 $$
In terms of [engineering constants](@entry_id:199413), this requires Young's modulus to be positive ($E>0$) and Poisson's ratio to be within the range $-1  \nu  0.5$ for most materials  .

### The Boundary Value Problem of Elastostatics

To solve a practical mechanics problem, we must combine the governing physical laws into a well-posed [boundary value problem](@entry_id:138753) (BVP). For a body in [static equilibrium](@entry_id:163498), the **strong form** of the [elastostatics](@entry_id:198298) BVP consists of finding the displacement field $\boldsymbol{u}(\boldsymbol{x})$ that satisfies the following set of equations simultaneously :
1.  **Equilibrium Equation**: $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \mathbf{0}$ within the domain $\Omega$. ($\boldsymbol{b}$ is the body force per unit volume).
2.  **Constitutive Law**: $\boldsymbol{\sigma} = \boldsymbol{C} : \boldsymbol{\varepsilon}$.
3.  **Kinematic Relation**: $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\boldsymbol{u} + (\nabla\boldsymbol{u})^{\top})$.
4.  **Boundary Conditions**:
    - **Dirichlet (essential) BC**: $\boldsymbol{u} = \bar{\boldsymbol{u}}$ on a part of the boundary $\Gamma_u$.
    - **Neumann (natural) BC**: $\boldsymbol{\sigma}\boldsymbol{n} = \bar{\boldsymbol{t}}$ on the remaining boundary $\Gamma_t$.

This system of partial differential equations is often difficult to solve analytically, especially for complex geometries or [heterogeneous materials](@entry_id:196262). For computational methods, such as the Finite Element Method (FEM), we reformulate the problem into an equivalent integral form, known as the **weak or variational form**.

The weak form is derived by multiplying the [equilibrium equation](@entry_id:749057) by an arbitrary (but admissible) vector [test function](@entry_id:178872) $\boldsymbol{v}$ and integrating over the domain. After applying the divergence theorem (integration by parts) and substituting the boundary conditions, we arrive at the following problem: Find the [displacement field](@entry_id:141476) $\boldsymbol{u}$ that satisfies the [essential boundary conditions](@entry_id:173524) and the following integral equation for *all* [test functions](@entry_id:166589) $\boldsymbol{v}$ that vanish on the Dirichlet boundary $\Gamma_u$:
$$ \int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\boldsymbol{v})\,dx = \int_{\Omega} \boldsymbol{b} \cdot \boldsymbol{v}\,dx + \int_{\Gamma_{t}} \bar{\boldsymbol{t}} \cdot \boldsymbol{v}\,ds $$
Substituting the constitutive law, we obtain:
$$ \int_{\Omega} (\boldsymbol{C} : \boldsymbol{\varepsilon}(\boldsymbol{u})) : \boldsymbol{\varepsilon}(\boldsymbol{v})\,dx = \int_{\Omega} \boldsymbol{b} \cdot \boldsymbol{v}\,dx + \int_{\Gamma_{t}} \bar{\boldsymbol{t}} \cdot \boldsymbol{v}\,ds $$
This [variational statement](@entry_id:756447) forms the basis for nearly all modern [computational solid mechanics](@entry_id:169583). It embeds the equilibrium and Neumann boundary conditions in an integral form, which is more amenable to [numerical approximation](@entry_id:161970). In multiscale simulations, it is this formulation that is used to solve for the displacement field at the continuum scale, driven by properties determined from finer scales.