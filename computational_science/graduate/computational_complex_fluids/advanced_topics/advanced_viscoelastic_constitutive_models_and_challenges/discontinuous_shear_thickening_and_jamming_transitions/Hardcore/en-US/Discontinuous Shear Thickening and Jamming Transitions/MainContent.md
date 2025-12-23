## Introduction
Dense suspensions, such as cornstarch in water, can exhibit a startling transformation, shifting from a fluid-like state to a rigid, solid-like one when subjected to sufficient stress. This dramatic phenomenon, known as discontinuous [shear thickening](@entry_id:136720) (DST), is intimately linked to the concept of jamming—the point at which disordered particles can no longer rearrange and begin to bear a load. While widely observed, the underlying microscopic physics that drives this abrupt transition has been the subject of intense research. This article bridges the gap between the macroscopic rheological curiosity and its fundamental, particle-scale origins.

Across the following chapters, you will gain a comprehensive, graduate-level understanding of this complex behavior. The "Principles and Mechanisms" chapter will deconstruct the phenomenon, establishing the connection between macroscopic constitutive instability and the microscopic theory of stress-activated friction and jamming. Following this, the "Applications and Interdisciplinary Connections" chapter will explore the far-reaching consequences of these principles, from flow instabilities in industrial settings and advanced material design to processes in [geophysics](@entry_id:147342) and biophysics. Finally, the "Hands-On Practices" section will provide computational exercises to solidify your grasp of the core concepts, translating theoretical knowledge into practical skill. We begin by elucidating the fundamental principles and microscopic mechanisms that govern DST and its connection to jamming transitions.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and microscopic mechanisms that govern discontinuous [shear thickening](@entry_id:136720) (DST) and its intimate connection to jamming transitions in dense suspensions. We will move from the macroscopic rheological signatures that define the phenomenon to the particle-scale interactions and collective behaviors that produce them.

### Macroscopic Signatures and Constitutive Instability

The rheological behavior of a fluid is characterized by its flow curve, which describes the relationship between the applied shear stress, $\sigma$, and the resulting shear rate, $\dot{\gamma}$. The [apparent viscosity](@entry_id:260802), $\eta$, is defined as the ratio $\eta = \sigma / \dot{\gamma}$. While simple fluids exhibit a constant viscosity (Newtonian behavior) or a smoothly decreasing viscosity with shear rate ([shear thinning](@entry_id:274107)), complex fluids such as dense suspensions can exhibit [shear thickening](@entry_id:136720), where viscosity increases with shear rate.

Shear thickening phenomena can be broadly classified into two categories. **Continuous [shear thickening](@entry_id:136720) (CST)** is characterized by a smooth, monotonic increase in apparent viscosity, where the derivative $d\eta/d\dot{\gamma}$ is positive but finite over a range of shear rates. In this case, the stress $\sigma(\dot{\gamma})$ is also a strictly [monotonic function](@entry_id:140815), meaning that for every stress there is a unique, stable shear rate.

In contrast, **discontinuous [shear thickening](@entry_id:136720) (DST)** is a more dramatic phenomenon characterized by an abrupt, often multi-order-of-magnitude jump in viscosity at a critical shear rate or shear stress. This discontinuous behavior is the macroscopic manifestation of an underlying constitutive instability . The theoretical steady-state flow curve, $\sigma(\dot{\gamma})$, for a material exhibiting DST is non-monotonic, typically having an "S" shape. To understand the implications, we examine the condition for mechanical stability in a homogeneous [shear flow](@entry_id:266817). Stability requires that an increase in shear rate leads to an increase in shear stress, i.e., $d\sigma/d\dot{\gamma} > 0$. The S-shaped curve, however, possesses a region with a negative slope, $d\sigma/d\dot{\gamma} < 0$. This region is inherently unstable to perturbations and cannot be observed in a steady, homogeneous flow.

Instead of tracing the unstable branch, the system undergoes a discontinuous transition. In a stress-[controlled experiment](@entry_id:144738), as the stress is increased to a critical value $\sigma^\star$, the shear rate abruptly drops from a high value on the lower, fluid-like branch to a low value on the upper, solid-like branch. This corresponds to the sudden jump in viscosity. In a rate-[controlled experiment](@entry_id:144738), the system may exhibit [shear banding](@entry_id:1131556), where regions of low and high shear rate coexist to avoid the unstable regime. This non-monotonicity is the key feature that differentiates DST from CST and points to a profound change in the underlying microstructure of the suspension .

