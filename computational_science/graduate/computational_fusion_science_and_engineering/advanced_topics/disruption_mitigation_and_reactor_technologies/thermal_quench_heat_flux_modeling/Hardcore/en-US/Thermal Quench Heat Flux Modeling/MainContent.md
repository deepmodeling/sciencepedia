## Introduction
The quest for fusion energy hinges on confining a plasma hotter than the sun's core within a magnetic vessel. A major disruption, the sudden loss of this confinement, poses one of the most significant threats to the structural integrity of a [tokamak reactor](@entry_id:756041). The most violent phase of a disruption is the **thermal quench (TQ)**, a sub-millisecond event where the plasma's immense thermal energy is catastrophically dumped onto the machine's inner walls, creating heat fluxes capable of melting or vaporizing any known material. Accurately predicting and mitigating these heat loads is therefore not just an academic challenge but a critical engineering necessity for the future of fusion power.

This article provides a comprehensive overview of the physics and modeling of [thermal quench](@entry_id:755893) heat fluxes. To build a robust understanding, we will explore this complex phenomenon across three distinct chapters. First, in **"Principles and Mechanisms,"** we will dissect the fundamental physics, from the large-scale magnetohydrodynamic (MHD) instabilities that trigger the quench to the microscopic [transport processes](@entry_id:177992) that govern [energy flow](@entry_id:142770) along chaotic magnetic fields. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these models are applied to design resilient [plasma-facing components](@entry_id:1129762), interpret experimental data, and develop active mitigation strategies, while also revealing surprising connections to other scientific fields. Finally, **"Hands-On Practices"** will offer a chance to engage directly with the core concepts through guided problems, solidifying your grasp of this critical subject in fusion science. We begin by examining the foundational principles that set the stage for this rapid and powerful event.

## Principles and Mechanisms

The catastrophic loss of thermal energy during a [tokamak disruption](@entry_id:756033), known as the **thermal quench (TQ)**, represents one of the most significant challenges to the design and operation of future fusion reactors. Understanding and predicting the intense heat fluxes delivered to plasma-facing components (PFCs) during these events is a primary focus of fusion science and engineering. This chapter delves into the fundamental principles and mechanisms governing heat transport during a [thermal quench](@entry_id:755893), from the large-scale magnetohydrodynamic (MHD) triggers to the microscopic kinetic processes that dictate the flow of energy.

### The Anatomy of a Disruption: Thermal and Current Quench Dynamics

A major disruption is not a single, instantaneous event but a complex sequence of phases, each characterized by distinct physical processes and timescales. The two most prominent phases are the thermal quench and the subsequent **current quench (CQ)**. A clear understanding of their distinction and causal relationship is paramount.

The thermal quench is the rapid collapse of the plasma's thermal energy content. It is initiated by the growth of large-scale MHD instabilities which destroy the nested magnetic flux surfaces that normally provide thermal insulation. This destruction, or **stochastization**, of the magnetic field topology suddenly connects the hot plasma core to the much colder material walls via chaotic field lines. The plasma's immense thermal energy is then rapidly dumped onto the PFCs.

Following this rapid cooling, the plasma, now cold but still carrying a large toroidal current, enters the current quench phase. The [electrical resistivity](@entry_id:143840) of a plasma is strongly dependent on its temperature, scaling approximately as the **Spitzer resistivity**, $\eta \propto T_e^{-3/2}$. The precipitous drop in electron temperature $T_e$ during the [thermal quench](@entry_id:755893) causes the [plasma resistivity](@entry_id:196902) to increase by several orders of magnitude. This highly resistive plasma can no longer sustain the large current, which then decays on a resistive diffusion timescale.

