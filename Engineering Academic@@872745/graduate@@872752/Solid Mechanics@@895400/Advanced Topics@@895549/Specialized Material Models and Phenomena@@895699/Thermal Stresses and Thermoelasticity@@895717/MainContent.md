## Introduction
When solid materials are subjected to changes in temperature, they expand or contract. If this natural deformation is prevented, internal stresses arise—a phenomenon central to the field of **[thermoelasticity](@entry_id:158447)**. This coupling of thermal and mechanical behavior is not a niche academic curiosity; it is a critical consideration in the design and analysis of countless engineering systems, from the integrity of aerospace vehicles undergoing thermal cycling to the reliability of microelectronic components and the development of residual stresses in advanced manufacturing processes like 3D printing. The core problem addressed by [thermoelasticity](@entry_id:158447) is the development of a rigorous, predictive framework that unifies the principles of thermodynamics with those of continuum mechanics to quantify how thermal loads translate into mechanical stress and deformation.

This article provides a comprehensive exploration of [thermoelasticity](@entry_id:158447), structured to build understanding from fundamental principles to practical applications. We will begin in the **Principles and Mechanisms** section by establishing the thermodynamic foundations of the theory, defining the concept of [thermal strain](@entry_id:187744), and deriving the crucial [constitutive laws](@entry_id:178936) that govern thermoelastic behavior. Next, the **Applications and Interdisciplinary Connections** section will demonstrate the power of these principles by applying them to diverse engineering challenges, including structural stability, [material failure](@entry_id:160997) modes like [thermal shock](@entry_id:158329) and fatigue, and the behavior of advanced materials. Finally, the **Hands-On Practices** section offers a curated set of problems designed to solidify your grasp of the core concepts through direct application.

## Principles and Mechanisms

The study of how temperature changes induce mechanical stresses in solid bodies rests upon a synthesis of thermodynamics and [continuum mechanics](@entry_id:155125). This field, known as [thermoelasticity](@entry_id:158447), provides the theoretical framework for understanding and predicting a vast range of phenomena, from the integrity of aerospace components subjected to thermal cycling to the generation of residual stresses during manufacturing processes like welding and additive manufacturing. This chapter elucidates the fundamental principles and mechanisms governing thermoelastic behavior, beginning with the thermodynamic foundations and building towards a comprehensive [constitutive model](@entry_id:747751) capable of addressing complex engineering scenarios.

### The Thermodynamic Foundation of Thermoelasticity

To rigorously establish the coupling between thermal and mechanical states, we turn to the laws of thermodynamics as applied to a deformable continuum. For a chemically inert, [closed system](@entry_id:139565) undergoing a [reversible process](@entry_id:144176), the combined first and second laws of thermodynamics provide a fundamental relationship for the change in specific internal energy, $u$ (energy per unit mass). This relationship, known as the Gibbs relation, is given by:

$$
du = T ds + \frac{1}{\rho} \sigma_{ij} d\varepsilon_{ij}
$$

Here, $T$ is the absolute temperature, $s$ is the specific entropy, $\rho$ is the mass density, $\sigma_{ij}$ is the Cauchy stress tensor, and $\varepsilon_{ij}$ is the small [strain tensor](@entry_id:193332). The term $Tds$ represents the heat added to the system per unit mass, while the term $\frac{1}{\rho} \sigma_{ij} d\varepsilon_{ij}$ represents the mechanical work done on the system per unit mass. It is crucial to note that for a general solid, mechanical work is performed by all components of the stress tensor during deformation, not just by hydrostatic pressure as is the case for [fluids at rest](@entry_id:187621) [@problem_id:2701610].

The Gibbs relation reveals that the specific internal energy $u$ is most naturally expressed as a function of the specific entropy $s$ and the strain tensor $\varepsilon_{ij}$. These are termed the **[natural variables](@entry_id:148352)** of the internal energy, i.e., $u = u(s, \varepsilon_{ij})$.