### The Role of Frictional Constraints in Jamming

To understand the origin of this constitutive instability, we must examine the microscopic structure of dense suspensions. DST is fundamentally linked to the concept of **jamming**, the transition from a flowing, fluid-like state to a rigid, solid-like state where the constituent particles can form a load-bearing network. For athermal (non-Brownian) particles, jamming is a purely geometric and mechanical phenomenon, dictated by the number and type of contacts between particles.

The rigidity of a disordered particle packing is governed by a principle of **[isostaticity](@entry_id:194321)**, a constraint-counting argument analogous to Maxwell's criterion for the stability of frames. A system is considered marginally rigid, or isostatic, when the number of independent constraints equals the number of degrees of freedom. In a packing of $N$ particles with a mean [coordination number](@entry_id:143221) (average contacts per particle) of $Z$, the total number of contacts is $NZ/2$.

Let us apply this principle to a packing of rigid spheres in $d$ spatial dimensions .

First, consider the case of **frictionless contacts**. Each contact can only transmit a [normal force](@entry_id:174233) along the line connecting particle centers. This introduces one unknown force magnitude per contact, for a total of $NZ/2$ unknowns. The constraints are the force-balance equations for each of the $N$ particles, providing $Nd$ scalar equations. (Torque balance is trivially satisfied for [central forces](@entry_id:267832)). The isostatic condition, where constraints equal unknowns, is:
$Nd = \frac{NZ_c^{\text{frictionless}}}{2}$, which gives the isostatic coordination number for frictionless packings:
$$
Z_c^{\text{frictionless}} = 2d
$$

Now, consider the case of **frictional contacts**. Each contact can transmit a normal force and $d-1$ tangential force components. This introduces $d$ unknown force components per contact, for a total of $d \cdot (NZ/2)$ unknowns. The constraints now include both force balance ($d$ equations per particle) and torque balance ($d(d-1)/2$ equations per particle). The isostatic condition is:
$N(d + \frac{d(d-1)}{2}) = d \frac{N Z_c^{\text{frictional}}}{2}$, which simplifies to:
$$
Z_c^{\text{frictional}} = d+1
$$

For any physical dimension $d \ge 2$, it is clear that $d+1  2d$. This result is profound: **the presence of friction significantly reduces the number of contacts required to form a rigid, load-bearing network**. A system that is unjammed and fluid in a frictionless state may become jammed and solid if its contacts become frictional . This insight forms the bedrock of the modern theory of DST.

### The Stress-Activated Friction Model

The connection between the macroscopic phenomenon of DST and the microscopic physics of jamming is made through the **stress-activated friction model**. This model posits that particles in a dense suspension can exist in one of two states:
1.  **Lubricated (effectively frictionless)**: At low shear stresses, particles are separated by thin layers of the suspending fluid. The interactions are dominated by [hydrodynamic lubrication](@entry_id:262415) forces, and solid-on-solid contact is prevented.
2.  **Frictional**: As the shear stress increases, the compressive forces between particles become strong enough to overcome any stabilizing repulsive forces and squeeze out the lubricating fluid layer, leading to direct solid-on-solid, [frictional contact](@entry_id:749595).

This stress-induced transition from frictionless to frictional contacts dynamically alters the jamming condition of the suspension. We can define a jamming [volume fraction](@entry_id:756566), $\phi_J$, which depends on the fraction of frictional contacts, $f$. Let $\phi_0$ be the jamming fraction for a purely frictionless system ($f=0$) and $\phi_m$ be the jamming fraction for a fully frictional system ($f=1$). From our analysis of [isostaticity](@entry_id:194321), we know that frictional systems jam more easily, which means they jam at a lower particle density. Therefore, $\phi_m  \phi_0$.

Now consider a suspension prepared at a fixed [volume fraction](@entry_id:756566) $\phi$ that lies in the intermediate range: $\phi_m  \phi  \phi_0$.
- At low stress, $f \approx 0$, and the relevant jamming threshold is $\phi_J \approx \phi_0$. Since $\phi  \phi_0$, the system is below the jamming point and flows with a relatively low viscosity.
- As stress increases, $f$ increases towards 1. The effective jamming threshold, $\phi_J(f)$, decreases from $\phi_0$ towards $\phi_m$. At a critical stress $\sigma^\star$, the jamming threshold drops to the system's actual volume fraction, i.e., $\phi_J(f(\sigma^\star)) = \phi$.
- At this point, the system abruptly jams, causing a discontinuous jump in viscosity. This provides a direct, mechanistic explanation for DST based on a stress-induced [jamming transition](@entry_id:143113)  .

