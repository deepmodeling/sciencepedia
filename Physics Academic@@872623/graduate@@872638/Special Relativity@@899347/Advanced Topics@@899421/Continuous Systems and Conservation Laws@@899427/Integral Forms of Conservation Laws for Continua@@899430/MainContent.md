## Introduction
In the study of special relativity, the stress-energy tensor, $T^{\mu\nu}$, provides a complete local description of a continuous medium's energy, momentum, and stress. The fundamental postulate that energy and momentum are conserved locally is elegantly captured by the differential equation $\partial_\mu T^{\mu\nu} = 0$. While this equation governs the dynamics at every point in spacetime, its true power is often realized when applied to finite regions or entire physical systems. This article bridges the gap between local differential laws and global conservation principles by developing and applying the integral forms of conservation laws for continua.

This exploration will provide a robust framework for analyzing the global properties of relativistic systems and their interactions. By integrating the local laws, we can make concrete predictions about total energy, total momentum, and the behavior of composite bodies, moving beyond the infinitesimal to the macroscopic. The following chapters are structured to build this understanding systematically. The **Principles and Mechanisms** chapter will lay the theoretical groundwork, formally deriving the integral [conservation of four-momentum](@entry_id:269410) and defining related quantities like the [center of energy](@entry_id:181397). Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the utility of this framework by applying it to a wide range of physical scenarios, from [relativistic fluid dynamics](@entry_id:198775) and [hydrostatics](@entry_id:273578) to the momentum stored in electromagnetic fields. Finally, the **Hands-On Practices** section will offer an opportunity to solidify these concepts through guided problem-solving, tackling specific challenges that highlight the profound consequences of [relativistic conservation laws](@entry_id:193050).

## Principles and Mechanisms

In the preceding chapter, we introduced the formalism of the [symmetric stress-energy tensor](@entry_id:201187), $T^{\mu\nu}$, as the central object describing the state of a continuous medium in special relativity. The fundamental postulate of local [conservation of energy and momentum](@entry_id:193044) is elegantly expressed by the vanishing four-divergence of this tensor, $\partial_\mu T^{\mu\nu} = 0$, in any region devoid of external force densities. While this differential law provides a complete description of the local dynamics, its implications are often most powerfully harnessed through its integral form. This chapter explores the integral forms of conservation laws, which govern the global properties of physical systems and their interactions.

### The Integral Conservation of Four-Momentum

The [local conservation law](@entry_id:261997), $\partial_\mu T^{\mu\nu} = 0$, can be integrated over a four-dimensional volume of spacetime. By applying Gauss's theorem in four dimensions, this statement is equivalent to the statement that the flux of the conserved quantity through the boundary of that volume is zero. A particularly useful choice of volume is a slice of spacetime between two constant-time [hyperplanes](@entry_id:268044), $t = t_1$ and $t = t_2$. This leads to the conclusion that the total four-momentum of an [isolated system](@entry_id:142067) is constant in time.

The total [four-momentum](@entry_id:161888), $P^\nu$, of a system contained within a spatial volume $V$ at a fixed time $t$ is defined as the integral of the energy-momentum density components over that volume:

$$
P^\nu = \frac{1}{c} \int_V T^{\nu 0} \, d^3x
$$

The components of this [four-vector](@entry_id:160261) have direct physical interpretations. The time-like component, $P^0$, is the total energy of the system divided by the speed of light, $E/c$, where the energy density is $T^{00}$.

$$
P^0 = \frac{E}{c} = \frac{1}{c} \int_V T^{00} \, d^3x
$$

The space-like components, $P^i$, constitute the total three-momentum of the system, $\mathbf{P}$, where the [momentum density](@entry_id:271360) is given by the vector with components $T^{i0}/c$.

$$
P^i = \frac{1}{c} \int_V T^{i0} \, d^3x
$$

For an isolated system, the total four-momentum $P^\nu$ is conserved, meaning $P^\nu(t_1) = P^\nu(t_2)$ for any two times $t_1$ and $t_2$. This principle is the cornerstone for analyzing interactions, particularly collisions, in [relativistic mechanics](@entry_id:263483).