While fundamental, the variables $(s, \varepsilon_{ij})$ are not always convenient for practical applications, where temperature and stress are more readily controlled or measured. Thermodynamic potentials can be systematically derived via **Legendre transformations** to change the set of [natural variables](@entry_id:148352). A particularly important potential is the **specific Helmholtz free energy**, $\psi$, defined as $\psi = u - Ts$. This transformation replaces the entropy $s$ with its conjugate variable, temperature $T$. The differential of $\psi$ is found to be:

$$
d\psi = du - d(Ts) = (T ds + \frac{1}{\rho} \sigma_{ij} d\varepsilon_{ij}) - (T ds + s dT) = -s dT + \frac{1}{\rho} \sigma_{ij} d\varepsilon_{ij}
$$

This shows that the [natural variables](@entry_id:148352) of the Helmholtz free energy are temperature and strain, $\psi = \psi(T, \varepsilon_{ij})$. This potential is particularly useful as many engineering processes occur under controlled temperature conditions. From its differential, we can derive the [constitutive relations](@entry_id:186508) for entropy and stress as partial derivatives of the free energy function: $s = -\frac{\partial \psi}{\partial T}$ and $\sigma_{ij} = \rho \frac{\partial \psi}{\partial \varepsilon_{ij}}$. A system at constant temperature and strain will evolve to a state that minimizes its Helmholtz free energy [@problem_id:2701610].

Similarly, a **specific Gibbs-type free energy**, $g$, can be defined to have temperature and stress as its [natural variables](@entry_id:148352), $g = g(T, \sigma_{ij})$, by performing a further Legendre transformation on $\psi$. This thermodynamic structure provides the rigorous basis for deriving the constitutive laws that connect temperature, strain, and stress.

### The Origin of Thermal Strain: Isotropic Materials

The physical mechanism linking temperature to mechanical deformation is **[thermal expansion](@entry_id:137427)**. When an unconstrained solid body is heated uniformly, it changes its volume and shape. The strain associated with this [free expansion](@entry_id:139216) is known as **[thermal strain](@entry_id:187744)**, denoted $\varepsilon^{\mathrm{th}}_{ij}$. This is a form of non-mechanical strain, meaning it is not directly caused by applied forces.

The concept of [thermal strain](@entry_id:187744) is defined relative to a **stress-free reference temperature**, $T_0$. This is the temperature at which the material is in its natural, unstressed state. The relevant thermal variable is the temperature change from this reference, $\Delta T = T - T_0$ [@problem_id:2701584]. Importantly, the theory is invariant to a uniform shift in the temperature scale; replacing both $T$ and $T_0$ by $T+c$ and $T_0+c$ respectively leaves the physics unchanged, as $\Delta T$ remains the same [@problem_id:2701584].

For a homogeneous and isotropic material, a uniform temperature change cannot induce a preferred direction of deformation. Consequently, the resulting [thermal strain](@entry_id:187744) tensor must also be isotropic. The only second-order tensor that is isotropic is a scalar multiple of the identity tensor, $\delta_{ij}$. For small temperature changes, the magnitude of this strain is linearly proportional to $\Delta T$. This leads to the fundamental definition of [thermal strain](@entry_id:187744) for an isotropic solid:

$$
\varepsilon^{\mathrm{th}}_{ij} = \alpha \Delta T \delta_{ij}
$$

The scalar proportionality constant, $\alpha$, is the **linear coefficient of thermal expansion**. It is physically defined as the fractional change in length of a material line element per unit change in temperature, under stress-free conditions [@problem_id:2928399]. In the context of small strain theory, this is equivalent to the rate of change of a [normal strain](@entry_id:204633) component with respect to temperature at zero stress: $\alpha = (\partial \varepsilon_{11} / \partial T)_{\sigma=0}$.

