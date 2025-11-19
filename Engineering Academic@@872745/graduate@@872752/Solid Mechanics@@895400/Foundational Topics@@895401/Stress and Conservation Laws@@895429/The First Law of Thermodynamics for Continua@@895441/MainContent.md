## Introduction
The First Law of Thermodynamics, the principle of [energy conservation](@entry_id:146975), is a cornerstone of physical science. While universally understood in its general form, its application to deforming materials—the realm of [continuum mechanics](@entry_id:155125)—requires a more rigorous and detailed formulation. Moving beyond simple energy accounting, the law becomes a powerful tool for predicting how materials heat up, change properties, and even fail under mechanical load. This article bridges the gap between the conceptual law and its practical application by developing the complete thermomechanical framework for a continuous medium.

The following chapters will guide you through this framework systematically. In "Principles and Mechanisms," we will derive the local [energy balance equation](@entry_id:191484), dissecting the roles of [stress power](@entry_id:182907), heat flux, and internal sources. "Applications and Interdisciplinary Connections" will then showcase the law's predictive power in real-world scenarios, from plastic deformation and [material failure](@entry_id:160997) in solids to coupled phenomena in fluid dynamics and electromagnetism. Finally, "Hands-On Practices" will provide an opportunity to apply these principles to solve concrete engineering problems, solidifying your understanding of the intricate link between mechanics and thermodynamics.

## Principles and Mechanisms

The First Law of Thermodynamics, a fundamental statement of energy conservation, provides the bedrock for analyzing the coupled thermal and mechanical behavior of materials. While the introductory chapter established the conceptual basis for this law, this chapter delves into its rigorous mathematical formulation for a continuous medium. We will derive the local differential equations that govern [energy transport](@entry_id:183081) and conversion within a deforming body and explore the physical meaning of each term, laying the foundation for modeling complex thermomechanical phenomena.

### The Global Statement of Energy Conservation

We begin with the most general statement of the First Law, applied to an arbitrary material volume $V(t)$ that moves and deforms with the continuum. This volume contains a fixed set of material particles. The law states that the time rate of change of the total energy contained within this volume is equal to the sum of the rate at which mechanical work is done on the volume and the rate at which heat is supplied to it.

The **total energy** $E$ of the material volume is the sum of its kinetic energy and its total internal energy. The kinetic energy arises from the macroscopic motion of the material, while the internal energy encompasses the microscopic thermal and potential energies stored within the material's structure. For a continuum with mass density $\rho$, velocity field $\mathbf{v}$, and specific internal energy (internal energy per unit mass) $u$, the total energy is expressed as the integral:
$$
E = \int_{V(t)} \rho \left(u + \frac{1}{2} |\mathbf{v}|^2 \right) dV
$$

The **rate of mechanical work**, or power, $\dot{W}$, is delivered to the body by two types of forces: [surface forces](@entry_id:188034) and body forces. Surface forces are exerted on the boundary $\partial V(t)$ of the volume, represented by the traction vector $\mathbf{t}$. Body forces, such as gravity, act on the material throughout the volume and are represented by a force per unit mass, $\mathbf{b}$. The total [mechanical power](@entry_id:163535) is the integral of these forces dotted with the velocity at which they act:
$$
\dot{W} = \int_{\partial V(t)} \mathbf{t} \cdot \mathbf{v} \, dA + \int_{V(t)} \rho \mathbf{b} \cdot \mathbf{v} \, dV
$$

The **rate of heat transfer**, $\dot{Q}$, also has two contributions. Heat can be conducted across the boundary, described by the heat flux vector $\mathbf{q}$, which represents the flow of thermal energy per unit area per unit time. By convention, $\mathbf{q}$ is positive for heat flowing out of the surface, so the heat input is given by a surface integral with a negative sign. Additionally, heat may be generated internally throughout the volume by processes such as chemical reactions, [phase transformations](@entry_id:200819), or electromagnetic effects. This is represented by a volumetric heat source term $r$ (power per unit volume). The total rate of heat transfer is:
$$
\dot{Q} = -\int_{\partial V(t)} \mathbf{q} \cdot \mathbf{n} \, dA + \int_{V(t)} r \, dV
$$
where $\mathbf{n}$ is the outward [unit normal vector](@entry_id:178851) to the surface element $dA$.

