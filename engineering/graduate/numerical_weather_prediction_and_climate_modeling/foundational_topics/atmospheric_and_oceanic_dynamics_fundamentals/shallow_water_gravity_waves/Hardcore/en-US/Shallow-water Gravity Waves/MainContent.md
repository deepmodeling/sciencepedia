## Introduction
Shallow-water gravity waves represent a fundamental concept in geophysical fluid dynamics, offering a simplified yet powerful lens through which to understand the large-scale motions of atmospheres and oceans. Their study is crucial for fields ranging from numerical weather prediction to [coastal engineering](@entry_id:189157). This article addresses the need for a comprehensive understanding of these waves, bridging the gap between abstract theory and practical application. By exploring the core principles, real-world implications, and practical problem-solving techniques, readers will gain a robust grasp of this essential topic. The following chapters will first dissect the principles and mechanisms of shallow-water dynamics, including the hydrostatic approximation and the process of geostrophic adjustment. We will then explore the wide-ranging applications of this theory in various scientific and engineering disciplines. Finally, a series of hands-on practices will provide an opportunity to apply these concepts to solve concrete problems in fluid dynamics.

## Principles and Mechanisms

The shallow-water system is a cornerstone of [geophysical fluid dynamics](@entry_id:150356), providing a simplified yet powerful framework for understanding a wide range of phenomena in both the atmosphere and oceans. Its utility in [numerical weather prediction](@entry_id:191656) (NWP) and climate modeling stems from its ability to capture the essential dynamics of large-scale, barotropic motions, including the propagation of gravity waves and the adjustment of flow to a [balanced state](@entry_id:1121319). This chapter elucidates the core principles and mechanisms governing shallow-water gravity waves, from the system's fundamental assumptions to its canonical wave solutions and its response to imbalances.

### The Shallow-Water Approximation: A Hydrostatic, Barotropic Model

The shallow-water equations are most rigorously understood as a reduction of the more comprehensive primitive equations, which govern rotating, [stratified fluid](@entry_id:201059) motion. The reduction is achieved by projecting the full three-dimensional dynamics onto a single vertical mode: the external, or **barotropic mode**. This process inherently involves a set of strong physical and mathematical assumptions that define the scope and validity of the shallow-water model.

A central pillar of this model is the **[hydrostatic approximation](@entry_id:1126281)**. For many large-scale geophysical flows, the horizontal length scale, $L$, is vastly greater than the vertical length scale, or fluid depth, $H$. This small aspect ratio, $\delta = H/L \ll 1$, has profound consequences for the vertical [momentum balance](@entry_id:1128118). Consider the vertical momentum equation for an incompressible fluid:

$$
\frac{Dw}{Dt} = -\frac{1}{\rho_0}\frac{\partial p}{\partial z} - g
$$

Here, $w$ is the vertical velocity, $p$ is pressure, $\rho_0$ is a constant reference density, and $g$ is the [acceleration due to gravity](@entry_id:173411). The material derivative on the left-hand side, $\frac{Dw}{Dt} = \frac{\partial w}{\partial t} + u\frac{\partial w}{\partial x} + v\frac{\partial w}{\partial y} + w\frac{\partial w}{\partial z}$, represents the total vertical acceleration of a fluid parcel. Through a careful [order-of-magnitude analysis](@entry_id:184866), we can assess the importance of this acceleration. The continuity equation for an [incompressible fluid](@entry_id:262924) implies that the scale of vertical velocity, $W$, is related to the horizontal velocity scale, $U$, by $W \sim (H/L)U = \delta U$. For gravity waves, the relevant horizontal velocity scale is related to the [wave speed](@entry_id:186208), $U \sim \sqrt{gH}$. Comparing the magnitude of the vertical acceleration terms to gravity, we find that each term is of order $O(\delta^2 \mathrm{Fr}^2)$ relative to $g$, where $\mathrm{Fr} = U/\sqrt{gH}$ is the Froude number. For the geophysical phenomena of interest, $\mathrm{Fr}$ is of order one. Since $\delta \ll 1$, the vertical acceleration is asymptotically small compared to the pressure gradient and gravitational terms .

Neglecting the vertical acceleration, the [vertical momentum equation](@entry_id:1133792) simplifies to the **hydrostatic balance**:

$$
\frac{\partial p}{\partial z} = -\rho_0 g
$$

Integrating this from an arbitrary depth $z$ to the free surface at $z=\eta(x,y,t)$ yields the [pressure distribution](@entry_id:275409):