From the tensor form of the [thermal strain](@entry_id:187744), we can determine the corresponding volumetric [thermal strain](@entry_id:187744), $\varepsilon^{\mathrm{th}}_{\mathrm{vol}}$, which is the trace of the [thermal strain](@entry_id:187744) tensor:

$$
\varepsilon^{\mathrm{th}}_{\mathrm{vol}} = \mathrm{tr}(\varepsilon^{\mathrm{th}}_{ij}) = \varepsilon^{\mathrm{th}}_{kk} = \alpha \Delta T \delta_{kk} = \alpha \Delta T (1+1+1) = 3\alpha \Delta T
$$

This shows that the coefficient of volumetric [thermal expansion](@entry_id:137427) is exactly three times the linear [coefficient of thermal expansion](@entry_id:143640) for an isotropic material. The rate of change of volumetric strain with temperature under zero stress is therefore $(\partial \varepsilon_{\mathrm{vol}} / \partial T)_{\sigma=0} = 3\alpha$ [@problem_id:2928399].

### The Constitutive Law of Linear Isotropic Thermoelasticity

The cornerstone of linear [thermoelasticity](@entry_id:158447) is the principle of **[strain decomposition](@entry_id:186005)**. It postulates that the total observable strain, $\varepsilon_{ij}$, can be additively decomposed into an elastic (mechanical) part, $\varepsilon^{\mathrm{e}}_{ij}$, and a thermal part, $\varepsilon^{\mathrm{th}}_{ij}$:

$$
\varepsilon_{ij} = \varepsilon^{\mathrm{e}}_{ij} + \varepsilon^{\mathrm{th}}_{ij}
$$

Crucially, stress is generated *only* by the elastic part of the strain. This [elastic strain](@entry_id:189634) represents the distortion of the material's atomic lattice away from its natural configuration. The [thermal strain](@entry_id:187744), if allowed to occur freely, does not distort the lattice and therefore does not generate stress. The relationship between stress and elastic strain is given by the generalized Hooke's Law for an [isotropic material](@entry_id:204616):

$$
\sigma_{ij} = \lambda \varepsilon^{\mathrm{e}}_{kk} \delta_{ij} + 2\mu \varepsilon^{\mathrm{e}}_{ij}
$$

where $\lambda$ and $\mu$ are the Lamé [elastic moduli](@entry_id:171361).

By substituting the [strain decomposition](@entry_id:186005), $\varepsilon^{\mathrm{e}}_{ij} = \varepsilon_{ij} - \varepsilon^{\mathrm{th}}_{ij}$, into Hooke's law, we derive the comprehensive [constitutive relation](@entry_id:268485) for [thermoelasticity](@entry_id:158447), expressing stress in terms of the total observable strain and the temperature change. This is known as the **Duhamel-Neumann relation**:

$$
\sigma_{ij} = \lambda (\varepsilon_{kk} - 3\alpha \Delta T) \delta_{ij} + 2\mu (\varepsilon_{ij} - \alpha \Delta T \delta_{ij})
$$

Rearranging this expression gives an alternative and commonly used form:

$$
\sigma_{ij} = (\lambda \varepsilon_{kk} \delta_{ij} + 2\mu \varepsilon_{ij}) - (3\lambda + 2\mu) \alpha \Delta T \delta_{ij}
$$

The first term is the standard expression for stress in isothermal elasticity. The second term is a thermally induced hydrostatic stress (a pressure). Recognizing that the bulk modulus is $K = \lambda + \frac{2}{3}\mu$, we can write $3K = 3\lambda + 2\mu$. The [constitutive law](@entry_id:167255) then becomes:

$$
\sigma_{ij} = \lambda \varepsilon_{kk} \delta_{ij} + 2\mu \varepsilon_{ij} - 3K \alpha \Delta T \delta_{ij}
$$

This equation elegantly captures the interplay between mechanical deformation and thermal effects [@problem_id:2701587]. The roles of the [elastic moduli](@entry_id:171361) become clear when we consider two limiting cases:

