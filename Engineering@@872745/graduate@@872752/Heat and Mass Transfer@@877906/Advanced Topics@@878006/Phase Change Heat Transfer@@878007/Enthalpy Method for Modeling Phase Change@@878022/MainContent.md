## Introduction
Modeling phenomena involving a change of phase, such as the melting of ice or the [solidification](@entry_id:156052) of a metal alloy, is a cornerstone of thermal engineering and materials science. A central challenge in these "moving boundary" problems is the complex task of tracking the [solid-liquid interface](@entry_id:201674) and applying the appropriate energy balance, known as the Stefan condition, across it. Explicitly tracking this moving interface can be computationally demanding and difficult to implement for complex geometries. The enthalpy method provides an elegant and powerful alternative, reformulating the problem to implicitly capture the physics of phase change on a fixed computational grid. This article offers a comprehensive exploration of this indispensable technique. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, explaining the [enthalpy formulation](@entry_id:749008) of the [energy equation](@entry_id:156281) and how it unifies sensible and [latent heat](@entry_id:146032). The second chapter, **Applications and Interdisciplinary Connections**, broadens the scope to showcase how the method is adapted to solve complex problems in computational fluid dynamics, [materials processing](@entry_id:203287), and [aerospace engineering](@entry_id:268503). Finally, the **Hands-On Practices** section provides concrete problems to build practical skills in implementing the enthalpy method, bridging the gap between theory and application.

## Principles and Mechanisms

The modeling of [phase change](@entry_id:147324) phenomena, such as melting and solidification, presents a significant challenge due to the presence of a moving interface separating the phases. The **enthalpy method** provides a powerful and elegant framework for tackling these problems by reformulating the [energy conservation equation](@entry_id:748978) in a way that implicitly captures the physics of the interface, thus avoiding the complexities of explicitly tracking its position. This chapter elucidates the fundamental principles and mechanisms underpinning this approach.

### The Enthalpy Formulation of the Energy Equation

The foundation of the enthalpy method is the integral law of energy conservation applied to a fixed control volume $V$ with boundary surface $S$. For a system with no bulk motion and no internal heat sources, the rate of change of total energy within the volume must equal the net rate of heat conducted into it across its boundary. Let $H$ be the **volumetric enthalpy** (energy per unit volume). The energy balance can be written as [@problem_id:2482061]:
$$
\int_V \frac{\partial H}{\partial t} \, dV = - \int_S \mathbf{q} \cdot \mathbf{n} \, dS
$$
where $\mathbf{q}$ is the heat [flux vector](@entry_id:273577) and $\mathbf{n}$ is the outward [unit normal vector](@entry_id:178851). By applying Fourier's law of conduction, $\mathbf{q} = -k \nabla T$, where $k$ is the thermal conductivity and $T$ is the temperature, and then using the [divergence theorem](@entry_id:145271), we arrive at the differential form of the energy equation:
$$
\frac{\partial H}{\partial t} = \nabla \cdot (k \nabla T)
$$
This equation is expressed in a **[conservative form](@entry_id:747710)**, meaning it equates the time rate of change of a conserved quantity (enthalpy) to the divergence of its flux. This mathematical structure is of paramount importance. When thermal properties like conductivity $k$ depend on the phase (and thus on temperature), the expansion of the right-hand side yields $\nabla \cdot (k(T) \nabla T) = k \nabla^2 T + (\nabla k) \cdot (\nabla T)$. A "non-conservative" formulation that omits the second term, $(\nabla k) \cdot (\nabla T)$, would fail to properly conserve energy across the phase interface where $k$ changes abruptly. The [conservative form](@entry_id:747710) ensures that the energy balance is correctly satisfied even in the presence of sharp property variations, making it the correct and robust choice for phase-change modeling [@problem_id:2482064].

The total volumetric enthalpy $H$ is related to the [specific enthalpy](@entry_id:140496) $h$ (energy per unit mass) by $H = \rho h$, where $\rho$ is the density. The governing equation is often written in terms of [specific enthalpy](@entry_id:140496):
$$
\rho \frac{\partial h}{\partial t} = \nabla \cdot (k \nabla T)
$$

