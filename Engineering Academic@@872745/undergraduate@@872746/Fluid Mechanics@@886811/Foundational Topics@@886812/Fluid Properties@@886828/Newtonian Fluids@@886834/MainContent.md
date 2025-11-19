## Introduction
The motion of fluids is central to countless natural phenomena and engineering systems. Understanding how a fluid responds to an applied force is a cornerstone of fluid mechanics, and this article focuses on a particularly important and widespread class of fluids: Newtonian fluids, which include common substances like water, air, and oil. While the behavior of fluids can seem complex, the Newtonian model provides a powerful and elegantly simple framework for describing their flow. The knowledge gap this article addresses is the transition from a qualitative understanding of "[fluid friction](@entry_id:268568)" to a quantitative, predictive model based on the concept of viscosity.

The reader will embark on a structured journey to master this topic. The first chapter, **"Principles and Mechanisms,"** will lay the theoretical groundwork, defining the linear relationship between [stress and strain rate](@entry_id:263123) and introducing the tensor formulation for general flows. Following this, **"Applications and Interdisciplinary Connections"** will demonstrate the immense practical utility of the Newtonian model in fields ranging from mechanical engineering to biomechanics. Finally, **"Hands-On Practices"** will offer a chance to apply these concepts to solve concrete problems, solidifying your understanding. Let's begin by exploring the fundamental principles that govern Newtonian fluid behavior.

## Principles and Mechanisms

The behavior of fluids under the influence of external forces is governed by their internal resistance to motion. This resistance, a form of internal friction, is quantified by the property of viscosity. For a broad and important class of fluids, known as **Newtonian fluids**, the relationship between the applied stress and the resulting [fluid motion](@entry_id:182721) is elegantly simple and linear. This chapter elucidates the fundamental principles and mechanisms that define this behavior, moving from simple shear flows to a generalized tensor description, and exploring the physical implications of the Newtonian model.

### The Constitutive Relation: Stress and the Rate of Strain

The defining characteristic of a fluid, which distinguishes it from an elastic solid, is its response to a **shear stress**. A shear stress is a force applied tangentially to a surface. While an elastic solid deforms by a finite amount under a constant shear stress, a fluid will continue to deform, or flow, as long as the stress is applied.

Consider a thin layer of a substance placed between two large parallel plates. If the substance is an ideal elastic solid (a Hookean solid), applying a constant shear stress $\tau$ to the top plate causes a fixed displacement. The material deforms, creating an internal **shear strain**, $\gamma$, which is the displacement of the top plate divided by the layer thickness. The relationship is given by Hooke's Law, $\tau = G\gamma$, where $G$ is the [shear modulus](@entry_id:167228). The deformation ceases once the internal stress balances the applied stress.

In contrast, if the substance is a fluid, the same constant shear stress $\tau$ will cause the top plate to move with a [constant velocity](@entry_id:170682). The fluid continuously deforms. The key insight, first formulated by Sir Isaac Newton, is that for many common fluids like water, air, and oil, the shear stress is not proportional to the strain itself, but to the **[rate of shear strain](@entry_id:270048)**, denoted as $\dot{\gamma}$. This [rate of strain](@entry_id:267998) represents how quickly the fluid is being deformed. For a [simple shear](@entry_id:180497) flow between two plates, this is equivalent to the [velocity gradient](@entry_id:261686) across the fluid layer. This fundamental relationship is known as **Newton's Law of Viscosity**:

$$
\tau = \mu \dot{\gamma} = \mu \frac{du}{dy}
$$

Here, $\mu$ is the **dynamic viscosity**, a property of the fluid that measures its [intrinsic resistance](@entry_id:166682) to shear flow. The term $\frac{du}{dy}$ is the velocity gradient, where $u$ is the [fluid velocity](@entry_id:267320) parallel to the plates and $y$ is the coordinate perpendicular to them. A fluid that obeys this linear relationship is, by definition, a **Newtonian fluid**.

The stark difference in behavior between a solid and a fluid under shear stress is profound. For a solid, the displacement is proportional to the stress, while for a fluid, the *velocity* is proportional to the stress. Consequently, under a constant applied shear stress for a duration of time $T$, the final displacement of the fluid will grow linearly with time, whereas the solid's displacement remains constant after reaching equilibrium [@problem_id:1795077]. The viscosity $\mu$ for a fluid plays a role analogous to the shear modulus $G$ for a solid, but it relates stress to the *rate* of deformation, not the deformation itself.

