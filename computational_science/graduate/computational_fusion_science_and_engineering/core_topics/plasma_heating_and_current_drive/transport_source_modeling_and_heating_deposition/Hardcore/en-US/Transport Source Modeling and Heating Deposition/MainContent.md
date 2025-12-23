## Introduction
Predictive modeling of plasma behavior is a cornerstone of modern fusion science, essential for designing and operating future reactors like ITER. At the heart of these predictive models are transport equations, which describe the evolution of plasma density, temperature, and rotation profiles. However, these equations are incomplete without an accurate accounting of the sources and sinks that add or remove particles, energy, and momentum. The central challenge, which this article addresses, is how to translate complex, spatially localized physical processes—such as heating from a particle beam or radiation from impurities—into mathematically consistent terms that can drive a transport simulation.

This article provides a comprehensive overview of the theory and application of source modeling in transport analysis. Across three chapters, you will gain a graduate-level understanding of this critical topic.
*   The first chapter, **Principles and Mechanisms**, lays the mathematical groundwork, explaining how 3D physical sources are averaged onto magnetic flux surfaces and introduces the fundamental models for particle, energy, and momentum [sources and sinks](@entry_id:263105).
*   The second chapter, **Applications and Interdisciplinary Connections**, explores how these source models are utilized in integrated simulations, revealing the tight feedback loops between heating, transport, and stability, and connecting plasma physics to fields like [atomic physics](@entry_id:140823) and nuclear engineering.
*   Finally, **Hands-On Practices** will guide you through computational exercises to solidify your understanding, from calculating power deposition to implementing and verifying source terms in a transport code.

## Principles and Mechanisms

The evolution of plasma profiles, such as density, temperature, and momentum, is governed by a set of transport equations. These equations describe how quantities are redistributed in space by transport processes and how their overall inventory is changed by local sources and sinks. In this chapter, we will delve into the fundamental principles and physical mechanisms that constitute the [source and sink](@entry_id:265703) terms in transport equations, which are essential for [predictive modeling](@entry_id:166398) of fusion plasmas.

### The Role of Sources and Sinks in Macroscopic Transport

A general conservation law for a plasma quantity, represented by its density $U(\mathbf{x}, t)$, can be written in the form of a continuity equation:
$$
\frac{\partial U}{\partial t} + \nabla \cdot \mathbf{F} = S - L
$$
Here, $\mathbf{F}$ is the flux of the quantity $U$, representing its transport through space, while $S$ and $L$ are the volumetric [source and sink](@entry_id:265703) rates, respectively. In a magnetically confined plasma, transport is highly anisotropic, with rapid motion along magnetic field lines and much slower transport across them. This feature motivates a description based on **[magnetic flux surfaces](@entry_id:751623)**, which are surfaces of constant magnetic flux.