### The Enthalpy-Temperature Relationship

The key innovation of the enthalpy method lies in how it defines the relationship between enthalpy and temperature. Instead of treating sensible and [latent heat](@entry_id:146032) separately, they are unified within a single state variable, $h(T)$. The [specific enthalpy](@entry_id:140496) is defined relative to a [reference state](@entry_id:151465) $(T_{\mathrm{ref}}, h_{\mathrm{ref}})$ as the integral of an effective specific heat capacity, $c_{\mathrm{eff}}(T)$:
$$
h(T) = h_{\mathrm{ref}} + \int_{T_{\mathrm{ref}}}^{T} c_{\mathrm{eff}}(\xi) \, d\xi
$$
This effective heat capacity incorporates both the sensible heat capacity of the material, $c_p(T)$, and the latent heat of [phase transformation](@entry_id:146960), $L$. For a pure substance that melts at a sharp temperature $T_m$, the latent heat is absorbed isothermally. This is mathematically represented by including a Dirac delta function in the effective heat capacity:
$$
c_{\mathrm{eff}}(T) = c_p(T) + L \delta(T - T_m)
$$
where $\delta(T-T_m)$ is the Dirac delta centered at the melting temperature.

A more general and practical way to express the enthalpy is through the concept of a **liquid fraction**, $f_{\ell}(T)$, which varies from $0$ in the solid phase to $1$ in the liquid phase. The [specific enthalpy](@entry_id:140496) can then be written as the sum of the accumulated sensible heat and the released [latent heat](@entry_id:146032):
$$
h(T) = \int_{T_{\mathrm{ref}}}^{T} c_p(\xi) \, d\xi + L f_{\ell}(T)
$$
where for simplicity we can set $h_{\mathrm{ref}}=0$ at $T_{\mathrm{ref}}$. The derivative of this expression with respect to temperature recovers the effective heat capacity: $c_{\mathrm{eff}}(T) = c_p(T) + L \frac{df_{\ell}}{dT}$.

An important theoretical point is that the choice of the [reference state](@entry_id:151465) $(T_{\mathrm{ref}}, h_{\mathrm{ref}})$ is arbitrary and does not affect the physical predictions of the model. If we choose a new reference state $(T_{\mathrm{ref}}^{\star}, h_{\mathrm{ref}}^{\star})$, the enthalpy function $h^{\star}(T)$ is simply shifted by a constant value relative to the original $h(T)$. Since the governing [energy equation](@entry_id:156281) involves only time and spatial derivatives of enthalpy, this constant vanishes, leaving the equation for the temperature field unchanged. As boundary conditions are typically prescribed on temperature or heat flux, the resulting temperature solution $T(\mathbf{x}, t)$ is invariant to the choice of enthalpy reference [@problem_id:2482065].

### Implicit Handling of Interfacial Physics

The enthalpy method's most significant advantage is its ability to handle the physics of the moving interface without explicitly tracking its position or enforcing the Stefan condition as a boundary condition. The Stefan condition states that the jump in heat flux across the interface is proportional to the latent heat absorbed or released, $k_s (\nabla T_s) \cdot \mathbf{n} - k_l (\nabla T_l) \cdot \mathbf{n} = \rho L v_n$, where $v_n$ is the normal velocity of the interface.

In the [enthalpy formulation](@entry_id:749008), this physics is embedded within the transient term $\rho \frac{\partial h}{\partial t}$. This term can be expanded using the chain rule as $\rho \frac{\partial h}{\partial t} = \rho \frac{dh}{dT} \frac{\partial T}{\partial t} = \rho c_{\mathrm{eff}}(T) \frac{\partial T}{\partial t}$. The component of this term arising from the [latent heat](@entry_id:146032), $\rho L \frac{df_{\ell}}{dT} \frac{\partial T}{\partial t}$, acts as an extremely powerful volumetric heat source (or sink) that is active only in the region undergoing [phase change](@entry_id:147324). To balance this intense local source/sink, the divergence of the heat flux, $\nabla \cdot (k \nabla T)$, must become correspondingly large. This forces a high curvature in the temperature profile within the phase-change region, which implicitly satisfies the energy balance that the explicit Stefan condition enforces [@problem_id:2482061].