### The Stress and Strain-Rate Tensors

While Newton's law of viscosity in its scalar form, $\tau = \mu \frac{du}{dy}$, is exceptionally useful for simple [one-dimensional flows](@entry_id:200507), a more general description is required for complex three-dimensional [fluid motion](@entry_id:182721). This is achieved using the language of tensors.

The state of deformation in a fluid element is completely described by the **[rate-of-strain tensor](@entry_id:260652)**, often denoted as $\boldsymbol{\varepsilon}$ or $\mathbf{D}$. Its components are given by:

$$
\varepsilon_{ij} = \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right)
$$

where $u_i$ is the velocity component in the $x_i$ direction (e.g., $u_1=u, u_2=v, u_3=w$) and $x_j$ is the coordinate in the $j$-th direction. The diagonal components ($\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{zz}$) represent the rates of linear extension or compression of a fluid element along the coordinate axes. The off-diagonal components ($\varepsilon_{xy}, \varepsilon_{yz}$, etc.) represent half the rate of angular deformation, or shearing, of the element. By its definition, the [rate-of-strain tensor](@entry_id:260652) is symmetric, meaning $\varepsilon_{ij} = \varepsilon_{ji}$.

The state of [internal forces](@entry_id:167605) within the fluid is described by the **stress tensor**, $\boldsymbol{\sigma}$. A component $\sigma_{ij}$ represents the force per unit area on a surface with its normal in the $i$-th direction, with the force itself acting in the $j$-th direction. The diagonal components ($\sigma_{xx}, \sigma_{yy}, \sigma_{zz}$) are **[normal stresses](@entry_id:260622)** (pressures or tensions), while the off-diagonal components ($\sigma_{xy}, \sigma_{yx}$, etc.) are **shear stresses**.

For an incompressible Newtonian fluid, the [constitutive relation](@entry_id:268485) connecting the stress and rate-of-strain tensors is:

$$
\sigma_{ij} = -p\delta_{ij} + 2\mu\varepsilon_{ij}
$$

Here, $p$ is the thermodynamic **pressure**, an isotropic stress component that exists even in a fluid at rest. The term $\delta_{ij}$ is the **Kronecker delta**, which is 1 if $i=j$ and 0 if $i \neq j$. The term $2\mu\varepsilon_{ij}$ is the **viscous stress tensor**, which represents the stresses that arise purely due to [fluid motion](@entry_id:182721).

Let us apply this general formulation to the [simple shear](@entry_id:180497) flow between two [parallel plates](@entry_id:269827), known as **planar Couette flow**. The velocity field is given by $\mathbf{v} = (u(y), 0, 0)$, with $u(y) = U \frac{y}{h}$, where $U$ is the speed of the top plate and $h$ is the gap distance. Let's find the components of the [rate-of-strain tensor](@entry_id:260652). The only non-zero [velocity gradient](@entry_id:261686) is $\frac{\partial u}{\partial y} = \frac{U}{h}$.
The components of $\boldsymbol{\varepsilon}$ are then:

$$
\varepsilon_{xy} = \varepsilon_{yx} = \frac{1}{2} \left( \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x} \right) = \frac{1}{2} \left( \frac{U}{h} + 0 \right) = \frac{U}{2h}
$$

All other components, including the diagonal ones ($\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{zz}$), are zero. Now, let's find the shear stress component $\sigma_{xy}$ using the constitutive law. Since $i \neq j$, $\delta_{xy}=0$:

$$
\sigma_{xy} = -p\delta_{xy} + 2\mu\varepsilon_{xy} = 0 + 2\mu \left( \frac{U}{2h} \right) = \mu \frac{U}{h}
$$

This result precisely recovers the simple scalar form of Newton's law of viscosity, demonstrating the consistency of the tensor formulation [@problem_id:1795116]. It also shows that the [viscous stress](@entry_id:261328) tensor is symmetric, i.e., $\tau_{xy} = \tau_{yx}$ (using $\tau$ here to denote the viscous part of the stress), which is a consequence of the [conservation of angular momentum](@entry_id:153076) for a non-polar fluid element [@problem_id:1794896].

### Defining Characteristics of Newtonian Behavior

The linear tensor relationship $\sigma_{ij} = -p\delta_{ij} + 2\mu\varepsilon_{ij}$ carries several important physical implications that define Newtonian fluid behavior.

