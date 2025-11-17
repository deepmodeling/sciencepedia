## Introduction
In the quantum realm of [many-body physics](@entry_id:144526), systems of interacting fermions—such as electrons in a metal or atoms in [liquid helium-3](@entry_id:147785)—exhibit behavior far richer than a simple collection of independent particles. While the concept of the quasiparticle successfully describes individual low-energy excitations, it is the interactions between these quasiparticles that give rise to a fascinating class of [emergent phenomena](@entry_id:145138): **collective modes**. These are not single-particle states, but rather coherent, wave-like motions of the entire system, crucial for understanding a material's fundamental properties, from sound propagation to its ultimate stability. This article addresses the knowledge gap between single-particle descriptions and the complex, cooperative dynamics of interacting fermions.

Across three comprehensive chapters, this article provides a graduate-level exploration of these fundamental excitations. The journey begins with **"Principles and Mechanisms"**, where we will formally distinguish collective modes from quasiparticles and dissect the theoretical underpinnings of canonical examples like [zero sound](@entry_id:142772), Landau damping, and [plasmons](@entry_id:146184). We will then transition to **"Applications and Interdisciplinary Connections"**, showcasing how this theoretical framework is applied to understand real-world systems, from the canonical Fermi liquid $^3\text{He}$ to modern [topological materials](@entry_id:142123), and how these modes are probed experimentally. Finally, the **"Hands-On Practices"** chapter offers a series of guided problems to build analytical proficiency and a deeper intuition for the physics of collective modes.

## Principles and Mechanisms

In the preceding chapter, we established the concept of quasiparticles as the low-energy elementary excitations of an interacting Fermi liquid. These quasiparticles, while resembling the bare particles of the non-interacting system, possess renormalized properties such as an effective mass and a finite lifetime due to their interactions with the surrounding medium. However, the physics of interacting fermions is not solely described by the behavior of these individual quasiparticles. The interactions themselves give rise to a rich spectrum of coherent, many-body excitations known as **collective modes**. These modes are not single-particle in nature but rather represent organized, wave-like motions of the entire system, such as propagating distortions of the Fermi surface. This chapter delves into the principles governing the existence and properties of these collective modes, with a primary focus on the canonical example of [zero sound](@entry_id:142772).

### Quasiparticles versus Collective Modes: A Formal Distinction

Before exploring specific collective modes, it is crucial to formalize the distinction between single-[quasiparticle excitations](@entry_id:138475) and collective excitations. This distinction is made precise within the powerful framework of many-body Green's functions.

A **quasiparticle** is formally identified as a pole in the single-particle retarded Green's function, $G^R(\mathbf{k}, \omega)$. Near the Fermi surface, for a stable or quasi-stable Fermi liquid, this function can be approximated as:
$$
G^R(\mathbf{k}, \omega) = \frac{Z_{\mathbf{k}}}{\omega - E^*_{\mathbf{k}} + i\Gamma_{\mathbf{k}}} + G^R_{\text{incoherent}}
$$
Here, $E^*_{\mathbf{k}}$ is the renormalized energy of the quasiparticle, which defines its dispersion and effective mass. The residue of the pole, $Z_{\mathbf{k}}$, known as the **[quasiparticle weight](@entry_id:140100)**, represents the overlap between the physical quasiparticle state and a bare particle state; for an interacting system, it satisfies $0  Z_{\mathbf{k}}  1$. The term $\Gamma_{\mathbf{k}}$ is the [quasiparticle decay](@entry_id:137436) rate, or inverse lifetime, which is proportional to the imaginary part of the [self-energy](@entry_id:145608), $\operatorname{Im}\Sigma^R(\mathbf{k}, \omega)$. A key feature of a Landau Fermi liquid is that this decay rate vanishes quadratically as the quasiparticle approaches the Fermi surface: $\Gamma_{\mathbf{k}} \propto (\omega - \mu)^2 + (v_F^*(|\mathbf{k}|-k_F))^2$, ensuring that quasiparticles at the Fermi surface are sharp, well-defined excitations. The quasiparticle energy $E^*_{\mathbf{k}}$ and weight $Z_{\mathbf{k}}$ are determined by the real part of the [self-energy](@entry_id:145608) and its frequency derivative, respectively [@problem_id:3013236].