Combining these definitions, the integral or global form of the First Law of Thermodynamics is:
$$
\frac{D}{Dt} \int_{V(t)} \rho \left(u + \frac{1}{2} |\mathbf{v}|^2 \right) dV = \int_{\partial V(t)} \mathbf{t} \cdot \mathbf{v} \, dA + \int_{V(t)} \rho \mathbf{b} \cdot \mathbf{v} \, dV - \int_{\partial V(t)} \mathbf{q} \cdot \mathbf{n} \, dA + \int_{V(t)} r \, dV
$$
Here, $\frac{D}{Dt}$ denotes the [material time derivative](@entry_id:190892), which follows the material as it moves. This global balance is a powerful statement, allowing for the calculation of the total energy change in a body by accounting for all power inputs across its boundaries and within its volume, as illustrated in complex scenarios involving simultaneous mechanical loading and thermal fluxes [@problem_id:2696679]. For a simple stationary rod, this integral law can be used directly to find the rate of change of the total internal energy by integrating the volumetric source and accounting for the heat flux at the ends [@problem_id:2696680].

### From Global Balance to Local Law: The Internal Energy Equation

While the global balance is fundamental, a local differential form of the energy equation is often more useful for solving problems, as it describes the behavior at every point in the continuum. To derive this, we transform the [surface integrals](@entry_id:144805) into [volume integrals](@entry_id:183482) using the Divergence Theorem and apply the Reynolds Transport Theorem. First, the traction vector $\mathbf{t}$ is related to the symmetric Cauchy stress tensor $\boldsymbol{\sigma}$ by $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$. The [mechanical power](@entry_id:163535) and heat flux [surface integrals](@entry_id:144805) become:
$$
\int_{\partial V(t)} \mathbf{t} \cdot \mathbf{v} \, dA = \int_{V(t)} \nabla \cdot (\boldsymbol{\sigma} \mathbf{v}) \, dV \quad \text{and} \quad \int_{\partial V(t)} \mathbf{q} \cdot \mathbf{n} \, dA = \int_{V(t)} \nabla \cdot \mathbf{q} \, dV
$$
Applying these transformations and the Reynolds Transport Theorem, and recognizing that the resulting integral equation must hold for any arbitrary volume $V(t)$, we arrive at the local balance of total energy:
$$
\rho \frac{D}{Dt} \left(u + \frac{1}{2} |\mathbf{v}|^2 \right) = \nabla \cdot (\boldsymbol{\sigma} \mathbf{v}) + \rho \mathbf{b} \cdot \mathbf{v} - \nabla \cdot \mathbf{q} + r
$$