The key distinction lies in the timescales. The [thermal quench](@entry_id:755893) is governed by transport processes, primarily the near-free-streaming of electrons along stochastic magnetic field lines. The current quench is governed by resistive [magnetic diffusion](@entry_id:187718). A quantitative comparison illustrates the dramatic difference . Consider a tokamak with a pre-quench electron temperature of $T_{e0} = 1\,\mathrm{keV}$ and a post-quench temperature of $T_{e1} = 20\,\mathrm{eV}$. The TQ timescale, $\tau_{\mathrm{TQ}}$, can be estimated as the time for electrons to traverse a stochastic connection length, $L_c$, at their thermal speed, $v_{te}$. For a typical $L_c = 2000\,\mathrm{m}$, the initial thermal speed is $v_{te}(T_{e0}) \approx 1.9 \times 10^7\,\mathrm{m/s}$, yielding a quench time of $\tau_{\mathrm{TQ}} \sim L_c / v_{te}(T_{e0}) \approx 0.1\,\mathrm{ms}$. The CQ timescale, $\tau_{\mathrm{CQ}}$, is the [resistive time](@entry_id:754275) $\tau_R \sim \mu_0 a^2 / \eta(T_{e1})$, where $a$ is the plasma minor radius. The resistivity increases by a factor of $(T_{e0}/T_{e1})^{3/2} = (1000/20)^{3/2} \approx 354$. This leads to a $\tau_{\mathrm{CQ}}$ on the order of $1\,\mathrm{ms}$.

This [timescale separation](@entry_id:149780), $\tau_{\mathrm{TQ}} \ll \tau_{\mathrm{CQ}}$, establishes the canonical disruption sequence:
1.  Pre-disruptive MHD precursor growth.
2.  Magnetic field stochastization.
3.  **Thermal Quench**: A rapid (sub-millisecond) loss of thermal energy, leading to extreme heat fluxes on PFCs.
4.  **Current Quench**: A slower (millisecond-scale) decay of the [plasma current](@entry_id:182365).

The primary engineering threat from the TQ is the immense power density deposited on the walls. The total pre-quench thermal energy, $W_{\mathrm{th}}$, which can be several megajoules, is deposited over the small area $A_w$ that the stochastic field lines connect to, and within the very short time $\tau_{\mathrm{TQ}}$. The average heat flux, $q \sim W_{\mathrm{th}}/(A_w \tau_{\mathrm{TQ}})$, can readily reach gigawatts per square meter, posing a severe threat of material melting and evaporation .

### The Origin of Rapid Heat Loss: Magnetic Field Stochastization

In a stable tokamak plasma, particles and heat are well-confined, diffusing slowly *across* magnetic flux surfaces. Parallel transport, while intrinsically much faster, is restricted to flow *within* a flux surface, which closes on itself. The thermal quench is triggered when this ordered structure is destroyed.

The growth and interaction of multiple MHD instabilities, such as [tearing modes](@entry_id:194294), can lead to the overlap of their associated magnetic islands. When this overlap is sufficiently widespread, the magnetic field lines no longer lie on well-defined surfaces. Instead, they wander chaotically in the radial direction as they traverse the torus. This state is known as a **stochastic magnetic field**.

The radial wandering of a field line can be modeled as a random walk. The fundamental equation describing this process is $dr/ds = B_r(s)/B$, where $r$ is the [radial coordinate](@entry_id:165186), $s$ is the distance along the field line, $B$ is the magnitude of the main field, and $B_r(s)$ is the small, spatially fluctuating radial component of the magnetic field. For a [stochastic process](@entry_id:159502), the mean-square radial displacement $\langle (\Delta r)^2 \rangle$ grows with distance $s$. In the limit of large distances, this growth becomes diffusive, characterized by the **[field-line diffusion](@entry_id:749315) coefficient**, $D_{FL}$:
$$ D_{FL} \equiv \lim_{s \to \infty} \frac{\langle (\Delta r)^2 \rangle}{2s} $$
Using [quasi-linear theory](@entry_id:182724), one can relate $D_{FL}$ to the statistical properties of the [magnetic fluctuations](@entry_id:1127582). The result, first derived by Rechester and Rosenbluth, is fundamental to [stochastic transport](@entry_id:182026):
$$ D_{FL} \approx L_{\parallel} \left( \frac{\delta B}{B} \right)^2 $$
Here, $\delta B / B$ is the normalized amplitude of the magnetic perturbations, and $L_{\parallel}$ is the parallel correlation length of these fluctuations . This coefficient quantifies the geometric "brokenness" of the [magnetic topology](@entry_id:751637) and is a crucial input for TQ models. It demonstrates that even small magnetic fluctuations ($\delta B/B \ll 1$) can lead to significant radial transport when combined with the extremely fast transport of energy parallel to the magnetic field.