1.  **Unconstrained Uniform Heating:** If a body is heated by $\Delta T$ and is completely free to expand, it will do so without generating any stress ($\sigma_{ij} = 0$). The total strain that develops is precisely the free [thermal strain](@entry_id:187744), $\varepsilon_{ij} = \alpha \Delta T \delta_{ij}$. This result is independent of the [elastic moduli](@entry_id:171361) $\lambda$ and $\mu$ [@problem_id:2701587].

2.  **Fully Constrained Uniform Heating:** If a body is heated by $\Delta T$ but is rigidly constrained so that it cannot deform at all (i.e., the total strain $\varepsilon_{ij} = 0$), it cannot accommodate the [thermal expansion](@entry_id:137427). This frustrated expansion manifests as a purely elastic, compressive strain, $\varepsilon^{\mathrm{e}}_{ij} = -\alpha \Delta T \delta_{ij}$. This [elastic strain](@entry_id:189634) generates a purely hydrostatic (uniform in all directions) compressive stress: $\sigma_{ij} = -3K \alpha \Delta T \delta_{ij}$. The magnitude of this stress is governed by the bulk modulus $K$, which measures the material's resistance to volume change [@problem_id:2701587].

### Generation of Thermal Stresses: Constraints and Incompatibility

The preceding examples reveal a universal principle: [thermal stresses](@entry_id:180613) do not arise from temperature changes per se, but from the **prevention of free thermal deformation**. This prevention can be caused by two distinct mechanisms: external constraints imposed on the body's boundaries, or internal constraints arising from the geometry of the temperature field itself. The [thermal strain](@entry_id:187744), $\varepsilon^{\mathrm{th}}_{ij}$, can be conceptualized as a prescribed **[eigenstrain](@entry_id:198120)**—a non-mechanical strain field that the body "wants" to adopt [@problem_id:2701584]. Stress is the body's reaction when it is not allowed to do so freely.

#### External Constraints

The most straightforward way to generate [thermal stress](@entry_id:143149) is to mechanically restrain a body while changing its temperature. Consider a straight [prismatic bar](@entry_id:190143) of length $L_0$, Young's modulus $E$, and [thermal expansion coefficient](@entry_id:150685) $\alpha$, heated uniformly by $\Delta T$ [@problem_id:2701632].

If the bar is free, it would elongate by $\Delta L = \alpha \Delta T L_0$, corresponding to a free [thermal strain](@entry_id:187744) $\varepsilon^{\mathrm{th}} = \alpha \Delta T$.

Now, suppose the bar is rigidly fixed at both ends, such that its total length cannot change. The boundary conditions impose a total [axial strain](@entry_id:160811) of $\varepsilon = 0$. Since $\varepsilon = \varepsilon^{\mathrm{e}} + \varepsilon^{\mathrm{th}}$, the elastic strain must be $\varepsilon^{\mathrm{e}} = \varepsilon - \varepsilon^{\mathrm{th}} = 0 - \alpha \Delta T = -\alpha \Delta T$. This compressive elastic strain gives rise to a uniform compressive axial stress:

$$
\sigma = E \varepsilon^{\mathrm{e}} = -E \alpha \Delta T
$$

This reactive stress depends on the material's stiffness $E$ and its tendency to expand $\alpha$, but interestingly, not on the bar's length or cross-sectional area.

Conversely, if the boundary conditions are designed to perfectly match the free thermal deformation—for instance, by moving one end by the precise amount $\Delta L = \alpha \Delta T L_0$—the total strain becomes $\varepsilon = \Delta L / L_0 = \alpha \Delta T$. In this case, the [elastic strain](@entry_id:189634) is zero, and the resulting stress is zero [@problem_id:2701632]. This highlights that reactive stresses arise exactly when the kinematically imposed total strain differs from the free [thermal strain](@entry_id:187744).

#### Internal Constraints and Incompatibility