#### Isotropy

The use of a single scalar coefficient, the [dynamic viscosity](@entry_id:268228) $\mu$, assumes the fluid is **isotropic**, meaning its properties are independent of direction. The fluid responds to deformation in the same way regardless of its orientation. If a fluid were **anisotropic**, possessing a preferred internal structure or direction, its constitutive law would be more complex. For instance, a hypothetical fluid with a preferred direction $\mathbf{k}$ might have a stress tensor that depends on the orientation of the strain relative to $\mathbf{k}$ [@problem_id:1795051]. In such a case, the stresses generated by a given flow field would differ from those in a Newtonian fluid, and a single scalar viscosity would be insufficient to describe its behavior. The Newtonian model's simplicity and broad applicability stem directly from this assumption of [isotropy](@entry_id:159159).

#### Absence of Normal Stress Differences

A crucial feature of Newtonian fluids is their behavior regarding [normal stresses](@entry_id:260622) in simple shear. As we calculated for Couette flow, all diagonal components of the [rate-of-strain tensor](@entry_id:260652) ($\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{zz}$) are zero. According to the [constitutive law](@entry_id:167255), the viscous contributions to the normal stresses are therefore also zero:

$$
\sigma_{xx} = -p + 2\mu\varepsilon_{xx} = -p
$$
$$
\sigma_{yy} = -p + 2\mu\varepsilon_{yy} = -p
$$
$$
\sigma_{zz} = -p + 2\mu\varepsilon_{zz} = -p
$$

This leads to the remarkable conclusion that for a Newtonian fluid in [simple shear](@entry_id:180497), all three [normal stresses](@entry_id:260622) are equal to each other and equal to the local thermodynamic pressure, $\sigma_{xx} = \sigma_{yy} = \sigma_{zz} = -p$ [@problem_id:1795093]. There are no "[normal stress differences](@entry_id:191914)." This is in sharp contrast to many non-Newtonian fluids, which can generate significant tensions along streamlines (e.g., the rod-climbing Weissenberg effect), a phenomenon that arises from non-zero [normal stress differences](@entry_id:191914).

#### Constant Viscosity

The linearity of the Newtonian model implies that the [dynamic viscosity](@entry_id:268228) $\mu$ is a material property that is independent of the shear rate $\dot{\gamma}$. For many fluids, this is an excellent approximation. However, numerous fluids, often called **non-Newtonian**, exhibit a viscosity that changes with the rate of shear. These are often described by a **[power-law model](@entry_id:272028)**, $\tau = K (\dot{\gamma})^n$, where $K$ is the consistency index and $n$ is the [flow behavior index](@entry_id:265017).
- If $n  1$, the [apparent viscosity](@entry_id:260802) decreases as the shear rate increases. Such fluids, like paint or ketchup, are called **shear-thinning**.
- If $n > 1$, the [apparent viscosity](@entry_id:260802) increases with the shear rate. These fluids, like a cornstarch and water mixture, are called **[shear-thickening](@entry_id:260777)**.
- A Newtonian fluid is a special case of the [power-law model](@entry_id:272028) where $n=1$ and $K=\mu$ [@problem_id:1775807]. This highlights that the "Newtonian" label applies to a specific, albeit common, type of fluid response.

### Understanding Viscosity

Viscosity is the central parameter in the study of Newtonian fluids, and it is important to understand its nuances.

#### Dynamic versus Kinematic Viscosity

We have focused on the **dynamic viscosity**, $\mu$, which has units of Pascal-seconds ($Pa \cdot s$) or $kg/(m \cdot s)$. It is the direct measure of a fluid's resistance to shear and is the property that determines the magnitude of shear stress for a given [rate of strain](@entry_id:267998).

However, in many fluid dynamics equations, such as the Navier-Stokes equations, the term that appears is the ratio of [dynamic viscosity](@entry_id:268228) to density, $\rho$. This ratio is called the **[kinematic viscosity](@entry_id:261275)**, $\nu$:

$$
\nu = \frac{\mu}{\rho}
$$