### Modeling Parallel Energy Transport: The Fluid Approach

With the magnetic confinement broken, the primary mechanism for energy loss is transport along the now-stochastic field lines. In many TQ scenarios, this process can be approximated using a one-dimensional fluid model describing the evolution of plasma temperature and density along a representative magnetic field line, parameterized by a coordinate $s$.

The cornerstone of this approach is the **parallel energy balance equation**, which arises from local energy conservation . Assuming a quasi-neutral plasma with equal electron and ion temperatures ($T_e \approx T_i \equiv T$), the rate of change of the internal energy density, $U = 3nT$ (where $k_B$ is absorbed into the temperature unit), is balanced by the divergence of the [parallel heat flux](@entry_id:753124), $q_\parallel$, and volumetric sources and sinks:
$$ \frac{\partial (3nT)}{\partial t} = -\frac{\partial q_\parallel}{\partial s} - P_{rad} + S $$
Here, $P_{rad}$ represents the volumetric power loss due to radiation (e.g., from impurities), and $S$ represents any volumetric heating sources (such as Ohmic heating).

The physics of transport is contained within the expression for the [parallel heat flux](@entry_id:753124), $q_\parallel$. In a collisional plasma, heat is conducted down a temperature gradient according to Fourier's law:
$$ q_\parallel = -\kappa_\parallel \frac{\partial T}{\partial s} $$
Substituting this into the energy balance gives the standard reaction-diffusion equation for temperature:
$$ \frac{\partial (3nT)}{\partial t} = \frac{\partial}{\partial s} \left( \kappa_\parallel \frac{\partial T}{\partial s} \right) - P_{rad} + S $$
The dominant transport coefficient in this equation is the **parallel electron thermal conductivity**, $\kappa_\parallel$. Due to their small mass and high mobility, electrons are far more effective at transporting heat than ions. For a collisional plasma, this coefficient was first calculated by Spitzer and Härm from kinetic theory. A simplified kinetic argument reveals its essential scaling . The conductivity can be estimated as $\kappa_\parallel \propto n_e v_{te}^2 \tau_e$, where $v_{te} \propto T_e^{1/2}$ is the electron thermal speed and $\tau_e$ is the electron [collision time](@entry_id:261390). For Coulomb collisions, $\tau_e \propto T_e^{3/2}/(n_e Z_{\mathrm{eff}})$, where $Z_{\mathrm{eff}}$ is the effective ion charge. Combining these scalings gives the celebrated **Spitzer-Härm conductivity**:
$$ \kappa_\parallel \propto \frac{T_e^{5/2}}{Z_{\mathrm{eff}}} $$
Notably, the [density dependence](@entry_id:203727) cancels out. The strong temperature dependence, $\kappa_\parallel \propto T_e^{5/2}$, signifies that hotter plasmas are extremely effective at conducting heat along magnetic field lines. The inverse dependence on $Z_{\mathrm{eff}}$ indicates that higher impurity content increases collisionality and impedes parallel heat flow. This fluid model, equipped with the Spitzer-Härm conductivity, forms the classical basis for TQ simulations.

### Breakdown of Local Transport: Kinetic Effects and Advanced Closures

The classical fluid model described above is built on the assumption of a **local**, **collisional** plasma. This assumption holds only when the [electron mean free path](@entry_id:185806), $\lambda_{mfp}$, is much shorter than the characteristic length scale of the temperature gradient, $L_T = |T/\nabla_\parallel T|$. When this condition is not met, the fluid model fails, and a more sophisticated, kinetic description of heat transport is required.

#### Collisionality Regimes and the Knudsen Number