More subtly, [thermal stresses](@entry_id:180613) can arise in a body with completely free boundaries and no external forces, provided the temperature field is non-uniform in a specific way. For any given strain field $\varepsilon_{ij}(x,y,z)$ to be derivable from a continuous, single-valued [displacement field](@entry_id:141476) $u_i(x,y,z)$, it must satisfy a set of differential equations known as the **Saint-Venant [compatibility conditions](@entry_id:201103)**. A strain field satisfying these conditions is termed **compatible**.

The total strain field $\varepsilon_{ij}$ must always be compatible. However, the thermal eigenstrain field, $\varepsilon^{\mathrm{th}}_{ij} = \alpha \Delta T(\mathbf{x}) \delta_{ij}$, may not be. If the [eigenstrain](@entry_id:198120) field is **incompatible**, the body cannot simply deform to accommodate it without tearing or overlapping. To maintain continuity, an [elastic strain](@entry_id:189634) field $\varepsilon^{\mathrm{e}}_{ij}$ must develop such that the sum, $\varepsilon_{ij} = \varepsilon^{\mathrm{e}}_{ij} + \varepsilon^{\mathrm{th}}_{ij}$, *is* compatible. This forced [elastic strain](@entry_id:189634) gives rise to a **[residual stress](@entry_id:138788)** field, which is self-equilibrated (i.e., its [net force](@entry_id:163825) and moment are zero) [@problem_id:2701619].

The incompatibility of a strain field can be measured by applying the incompatibility operator, denoted $\mathrm{inc}$. The requirement that the total strain is compatible ($\mathrm{inc}(\varepsilon) = 0$) leads to the fundamental relationship:

$$
\mathrm{inc}(\varepsilon^{\mathrm{e}}) = - \mathrm{inc}(\varepsilon^{\mathrm{th}})
$$

This shows that an incompatible eigenstrain acts as a source for an incompatible (and therefore non-zero) [elastic strain](@entry_id:189634) field, which in turn means non-zero stress. For a 2D plane problem with isotropic thermal expansion, the compatibility condition simplifies, and the incompatibility of the [thermal strain](@entry_id:187744) can be shown to be directly proportional to the Laplacian of the temperature field [@problem_id:2701624]:

$$
\mathrm{inc}(\varepsilon^{\mathrm{th}}) \propto \alpha \nabla^2 T
$$

where $\nabla^2 = \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}$ is the Laplace operator. If the temperature field is harmonic ($\nabla^2 T = 0$), such as a linear temperature distribution, the [thermal strain](@entry_id:187744) field is compatible. In a simply connected body with no external tractions, this will result in a stress-free state [@problem_id:2701619]. However, if the temperature field is not harmonic—for example, a [quadratic field](@entry_id:636261) $T(x,y) = c x^2 + e y^2$ with $c+e \neq 0$ [@problem_id:2701624], or a field like $T(x,y) = \cos(\frac{\pi x}{L})\cos(\frac{\pi y}{L})$ [@problem_id:2701619]—then $\nabla^2 T \neq 0$. The [thermal strain](@entry_id:187744) is incompatible, and a non-zero [residual stress](@entry_id:138788) field must exist within the body, even if its boundaries are completely free.

### Advanced Topics in Thermoelasticity

#### Anisotropy

Many modern materials, such as single crystals and [fiber-reinforced composites](@entry_id:194995), are anisotropic, meaning their properties depend on direction. For such materials, the scalar coefficient of thermal expansion $\alpha$ is replaced by a symmetric, [second-rank tensor](@entry_id:199780), $\alpha_{ij}$. The [thermal strain](@entry_id:187744) is then given by:

$$
\varepsilon^{\mathrm{th}}_{ij} = \alpha_{ij} \Delta T
$$