We can formalize this concept by defining a stress-dependent jamming fraction $\phi_J(\sigma)$ that interpolates between the two limits. A common functional form used in computational models is :
$$
\phi_J(\sigma) = \phi_m + \frac{\phi_0 - \phi_m}{1 + (\sigma/\sigma^\star)^n}
$$
Here, $\sigma^\star$ is the characteristic stress for the activation of friction, and $n$ controls the sharpness of the transition. This function correctly captures the limits $\phi_J(0) = \phi_0$ and $\lim_{\sigma\to\infty}\phi_J(\sigma) = \phi_m$. Another valid form uses an exponential decay: $\phi_J(\sigma) = \phi_m + (\phi_0 - \phi_m)\exp[-(\sigma/\sigma^\star)^n]$ . Given such a model, the onset of DST occurs at a stress $\sigma_{\text{on}}$ where $\phi_J(\sigma_{\text{on}}) = \phi$.

### The Force Balance for Contact Activation

The transition from lubricated to [frictional contact](@entry_id:749595) is governed by a [force balance](@entry_id:267186) at the scale of individual particle pairs. Two primary forces are in competition: the [hydrodynamic lubrication](@entry_id:262415) force that pushes particles together, and a short-range repulsive force that keeps them apart.

**Short-range repulsive forces** are essential for stabilizing a suspension against aggregation at rest. These can be electrostatic (due to surface charges creating a double-layer repulsion) or steric (due to adsorbed polymer layers). Such forces can be described by a potential energy function $U(h)$, where $h$ is the surface-to-surface gap. The repulsive force is $F_{\text{rep}}(h) = -dU/dh$. The critical stress for DST, $\sigma^\star$, is related to the force scale required to overcome this repulsive barrier. For instance, for an exponential repulsion $U(h) = U_0 \exp(-\kappa h)$, the characteristic force scale is $F^\star \sim U_0 \kappa$. For a power-law repulsion $U(h) = A h^{-m}$, the force scales as $F^\star \sim mA/\ell_s^{m+1}$, where $\ell_s$ is the stabilization length scale . The activation stress then scales as $\sigma^\star \sim F^\star / a^2$, where $a$ is the particle radius.

The force driving particles together is the **[hydrodynamic lubrication](@entry_id:262415) force**. As two spheres of radius $a$ in a fluid of viscosity $\eta_0$ approach each other with relative speed $V$, the fluid squeezed from the narrow gap $h$ generates a large pressure. In the inertia-less Stokes regime, this lubrication force is given by :
$$
F_{\text{lub}} = \frac{3}{2}\pi \eta_0 a^2 \frac{V}{h}
$$
This force diverges as $h^{-1}$ as the gap closes, seemingly preventing contact. However, this divergence is regularized by the presence of the short-range repulsive force. Frictional contact is initiated when the lubrication force, evaluated at the characteristic range of the repulsion, $h_r$, becomes comparable to the peak repulsive force, $F_{\text{rep}}^\star$ .

This provides a first-principles definition of the onset stress . The relative approach speed in a [shear flow](@entry_id:266817) scales with the shear rate, $V \sim c_n \dot{\gamma} a$, where $c_n$ is a geometric factor. The force balance condition at onset is:
$$
F_{\text{rep}}^\star \approx F_{\text{lub}}(h_r) = \frac{6\pi \eta_0 a^2}{h_r} (c_n \dot{\gamma}^\star a)
$$
(Note: The prefactor $6\pi$ used here is for a sphere approaching a plane, often used for simplicity. The result for two spheres, $\frac{3}{2}\pi$, yields a quantitatively different but qualitatively similar scaling). Recognizing that the macroscopic stress scale is $\sigma^\star \sim \eta_0 \dot{\gamma}^\star$, we can solve for the critical stress:
$$
\sigma^\star \sim \eta_0 \dot{\gamma}^\star \sim \frac{F_{\text{rep}}^\star h_r}{6\pi c_n a^3}
$$
This expression beautifully links the macroscopic critical stress to the microscopic particle properties: the repulsive force barrier ($F_{\text{rep}}^\star$), the stabilization length ($h_r$), particle size ($a$), and [fluid viscosity](@entry_id:261198) ($\eta_0$).

### The Frictional State: Percolation and Rate-Independent Stress