Kinematic viscosity has units of meters-squared per second ($m^2/s$) and represents the **diffusivity of momentum**. It describes how quickly momentum is transported through the fluid by molecular motion. A common point of confusion is the distinction between these two properties. A simple experiment can clarify their roles: if two fluids with identical [kinematic viscosity](@entry_id:261275) ($\nu$) but different densities ($\rho_A \neq \rho_B$) are subjected to the same [shear flow](@entry_id:266817) (e.g., Couette flow), they will produce different shear stresses. The shear stress is given by $\tau = \mu \frac{U}{h} = (\rho\nu)\frac{U}{h}$. Since $\nu$, $U$, and $h$ are the same, the ratio of the shear stresses will be equal to the ratio of the densities: $\frac{\tau_B}{\tau_A} = \frac{\rho_B}{\rho_A}$ [@problem_id:1795043]. This demonstrates that it is the dynamic viscosity $\mu$ that directly governs the forces in a flow.

#### Temperature Dependence

While we treat viscosity as a constant for a given fluid under fixed conditions, it is, in reality, a strong function of temperature. For liquids, viscosity typically decreases sharply as temperature increases. This is because the molecules have more thermal energy, allowing them to overcome cohesive intermolecular forces more easily. For many oils, this relationship can be modeled with an Arrhenius-type equation, such as $\mu(T) = C \exp(B/T)$, where $T$ is the [absolute temperature](@entry_id:144687) and $B$ and $C$ are constants. A modest increase in temperature, for instance from $25^\circ C$ to $85^\circ C$ for a typical oil, can cause the viscosity—and therefore the drag force in a lubrication system—to decrease by nearly 90% [@problem_id:1775814]. This dependence is a critical consideration in engineering applications like lubrication and heat transfer. For gases, in contrast, viscosity increases with temperature, as it arises primarily from molecular collisions, which become more frequent and energetic at higher temperatures.

### Energy Dissipation and Thermodynamic Constraints

The internal friction described by viscosity is not just a source of force; it is also a mechanism for [energy conversion](@entry_id:138574). When work is done on a fluid to make it flow against [viscous forces](@entry_id:263294), that [mechanical energy](@entry_id:162989) is irreversibly converted into internal energy, manifesting as heat. This process is called **[viscous dissipation](@entry_id:143708)**.

For a simple shear flow, the rate of [viscous dissipation](@entry_id:143708) per unit volume, $\Phi$, is the product of the shear stress and the shear rate:

$$
\Phi = \tau \dot{\gamma} = (\mu \dot{\gamma}) \dot{\gamma} = \mu \dot{\gamma}^2 = \mu \left(\frac{du}{dy}\right)^2
$$

Since $\mu$ is positive and the shear rate is squared, the dissipation is always non-negative, consistent with the second law of thermodynamics. In more complex flows, such as a layered Couette flow with two different fluids, the [dissipation rate](@entry_id:748577) can be calculated in each layer and averaged to find the total energy loss for the system [@problem_id:1744101].

This thermodynamic requirement—that viscous processes must always be dissipative or, in the limit of no motion, neutral—places fundamental constraints on the material properties themselves. For a general **compressible** isotropic Newtonian fluid, the viscous stress tensor has a slightly more complex form that includes resistance to volumetric changes:

$$
\tau'_{ij} = 2\mu \left(\varepsilon_{ij} - \frac{1}{3} \varepsilon_{kk} \delta_{ij}\right) + K \varepsilon_{kk} \delta_{ij}
$$

Here, $\varepsilon_{kk} = \nabla \cdot \mathbf{v}$ is the rate of [volumetric expansion](@entry_id:144241), and $K$ is the **[bulk viscosity](@entry_id:187773)**. The total rate of [viscous dissipation](@entry_id:143708) is $\Phi_v = \tau'_{ij}\varepsilon_{ij}$. By substituting the [constitutive relation](@entry_id:268485) and decomposing the [strain rate tensor](@entry_id:198281), this can be shown to be equivalent to:

$$
\Phi_v = 2\mu S'_{ij}S'_{ij} + K (\varepsilon_{kk})^2
$$

where $S'_{ij}$ is the deviatoric (shear) part of the [strain-rate tensor](@entry_id:266108). For $\Phi_v$ to be non-negative for any arbitrary flow, both coefficients in this [sum of squares](@entry_id:161049) must be non-negative. This leads to the fundamental thermodynamic constraints on the viscosity coefficients:

$$
\mu \ge 0 \quad \text{and} \quad K \ge 0
$$

This ensures that a fluid always resists both shear deformation and volumetric compression, dissipating energy in the process, as required by the laws of physics [@problem_id:1744157].