$$
p(x,y,z,t) = p_a + \rho_0 g (\eta(x,y,t) - z)
$$

where $p_a$ is the [atmospheric pressure](@entry_id:147632) at the surface. A key consequence is that the horizontal pressure gradient, $\nabla_H p = \rho_0 g \nabla_H \eta$, is independent of depth. This means that the horizontal pressure force is uniform throughout the water column.

This depth-independent forcing is consistent with the primary assumption of the barotropic mode: the horizontal velocity, $\boldsymbol{u}$, is also independent of depth. This simplification removes several degrees of freedom from the full [primitive equations](@entry_id:1130162). Specifically, the shallow-water system filters out all dynamics related to vertical shear ($\partial_z \boldsymbol{u}$), internal buoyancy variations, and the associated baroclinic pressure gradients. It retains only the depth-averaged velocity and the total fluid thickness, effectively modeling the fluid as a single, homogeneous layer . This reduction is dynamically self-consistent under specific conditions: the flow must be predominantly barotropic (e.g., in an unstratified fluid), the [hydrostatic approximation](@entry_id:1126281) must hold, and there should be no significant processes (like diabatic heating) that could excite the truncated [baroclinic modes](@entry_id:1121346).

Under these conditions, the governing equations for a rotating shallow-water layer of thickness $h(x,y,t)$ and depth-averaged velocity $\boldsymbol{u}(x,y,t)$ over a bottom topography $b(x,y)$ can be written in a **[conservative form](@entry_id:747710)**, which is particularly advantageous for numerical methods that conserve mass and momentum. The state vector of conserved quantities is $\mathbf{q} = \begin{pmatrix} h & hu & hv \end{pmatrix}^T$. The system is expressed as $\partial_t \mathbf{q} + \nabla \cdot \mathbf{F}(\mathbf{q}) = \mathbf{S}(\mathbf{q})$, where the flux vectors and source vector are:

$$
\mathbf{F}_x(\mathbf{q}) = \begin{pmatrix} hu \\ hu^2 + \frac{1}{2}gh^2 \\ huv \end{pmatrix}, \quad 
\mathbf{F}_y(\mathbf{q}) = \begin{pmatrix} hv \\ huv \\ hv^2 + \frac{1}{2}gh^2 \end{pmatrix}, \quad 
\mathbf{S}(\mathbf{q}) = \begin{pmatrix} 0 \\ -gh\frac{\partial b}{\partial x} + fhv \\ -gh\frac{\partial b}{\partial y} - fhu \end{pmatrix}
$$

Here, the terms $hu$ and $hv$ represent mass fluxes. The momentum fluxes include advection of momentum (e.g., $hu^2$) and the depth-integrated pressure force, $\frac{1}{2}gh^2$. The source terms account for forces that are not expressed as a flux divergence: the pressure [gradient force](@entry_id:166847) due to bottom topography and the Coriolis force, which depends on the constant Coriolis parameter $f$ .

### Plane Waves: Dispersion and the Role of Non-Hydrostatic Effects

The most [fundamental solutions](@entry_id:184782) to the [shallow-water equations](@entry_id:754726) are plane waves. Let us first consider an unbounded, non-rotating fluid of constant mean depth $H$. The linearized equations for small perturbations about a state of rest are:
$$
\frac{\partial u}{\partial t} = -g \frac{\partial \eta}{\partial x}, \quad \frac{\partial v}{\partial t} = -g \frac{\partial \eta}{\partial y}, \quad \frac{\partial \eta}{\partial t} + H\left(\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y}\right) = 0
$$
Seeking plane-wave solutions of the form $\exp[i(kx + ly - \omega t)]$ leads directly to the **dispersion relation** for shallow-water gravity waves:
$$
\omega^2 = gH(k^2+l^2) = gH K^2
$$
where $K = \sqrt{k^2+l^2}$ is the total horizontal wavenumber. The angular frequency $\omega$ is linearly proportional to the wavenumber $K$. This has a profound consequence. The **[phase velocity](@entry_id:154045)**, the speed at which crests and troughs propagate, is $c_p = \omega/K = \sqrt{gH}$. The **[group velocity](@entry_id:147686)**, the speed at which the energy of a [wave packet](@entry_id:144436) propagates, is $c_g = \partial \omega / \partial K = \sqrt{gH}$.