Once the repulsive barrier is overcome and frictional contacts form, the nature of stress transmission in the suspension changes fundamentally. The stress is no longer purely hydrodynamic.

The behavior of frictional contacts is described by the **Coulomb friction law**: the tangential force $F_t$ is limited by the [normal force](@entry_id:174233) $F_n$ via $|F_t| \le \mu F_n$, where $\mu$ is the friction coefficient. When contacts slide, $|F_t| = \mu F_n$. A crucial feature of this law is that the [frictional force](@entry_id:202421) is independent of the sliding velocity.

The power dissipated by a single sliding contact is $P_c = F_t v_t$, where $v_t$ is the sliding velocity. Since $F_t$ is rate-independent, the [power dissipation](@entry_id:264815) is linear in velocity. The contribution of these frictional contacts to the macroscopic shear stress, $\sigma_{\text{fric}}$, can be found from a power balance: $\sigma_{\text{fric}}\dot{\gamma} = n_c P_c$, where $n_c$ is the [number density](@entry_id:268986) of contacts. Since $v_t \propto \dot{\gamma}$, this leads to a remarkable conclusion:
$$
\sigma_{\text{fric}} \propto \mu P
$$
where $P$ is the confining pressure on the suspension that sets the scale of the normal forces $F_n$ . This frictional component of the stress is independent of the shear rate $\dot{\gamma}$. It acts as a constant stress offset, akin to a [yield stress](@entry_id:274513), that is "switched on" when frictional contacts become active. For example, in a system with particle radius $a=10\,\mu\text{m}$, volume fraction $\phi=0.55$, [coordination number](@entry_id:143221) $z=6$, friction coefficient $\mu=0.5$, under a confining pressure $P_c=10^3\,\text{Pa}$, this rate-independent frictional stress can be estimated to be on the order of $\sigma_{\text{fric}} \approx 6.19 \times 10^2\,\text{Pa}$ .

The collective activation of these contacts can be understood through the lens of **[percolation theory](@entry_id:145116)** . As the applied stress $\sigma$ increases, the fraction of frictional contacts $f(\sigma)$ increases. There exists a critical fraction $f_c$ at which these contacts form a system-spanning network. This is the percolation threshold.
- For $f  f_c$, contacts form only finite clusters. The system cannot support a load across its boundaries, and the stress is primarily hydrodynamic ($\sigma \propto \eta_0 \dot{\gamma}$).
- For $f \ge f_c$, a rigid "backbone" of frictional contacts percolates through the sample. This network is capable of bearing a load, and its stress is dictated by the confining pressure, $\sigma \approx \sigma_{\text{fric}} \propto \mu P$.

The transition at the DST onset is thus the transition across the frictional [percolation threshold](@entry_id:146310). The system switches from a state where stress is rate-dependent to one where it is dominated by a large, rate-independent frictional stress. This abrupt change in the stress-bearing mechanism is what produces the discontinuous jump in viscosity.

### Dynamic Effects: Hysteresis

The discussion thus far has focused on steady-state behavior. However, the formation and breakage of frictional contacts are not instantaneous processes. The microstructure of the suspension, represented by the fraction of frictional contacts $f$, has a finite relaxation time, $\tau_f$. This can be modeled with a kinetic equation of the form :
$$
\frac{df}{dt} = \frac{f_{\text{eq}}(\sigma) - f}{\tau_f}
$$
where $f_{\text{eq}}(\sigma)$ is the equilibrium fraction of frictional contacts at a given stress $\sigma$.

This finite relaxation time, combined with the underlying S-shaped flow curve (which represents [multistability](@entry_id:180390) of the microstructure), gives rise to **[rheological hysteresis](@entry_id:1131009)**. When the shear rate is swept upwards, the system may remain on the lower, fluid-like branch beyond the point where the upper branch becomes stable, because it takes time for the frictional network to form. Conversely, when the rate is swept downwards, the system may remain on the upper, high-viscosity branch because it takes time for the frictional contacts to relax.

The result is a [hysteresis loop](@entry_id:160173) in the $\sigma(\dot{\gamma})$ plane, where the stress measured during the upsweep is lower than the stress measured during the downsweep in the region of bistability. This hysteresis is an intrinsic material property arising from the interplay of microstructural [multistability](@entry_id:180390) and finite [relaxation kinetics](@entry_id:191610), and it would be present even in an ideal, inertia-free rheometer . It is a hallmark of DST and a direct consequence of the dynamic nature of the underlying jamming/unjamming transition.