### Application to Inelastic Collisions

Inelastic collisions, where colliding bodies stick together to form a new composite object, provide a dramatic illustration of [mass-energy equivalence](@entry_id:146256). In such collisions, kinetic energy is not conserved but is instead converted into the internal energy (e.g., heat) of the final object, thereby increasing its rest mass. The conservation of total [four-momentum](@entry_id:161888) $P^\nu$ remains the supreme guiding principle.

The rest mass of any system, $M$, is related to the invariant magnitude of its total [four-momentum](@entry_id:161888) by the fundamental relation $M^2 c^2 = P^\mu P_\mu$. Since $P^\mu$ is conserved for an [isolated system](@entry_id:142067), the final rest mass of a composite object formed after a collision can be determined directly from the initial four-momenta of its constituents.

Consider a perfectly inelastic head-on collision between a point-like particle of rest mass $M$ moving at velocity $\mathbf{v}=(v,0,0)$ and a stationary uniform rod of the same rest mass $M$ [@problem_id:389089]. Let the rod lie along the x-axis. The initial total [four-momentum](@entry_id:161888) of the system is the sum of the four-momentum of the moving particle, $P^\mu_{particle} = (\gamma M c, \gamma M v, 0, 0)$, and that of the stationary rod, $P^\mu_{rod} = (M c, 0, 0, 0)$, where $\gamma = (1-v^2/c^2)^{-1/2}$. The total initial [four-momentum](@entry_id:161888) is thus:

$$
P^\mu_{initial} = P^\mu_{particle} + P^\mu_{rod} = ((\gamma+1)Mc, \gamma M v, 0, 0)
$$

After the collision, the particle and rod form a single composite object of final rest mass $M_{final}$ moving with a final velocity $V$. Its [four-momentum](@entry_id:161888) is $P^\mu_{final} = (\gamma_f M_{final} c, \gamma_f M_{final} V, 0, 0)$. By conservation, $P^\mu_{final} = P^\mu_{initial}$. The invariant magnitude of the [four-momentum](@entry_id:161888) is conserved: $P^\mu_{final}P_{f\mu} = P^\mu_{initial}P_{i\mu}$. For the final object, this magnitude is simply $(M_{final}c)^2$. For the initial system, we calculate:

$$
P^\mu_{initial}P_{i\mu} = ((\gamma+1)Mc)^2 - (\gamma Mv)^2 = M^2c^2(\gamma+1)^2 - M^2c^2(\gamma^2 v^2/c^2) = M^2c^2 [(\gamma^2+2\gamma+1) - (\gamma^2-1)] = M^2c^2(2\gamma+2)
$$

Equating the magnitudes, we find the final rest mass:

$$
(M_{final}c)^2 = M^2c^2(2\gamma+2) \implies M_{final} = M\sqrt{2(\gamma+1)}
$$

The total initial rest mass was $M_{initial} = M+M=2M$. The ratio of final to initial rest mass is:

$$
\frac{M_{final}}{M_{initial}} = \frac{M\sqrt{2(\gamma+1)}}{2M} = \sqrt{\frac{\gamma+1}{2}} = \sqrt{\frac{1 + (1-v^2/c^2)^{-1/2}}{2}}
$$

As $\gamma \ge 1$, this ratio is always greater than 1, explicitly showing that the rest mass of the system has increased. The initial kinetic energy of the particle has been partially converted into the final rest mass of the composite object.

This principle can also be applied differentially. Imagine a relativistic sphere of rest mass $M$ moving at speed $v$ that perfectly absorbs stationary dust from a cloud of proper density $\rho_0$ [@problem_id:389121]. In a time $dt$, it sweeps up a dust mass $dm = \rho_0 A v dt$, where $A$ is the sphere's cross-section. This is an infinitesimal [inelastic collision](@entry_id:175807). The change in the sphere's rest mass, $dM$, is not equal to $dm$. By applying energy and momentum conservation to this infinitesimal event, one can show that the rest mass increases according to $dM = \gamma \, dm$. The rate of rest mass increase is therefore:

$$
\frac{dM}{dt} = \gamma \frac{dm}{dt} = \gamma (\rho_0 A v) = \frac{\rho_0 A v}{\sqrt{1-v^2/c^2}}
$$

The factor of $\gamma$ accounts for the kinetic energy of the accreted dust *relative to the sphere's frame* which is converted into the internal energy of the accreting body.

### Flux, Current Density, and Flow of Conserved Quantities

While total [four-momentum conservation](@entry_id:200281) is a global statement about a system, many physical questions concern the flow of quantities across boundaries. This is described by the concepts of **current density** and **flux**. For any conserved quantity with density $\rho$, there is an associated current density $\mathbf{j}$ such that the [local conservation](@entry_id:751393) is expressed by a continuity equation: $\frac{\partial \rho}{\partial t} + \nabla \cdot \mathbf{j} = 0$. The flux, $\Phi$, of the quantity through a surface $S$ is the surface integral of the [current density](@entry_id:190690):

$$
\Phi = \int_S \mathbf{j} \cdot d\mathbf{A}
$$

The total amount of the quantity crossing the surface over a time interval is then the time integral of the flux, $\int \Phi(t) dt$.

A straightforward application is the conservation of particle number [@problem_id:389116]. For a collection of non-interacting particles (dust), we can define a particle [number density](@entry_id:268986) $n(\mathbf{r}, t)$ and a particle number current density $\mathbf{j}(\mathbf{r}, t) = n(\mathbf{r}, t) \mathbf{v}(\mathbf{r}, t)$. The instantaneous flux of particles through a spherical surface of radius $R$ is $\Phi(t) = 4\pi R^2 j_r(R,t)$, where $j_r$ is the radial component of the [current density](@entry_id:190690). By determining the flux as a function of time, we can calculate the total number of particles, $N_{cross}$, that have passed through this surface by a time $t$ by integrating: $N_{cross}(t) = \int_0^t \Phi(t') dt'$.

A more subtle application arises with Lorentz-invariant conserved quantities, such as electric charge. The total charge $Q$ that flows through a surface can be calculated by integrating the charge [current density](@entry_id:190690). However, because total charge is an invariant, it is sometimes much simpler to determine which portion of a charged object will pass through a given surface and calculate the charge of that portion in a convenient reference frame.

For instance, consider a uniformly charged rod of rest length $L_0$ and proper [linear charge density](@entry_id:267995) $\lambda_0$, moving at relativistic speed $v$ along the x-axis. The rod is oriented at an angle $\theta_0$ to the x'-axis in its own rest frame, and it passes through the y-z plane in the [lab frame](@entry_id:181186) [@problem_id:389107]. To find the total charge that passes through a rectangular strip defined by $|y| \le W/2$ on this plane, we can transform to the rod's rest frame. A boost along the x-axis leaves transverse coordinates unchanged, so $y = y'$. The lab-frame strip $|y| \le W/2$ corresponds to the same strip $|y'| \le W/2$ in the rest frame. In this frame, the rod is stationary, described by $y' = s \sin\theta_0$, where $s$ is the [proper length](@entry_id:180234) parameter along the rod, $s \in [-L_0/2, L_0/2]$. The part of the rod that will eventually cross the strip is the part for which $|s \sin\theta_0| \le W/2$, or $|s| \le \frac{W}{2\sin\theta_0}$. The total length of the rod segment that satisfies this is $\Delta s = \min(L_0, W/\sin\theta_0)$. Since the charge $\lambda_0 \Delta s$ is a Lorentz invariant, this is the total charge that passes through the strip in the lab frame.

$$
Q = \lambda_0 \Delta s = \lambda_0 \min\left(L_0, \frac{W}{\sin\theta_0}\right)
$$

This example demonstrates the power of choosing an appropriate [inertial frame](@entry_id:275504) to simplify a problem involving [integral conservation laws](@entry_id:202878).

### Momentum Flux, Pressure, and Stress

The spatial components of the [stress-energy tensor](@entry_id:146544), $T^{ij}$, represent the flux of the $i$-th component of momentum in the $j$-th direction. The diagonal components, such as $T^{xx}$, represent the flux of x-momentum in the x-direction, which is interpreted as **pressure**. More generally, the pressure $P$ on a surface is the rate of momentum transfer normal to that surface, per unit area.

This can be calculated from first principles by considering a beam of particles impinging on a surface [@problem_id:389102]. For a beam of ultra-relativistic particles specularly reflecting from a plate at $x=0$, each particle with momentum $\mathbf{p}$ transfers a momentum of $2 p_x$ to the plate. The number of particles with momentum in $d^3\mathbf{p}$ hitting an area $dA$ in time $dt$ is $f(\mathbf{p}) v_x dA dt d^3\mathbf{p}$, where $f(\mathbf{p})$ is the [number density](@entry_id:268986) distribution in [momentum space](@entry_id:148936) and $v_x = c p_x/p$ is the x-component of velocity. The total pressure is the integrated momentum transfer rate per unit area:

$$
P = \int (2p_x) (v_x f(\mathbf{p})) d^3\mathbf{p} = \int \frac{2c p_x^2}{p} f(\mathbf{p}) d^3\mathbf{p}
$$

Evaluating this integral for a given [distribution function](@entry_id:145626) $f(\mathbf{p})$ yields the macroscopic pressure exerted by the fluid of particles. For an incident distribution $f_{inc}(\mathbf{p}) = A \exp(-|\mathbf{p}|/p_c)$ within a cone of angle $\theta_0$ to the normal, the pressure is found to be $P = 8\pi A c p_c^4 (1 - \cos^3\theta_0)$.

Internal forces within a continuous body are also described by the stress tensor. For a relativistic ring rotating with [angular velocity](@entry_id:192539) $\omega$ at radius $R$, an internal [hoop stress](@entry_id:190931) is required to provide the necessary [centripetal force](@entry_id:166628) and prevent it from flying apart [@problem_id:389144]. The required [centripetal force](@entry_id:166628) on a small element of rest mass $dm_0$ is $dF_c = (\gamma dm_0) \frac{v^2}{R}$. This force is provided by the tension $T$ in the ring. Relating tension to [hoop stress](@entry_id:190931) $\sigma$ (force per proper area), one finds that the required stress is:

$$
\sigma = \rho_0 \gamma^2 v^2 = \frac{\rho_0 \omega^2 R^2}{1 - \omega^2 R^2/c^2}
$$

where $\rho_0$ is the proper mass density and $v = \omega R$. The stress diverges as the tangential speed approaches $c$, indicating that no material can be spun at the speed of light.

The concept that stress itself contributes to the effective mass-energy of a system is a profound consequence of relativity. This can be seen by considering a rod undergoing constant proper acceleration $a$ (Born rigidity). By the [principle of equivalence](@entry_id:157518), this is equivalent to a rod at rest in a uniform gravitational field. The equation for [mechanical equilibrium](@entry_id:148830) must account for the "weight" of the energy associated with the pressure $p$ itself. The effective mass density becomes $\rho_{eff} = \rho_0 + p/c^2$, where $\rho_0$ is the rest-mass density. The [equilibrium equation](@entry_id:749057) is then $\frac{dp}{d\xi} = \rho_{eff} a$, where $\xi$ is the [proper distance](@entry_id:162052) along the rod [@problem_id:389141]. Solving this differential equation reveals an exponential pressure profile within the rod. For a rod being pushed from the rear, with the front end free, the boundary condition is that the pressure at the front end must be zero. Consequently, the pressure at the free front end is precisely zero.

### Energy Flux, Momentum of Heat, and the Center of Energy

The components $cT^{0i}$ of the [stress-energy tensor](@entry_id:146544) represent the **energy flux**, often denoted by the vector $\mathbf{S}$. One of the most striking predictions of relativity is that a flow of energy must also carry momentum. The [momentum density](@entry_id:271360) $\mathbf{g}$ associated with an [energy flux](@entry_id:266056) $\mathbf{S}$ is given by:

$$
\mathbf{g} = \frac{\mathbf{S}}{c^2}
$$

This implies that even in a stationary object, a flow of heat corresponds to a net momentum stored within the object. Consider a stationary rod of length $L$ and area $A$ with its ends held at different temperatures, $T_H > T_C$. A [steady-state heat](@entry_id:163341) flux $q_x$ flows from the hot end to the cold end. According to Fourier's law, $q_x = \kappa (T_H - T_C)/L$, where $\kappa$ is the thermal conductivity [@problem_id:389104]. This [energy flux](@entry_id:266056) gives rise to a uniform momentum density throughout the rod:

$$
g_x = \frac{q_x}{c^2} = \frac{\kappa (T_H - T_C)}{L c^2}
$$

The total momentum stored in the "stationary" rod is the integral of this density over its volume $V = AL$:

$$
P = \int_V g_x \, dV = g_x (AL) = \frac{\kappa A (T_H - T_C)}{c^2}
$$

This "[hidden momentum](@entry_id:266575)" is a purely relativistic effect, carried by the microscopic agents of [heat conduction](@entry_id:143509) (e.g., phonons or electrons).

The concept of center of mass must also be generalized in relativity. Since mass is not a conserved quantity, but energy is, the appropriate generalization is the **[center of energy](@entry_id:181397)**. For a distribution of energy density $T^{00}$, the coordinate of the [center of energy](@entry_id:181397) $\bar{\mathbf{x}}_E$ is defined as the energy-weighted average position:

$$
\bar{\mathbf{x}}_E = \frac{\int \mathbf{x} T^{00} \, d^3x}{\int T^{00} \, d^3x} = \frac{\int \mathbf{x} u(\mathbf{x}) \, d^3x}{E_{tot}}
$$
where $u(\mathbf{x}) = T^{00}$ is the energy density and $E_{tot}$ is the total energy.

We can calculate the [center of energy](@entry_id:181397) for a system with a non-uniform energy distribution, such as the [photon gas](@entry_id:143985) in a stationary cylinder whose ends are held at different temperatures, $T_1$ and $T_2$ [@problem_id:389092]. In a steady state, there is a constant [energy flux](@entry_id:266056), which implies a linear gradient in $T(x)^4$. The energy density of the [photon gas](@entry_id:143985) is $u(x) = a T(x)^4$, which is therefore a linear function of $x$. By first solving for the energy density profile $u(x)$ and then performing the integrals in the definition of $\bar{x}$, one finds the [center of energy](@entry_id:181397) is shifted towards the hotter, more energy-dense region. For a cylinder of length $L$, the [center of energy](@entry_id:181397) is located at:

$$
\bar{x} = L \frac{T_1^4 + 2T_2^4}{3(T_1^4 + T_2^4)}
$$

Finally, the [center of energy](@entry_id:181397) is intimately connected to the **relativistic [angular momentum tensor](@entry_id:200689)**, $M^{\mu\nu}$. This tensor is defined by the integral:

$$
M^{\mu\nu} = \frac{1}{c} \int_{t=\text{const}} (x^\mu T^{\nu 0} - x^\nu T^{\mu 0}) \, d^3x
$$

The components $M^{0i}$ relate the total energy $E$, total momentum $P^i$, and the [center of energy](@entry_id:181397) $X_E^i$ via the important relation $M^{0i} = t P^i - \frac{1}{c^2}X_E^i E$. At time $t=0$, this simplifies to $M^{0i} = - \frac{1}{c^2} E X_E^i$. Thus, calculating the $M^{01}$ component for a system is equivalent to calculating the first moment of its energy distribution [@problem_id:389119]. For a moving rod with a [non-uniform mass distribution](@entry_id:170100), this provides a direct method to probe the location of its energetic center, confirming that the [integral conservation laws](@entry_id:202878) for four-momentum and angular momentum form a closed and consistent framework for relativistic [continuum mechanics](@entry_id:155125).