Because the phase and group velocities are equal and independent of the wavenumber, shallow-water gravity waves are **non-dispersive**. This means that a localized [wave packet](@entry_id:144436), which is a superposition of many different wavenumbers, will propagate at the speed $c = \sqrt{gH}$ without changing its shape .

This non-dispersive character is a direct result of the [hydrostatic approximation](@entry_id:1126281). To understand this, we must briefly consider the full problem of [surface gravity waves](@entry_id:1132678) without assuming hydrostatic balance. When vertical accelerations are retained, the dynamics are governed by Laplace's equation, and the boundary conditions at the free surface and the bottom impose a vertical structure on the flow that depends on the horizontal wavenumber. This leads to the full dispersion relation for surface gravity waves over a finite depth $H$:
$$
\omega^2 = gK \tanh(KH)
$$
Here, the phase speed $c_p = \sqrt{(g/K)\tanh(KH)}$ clearly depends on the wavenumber $K$, so these waves are dispersive. The mathematical source of this dispersion is the non-hydrostatic [vertical mode structure](@entry_id:1133791), encapsulated in the $\tanh(KH)$ term . In the "shallow-water" limit, defined by long wavelengths ($K \to 0$ or $KH \ll 1$), we can use the approximation $\tanh(KH) \approx KH$. The full dispersion relation then simplifies to $\omega^2 \approx gK(KH) = gH K^2$, recovering the non-dispersive shallow-water result. The hydrostatic, depth-averaged shallow-water model is therefore the long-wave limit of the more general theory of [surface gravity waves](@entry_id:1132678).

### The Influence of Rotation, Boundaries, and Stratification

In geophysical contexts, two factors are rarely absent: planetary rotation and density stratification. Their inclusion dramatically enriches the dynamics of gravity waves.

#### Inertia-Gravity Waves

On a rotating planet, the Coriolis force deflects moving parcels. On a plane with constant Coriolis parameter $f$, the dispersion relation for shallow-[water waves](@entry_id:186869) becomes:
$$
\omega^2 = f^2 + gH K^2 = f^2 + c^2 K^2
$$
These are known as **inertia-gravity waves**. The dispersion relation reveals a low-frequency cutoff: no free waves can exist with a frequency $|\omega|  |f|$. The Coriolis force also alters the wave structure. For a non-rotating gravity wave, fluid parcels oscillate back and forth parallel to the direction of wave propagation. For an inertia-gravity wave, the Coriolis force causes parcels to move in [elliptical orbits](@entry_id:160366). The velocity vector can be decomposed into a component parallel to the [wave vector](@entry_id:272479) $\boldsymbol{k}$, which is in-phase with the surface displacement $\eta$, and a component perpendicular to $\boldsymbol{k}$, which is in phase quadrature ($90^\circ$ phase shift) and arises from the Coriolis acceleration . This [rotational motion](@entry_id:172639) also alters the energy balance. For non-rotating waves, kinetic and potential energy are in equipartition. For inertia-gravity waves, the kinetic energy exceeds the potential energy, with the ratio given by $\overline{\mathrm{KE}}/\overline{\mathrm{PE}} = 1 + 2f^2/(c^2 K^2)$. In the high-frequency limit ($\omega \gg f$), the rotational effects become negligible, and the wave properties approach those of a non-rotating gravity wave.

#### Coastal Kelvin Waves

Boundaries, such as coastlines, provide a [waveguide](@entry_id:266568) for a special class of trapped waves. The most fundamental of these is the **coastal Kelvin wave**. This wave mode is remarkable because it achieves an exact geostrophic balance in the cross-shore direction. Consider a coast at $y=0$ in the Northern Hemisphere ($f0$). A Kelvin wave propagating in the positive $x$-direction has a cross-shore velocity $v$ that is identically zero everywhere. This automatically satisfies the no-normal-flow boundary condition at the coast. With $v \equiv 0$, the cross-shore momentum balance becomes a simple geostrophic balance between the Coriolis force acting on the alongshore flow and the cross-shore pressure gradient:
$$
fu = -g \frac{\partial \eta}{\partial y}
$$
The alongshore momentum balance and continuity equation combine to show that the wave propagates at the non-rotating shallow-water speed, $c = \omega/k = \sqrt{gH}$. Substituting this into the geostrophic balance equation leads to a differential equation for the cross-shore structure of the wave: $\partial_y \eta = -(f/c)\eta$. The solution is an exponential decay away from the coast:
$$
\eta(x,y,t) = \eta_0 \exp(-y/L_R) \exp[i(kx-\omega t)]
$$
where $L_R = c/f$ is the **Rossby radius of deformation**, a fundamental length scale in [geophysical fluid dynamics](@entry_id:150356) representing the distance over which geostrophic adjustment occurs . The wave is trapped within a coastal band of width $L_R$. It is crucial to note that this solution requires a non-zero surface displacement at the coast, $\eta_0$. Imposing an additional, physically unwarranted boundary condition like $\eta(0,t)=0$ would over-constrain the system and force the [trivial solution](@entry_id:155162) $\eta \equiv 0$. The proper derivation of the Kelvin wave relies only on the no-normal-flow condition and a [boundedness](@entry_id:746948) condition far from the coast .