In stark contrast, **collective modes** do not appear as poles of the single-particle Green's function. Instead, they manifest as poles in two-particle correlation functions, such as the density-density response function, $\chi^R(\mathbf{q}, \omega)$. A pole in $\chi^R(\mathbf{q}, \omega)$ at a specific $(\omega, \mathbf{q})$ signifies a self-sustaining density oscillation of the system, a coherent superposition of many particle-hole pairs that propagates with the dispersion $\omega(\mathbf{q})$ [@problem_id:3013236, 3013291]. This distinction is fundamental: quasiparticles describe the addition or removal of a single particle-like entity, whereas collective modes describe the emergent, cooperative behavior of the system as a whole.

### The Particle-Hole Continuum and Landau Damping

To understand when a collective mode can exist as a stable, propagating wave, we must first characterize the spectrum of the most basic excitations: particle-hole pairs. At zero temperature, creating an excitation involves promoting a quasiparticle from an occupied state $|\mathbf{k}|  k_F$ to an unoccupied state $|\mathbf{k}+\mathbf{q}| > k_F$. The energy of such a pair is $\omega = E^*_{\mathbf{k}+\mathbf{q}} - E^*_{\mathbf{k}}$. For small energy and momentum transfer, this is approximately $\omega \approx \mathbf{v}_{\mathbf{k}} \cdot \mathbf{q}$, where $\mathbf{v}_{\mathbf{k}}$ is the quasiparticle velocity on the Fermi surface. Since the velocity component along $\mathbf{q}$ is bounded, $|\mathbf{v}_{\mathbf{k}} \cdot \hat{\mathbf{q}}| \le v_F$, the allowed energies for [particle-hole excitations](@entry_id:137289) lie within a specific region of the $(\omega, q)$ plane defined by $|\omega| \le v_F q$. This region is known as the **[particle-hole continuum](@entry_id:191825)**.

A collective mode whose dispersion $\omega(q)$ falls within this continuum can resonantly decay by creating particle-hole pairs. This is a powerful, collisionless decay mechanism known as **Landau damping**. The [phase velocity](@entry_id:154045) of the mode, $v_{ph} = \omega/q$, matches the velocity component of some quasiparticles on the Fermi surface, $v_{ph} = \mathbf{v}_{\mathbf{k}} \cdot \hat{\mathbf{q}}$. These resonant quasiparticles can absorb energy from the wave, causing it to damp out even in the absence of collisions.

Therefore, a necessary condition for a collective mode to be an undamped, propagating excitation is that its dispersion must lie *outside* the [particle-hole continuum](@entry_id:191825) [@problem_id:3024883]. In terms of the dimensionless [phase velocity](@entry_id:154045) $s = \omega/(q v_F)$, this crucial condition is $s > 1$ [@problem_id:3013291, 3024871]. When $s > 1$, the [phase velocity](@entry_id:154045) of the mode is greater than the maximum possible velocity of any quasiparticle along the direction of propagation. No quasiparticle can "keep up" with the wave to absorb energy from it, and Landau damping is kinematically forbidden.

### Zero Sound: A Propagating Distortion of the Fermi Surface

The canonical collective mode of a neutral Fermi liquid is **[zero sound](@entry_id:142772)**. This mode arises in the **collisionless regime**, where the [oscillation frequency](@entry_id:269468) is much higher than the quasiparticle collision rate ($\omega \tau \gg 1$). In this limit, the Fermi surface does not have time to relax to [local equilibrium](@entry_id:156295) via collisions. Instead, a coherent distortion of the Fermi surface itself can propagate through the liquid. This contrasts with **[first sound](@entry_id:144225)**, the familiar pressure wave that propagates in the **hydrodynamic regime** ($\omega \tau \ll 1$), where frequent collisions maintain [local thermodynamic equilibrium](@entry_id:139579) [@problem_id:3013291, 2999031].

#### Derivation of the Zero Sound Dispersion