To reduce the dimensionality of the transport problem from three dimensions (3D) to one dimension (1D) in the radial coordinate, we employ the technique of **[flux-surface averaging](@entry_id:1125140) (FSA)**. For a scalar quantity $f(\mathbf{x}, t)$, its flux-surface average on a surface labeled by a coordinate $\psi$ is defined as:
$$
\langle f \rangle(\psi,t) \equiv \frac{1}{V'(\psi)} \oint_{\psi=\text{const}} \frac{f}{|\nabla \psi|}\mathrm{d}S
$$
where $V'(\psi) \equiv \oint_{\psi=\text{const}} \frac{1}{|\nabla \psi|} \mathrm{d}S$ is the derivative of the volume enclosed by the flux surface with respect to $\psi$.

Let us apply this to the particle continuity equation, where $U$ is the particle density $n$, $\mathbf{F}$ is the particle flux $\mathbf{\Gamma}$, $S$ is the particle source rate $S_n$, and $L$ is the particle loss rate $L_n$. For stationary [magnetic flux surfaces](@entry_id:751623), the FSA of the time derivative term simplifies to the time derivative of the FSA: $\langle \partial_t n \rangle = \partial_t \langle n \rangle$. The most critical term is the FSA of the flux divergence, $\langle \nabla \cdot \mathbf{\Gamma} \rangle$. By applying the divergence theorem to an infinitesimally thin shell between two flux surfaces, $\psi$ and $\psi+\mathrm{d}\psi$, one can show that this term represents the net flux of particles out of the surface. The result is a fundamental relation in transport theory:
$$
\langle \nabla \cdot \mathbf{\Gamma} \rangle = \frac{1}{V'(\psi)} \frac{\partial}{\partial \psi} \left[ V'(\psi) \langle \mathbf{\Gamma} \cdot \nabla \psi \rangle \right]
$$
This term quantifies the change in the net [particle flux](@entry_id:753207), $V' \langle \mathbf{\Gamma} \cdot \nabla \psi \rangle$, as one moves from one flux surface to another. Putting these pieces together, we obtain the 1D radial [particle transport equation](@entry_id:1129402):
$$
\frac{\partial \langle n \rangle}{\partial t} + \frac{1}{V'(\psi)} \frac{\partial}{\partial \psi} \left( V'(\psi) \langle \mathbf{\Gamma} \cdot \nabla \psi \rangle \right) = \langle S_n \rangle - \langle L_n \rangle
$$
This equation shows that the evolution of the radially-dependent, flux-surface-averaged [density profile](@entry_id:194142) $\langle n \rangle(\psi, t)$ is driven by the divergence of the radial flux and, crucially for this chapter, by the flux-surface-averaged particle sources $\langle S_n \rangle$ and sinks $\langle L_n \rangle$. Similar equations govern the evolution of energy (temperature) and momentum (rotation), all featuring averaged source and sink terms that drive the system. 

### Modeling Spatially Distributed Sources

The physical processes that give rise to sources of particles, energy, and momentum are often highly localized in 3D space. For instance, [neutral beam injection](@entry_id:204293) (NBI) is typically aimed along a specific tangential path, and radio-frequency (RF) wave heating can be focused on particular regions. Transport codes, however, often require these sources to be provided in a lower-dimensional form, either as 1D flux-surface averages or as 2D functions of radius and poloidal angle. This requires a systematic procedure of averaging.

A first step is often to average over the toroidal angle $\phi$, as many tokamaks are designed to be nearly axisymmetric. The **toroidal average** of a quantity $Q(\psi, \theta, \phi)$ is defined as:
$$
\langle Q \rangle_\phi(\psi,\theta) \equiv \frac{1}{2\pi}\int_0^{2\pi} Q(\psi,\theta,\phi)\mathrm{d}\phi
$$
Consider an NBI heating source that is sharply peaked at a toroidal angle $\phi_0$, modeled by a Gaussian function: $S(\psi, \theta, \phi) = S_0(\psi) h(\theta) \exp[-\frac{(\phi-\phi_0)^2}{2\sigma_\phi^2}]$. The peak local power density is $S_0(\psi) h(\theta)$. When we compute the toroidal average, assuming the width $\sigma_\phi$ is small, the integral of the Gaussian is approximately $\sqrt{2\pi}\sigma_\phi$. The averaged source becomes $\langle S \rangle_\phi(\psi, \theta) = S_0(\psi) h(\theta) \frac{\sqrt{2\pi}\sigma_\phi}{2\pi}$. The ratio of the averaged amplitude to the original peak amplitude is $\frac{\sigma_\phi}{\sqrt{2\pi}}$. For a narrow beam with $\sigma_\phi \ll 1$, this represents a significant reduction in amplitude. The toroidal averaging process effectively "smears" the localized hotspot over the entire torus. While this procedure conserves the total power deposited on a given poloidal cross-section, it completely loses information about the intense, localized toroidal peaking, which could be important for localized material interactions or nonlinear effects. 

After toroidal averaging, the source may still have a complex poloidal dependence, described by the function $h(\theta)$. To obtain a 1D source profile for a transport code, one must perform a flux-surface average. Let's consider a practical example of calculating the FSA of a poloidally-localized energy source, $S_E(\psi, \theta) = S_0(\psi) \exp(\kappa \cos\theta)$, in a simplified large-aspect-ratio tokamak where the magnetic field strength varies as $B(\psi, \theta) = B_0 \frac{R_0}{R_0 + r(\psi)\cos\theta}$. Using an appropriate definition of the FSA, the calculation involves integrals of the form $\int_0^{2\pi} \exp(\kappa \cos\theta) \cos(n\theta) \mathrm{d}\theta$, which are related to the modified Bessel functions of the first kind, $I_n(\kappa)$. The final result for the FSA source is:
$$
\langle S_E \rangle(\psi) = S_0(\psi) \left( I_0(\kappa) + \frac{r(\psi)}{R_0} I_1(\kappa) \right)
$$
This calculation demonstrates how the geometric factors (like the $1/R$ dependence of $B$) and the source anisotropy (parameterized by $\kappa$) combine to determine the net source strength on a flux surface. 

In many advanced simulations, retaining the poloidal variation of sources is critical. A common and efficient strategy is to expand the 2D toroidally-averaged source in a **poloidal Fourier series** on each flux surface:
$$
\langle S \rangle_\phi(\psi,\theta) = \sum_{m=0}^{M} S_m(\psi) \cos(m\theta) + \sum_{m=1}^{M} S'_m(\psi) \sin(m\theta)
$$
By keeping a modest number of modes (small $M$), this representation captures the essential poloidal asymmetries without the full cost of a 3D grid. The mode coefficients $S_m(\psi)$ are typically pre-calculated using more detailed, higher-fidelity codes that model the specific heating physics. 

### Particle Sources and Sinks

The primary source of particles in a fusion plasma is the ionization of neutral atoms. These neutrals may be introduced externally via **gas puffing** or **[pellet injection](@entry_id:753314)**, or they may be recycled from the plasma-facing walls. The process of ionization is a sink for the neutral population but a source for the plasma ion and electron populations.

A simplified but illustrative model can be constructed for [neutral transport](@entry_id:1128682) in a 1D slab geometry. Let's consider monoenergetic neutrals with speed $v_0$ traveling in the $+x$ direction from a wall at $x=0$. These neutrals are lost to the plasma via ionization at a rate $\nu_{\mathrm{ion}}(x)$. They can also be sourced volumetrically at a rate $S_n(x)$. The steady-state continuity equation for the neutral density $n_n(x)$ is a first-order ODE:
$$
v_0 \frac{d n_n}{dx} = S_n(x) - \nu_{\mathrm{ion}}(x) n_n(x)
$$
This equation balances the convective transport of neutrals with volumetric sources and sinks. Given a boundary condition for the incoming neutral density at the wall, $n_n(0)$, and specific forms for $S_n(x)$ and $\nu_{\mathrm{ion}}(x)$, this equation can be solved to find the neutral density profile $n_n(x)$.

The rate of ionization per unit volume is $\nu_{\mathrm{ion}}(x) n_n(x)$. This term acts as the dominant particle source for the plasma, $S_p(x) = \nu_{\mathrm{ion}}(x) n_n(x)$. Furthermore, each ionization event adds the kinetic energy of the neutral atom, $E_n = \frac{1}{2} m_n v_0^2$, to the plasma. This constitutes a volumetric energy source, with power density $q(x) = E_n S_p(x)$. Thus, the modeling of neutral particles is intrinsically linked to the calculation of both particle and energy sources for the plasma. 

### Energy Sources and Heating Mechanisms

To achieve fusion conditions, plasmas must be heated to extreme temperatures. The total power per unit volume transferred from electromagnetic fields to the plasma particles is given by the term $\mathbf{J} \cdot \mathbf{E}$, where $\mathbf{E}$ is the electric field and $\mathbf{J}$ is the current density.

The **Poynting theorem** provides the fundamental statement of [electromagnetic energy conservation](@entry_id:748884). In a stationary, time-averaged state, it relates the total power absorbed within a volume $V$ to the net power flowing across its boundary $\partial V$:
$$
\int_V \langle \mathbf{J} \cdot \mathbf{E} \rangle \mathrm{d}V = - \oint_{\partial V} \langle \mathbf{S} \rangle \cdot \mathbf{n}_{\mathrm{out}} \mathrm{d}A = \oint_{\partial V} \langle \mathbf{S} \rangle \cdot \mathbf{n}_{\mathrm{in}} \mathrm{d}A
$$
where $\langle \mathbf{S} \rangle$ is the time-averaged Poynting vector. This means the total [absorbed power](@entry_id:265908) is equal to the net inward flux of [electromagnetic energy](@entry_id:264720). For a system with an injection port delivering power $P_{\mathrm{in}}$ and an exit port radiating power $P_{\mathrm{rad}}$, the total power absorbed by the plasma is simply $P_{\mathrm{abs}} = P_{\mathrm{in}} - P_{\mathrm{rad}}$. 

In a complex plasma environment with multiple heating systems, it is crucial to accurately decompose the total [absorbed power](@entry_id:265908) $\int \langle \mathbf{J} \cdot \mathbf{E} \rangle \mathrm{d}V$ into contributions from different physical mechanisms. This can be achieved through a combination of frequency and species separation. We can decompose the total fields and currents into low-frequency (quasi-static or inductive) components (subscript $L$) and high-frequency (RF wave) components (subscript $H$): $\mathbf{E} = \mathbf{E}_L + \mathbf{E}_H$ and $\mathbf{J} = \mathbf{J}_L + \mathbf{J}_H$. Assuming a clear [separation of timescales](@entry_id:191220), the time-average of cross-terms like $\langle \mathbf{E}_L \cdot \mathbf{J}_H \rangle$ vanishes. The total [absorbed power](@entry_id:265908) then separates cleanly:
$$
\langle P_{\mathrm{abs}} \rangle = \int_V \mathbf{E}_L \cdot \mathbf{J}_L \, \mathrm{d}V + \int_V \langle \mathbf{E}_H \cdot \mathbf{J}_H \rangle \, \mathrm{d}V
$$
The high-frequency term is, by definition, the **RF heating power**, $P_{RF}$. The low-frequency term can be further decomposed by separating the current into contributions from different particle species: thermal electrons ($\mathbf{J}_{e,L}$), thermal ions, and fast beam ions ($\mathbf{J}_{b,L}$). This allows us to identify:
*   **Ohmic Heating**: The power transferred to thermal electrons, $P_{OH} = \int \mathbf{E}_L \cdot \mathbf{J}_{e,L} \mathrm{d}V$. This is the heating from the inductively driven [plasma current](@entry_id:182365).
*   **Beam-Field Interaction**: The power transferred to the beam ions, $P_{beam,field} = \int \mathbf{E}_L \cdot \mathbf{J}_{b,L} \mathrm{d}V$.
This rigorous decomposition is essential for validating heating schemes in comprehensive numerical simulations. 

#### Modeling Wave Heating (RF)

Auxiliary heating using [radio-frequency waves](@entry_id:195520) is a primary tool for fusion experiments. In many cases, the wavelength is short compared to the scale length of [plasma parameter](@entry_id:195285) variations, allowing the use of the **geometric optics (GO)** or **ray-tracing** approximation. In this limit, [wave energy](@entry_id:164626) is assumed to propagate along well-defined rays.

The power $P(\ell)$ carried by a ray decreases as it travels along its path length $\ell$ due to absorption by the plasma. By considering energy conservation in a differential segment of the ray, we can derive the governing equation for power attenuation:
$$
\frac{dP}{d\ell} = -\alpha(\ell) P(\ell)
$$
where $\alpha(\ell)$ is the local [absorption coefficient](@entry_id:156541), determined by the microscopic [wave-particle interaction](@entry_id:195662) physics. This equation integrates to the familiar exponential [absorption law](@entry_id:166563), also known as the Beer-Lambert law:
$$
P(L) = P(0) \exp\left( - \int_{0}^{L} \alpha(\ell') d\ell' \right)
$$
The quantity $A = P(L)/P(0)$ is the **single-pass [attenuation factor](@entry_id:1121239)**, and the integral in the exponent is the **[optical depth](@entry_id:159017)**. By calculating the [absorption coefficient](@entry_id:156541) $\alpha$ from plasma parameters (e.g., density and temperature) along the ray path, we can determine the power deposition profile. For example, for a ray traversing a plasma with a parabolic density profile $n_e(r) = n_0(1-r^2/a^2)$ and an [absorption coefficient](@entry_id:156541) proportional to density, $\alpha(r) \propto n_e(r)$, the total [optical depth](@entry_id:159017) can be calculated analytically, yielding the total power absorbed in a single pass. 

The geometric optics approximation breaks down when the wavelength is no longer short compared to the plasma scale lengths. This occurs prominently near a **cutoff**, a location where the wave's refractive index $n(x)$ goes to zero. Near a cutoff at $x_c$, the local wavenumber $k(x) = \omega n(x)/c$ also goes to zero. The validity criterion for the WKB approximation, $|(dk/dx)/k^2| \ll 1$, is severely violated as $k \to 0$. In this region, a full-wave solution is required.

By linearizing the squared wavenumber near the cutoff, $k^2(x) \approx \alpha(x-x_c)$, the wave equation $\frac{d^2E}{dx^2} + k^2(x)E = 0$ can be transformed into the canonical **Airy's equation**. The physically correct solution, which must decay in the evanescent region ($x  x_c$) and oscillate in the propagating region ($x > x_c$), is given by the Airy function $Ai$. By matching the asymptotic form of the Airy function in the propagating region to the WKB solution form, we find that a constant phase shift of $\pi/4$ must be added to the WKB [phase integral](@entry_id:1129582). This **connection formula** is critical for ray-tracing codes to correctly handle wave propagation across cutoffs and reflections, ensuring accurate calculation of the deposition profile. 

### Momentum Sources

In addition to providing particles and energy, external systems can also inject momentum, driving [plasma rotation](@entry_id:753506). Toroidal rotation is particularly important as its shear can suppress turbulent transport. A primary source of toroidal momentum in tokamaks is tangential **Neutral Beam Injection (NBI)**.

The torque density, or the source of toroidal momentum, can be derived from the conservation of **[canonical toroidal angular momentum](@entry_id:747109)**, $p_\phi$. For a particle with mass $m$ and charge $q$, this is given by $p_\phi = m R v_\phi + q \psi$, where $R$ is the major radius, $v_\phi$ is the toroidal velocity, and $\psi = R A_\phi$ is the [poloidal magnetic flux](@entry_id:1129914). For a [neutral beam](@entry_id:752451) atom, $q=0$, so its momentum is purely mechanical. Upon ionization at a major radius $R$, the newly created ion acquires a charge $q_i$ and its [canonical momentum](@entry_id:155151) becomes $p_{\phi,ion} = m_b R v_{\phi,b} + q_i \psi$.

While $p_\phi$ is conserved for charged particles in an axisymmetric system, the quantity of interest for [fluid rotation](@entry_id:273789) is the mechanical angular momentum, $L_\phi = m R v_\phi$. The source of mechanical angular [momentum density](@entry_id:271360) (the torque density, $S_\tau$) is not simply the source of $p_\phi$. A careful derivation shows that the contribution from the magnetic term $q_i \psi$ in the canonical momentum source is exactly cancelled by the change in the plasma's [electromagnetic momentum](@entry_id:268129) due to the addition of new charge carriers. The result is remarkably simple: the torque density is precisely the source rate of mechanical angular momentum from the newborn ions.
$$
S_\tau(r) = \int m_b R v_\phi S_{\mathrm{ion}}(E, \mu, r) \mathrm{d}E \mathrm{d}\mu
$$
where $S_{\mathrm{ion}}$ is the ionization rate density in terms of the [guiding-center](@entry_id:200181) invariants of energy $E$ and magnetic moment $\mu$. For a simplified beam model where all ions are born with the same velocity, this integral reduces to the product of the mechanical angular momentum per ion and the total ionization rate, providing a direct way to calculate the torque deposition profile from the beam's characteristics and the plasma's ionization properties. 

### Energy Sinks: Radiative Losses

While heating systems act as energy sources, there are also powerful energy sinks that must be overcome. Apart from energy transport out of the plasma, the most significant energy sink in the core of a hot plasma is often [electromagnetic radiation](@entry_id:152916). Bremsstrahlung radiation (from electron-ion collisions) is unavoidable, but **line radiation** from partially ionized impurity atoms can be a dominant loss channel.

Electrons colliding with impurity ions can excite them to higher energy levels. These ions then de-excite by emitting photons, which typically escape the plasma, carrying energy away. This process acts as a net energy sink for the electron population. The volumetric power radiated by a specific impurity species with density $n_z$ can be modeled as:
$$
p_{\mathrm{rad}} = n_e n_z L_z(T_e)
$$
where $n_e$ and $T_e$ are the electron density and temperature, respectively. The function $L_z(T_e)$, known as the **[radiative cooling](@entry_id:754014) function**, encapsulates the complex atomic physics of the impurity species and is strongly dependent on temperature.

To understand the impact of impurities, we can use a simple, core-averaged (0D) steady-state power balance model. In steady state, the total heating power, $P_{\mathrm{heat}}$, must be balanced by the total losses, which include conductive transport losses ($P_{\mathrm{cond}}$) and radiative losses ($P_{\mathrm{rad}}$).
$$
P_{\mathrm{heat}} = P_{\mathrm{cond}} + P_{\mathrm{rad}}
$$
Conductive losses are typically modeled as $P_{\mathrm{cond}} = W_e / \tau_E$, where $W_e$ is the total electron thermal energy and $\tau_E$ is the [energy confinement time](@entry_id:161117). The radiative losses are $P_{\mathrm{rad}} = p_{\mathrm{rad}} \times V$, where $V$ is the plasma volume. For a given heating power and a specific model for the cooling function (e.g., $L_z \propto T_e^{-1/2}$ for [line radiation](@entry_id:751334) in a certain regime), this algebraic equation can be solved for the steady-state electron temperature $T_e$. Calculations show that even small fractions of impurities (e.g., $f_z = n_z/n_e$ of a few tenths of a percent) can lead to significant [radiation power](@entry_id:267187). Doubling the impurity fraction can cause a noticeable drop in the achievable core temperature for a fixed heating power, underscoring the critical importance of impurity control for achieving high-performance fusion plasmas. 