#### Baroclinic Modes

Real oceans and atmospheres are stratified. A simple model for stratification is a two-layer fluid, with a less dense upper layer ($\rho_1$, depth $H_1$) over a denser lower layer ($\rho_2$, depth $H_2$). Such a system supports two types of gravity waves.

1.  The **barotropic (external) mode**: This involves in-phase motion of the free surface and the internal interface. The entire fluid column moves nearly in unison, and the [wave speed](@entry_id:186208) is very fast, determined by the total depth: $c_{\text{ext}} \approx \sqrt{g(H_1+H_2)}$. This is the mode analogous to the waves in the single-layer shallow-water system.

2.  The **baroclinic (internal) mode**: This involves out-of-phase motion, where the interface displacement is much larger than the surface displacement. There is significant [vertical shear](@entry_id:1133795) between the layers. The restoring force is provided not by the full gravity $g$, but by the **reduced gravity** $g' = g(\rho_2-\rho_1)/\rho_2$, which reflects the small [density contrast](@entry_id:157948). The wave speed is consequently much slower: $c_{\text{int}} = \sqrt{g' H_1 H_2 / (H_1+H_2)}$ .

For typical oceanic parameters, $c_{\text{ext}}$ can be $\sim 200 \text{ m/s}$, while $c_{\text{int}}$ may only be $\sim 2 \text{ m/s}$. The shallow-water equations studied in this chapter are a model for the fast, external barotropic mode.

### Synthesis: Geostrophic Adjustment

Shallow-water gravity waves are not just an academic curiosity; they are the primary mechanism by which a rotating fluid adjusts from an unbalanced state to a geostrophically balanced state. This process is known as **[geostrophic adjustment](@entry_id:191286)**.

Imagine an initial state at rest, where a localized mass perturbation (a "hump" of water) is suddenly introduced. This state is unbalanced: there is a pressure [gradient force](@entry_id:166847) directed outward from the hump, but no flow for the Coriolis force to act upon. The fluid immediately begins to accelerate, generating inertia-gravity waves that radiate energy away from the initial disturbance. The wavefront of this radiation expands at a speed of approximately $c = \sqrt{gH}$. This process of wave radiation cannot continue indefinitely. As the flow develops, the Coriolis force begins to act, deflecting the motion and spinning up a vortex. The adjustment process unfolds on a characteristic timescale set by the inertial period, $O(f^{-1})$.

Eventually, the system settles into a new, steady, geostrophically [balanced state](@entry_id:1121319), where the pressure gradient of the remaining [mass distribution](@entry_id:158451) is balanced by the Coriolis force of a resulting vortical flow. The properties of this final balanced remnant are determined by the conservation of **potential vorticity (PV)**. The key insight is that the partitioning of initial energy between the radiated waves and the final balanced state depends critically on the horizontal scale of the initial disturbance, $L$, compared to the Rossby radius of deformation, $L_R = c/f$ .

-   If the initial disturbance is on a **small scale** ($L \ll L_R$), the fluid has ample time to adjust and radiate waves before rotation becomes effective. Most of the initial potential energy is lost to gravity waves, leaving behind a weak, small-amplitude balanced vortex.
-   If the initial disturbance is on a **large scale** ($L \gg L_R$), the initial state is already close to geostrophic balance. Rotational constraints are dominant, and the fluid struggles to generate divergent flow. Very little energy is radiated away, and the final balanced state retains most of the initial energy, with its structure closely resembling the initial perturbation.

This scale-dependent nature of [geostrophic adjustment](@entry_id:191286) is a fundamental principle in NWP and [climate dynamics](@entry_id:192646). It dictates how the atmosphere and ocean respond to forcing and absorb observational data, determining which information is retained in the slow, balanced evolution of the climate system and which is radiated away as fast, transient gravity waves  .