The components of $\alpha_{ij}$ depend on the orientation of the coordinate system. If we know the tensor components in a principal material basis, where it is diagonal, $\alpha^{\mathrm{mat}} = \mathrm{diag}(\alpha_1, \alpha_2, \alpha_3)$, we can find its components in any other laboratory frame using the standard [tensor transformation rule](@entry_id:185176). For a rotation represented by the orthogonal matrix $Q_{ij}$, the transformed components $\alpha'_{ij}$ are given by $\alpha'_{ij} = Q_{ip} Q_{jq} \alpha_{pq}$ [@problem_id:2701591]. A significant consequence of this is that even a uniform temperature change can induce shear strains ($\varepsilon^{\mathrm{th}}_{ij} \neq 0$ for $i \neq j$) if the laboratory axes are not aligned with the principal axes of thermal expansion. For instance, a rotation of $30^\circ$ for a material with $\alpha_1 \neq \alpha_2$ will generate a non-zero off-diagonal component $\alpha'_{12}$ [@problem_id:2701591].

#### Coupled Thermoelasticity

The theory presented thus far is based on an **uncoupled** approximation: the temperature field $T(\mathbf{x}, t)$ is assumed to be governed by the standard heat conduction equation and is solved independently of the mechanical deformation. This temperature field then acts as a known input to the mechanical problem.

In a more general **fully coupled** theory, the deformation field also influences the temperature. This coupling arises from the energy balance and is manifest in the heat equation. For an [isotropic material](@entry_id:204616), the fully coupled, linearized heat equation is [@problem_id:2701601]:

$$
\rho c \dot{T} + 3K \alpha T_0 \mathrm{tr}(\dot{\varepsilon}) = k \nabla^2 T + r
$$

Here, $\dot{T}$ is the [material time derivative](@entry_id:190892) of temperature, $\dot{\varepsilon}$ is the [strain rate tensor](@entry_id:198281), $c$ is the specific heat, $k$ is the thermal conductivity, and $r$ is a volumetric heat source. The new term, $3K \alpha T_0 \mathrm{tr}(\dot{\varepsilon})$, is the **[thermoelastic coupling](@entry_id:183445) term**. It describes the temperature change due to a change in volume. A rapid expansion ($\mathrm{tr}(\dot{\varepsilon}) > 0$) causes a slight cooling, while a rapid compression causes heating. While this effect is often small and can be neglected in many static or quasi-static problems, it becomes important in dynamic problems, such as the propagation of [acoustic waves](@entry_id:174227), where it leads to [thermoelastic damping](@entry_id:203464).

#### Finite Strain Thermoelasticity

Extending these concepts to the regime of **finite strains** requires a more sophisticated mathematical framework. The small strain tensor $\varepsilon$ is replaced by a [finite strain](@entry_id:749398) measure, such as the **Green-Lagrange strain tensor** $E = \frac{1}{2}(F^T F - I)$, where $F$ is the [deformation gradient](@entry_id:163749). The Cauchy stress $\sigma$ is replaced by a [work-conjugate stress](@entry_id:182069) measure, such as the **second Piola-Kirchhoff stress** $S$.

The [constitutive laws](@entry_id:178936) are derived from a Helmholtz free energy function that depends on the [finite strain](@entry_id:749398) tensor and temperature, $\psi(E, T)$. For a [simple extension](@entry_id:152948) of the linear model to finite strains (a St. Venant-Kirchhoff type material), the potential can be formulated as [@problem_id:2701614]:

$$
\psi(E,T) = \frac{1}{2}\lambda(\mathrm{tr}E)^2 + \mu E:E - 3K\alpha_T(T-T_0)\mathrm{tr}E + \psi_{\mathrm{th}}(T)
$$

The [constitutive relations](@entry_id:186508) for stress and entropy are then obtained via [partial differentiation](@entry_id:194612), $S = \partial\psi/\partial E$ and $\eta = -\partial\psi/\partial T$, directly linking the model back to the fundamental [thermodynamic principles](@entry_id:142232) introduced at the beginning of this chapter. This provides a thermodynamically consistent path to modeling materials that undergo large deformations and significant temperature changes simultaneously.