Our primary interest is often in the evolution of the internal energy $u$, which is directly related to the material's temperature and state. To isolate the internal energy balance, we must subtract the rate of change of kinetic energy. This is achieved by invoking the local form of the [balance of linear momentum](@entry_id:193575), also known as **Cauchy's first law of motion**:
$$
\rho \frac{D\mathbf{v}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b}
$$
Taking the dot product of the [momentum equation](@entry_id:197225) with the velocity $\mathbf{v}$ yields an equation for the rate of change of kinetic energy:
$$
\rho \mathbf{v} \cdot \frac{D\mathbf{v}}{Dt} = \rho \frac{D}{Dt} \left(\frac{1}{2} |\mathbf{v}|^2 \right) = (\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{v} + \rho \mathbf{b} \cdot \mathbf{v}
$$
By expanding the divergence term $\nabla \cdot (\boldsymbol{\sigma}\mathbf{v}) = (\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{v} + \boldsymbol{\sigma}:\nabla\mathbf{v}$ in the total energy equation and then subtracting the kinetic [energy equation](@entry_id:156281), we eliminate the kinetic energy terms and the body force power term. This crucial step, which relies on the [balance of linear momentum](@entry_id:193575), separates the mechanical work that changes the bulk kinetic energy from the work that changes the internal state of the material [@problem_id:2924997]. The result is the local balance of internal energy:
$$
\rho \frac{Du}{Dt} = \boldsymbol{\sigma} : \nabla\mathbf{v} - \nabla \cdot \mathbf{q} + r
$$
Here, the term $\boldsymbol{\sigma} : \nabla\mathbf{v}$ is the **[stress power](@entry_id:182907)** per unit volume, representing the rate at which mechanical work is done by the stresses to deform the material element. Each term in this equation represents a rate of energy change per unit volume [@problem_id:2529335].

### The Physics of the Stress Power Term

The [stress power](@entry_id:182907) term, $\boldsymbol{\sigma} : \nabla\mathbf{v}$, is the gateway through which mechanical action affects the internal energy of the material. A deeper understanding of this term is essential. The tensor $\nabla\mathbf{v}$ is the **velocity gradient**, which describes how the velocity changes from point to point. It can be uniquely decomposed into a symmetric part and a skew-symmetric part:
$$
\nabla\mathbf{v} = \boldsymbol{d} + \boldsymbol{w}
$$
where
$$
\boldsymbol{d} = \frac{1}{2} \left(\nabla\mathbf{v} + (\nabla\mathbf{v})^T\right) \quad (\text{rate of deformation tensor})
$$
$$
\boldsymbol{w} = \frac{1}{2} \left(\nabla\mathbf{v} - (\nabla\mathbf{v})^T\right) \quad (\text{spin tensor})
$$
The [rate of deformation tensor](@entry_id:182598) $\boldsymbol{d}$ describes the rate of stretching and shearing of the material element, while the [spin tensor](@entry_id:187346) $\boldsymbol{w}$ describes its rate of [rigid-body rotation](@entry_id:268623).

For a classical (or Cauchy) continuum, which lacks internal couple stresses, the [balance of angular momentum](@entry_id:181848) requires the Cauchy stress tensor $\boldsymbol{\sigma}$ to be symmetric ($\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$). With this fundamental property, the [stress power](@entry_id:182907) can be simplified. The double contraction of a [symmetric tensor](@entry_id:144567) ($\boldsymbol{\sigma}$) with a [skew-symmetric tensor](@entry_id:199349) ($\boldsymbol{w}$) is identically zero. Therefore, the [stress power](@entry_id:182907) becomes:
$$
\boldsymbol{\sigma} : \nabla\mathbf{v} = \boldsymbol{\sigma} : (\boldsymbol{d} + \boldsymbol{w}) = \boldsymbol{\sigma} : \boldsymbol{d} + \boldsymbol{\sigma} : \boldsymbol{w} = \boldsymbol{\sigma} : \boldsymbol{d}
$$
The fact that $\boldsymbol{\sigma} : \boldsymbol{w} = 0$ carries a profound physical meaning: work done by stresses during pure rotation of a material element does not change its internal energy. Only the work done to deform the element (described by $\boldsymbol{d}$) contributes to the internal energy balance.

This allows us to write the internal energy balance in its most refined form, explicitly showing that the [mechanical power](@entry_id:163535) input is due to deformation [@problem_id:2924997]:
$$
\rho \frac{Du}{Dt} = \boldsymbol{\sigma} : \boldsymbol{d} - \nabla \cdot \mathbf{q} + r
$$
This equation is the cornerstone of continuum [thermomechanics](@entry_id:180251). It states that the internal energy of a material particle changes due to the rate of work done by stresses during deformation, the net heat conducted into the particle, and any volumetric heat generation.

### The General Heat Equation: Coupling Temperature and Deformation

The internal energy $u$ is a state variable that depends on the material's [thermodynamic state](@entry_id:200783), which can be described by temperature and deformation. To arrive at an equation for temperature $T$, we must relate $\frac{Du}{Dt}$ to $\frac{DT}{Dt}$. The internal energy change can be partitioned into a recoverable part associated with elastic deformation, an irrecoverable part associated with microstructural changes (like the generation of dislocations), and a thermal part associated with temperature.

Similarly, the deformation rate $\boldsymbol{d}$ can be decomposed into an elastic (reversible) part $\boldsymbol{d}^e$ and an inelastic or plastic (irreversible) part $\boldsymbol{d}^p$. The [stress power](@entry_id:182907) is then partitioned:
$$
\boldsymbol{\sigma} : \boldsymbol{d} = \boldsymbol{\sigma} : \boldsymbol{d}^e + \boldsymbol{\sigma} : \boldsymbol{d}^p
$$
The elastic power, $\boldsymbol{\sigma} : \boldsymbol{d}^e$, corresponds to the rate of change of recoverable [elastic strain energy](@entry_id:202243) stored in the material. This part of the work does not dissipate as heat. The plastic power, $\boldsymbol{\sigma} : \boldsymbol{d}^p$, represents work done during irreversible deformation processes. This work is largely dissipated as heat, though a fraction may be stored in the material's evolving [microstructure](@entry_id:148601) as "[stored energy of cold work](@entry_id:200373)" [@problem_id:2909210].

This partitioning of plastic work is quantified by the **Taylor-Quinney coefficient**, $\beta$, defined as the fraction of [plastic work](@entry_id:193085) rate that is instantaneously converted into heat [@problem_id:2909210]. The heat generated per unit volume due to [plastic dissipation](@entry_id:201273) is therefore $\beta(\boldsymbol{\sigma} : \boldsymbol{d}^p)$.

Relating the thermal part of the internal energy to temperature via the specific heat capacity $c$ (so that the rate of change of thermal energy per unit volume is $\rho c \frac{DT}{Dt}$), we can formulate the general heat equation. The rate of change of thermal energy is balanced by the heat supplied by conduction, the heat generated by [plastic dissipation](@entry_id:201273), and other external heat sources [@problem_id:2605827, @problem_id:2702531]:
$$
\rho c \frac{DT}{Dt} = - \nabla \cdot \mathbf{q} + \beta (\boldsymbol{\sigma} : \boldsymbol{d}^p) + r
$$
Finally, incorporating **Fourier's Law of Heat Conduction**, which relates the heat flux to the temperature gradient, $\mathbf{q} = -k \nabla T$ (where $k$ is the thermal conductivity), we obtain the general heat equation for a thermoplastic solid:
$$
\rho c \frac{DT}{Dt} = \nabla \cdot (k \nabla T) + \beta (\boldsymbol{\sigma} : \boldsymbol{d}^p) + r
$$
This equation elegantly captures the full coupling: mechanical deformation (via $\boldsymbol{d}^p$) acts as a source term for the temperature field, while the temperature field, in turn, influences the mechanical properties ($\boldsymbol{\sigma}$, $k$, $c$, etc.), creating a feedback loop.

### Sources of Thermal Energy: Dissipation and External Supply

The heat equation highlights two distinct types of source terms that drive temperature changes: internal dissipation and external supply.

**Internal Dissipation ($\beta (\boldsymbol{\sigma} : \boldsymbol{d}^p)$):** This term represents the conversion of mechanical work into heat. It is a consequence of the material's own irreversible deformation. A key application where this term dominates is in high-strain-rate phenomena, such as ballistic impact or [metal forming](@entry_id:188560). Under these conditions, deformation occurs so rapidly that there is little time for the generated heat to conduct away. This **[adiabatic heating](@entry_id:182901)** can cause significant temperature increases, leading to [thermal softening](@entry_id:187731) of the material. This softening can concentrate further deformation in a narrow region, leading to a failure mode known as an **adiabatic shear band** [@problem_id:2613664].

For example, for a metal undergoing adiabatic uniaxial [plastic deformation](@entry_id:139726) with a plastic strain increment of $\Delta\varepsilon_p$ at a nearly constant [flow stress](@entry_id:198884) $\sigma$, the temperature rise $\Delta T$ can be estimated by integrating the simplified heat equation: $\rho c \Delta T \approx \beta \sigma \Delta \varepsilon_p$. For a copper specimen with typical properties, a plastic strain of $0.20$ at a stress of $300 \, \mathrm{MPa}$ can result in a temperature rise of approximately $16 \, \mathrm{K}$ [@problem_id:2909210]. The heat generated per unit volume, $\beta \sigma \Delta \varepsilon_p$, depends only on the mechanical state and the material's dissipative properties, not its density.

**External Supply ($r$):** This term represents thermal energy added to the system from non-mechanical origins. It is a prescribed field in a problem and can represent heat from chemical reactions, [radioactive decay](@entry_id:142155), or absorption of [electromagnetic radiation](@entry_id:152916). Unlike the dissipation term, which is determined by the evolving mechanical state of the body, the external supply term is an independent input [@problem_id:2605827].

### Special Cases and Simplifications

The full [thermomechanical coupling](@entry_id:183230) described by the general heat equation is not always necessary. There are important limiting cases where the equation simplifies considerably. The decision to neglect mechanical source terms depends on the relative magnitude of the heat generated by work compared to other [energy transport](@entry_id:183081) mechanisms [@problem_id:2490691].

**Case 1: Stationary Solid.** For a solid that is not moving or deforming, the [velocity field](@entry_id:271461) is zero, $\mathbf{v} = \mathbf{0}$. This implies that the rate of deformation $\boldsymbol{d}$ is also zero, and the [stress power](@entry_id:182907) term $\boldsymbol{\sigma}:\boldsymbol{d}$ vanishes. Furthermore, the [material derivative](@entry_id:266939) $\frac{D}{Dt} = \frac{\partial}{\partial t} + \mathbf{v} \cdot \nabla$ reduces to the partial time derivative $\frac{\partial}{\partial t}$. The energy balance thus simplifies to the classical **heat conduction equation** [@problem_id:2526135]:
$$
\rho c \frac{\partial T}{\partial t} = \nabla \cdot (k \nabla T) + r
$$
This equation describes how temperature evolves in a rigid, stationary body due to conduction and external heat sources, a cornerstone of classical heat transfer analysis.

**Case 2: Low-Speed Incompressible Flow.** In many fluid dynamics and convection problems, the flow is at low speeds and can be treated as incompressible ($\nabla \cdot \mathbf{v} = 0$). In this regime, the heat generated by viscous forces (the fluid equivalent of [plastic dissipation](@entry_id:201273)) is often negligible compared to the heat transported by the bulk motion of the fluid (advection) and by conduction. The significance of [viscous heating](@entry_id:161646) is quantified by the dimensionless **Eckert number**, $\mathrm{Ec} = U^2 / (c_p \Delta T)$, which compares the kinetic energy of the flow to its thermal energy. When $\mathrm{Ec} \ll 1$, the dissipation term can be safely neglected. The [pressure work](@entry_id:265787) term is also typically negligible in these flows. This leads to the [advection-diffusion equation](@entry_id:144002) commonly used in [convective heat transfer](@entry_id:151349) [@problem_id:2490691].

### Complete Formulation: The Role of Boundary Conditions

A partial differential equation such as the heat equation is only a complete model when supplemented with [initial and boundary conditions](@entry_id:750648). Boundary conditions specify how the body interacts thermally with its surroundings. They arise physically from the [energy balance](@entry_id:150831) applied at the surface of the domain. Consistent with the sign convention for the global balance, the outward flux of heat by conduction, $-\mathbf{n} \cdot \mathbf{q} = k(\mathbf{n} \cdot \nabla T)$, must equal the flux of heat leaving the surface to the environment [@problem_id:2702531]. Common boundary conditions include:

1.  **Prescribed Temperature (Dirichlet Condition):** The temperature $T$ is specified on the boundary.
2.  **Prescribed Heat Flux (Neumann Condition):** The outward conductive heat flux is specified. A thermally insulated surface is a special case where the flux is zero, $k(\mathbf{n} \cdot \nabla T) = 0$.
3.  **Convection and Radiation (Robin Condition):** When a surface at temperature $T$ is exposed to a surrounding fluid at temperature $T_\infty$ and a radiative environment at temperature $T_{sur}$, the heat leaves the surface via convection and radiation. The boundary condition becomes:
    $$
    k(\mathbf{n} \cdot \nabla T) = h(T - T_\infty) + \varepsilon_{rad} \sigma_{SB} (T^4 - T_{sur}^4)
    $$
    Here, $h$ is the [convective heat transfer coefficient](@entry_id:151029), $\varepsilon_{rad}$ is the surface emissivity, and $\sigma_{SB}$ is the Stefan-Boltzmann constant. The left side is the heat conducted to the surface from the interior, and the right side is the total heat leaving the surface to the environment.

By combining the appropriate local [energy equation](@entry_id:156281) with a complete set of boundary and [initial conditions](@entry_id:152863), a well-posed mathematical problem can be formulated to predict the thermomechanical response of a continuum under a wide array of physical conditions.