The validity of local transport models is quantified by the **Knudsen number**, $K_n$, defined as the ratio of the mean free path to the gradient scale length:
$$ K_n = \frac{\lambda_{mfp}}{L_T} $$
An alternative, and equivalent, parameter is the **collisionality**, $\nu^* \equiv L_T / \lambda_{mfp} = 1/K_n$. This parameter represents the number of collisions an electron experiences while traversing the distance $L_T$. These dimensionless numbers define the transport regime :

*   **Collisional Regime ($K_n \ll 1$ or $\nu^* \gg 1$)**: Electrons collide many times before crossing the temperature gradient. Their motion is a random walk, and the heat flux at a point depends only on the local gradient. The local Spitzer-Härm model is valid.

*   **Collisionless Regime ($K_n \gg 1$ or $\nu^* \ll 1$)**: Electrons travel distances much larger than $L_T$ without colliding. The heat flux is no longer determined by the local gradient but by the global temperature profile. This is often called **free-streaming** or **ballistic** transport.

During a thermal quench, the plasma can transition between these regimes. Initially, the plasma is very hot, making the mean free path $\lambda_{mfp} \propto T_e^2/n_e$ very long. At the same time, the TQ itself creates extremely steep gradients, making $L_T$ very short. Both effects conspire to increase the Knudsen number, often pushing it into the range $K_n \gtrsim 1$ . In this situation, the Spitzer-Härm formula, which would predict an unphysically large heat flux, becomes invalid. This failure necessitates the use of kinetic models or advanced fluid [closures](@entry_id:747387) that can capture non-local and flux-limiting effects.

#### Flux-Limited Models: The Saturated Heat Flux

When $K_n$ becomes large, the heat flux can no longer be proportional to the temperature gradient. The simplest correction to the fluid model is to impose an upper bound on the heat flux, known as the **saturated heat flux**, $q_{sat}$.

A naive estimate for the maximum heat flux might be to assume that electrons carry their thermal energy at their thermal speed, leading to $q \sim n_e T_e v_{te}$. However, this picture is incorrect for a plasma. Because electrons are much lighter and faster than ions, their unimpeded streaming would create a massive charge separation. This, in turn, generates a strong parallel electric field that pulls the electrons back and accelerates the ions, enforcing [quasi-neutrality](@entry_id:197419). This coupling forces the plasma to flow together in an **ambipolar** manner.

The [characteristic limiting](@entry_id:747278) speed for this ambipolar flow is not the electron thermal speed, but the **ion sound speed**, $c_s = \sqrt{(Z T_e + \gamma_i T_i)/m_i}$. The maximum energy flux that can be sustained is then the enthalpy flux of a fluid moving at this sonic speed . For an ideal monoatomic gas, the enthalpy density is $h = \frac{5}{2} n T$. The saturated heat flux is therefore:
$$ q_{sat} \approx \frac{5}{2} n T c_s $$
In computational models, this is often implemented by using a harmonic average of the classical and saturated fluxes, $q_\parallel^{-1} = q_{SH}^{-1} + q_{sat}^{-1}$, ensuring a smooth transition between the collisional and [free-streaming](@entry_id:159506) regimes.

#### Nonlocal Transport Models

While flux-limiting is a pragmatic and widely used correction, it is an ad-hoc patch. A more physically rigorous approach to handling the $K_n \sim 1$ regime is to develop **[nonlocal transport](@entry_id:1128882) models**. The physical basis for nonlocality is that in a weakly collisional plasma, the heat flux at a point $s$ depends on the temperature profile over a region of size $\sim\lambda_{mfp}$ around $s$.