This approach is also consistent with fundamental thermodynamics. According to the **Gibbs phase rule**, for a [pure substance](@entry_id:150298) ($C=1$) with two phases in equilibrium ($P=2$) at a fixed pressure, the number of thermodynamic degrees of freedom is $F = C - P + 2 - (\text{fixed variables}) = 1 - 2 + 2 - 1 = 0$. This means that [phase change](@entry_id:147324) must occur at a single, fixed temperature, $T_m(p)$. The enthalpy method honors this by assuming that any control volume containing both solid and liquid (a "mixed-phase" or "mushy" cell) exists at a single temperature, $T_m$. This assumption of **[local thermodynamic equilibrium](@entry_id:139579) (LTE)** allows the liquid fraction $f_{\ell}$ to vary within the cell from $0$ to $1$ as enthalpy is added or removed, while the temperature remains fixed. The liquid fraction is not an independent degree of freedom in the Gibbsian sense but rather an extensive property determined by the cell's [total enthalpy](@entry_id:197863) [@problem_id:2482037].

### Numerical Implementation and Regularization

In a typical numerical scheme, the conservative energy equation is solved for the enthalpy field $h$. To proceed with the calculation, however, we need to recover the temperature $T$ to evaluate the thermal conductivity $k(T)$ and the heat flux. This requires inverting the $h(T)$ relationship to find $T(h)$. For this inverse mapping to be unique and single-valued, the function $h(T)$ must be strictly monotonic. This physical requirement translates to the condition that the effective heat capacity, $\frac{dh}{dT} = c_{\mathrm{eff}}(T)$, must be strictly positive. Given a strictly increasing $h(T)$, we can construct a unique, piecewise function for $T(h)$. Subsequently, the liquid fraction can also be expressed as a function of enthalpy, $f_{\ell}(h) = f_{\ell}(T(h))$ [@problem_id:2482088].

The presence of the Dirac [delta function](@entry_id:273429) in the definition of $c_{\mathrm{eff}}(T)$ for a pure substance poses a significant numerical challenge. To make the problem computationally tractable, this [delta function](@entry_id:273429) is replaced by a **regularization kernel**, $\delta_{\epsilon}(T-T_m)$. This kernel is a function with a finite peak and a unit integral, which effectively "smears" the [latent heat](@entry_id:146032) release over a small, artificial temperature interval $\Delta T$. This creates a numerical [mushy zone](@entry_id:147943). Common choices for the kernel include a simple box (rectangular) function, a hat (triangular) function, or a smooth Gaussian function [@problem_id:2482075].

The choice of kernel has important numerical implications.
-   A **box kernel** results in a discontinuous apparent heat capacity, which can hinder the convergence of sophisticated nonlinear solvers like Newton's method.
-   A **hat kernel** yields a continuous but not continuously differentiable ($C^0$) heat capacity, which generally improves stability over the box kernel but may still limit the convergence rate of Newton's method.
-   A **Gaussian kernel** provides an infinitely differentiable ($C^{\infty}$) heat capacity. This smoothness is ideal for Newton-based solvers, typically enabling robust and rapid (quadratic) convergence [@problem_id:2482075].

Regardless of the kernel, the regularization creates a region where the apparent heat capacity $c_{\mathrm{eff}}$ is very large ($c_{\mathrm{eff}} \propto L/\Delta T$). This introduces significant **[numerical stiffness](@entry_id:752836)**. In fully coupled solvers, such as those for convective melting using the SIMPLE algorithm, this stiffness necessitates careful treatment. A large change in enthalpy may correspond to a very small change in temperature, but this small temperature change can induce a large change in liquid fraction, which in turn affects flow properties like buoyancy and permeability. To manage this stiff coupling and prevent [numerical oscillations](@entry_id:163720) or divergence, **[under-relaxation](@entry_id:756302)** is essential. Small [under-relaxation](@entry_id:756302) factors are typically applied to the updates of temperature, enthalpy, and liquid fraction to damp the iterations and guide the system toward a converged solution [@problem_id:2482067].

### Dimensionless Analysis and Extended Applications