We can derive the properties of [zero sound](@entry_id:142772) from the linearized Landau kinetic equation in the collisionless limit. Consider a longitudinal density wave in a 3D isotropic system, where for simplicity we assume the interaction is dominated by the constant s-wave component, $f_{\mathbf{p}\mathbf{p}'} = f_0^s = F_0^s / N(0)$, where $N(0)$ is the density of states. A plane-wave disturbance $\delta n_{\mathbf{p}} \propto e^{i(\mathbf{q}\cdot\mathbf{r} - \omega t)}$ confined to the Fermi surface leads to the following [self-consistency equation](@entry_id:155949) for the angular deformation of the Fermi surface [@problem_id:1177355, 2999054]:
$$
1 = F_0^s \int \frac{d\Omega}{4\pi} \frac{\mathbf{q} \cdot \mathbf{v}_{\mathbf{p}}}{\omega - \mathbf{q} \cdot \mathbf{v}_{\mathbf{p}}}
$$
Defining the dimensionless velocity $s = \omega/(q v_F)$ and letting $\mu = \cos\theta = \hat{\mathbf{p}} \cdot \hat{\mathbf{q}}$, the integral can be evaluated, yielding the implicit dispersion relation for [zero sound](@entry_id:142772):
$$
\frac{1}{F_0^s} = \frac{s}{2} \ln\left(\frac{s+1}{s-1}\right) - 1
$$
For an undamped mode, we require a solution with $s > 1$. The right-hand side of this equation is a real, positive function that decreases monotonically from $\infty$ (at $s \to 1^+$) to $0$ (as $s \to \infty$). A solution can therefore only exist if the left-hand side, $1/F_0^s$, is also positive. This leads to the fundamental condition for the existence of longitudinal [zero sound](@entry_id:142772): the interaction must be repulsive, $F_0^s > 0$ [@problem_id:3013291, 3024871]. A repulsive interaction provides the necessary "stiffness" or restoring force against compression for a [density wave](@entry_id:199750) to propagate.

Furthermore, since the function on the right-hand side is monotonically decreasing, a larger (more repulsive) value of $F_0^s$ corresponds to a larger value of $s$. Thus, stronger repulsive interactions increase the speed of [zero sound](@entry_id:142772), pushing it further away from the [particle-hole continuum](@entry_id:191825) [@problem_id:3024871]. In the limit of very strong repulsion ($F_0^s \gg 1$), the velocity approaches the asymptotic value $s \approx \sqrt{F_0^s/3}$ [@problem_id:1177355, 2999054].

#### Dimensionality Effects: Zero Sound in Two Dimensions

The properties of collective modes can be sensitive to the dimensionality of the system. If we repeat the derivation for a 2D isotropic Fermi liquid, the dispersion relation takes a different form [@problem_id:436384, 3024865]:
$$
1 = F_0^s \left( \frac{s}{\sqrt{s^2-1}} - 1 \right)
$$
Unlike the 3D case, this equation can be solved analytically for $s$, yielding:
$$
s(F_0^s) = \frac{F_0^s+1}{\sqrt{2F_0^s+1}}
$$
This result also requires $F_0^s > 0$ for a propagating mode with $s>1$. A key qualitative difference emerges when we consider weak repulsive interactions ($F_0^s \to 0^+$). In 3D, the sound velocity approaches the Fermi velocity exponentially, $s-1 \sim \exp(-2/F_0^s)$, meaning the mode is very tightly "bound" to the edge of the [particle-hole continuum](@entry_id:191825). In 2D, the approach is a much gentler power law, $s-1 \sim (F_0^s)^2$. This shows that collective modes are more readily formed and separated from the continuum in lower dimensions [@problem_id:3024865].

### A Menagerie of Collective Modes

Longitudinal density waves are not the only type of collective motion a Fermi liquid can support. Deformations of the Fermi surface with different angular momentum character ($\ell > 0$) or involving spin degrees of freedom also lead to distinct collective modes, governed by the corresponding Landau parameters $F_\ell^s$ and $F_\ell^a$.

**Transverse Zero Sound**: A distortion of the Fermi surface corresponding to a propagating transverse current (a shear mode) can exist. Its properties are governed primarily by the $\ell=1$ Landau parameter, $F_1^s$. An undamped transverse sound mode requires a sufficiently strong repulsive interaction, emerging when $F_1^s > 6$ in 3D [@problem_id:267748].

**Spin Modes**: The spin-antisymmetric Landau parameters $F_\ell^a$ govern collective modes involving spin.
- **Transverse Spin Waves**: A propagating wave of transverse [spin polarization](@entry_id:164038) can exist, governed by the parameter $F_1^a$. These modes require a repulsive interaction in this channel, with a solution existing for $F_1^a > 3$ in 3D [@problem_id:1112355].
- **Paramagnons**: In a system that is close to a [ferromagnetic instability](@entry_id:157649) (i.e., where the static [spin susceptibility](@entry_id:141223) is large, corresponding to $F_0^a \to -1^+$), there exist heavily damped, long-wavelength [spin fluctuations](@entry_id:141847) known as **paramagnons**. These are not propagating waves but rather relaxational modes with a purely [imaginary frequency](@entry_id:153433), $\omega = -i\Gamma(q)$. The damping rate for these modes can be calculated from the pole of the [spin susceptibility](@entry_id:141223) and is found to be linear in wavevector for small $q$, with a coefficient that depends critically on how close the system is to the instability, i.e., on the value of $1+F_0^a$ [@problem_id:1112360].

### Plasmons in a Charged Fermi Liquid

When the constituent fermions are charged, as in the electron gas in a metal, the long-range Coulomb interaction dramatically alters the nature of the longitudinal [density wave](@entry_id:199750). The total interaction is now a sum of the short-range Landau interaction $f_0^s$ and the long-range Coulomb interaction, which in Fourier space is $V_C(q) = e^2/(\epsilon_0 q^2)$.

The divergence of the Coulomb interaction as $q \to 0$ has a profound effect. It pushes the collective mode frequency up from zero to a finite value even at zero [wavevector](@entry_id:178620). The [zero sound](@entry_id:142772) mode is transformed into the **[plasmon](@entry_id:138021)**. The [dispersion relation](@entry_id:138513) for the plasmon starts at the finite **plasma frequency**, $\omega_p$. The leading correction to the dispersion at small $q$ can be calculated by including both the Coulomb term and the short-range Landau interaction. This reveals how the underlying Fermi liquid physics modifies the [plasmon](@entry_id:138021) behavior [@problem_id:1112380]:
$$
\omega(q) \approx \omega_p + C_2 q^2
$$
The coefficient $C_2$ depends on both the Fermi velocity and the short-range Landau parameter $F_0^s$, explicitly demonstrating that the [plasmon](@entry_id:138021) is the [zero sound](@entry_id:142772) of a charged system. The problem [@problem_id:1112380] provides a specific calculation, showing that $C_2 = \frac{v_F^2 (5F_0^s + 9)}{30 \omega_p}$.

### Instabilities of the Fermi Liquid State

The Landau parameters not only determine the properties of collective modes but also govern the very stability of the Fermi liquid ground state itself. If an interaction in a particular channel becomes sufficiently attractive, the energy cost to deform the Fermi surface can become negative, leading to a spontaneous symmetry-breaking phase transition. This is known as a **Pomeranchuk instability**.

The stability criterion for a deformation with angular momentum $\ell$ is given by:
$$
1 + \frac{F_\ell^s}{2\ell+1}  0 \quad \text{and} \quad 1 + \frac{F_\ell^a}{2\ell+1}  0
$$
When one of these conditions is violated, the spherical Fermi surface becomes unstable. For example, a violation in the $\ell=2$ spin-[symmetric channel](@entry_id:274947) ($F_2^s  -5$) leads to a spontaneous quadrupolar distortion of the Fermi surface, breaking [rotational symmetry](@entry_id:137077) and forming a "nematic" state [@problem_id:1112362]. A violation in the $\ell=0$ channel ($F_0^s  -1$) corresponds to a negative [compressibility](@entry_id:144559), leading to phase separation.

These static instabilities have a dynamic signature in the collective mode spectrum. As a Landau parameter $F_\ell^s$ approaches the critical value $-(2\ell+1)$ from above, the stiffness of the system against that deformation vanishes. This causes the velocity of the corresponding [zero sound](@entry_id:142772) mode to go to zero. The mode is said to **soften**. At the critical point, the frequency $\omega(q)$ vanishes for any small $q$. For $F_\ell^s  -(2\ell+1)$, the squared velocity becomes negative, meaning the frequency becomes purely imaginary. This [imaginary frequency](@entry_id:153433) signifies an exponentially growing mode—the instability itself [@problem_id:2995994].

In one-dimensional systems, the Fermi surface consists of just two points, $\pm k_F$. This leads to perfect "nesting" for a [wavevector](@entry_id:178620) $q=2k_F$, meaning a single [momentum transfer](@entry_id:147714) can connect large regions of the Fermi surface. This geometric feature makes 1D Fermi liquids exceptionally prone to instabilities. The bare susceptibility diverges logarithmically at $q=2k_F$, causing an instability towards a [spin-density wave](@entry_id:139011) (SDW) or [charge-density wave](@entry_id:146282) (CDW) for any infinitesimal attractive interaction [@problem_id:1112370].

### Damping Mechanisms and Crossover Regimes

The lifetime of a collective mode is limited by various damping mechanisms. We have already discussed Landau damping, which is a collisionless process. In addition, there is **[collisional damping](@entry_id:202128)**, which arises from quasiparticle-quasiparticle scattering.

The relative importance of these processes defines two distinct dynamical regimes:
1.  **Collisionless Regime ($\omega \tau \gg 1$):** Zero sound propagates, and its attenuation is weak, arising from the small rate of collisions. The dimensionless damping scales as $\gamma/\omega \sim 1/(\omega \tau)$ [@problem_id:2999031].
2.  **Hydrodynamic Regime ($\omega \tau \ll 1$):** Frequent collisions drive the system to [local equilibrium](@entry_id:156295), and the propagating mode is [first sound](@entry_id:144225) (a pressure wave). Its attenuation is due to viscosity and [thermal conduction](@entry_id:147831), which are themselves proportional to $\tau$. The dimensionless damping scales as $\gamma/\omega \sim \omega \tau$ [@problem_id:2999031].

The [collision time](@entry_id:261390) itself has a strong temperature dependence, $\tau \propto 1/T^2$, due to phase space constraints on scattering near the Fermi surface. This means the damping rate of [zero sound](@entry_id:142772) due to collisions, $\Gamma \sim 1/\tau$, will exhibit a characteristic $T^2$ behavior at low temperatures [@problem_id:1161218]. Even at $T=0$, a subtle quantum damping effect can exist for [zero sound](@entry_id:142772) with $s1$, because the quasiparticles themselves have a finite lifetime from interactions, effectively blurring the sharp edge of the [particle-hole continuum](@entry_id:191825) [@problem_id:1136111].

### Collective Modes in Superfluid Fermi Liquids

The formation of a superconducting or superfluid ground state, characterized by a [pairing gap](@entry_id:160388) $\Delta$, significantly modifies the [excitation spectrum](@entry_id:139562). However, collective modes do not simply disappear. The Anderson-Bogoliubov mode is a sound-like collective mode that persists in the neutral superfluid state. It can be understood as the continuation of the [zero sound](@entry_id:142772)/[first sound](@entry_id:144225) mode from the normal state. Its velocity is determined by the compressibility and effective mass of the underlying normal state, and can thus be expressed in terms of the Landau parameters $F_0^s$ and $F_1^s$. A full derivation [@problem_id:2999018] shows that its squared velocity is given by $c^2 = \frac{p_F^2(1+F_0^s)}{m^2(3+F_1^s)}$, elegantly connecting the physics of the superfluid state back to the [fundamental interactions](@entry_id:749649) of the Fermi liquid from which it emerged.

In summary, the landscape of excitations in an interacting Fermi system is remarkably rich. Alongside the individual quasiparticles, a diverse zoo of collective modes exists, whose properties—be they propagating, damped, or unstable—are dictated by the strength, sign, and angular character of the underlying quasiparticle interactions, as systematically cataloged by the Landau parameters.