This physical picture can be formalized by solving a simplified kinetic equation. The result is a heat flux expression that is no longer a simple product, but a [convolution integral](@entry_id:155865) over the temperature gradient :
$$ q_\parallel(s) = -\int K(s, s') \, \frac{\partial T_e(s')}{\partial s'} \, ds' $$
The function $K(s,s')$ is a **nonlocal kernel**. It represents the influence of a temperature gradient at position $s'$ on the heat flux at position $s$. The kernel effectively encodes the probability that an electron will transport energy from $s'$ to $s$. The spatial extent of this kernel is determined by the [electron mean free path](@entry_id:185806). In a collisional plasma ($\lambda_{mfp} \to 0$), the kernel approaches a Dirac delta function, $K(s,s') \to \kappa_\parallel \delta(s-s')$, and the integral reduces to the local Spitzer-Härm law. As collisionality decreases, the kernel broadens, capturing the long-range influence of temperature gradients. These [nonlocal models](@entry_id:175315) provide a powerful and accurate bridge between the fluid and kinetic descriptions of heat transport.

### The Plasma-Material Interface: Sheath Heat Transmission

The energy transported along stochastic field lines is ultimately deposited onto a material surface. The interaction between the hot plasma and the solid wall is mediated by a thin, electrostatically charged boundary layer known as the **[plasma sheath](@entry_id:201017)**. The physics of the sheath acts as a final filter, determining the actual heat flux that impacts the material.

A [plasma sheath](@entry_id:201017) is typically a few Debye lengths thick and sustains a significant potential drop to ensure ambipolar particle fluxes to the wall. Ions are accelerated into the wall by this potential, while most electrons are repelled. The total heat flux to the surface, $q_{sheath}$, consists of the kinetic and potential energy of the incident ions, plus the kinetic energy of the high-energy electrons that are able to overcome the retarding sheath potential.

Modeling these kinetic processes in detail is complex. For fluid simulations of the larger plasma, the sheath is treated as a boundary condition. The heat flux is expressed through a simple and powerful relation :
$$ q_{sheath} = \gamma n_e T_e c_s $$
Here, $n_e$, $T_e$, and $c_s$ are the plasma parameters at the sheath entrance, and $\gamma$ is the dimensionless **[sheath heat transmission coefficient](@entry_id:1131561)**. This coefficient bundles all the complex [sheath physics](@entry_id:754767) into a single number. Kinetic sheath theory shows that $\gamma$ is not a universal constant but depends on factors like the ion-to-electron temperature ratio ($T_i/T_e$), the plasma composition, and [secondary electron emission](@entry_id:754608) from the surface. For a hydrogenic plasma with $T_i \sim T_e$, typical values of $\gamma$ are in the range of 5 to 7. This value arises from summing the contributions: about $2T_e$ from electrons, $0.5(T_e+T_i)$ from the ions' initial kinetic energy, $2T_i$ from the ions' thermal energy, and roughly $3T_e$ from the energy gained by ions accelerating through the sheath potential. The relation $q_{sheath} = \gamma n T c_s$ provides the [essential boundary condition](@entry_id:162668) that links the parallel transport models to the engineering reality of heat loads on the wall.

### Global Energy Balance and Partitioning

While the chapter has focused on the mechanisms of conducted heat flux, it is only one part of the overall energy loss during a TQ. A significant fraction of the plasma's initial thermal energy, $W_{th}$, can be converted into [electromagnetic radiation](@entry_id:152916) and dissipated volumetrically. The partitioning of energy between these two channels—conduction and radiation—is a critical factor determining the pattern and intensity of wall loading.

To quantify this, we define the **conducted fraction**, $f_{cond}$, and the **radiated fraction**, $f_{rad}$:
$$ f_{cond} = \frac{E_{cond}}{W_{th}}, \quad f_{rad} = \frac{E_{rad}}{W_{th}} $$
where $E_{cond}$ is the total energy conducted to PFCs and $E_{rad}$ is the total energy radiated. These fractions are constrained experimentally using diagnostics such as **[calorimetry](@entry_id:145378)** (measuring heat deposited in PFC cooling circuits) and **[bolometry](@entry_id:746904)** (measuring total photon emission) .

Energy conservation requires that $f_{cond} + f_{rad} \le 1$. An energy balance that does not close (i.e., $f_{cond} + f_{rad}  1$) often points to the existence of other energy sinks, most notably the generation of a beam of non-thermal **runaway electrons**. Accurately modeling the energy partitioning is a key goal of TQ simulations, as strategies for mitigating disruption damage often rely on injecting impurities to convert a large fraction of the thermal energy into radiation, which is dispersed over a much larger surface area than the localized conducted heat flux. The principles and models discussed in this chapter provide the foundation for simulating this complex interplay and predicting the ultimate impact of a thermal quench on the fusion device.