To understand the interplay of physical mechanisms, it is instructive to nondimensionalize the governing equations. Consider a system with advection at a characteristic velocity $U$ over a length scale $L$. By scaling the energy equation, two critical [dimensionless groups](@entry_id:156314) emerge [@problem_id:2482062].

1.  The **Peclet Number ($Pe$)**: $Pe = \frac{\rho c_p U L}{k}$. This number represents the ratio of [heat transport](@entry_id:199637) by advection to [heat transport](@entry_id:199637) by conduction. High Peclet numbers indicate that convection dominates.

2.  The **Stefan Number ($Ste$)**: $Ste = \frac{c_p \Delta T}{L}$. This number represents the ratio of a characteristic sensible heat to the [latent heat of fusion](@entry_id:144988). A small Stefan number ($Ste \ll 1$) indicates that the energy involved in phase change is much larger than the sensible heat stored in the material, making the accurate handling of latent heat paramount.

The enthalpy method's versatility extends beyond simple conduction problems. In modeling solidification processes where fluid flow is present (e.g., casting or [crystal growth](@entry_id:136770)), the **[enthalpy-porosity method](@entry_id:148711)** is widely used. In this extension, the [mushy zone](@entry_id:147943) is modeled as a porous medium where the solid dendrites form a rigid matrix. The flow of the remaining liquid is progressively impeded as the solid fraction $\phi = 1 - f_{\ell}$ increases. This is achieved by adding a momentum sink term to the Navier-Stokes equations that is a function of the solid fraction. This sink term acts as a drag force, becoming infinitely large as the material becomes fully solid ($\phi \to 1$), thereby extinguishing the velocity. A common model for this sink coefficient, $A(\phi)$, derived from Darcy's law and the Carman-Kozeny relation for permeability, is [@problem_id:2482048]:
$$
\mathbf{S}_m = -A(\phi)\mathbf{u} = -\left( \frac{\mu C_{KC} \phi^{2}}{d^{2} (1 - \phi)^{3}} \right) \mathbf{u}
$$
where $\mu$ is the liquid viscosity, $d$ is a microstructural length scale, and $C_{KC}$ is the Kozeny constant. This allows a single set of momentum equations to be solved across the entire liquid-mushy-solid domain.

### Limitations and Advanced Hybrid Methods

Despite its power and convenience, the pure enthalpy method has limitations that stem directly from its core feature: the smearing of the sharp physical interface into a numerical [mushy zone](@entry_id:147943). This approximation can lead to significant inaccuracies under certain conditions [@problem_id:2482056]:

-   **Interfacial Curvature Effects**: In many physical systems, the equilibrium melting temperature depends on the local interface curvature $\kappa$ (the Gibbs-Thomson effect). A smeared interface has no well-defined curvature, making it impossible for a pure enthalpy method to capture this crucial physical mechanism.

-   **Large Property Jumps**: When material properties like thermal conductivity differ greatly between phases ($k_s \neq k_l$), the enthalpy method's use of an averaged effective conductivity in the [mushy zone](@entry_id:147943) introduces errors in the computed heat flux, which in turn affects the predicted interface speed.

-   **Low Stefan Number Regimes**: When [latent heat](@entry_id:146032) dominates ($Ste \ll 1$), the interface dynamics are highly sensitive to the precise location of energy release. Smearing this release over several grid cells can introduce significant errors in the interface position.

To overcome these limitations, **hybrid methods** have been developed. A prominent example is the **enthalpy-[level-set method](@entry_id:165633)**, which combines the robust [energy conservation](@entry_id:146975) of the [enthalpy formulation](@entry_id:749008) with the geometric precision of a sharp-interface method like the [level-set](@entry_id:751248) technique. In this approach, a [level-set](@entry_id:751248) function is used to explicitly track a sharp interface, allowing for accurate computation of geometric quantities like curvature and normal vectors. This geometric information is then used to apply more physically accurate conditions—such as the Gibbs-Thomson effect or a sharp Stefan condition—within the broader enthalpy framework, leading to improved accuracy for a given grid resolution, especially in problems where the limitations of the pure enthalpy method are most pronounced [@problem_id:2482056].