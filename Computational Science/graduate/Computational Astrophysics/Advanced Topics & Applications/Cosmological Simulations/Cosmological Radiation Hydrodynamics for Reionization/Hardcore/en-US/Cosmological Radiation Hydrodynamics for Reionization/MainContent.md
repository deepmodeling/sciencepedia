## Introduction
The Epoch of Reionization marks one of the last major phase transitions of the universe, when the [first stars](@entry_id:158491) and galaxies bathed the cosmos in ultraviolet light, transforming the cold, neutral [intergalactic medium](@entry_id:157642) (IGM) into the hot, ionized plasma we see today. Understanding this transformative era is a cornerstone of [modern cosmology](@entry_id:752086), but it presents a formidable theoretical challenge. The process is governed by the intricate and non-linear interplay of radiation, gravity, [gas dynamics](@entry_id:147692), and chemistry, unfolding across an immense range of spatial and temporal scales. To accurately model how galaxies form and reshape their cosmic environment, we must develop a robust theoretical and computational framework known as [cosmological radiation hydrodynamics](@entry_id:747922) (RHD).

This article provides a graduate-level guide to the principles and applications of RHD for simulating [cosmic reionization](@entry_id:747915). It addresses the fundamental problem of how to mathematically describe and numerically solve the coupled system of equations that govern this multi-physics phenomenon. By mastering this material, you will gain a deep understanding of the physical processes that shaped the early universe and the numerical techniques used to model them.

The following chapters will systematically deconstruct this complex topic. The **Principles and Mechanisms** chapter will build the theoretical foundation, deriving the governing equations from first principles and exploring the key physics of ionization fronts and microphysical interactions. Next, **Applications and Interdisciplinary Connections** will demonstrate how this framework is applied to solve concrete astrophysical problems, from verifying code performance to modeling galaxy feedback and interpreting cosmological observations. Finally, the **Hands-On Practices** section offers targeted exercises to build practical skills in tackling the core numerical challenges of RHD, such as stiff chemistry and approximate radiative transfer schemes.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms underpinning [cosmological radiation hydrodynamics](@entry_id:747922) (RHD), the theoretical framework essential for simulating the Epoch of Reionization. We will construct the governing equations from first principles, explore the critical microphysical processes that drive the evolution of the [intergalactic medium](@entry_id:157642) (IGM), analyze the emergent physics of ionization fronts, and survey the landscape of numerical techniques employed to solve this complex, multi-physics problem.

### The Governing Equations of Cosmological Radiation Hydrodynamics

At the heart of any [radiative transfer](@entry_id:158448) problem is the **[specific intensity](@entry_id:158830)**, $I_\nu$, which describes the flow of radiation energy. However, in a cosmological context, the expansion of the universe requires a careful formulation of this quantity.

#### The Radiative Transfer Equation in an Expanding Universe

The fundamental quantity describing a radiation field is the physical [specific intensity](@entry_id:158830), $I_\nu^{\mathrm{phys}}(\mathbf{x}, \hat{\mathbf{n}}, \nu, t)$, defined as the energy passing through a physical area $dA_{\mathrm{phys}}$ at physical position $\mathbf{x}$ and cosmic time $t$, per unit time $dt$, per unit frequency $d\nu$, and per unit [solid angle](@entry_id:154756) $d\Omega$ in the direction $\hat{\mathbf{n}}$.

In General Relativity, Liouville's theorem dictates that the photon [phase-space distribution](@entry_id:151304) function, $f$, is conserved along a [null geodesic](@entry_id:261630) in the absence of interactions (collisions). The [specific intensity](@entry_id:158830) is directly related to this [distribution function](@entry_id:145626) by $I_\nu^{\mathrm{phys}} = (2h\nu^3/c^2)f$, where $h$ is the Planck constant and $c$ is the speed of light. Since $f$ is conserved along a geodesic, the quantity $I_\nu^{\mathrm{phys}}/\nu^3$ is also a relativistic invariant. As photons propagate through an expanding Friedmann-Robertson-Walker (FRW) universe, their frequency redshifts as $\nu \propto 1/a(t)$, where $a(t)$ is the [cosmic scale factor](@entry_id:161850).

For computational purposes, it is advantageous to work in **[comoving coordinates](@entry_id:271238)**. We define a **[conformal time](@entry_id:263727)** $d\eta \equiv dt/a(t)$ and a **comoving area** $dA_{\mathrm{com}}$, which are related to their physical counterparts by $dt = a\,d\eta$ and $dA_{\mathrm{phys}} = a^2\,dA_{\mathrm{com}}$. Following the definition of [specific intensity](@entry_id:158830) as energy per (area-time-frequency-angle), we can define a **comoving [specific intensity](@entry_id:158830)**, $I_\nu^{\mathrm{com}}$, such that the energy element $dE$ is invariant:
$dE = I_\nu^{\mathrm{phys}} dA_{\mathrm{phys}} dt\,d\nu d\Omega = I_\nu^{\mathrm{com}} dA_{\mathrm{com}} d\eta\,d\nu d\Omega$.
Substituting the relations for area and time, we find:
$I_\nu^{\mathrm{phys}} (a^2 dA_{\mathrm{com}}) (a\,d\eta) = I_\nu^{\mathrm{com}} dA_{\mathrm{com}} d\eta$, which yields the crucial transformation:
$$I_\nu^{\mathrm{com}} = a^3(t) I_\nu^{\mathrm{phys}}$$
This **comoving [specific intensity](@entry_id:158830)** is the natural quantity to evolve in [cosmological simulations](@entry_id:747925). The conservation of $I_\nu^{\mathrm{phys}}/\nu^3$ along a geodesic can be expressed in comoving terms. Since $I_\nu^{\mathrm{phys}} = I_\nu^{\mathrm{com}}/a^3$, the conserved quantity is $I_\nu^{\mathrm{com}}/(a^3 \nu^3)$. By defining a comoving frequency $\nu_c \equiv a\nu$, which is constant along a geodesic due to the redshift relation, the conserved quantity becomes $I_\nu^{\mathrm{com}}/\nu_c^3$ .

The full **equation of radiative transfer (RTE)** in an [expanding universe](@entry_id:161442), accounting for emission ($\eta_\nu^{\mathrm{com}}$) and absorption ($\kappa_\nu^{\mathrm{com}}$), takes the form:
$$ \frac{1}{c} \frac{\partial I_\nu^{\mathrm{com}}}{\partial \eta} + \hat{\mathbf{n}} \cdot \nabla_{\mathbf{x}} I_\nu^{\mathrm{com}} - H(\eta) \left( \nu \frac{\partial I_\nu^{\mathrm{com}}}{\partial \nu} - 3I_\nu^{\mathrm{com}} \right) = \eta_\nu^{\mathrm{com}} - \kappa_\nu^{\mathrm{com}} I_\nu^{\mathrm{com}} $$
Here, $\nabla_{\mathbf{x}}$ is the gradient with respect to [comoving coordinates](@entry_id:271238), and $H(\eta) = (1/a) da/d\eta$ is the conformal Hubble parameter. The term proportional to $H(\eta)$ accounts for cosmological effects: the $\partial/\partial\nu$ term represents the redshifting of photon frequencies, and the $-3I_\nu^{\mathrm{com}}$ term accounts for the aberration of angles.

#### Moment Methods and the Closure Problem

Solving the full RTE is computationally prohibitive due to its high dimensionality (3 spatial, 2 angular, 1 frequency, 1 time). A powerful simplification is to evolve only the angular moments of the [specific intensity](@entry_id:158830). The first three moments (in their frequency-integrated, or "grey," form for simplicity) are:
- **Radiation Energy Density ($E_r$)**: $E_r = \frac{1}{c} \int I \, d\Omega$
- **Radiation Flux ($\mathbf{F}_r$)**: $\mathbf{F}_r = \int I \hat{\mathbf{n}} \, d\Omega$
- **Radiation Pressure Tensor ($\mathsf{P}_r$)**: $\mathsf{P}_r = \frac{1}{c} \int I \hat{\mathbf{n}}\hat{\mathbf{n}} \, d\Omega$

By taking angular moments of the RTE, one can derive a hierarchy of [evolution equations](@entry_id:268137) for these moments. The first two equations, which govern the conservation of radiation energy and momentum, are:
$$ \frac{\partial E_r}{\partial t} + \nabla \cdot \mathbf{F}_r = S_E $$
$$ \frac{1}{c^2} \frac{\partial \mathbf{F}_r}{\partial t} + \nabla \cdot \mathsf{P}_r = \mathbf{S}_F $$
where $S_E$ and $\mathbf{S}_F$ are source terms representing energy and momentum exchange with the gas. The problem with this system is that the equation for the $n$-th moment depends on the $(n+1)$-th moment. Here, the flux equation depends on the [pressure tensor](@entry_id:147910). To solve the system, we must "close" this hierarchy by providing an algebraic relation that approximates the higher moment in terms of lower ones. This is the **[closure problem](@entry_id:160656)**.

A common approach is to define the **Eddington tensor**, $\mathsf{D} \equiv \mathsf{P}_r / E_r$. The closure is then an approximation for $\mathsf{D}$. The Eddington tensor encodes the [angular distribution](@entry_id:193827) of the radiation field.
- In an **isotropic** [radiation field](@entry_id:164265), symmetry demands that $\mathsf{P}_r = (E_r/3)\mathsf{I}$, where $\mathsf{I}$ is the identity tensor. Thus, the Eddington tensor is $\mathsf{D} = \frac{1}{3}\mathsf{I}$. This is the [diffusion limit](@entry_id:168181), which occurs in optically thick regions.
- For a perfectly collimated beam moving in direction $\hat{\mathbf{n}}$ (**[free-streaming limit](@entry_id:749576)**), all radiation travels in one direction. The integrals yield $\mathsf{P}_r = E_r \hat{\mathbf{n}}\hat{\mathbf{n}}$, so the Eddington tensor is $\mathsf{D} = \hat{\mathbf{n}}\hat{\mathbf{n}}$.
- The Eddington tensor is frame-dependent and, because the [angular distribution of radiation](@entry_id:196414) can vary with frequency (e.g., due to frequency-dependent opacity), it is generally a function of frequency, $D_\nu$. A frequency-integrated ("grey") simulation does not remove the angular dependence; it only uses a frequency-averaged Eddington tensor .

Various closure schemes, such as the popular **M1 closure**, provide an algebraic form for $\mathsf{D}$ as a function of the reduced flux, $f \equiv |\mathbf{F}_r|/(cE_r)$, that interpolates between the isotropic ($f \to 0$) and [free-streaming](@entry_id:159506) ($f \to 1$) limits.

#### The Coupled RHD System

The final piece of the puzzle is to couple the radiation [moment equations](@entry_id:149666) to the equations of [hydrodynamics](@entry_id:158871) for the gas. In the **mixed-frame formulation**, gas properties are typically evaluated in the comoving fluid frame, while radiation moments are evolved in the Eulerian (lab) frame. Ignoring cosmological terms for clarity and including Newtonian gravity ($\Phi$), the coupled system of equations can be written as :

**Gas Equations:**
- Mass Conservation (Continuity):
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = 0 $$
- Momentum Conservation (Euler):
$$ \frac{\partial (\rho \mathbf{v})}{\partial t} + \nabla \cdot \left(\rho \mathbf{v}\mathbf{v} + P \mathsf{I}\right) = - \rho \nabla \Phi + \mathbf{G} $$
- Total Energy Conservation:
$$ \frac{\partial E}{\partial t} + \nabla \cdot \left[(E + P)\mathbf{v}\right] = - \rho \mathbf{v} \cdot \nabla \Phi + c G^0 $$

**Radiation Moment Equations:**
- Radiation Energy Conservation:
$$ \frac{\partial E_r}{\partial t} + \nabla \cdot \mathbf{F}_r = - c G^0 $$
- Radiation Momentum Conservation (Flux Evolution):
$$ \frac{1}{c^2}\frac{\partial \mathbf{F}_r}{\partial t} + \nabla \cdot \mathsf{P}_r = - \mathbf{G} $$

Here, $\rho$ is the gas density, $\mathbf{v}$ is the gas velocity, $P$ is the gas pressure, and $E = \rho e + \frac{1}{2}\rho|\mathbf{v}|^2$ is the total gas energy density. The terms $(c G^0, \mathbf{G})$ represent the radiation [four-force](@entry_id:273918) density, quantifying the rate of energy and [momentum transfer](@entry_id:147714) from radiation to the gas per unit volume. Note the sign convention: a positive $\mathbf{G}$ accelerates the gas, while the [radiation field](@entry_id:164265) loses momentum at a rate $-\mathbf{G}$. This ensures that when the gas and radiation momentum equations are summed, the interaction term cancels, and total momentum is conserved. The same applies to energy. The term $\frac{1}{c^2}\frac{\partial \mathbf{F}_r}{\partial t}$ in the flux equation is the **radiation inertia**, essential for correct [momentum conservation](@entry_id:149964) in time-dependent problems.

### Microphysical Processes: Chemistry and Thermal Balance

The source terms in the RHD equations, $G^0$ and $\mathbf{G}$, are determined by the microphysical interactions between photons and gas atoms. For the primordial gas of hydrogen and helium that constitutes the IGM, the key processes are [ionization](@entry_id:136315), recombination, and the associated heating and cooling.

#### Non-Equilibrium Chemical Network

During [reionization](@entry_id:158356), the ionization state of the gas is governed by a competition between [ionization](@entry_id:136315) by photons and electrons, and recombination of ions with electrons. The evolution of the number fractions of different species (e.g., $x_{\mathrm{HI}}$ for neutral hydrogen, $x_{\mathrm{HII}}$ for ionized hydrogen) is described by a system of coupled ordinary differential equations (ODEs). For a primordial gas of hydrogen and helium, the key reactions are:
- **Photoionization**: e.g., $\mathrm{H}^0 + \gamma \to \mathrm{H}^+ + e^-$
- **Collisional Ionization**: e.g., $\mathrm{H}^0 + e^- \to \mathrm{H}^+ + e^- + e^-$
- **Radiative Recombination**: e.g., $\mathrm{H}^+ + e^- \to \mathrm{H}^0 + \gamma$
- **Dielectronic Recombination**: e.g., $\mathrm{He}^+ + e^- \to \mathrm{He}^{0*} \to \mathrm{He}^0 + \gamma$

The resulting system of ODEs for the number fractions is non-linear, as the rates for two-body processes (collisional [ionization](@entry_id:136315) and recombination) depend on the free electron density $n_e$, which itself depends on the [ionization](@entry_id:136315) state of both hydrogen and helium . For example, the rate of change for the [neutral hydrogen fraction](@entry_id:158767) $x_{\mathrm{HI}}$ is:
$$ \frac{d x_{\mathrm{HI}}}{d t} = n_{e}\,x_{\mathrm{HII}}\,\alpha_{\mathrm{HII}}(T) - x_{\mathrm{HI}}\left(\Gamma_{\mathrm{HI}} + n_{e}\,k_{\mathrm{HI}}(T)\right) $$
where $\Gamma_{\mathrm{HI}}$ is the [photoionization](@entry_id:157870) rate, $k_{\mathrm{HI}}$ is the collisional [ionization](@entry_id:136315) [rate coefficient](@entry_id:183300), and $\alpha_{\mathrm{HII}}$ is the [radiative recombination](@entry_id:181459) coefficient. Similar equations govern the helium species ($x_{\mathrm{HeI}}, x_{\mathrm{HeII}}, x_{\mathrm{HeIII}}$). This chemical network is a fundamental component of any [reionization](@entry_id:158356) simulation.

A critical feature of this system of ODEs is its **stiffness**. The characteristic timescales for [photoionization](@entry_id:157870) ($\sim \Gamma^{-1}$) and recombination ($\sim (n_e \alpha)^{-1}$) can be extremely short (years or less) compared to the hydrodynamic timescales of the simulation (e.g., the sound-crossing time of a grid cell, $\sim 10^5$ years) or the Hubble time. This vast [separation of scales](@entry_id:270204) requires specialized implicit or semi-implicit numerical solvers to evolve the chemistry without resorting to prohibitively small timesteps .

#### Thermal Equilibrium and IGM Temperature

Photoionization is not just a source of ions; it is also the primary heating mechanism for the IGM. An ionizing photon with energy $h\nu$ must have at least the [ionization potential](@entry_id:198846) energy $h\nu_{\text{thresh}}$ to unbind an electron. The excess energy, $h\nu - h\nu_{\text{thresh}}$, is converted into the kinetic energy of the newly freed electron, thereby heating the gas. The volumetric [photoheating](@entry_id:753413) rate is given by the number of photoionizations per unit volume per second, multiplied by the average excess energy per [photoionization](@entry_id:157870).

The gas cools through several processes, including [collisional excitation](@entry_id:159854) of atoms (followed by [radiative decay](@entry_id:159878)), [free-free emission](@entry_id:270512) (bremsstrahlung), and [radiative recombination](@entry_id:181459). In a highly ionized medium, recombination cooling is particularly important.

The equilibrium temperature of the gas is set by the balance between total heating and total cooling. We can derive a simple but powerful estimate for the typical temperature of a photoionized HII region. The average kinetic energy injected per [photoionization](@entry_id:157870) is $\langle E_{\text{kin}} \rangle = \mathcal{H}_{\text{atom}} / \zeta$, where $\mathcal{H}_{\text{atom}}$ is the heating rate per atom and $\zeta$ is the ionization rate per atom. In thermal equilibrium, this heating must be balanced by the energy lost to cooling. If recombination is the dominant cooling channel, each recombination removes on average an energy of order $k_B T$. This balance implies that the equilibrium temperature $T_{\mathrm{post}}$ is proportional to the average kinetic energy per [photoionization](@entry_id:157870).

For an incident radiation field with a [power-law spectrum](@entry_id:186309) $J_\nu \propto \nu^{-\alpha}$, the equilibrium temperature can be shown to be :
$$ T_{\mathrm{post}} \propto \frac{h \nu_{\mathrm{HI}}}{k_B} \frac{1}{\alpha+2} $$
This result reveals a key piece of physics: the **spectral hardness** of the [ionizing radiation](@entry_id:149143) determines the IGM temperature. Harder spectra (smaller $\alpha$) have a larger fraction of high-energy photons, leading to more heating per [photoionization](@entry_id:157870) and thus a higher equilibrium temperature. For example, a typical quasar-like spectrum with $\alpha=1.5$ can heat the IGM to $T \approx 3 \times 10^4$ K, whereas a softer spectrum from stars would result in a lower temperature around $1-2 \times 10^4$ K.

### The Physics of Ionization Fronts

The propagation of [ionizing radiation](@entry_id:149143) into the neutral IGM creates expanding bubbles of ionized gas known as HII regions. The boundary separating the ionized bubble from the neutral medium is called an **[ionization front](@entry_id:158872) (I-front)**. The dynamics of this front are governed by the interplay between the radiation flux and the hydrodynamical response of the gas.

The pressure inside the hot ($T \sim 10^4$ K) HII region is much greater than that in the surrounding cold ($T \ll 10^4$ K) neutral IGM. This pressure imbalance drives the expansion of the HII region. The speed of the I-front, $v_{\mathrm{IF}}$, is determined by the flux of ionizing photons arriving at the front. The evolution of this speed leads to two distinct types of fronts :

- **R-type (Rapid) Fronts:** When a source first turns on, the [photon flux](@entry_id:164816) at the front is enormous, and the front expands at a very high velocity, $v_{\mathrm{IF}} \gg c_{s,i}$, where $c_{s,i}$ is the sound speed in the hot, ionized gas. The gas has no time to react hydrodynamically; it is simply flash-ionized as the front passes. An R-type front is therefore **supersonic** with respect to both the upstream neutral gas and the downstream ionized gas. The propagation is purely radiation-driven.

- **D-type (Dense) Fronts:** As the HII region grows, the [photon flux](@entry_id:164816) at the front decreases due to geometric dilution ($1/r^2$) and absorption by recombinations within the bubble. Consequently, the I-front decelerates. When $v_{\mathrm{IF}}$ drops to become comparable to the ionized sound speed ($v_{\mathrm{IF}} \lesssim c_{s,i}$), the front can no longer outrun the pressure wave from the hot bubble. The overpressured HII region then acts like a piston, driving a strong **hydrodynamic shock** into the surrounding neutral gas. The I-front now follows this shock wave. This composite structure—a leading shock that compresses and heats the neutral gas, followed by a subsonic I-front that ionizes it—is a D-type front. The I-front itself is **subsonic** with respect to the ionized gas.

The **R-to-D transition** is the natural evolution for an expanding HII region. It occurs when the I-front decelerates to approximately the sound speed of the ionized gas, triggering the formation of a leading shock.

In addition to thermal pressure, radiation itself exerts a mechanical force. The **radiation force density** on the gas can be written in the grey approximation as $\mathbf{f}_{\mathrm{rad}} = (\rho \kappa_F \mathbf{F}_r)/c$, where $\kappa_F$ is the flux-mean [opacity](@entry_id:160442). In the highly ionized IGM, this force is dominated by Thomson scattering off free electrons. Comparing the magnitude of this force to the gas pressure gradient, $|\nabla P| \approx P/L$ over a scale $L$, we find the ratio is typically very small during [reionization](@entry_id:158356), $R \equiv |\mathbf{f}_{\mathrm{rad}}| / |\nabla P| \sim 10^{-3}$ for typical IGM conditions . This indicates that while radiation pressure can be important in other contexts (e.g., near massive stars), the large-scale dynamics of [reionization](@entry_id:158356) are primarily driven by gas pressure gradients established by [photoheating](@entry_id:753413).

### Numerical Methods and Implementation

Solving the full RHD system requires sophisticated numerical techniques to handle the challenges of multi-scale, multi-physics coupling.

#### Operator Splitting

The full RHD evolution equation, $\frac{d\mathbf{Y}}{dt} = (\mathcal{L}_{\mathrm{H}} + \mathcal{L}_{\mathrm{R}} + \mathcal{L}_{\mathrm{C}})\mathbf{Y}$, involves operators for hydrodynamics ($\mathcal{L}_{\mathrm{H}}$), [radiation transport](@entry_id:149254) ($\mathcal{L}_{\mathrm{R}}$), and chemistry/cooling ($\mathcal{L}_{\mathrm{C}}$) that act on vastly different timescales. A common computational strategy is **[operator splitting](@entry_id:634210)**, where the evolution over a single timestep $\Delta t$ is approximated by applying each operator in sequence. For example, a simple first-order **Lie-Trotter splitting** would be $\mathbf{Y}(t+\Delta t) \approx e^{\Delta t \mathcal{L}_{\mathrm{C}}} e^{\Delta t \mathcal{L}_{\mathrm{R}}} e^{\Delta t \mathcal{L}_{\mathrm{H}}} \mathbf{Y}(t)$.

This approximation introduces a [splitting error](@entry_id:755244) whose magnitude depends on the extent to which the operators fail to commute. The leading-order [local error](@entry_id:635842) is proportional to the sum of pairwise **[commutators](@entry_id:158878)**, e.g., $[\mathcal{L}_{\mathrm{H}}, \mathcal{L}_{\mathrm{R}}] = \mathcal{L}_{\mathrm{H}}\mathcal{L}_{\mathrm{R}} - \mathcal{L}_{\mathrm{R}}\mathcal{L}_{\mathrm{H}}$. For the splitting to be accurate, the action of these commutators over a timestep must be small. This is achieved through several strategies :
1.  **Implicit Solvers for Chemistry ($\mathcal{L}_{\mathrm{C}}$):** The extremely short timescales of chemistry make the operator $\mathcal{L}_{\mathrm{C}}$ stiff. Using an implicit solver finds the near-equilibrium solution over $\Delta t$, taming the stiffness and bounding the change in the state vector, thereby controlling the magnitude of [commutators](@entry_id:158878) involving $\mathcal{L}_{\mathrm{C}}$.
2.  **Reduced Speed of Light Approximation (RSLA) for Radiation ($\mathcal{L}_{\mathrm{R}}$):** The true speed of light $c$ would impose an impossibly small timestep for explicit [radiation transport](@entry_id:149254). The RSLA replaces $c$ with a smaller value $\tilde{c}$ that is still much larger than the gas sound speed ($ \tilde{c} \gg c_s$). This ensures that the radiation step still evolves much faster than the [hydrodynamics](@entry_id:158871) step, keeping the $[\mathcal{L}_{\mathrm{H}}, \mathcal{L}_{\mathrm{R}}]$ commutator small, while making the problem computationally tractable.

#### Methods for Radiative Transfer

The implementation of the radiation step, $e^{\Delta t \mathcal{L}_{\mathrm{R}}}$, can be accomplished by several families of algorithms, each with distinct strengths and weaknesses regarding [angular resolution](@entry_id:159247) and the ability to cast sharp shadows .

- **Long-Characteristics Ray Tracing:** This method integrates the RTE along rays cast from sources. It has excellent [angular resolution](@entry_id:159247) *along* the rays and preserves sharp shadows perfectly. However, with a finite number of rays, it suffers from angular discretization artifacts, creating wedge-shaped [ionization](@entry_id:136315) fronts that can bias morphological statistics.

- **Short-Characteristics:** A grid-based method that traces rays backward from cell centers to upwind faces and interpolates. This interpolation introduces [numerical diffusion](@entry_id:136300), which tends to blur sharp features and cause light to artificially leak into shadows.

- **Monte Carlo (MC) Transport:** This method tracks a large number of discrete "photon packets." It can achieve arbitrarily high [angular resolution](@entry_id:159247) with enough packets. However, at finite packet numbers, it suffers from Poisson [shot noise](@entry_id:140025). In the non-linear RHD system, this noise can be amplified into a systematic bias, for example, by stochastically ionizing a path through a dense clump, which then allows more photons to follow, artificially promoting [percolation](@entry_id:158786).

- **Moment Methods (e.g., M1):** These methods evolve the angular [moments of the radiation field](@entry_id:160501). Their primary weakness is the closure approximation. M1 closure, for instance, assumes a single [bulk flow](@entry_id:149773) direction for radiation in each cell. This fails catastrophically where radiation beams cross or in the penumbra of shadows, leading to artificial merging of beams and filling of shadows. This systematically biases simulations toward smoother [ionization](@entry_id:136315) fronts and earlier percolation.

#### Cosmological Boundary Conditions

Cosmological simulations are performed in a finite comoving box, intended to represent a small, statistically representative volume of the universe. To mimic an infinite universe, **periodic boundary conditions** are used for both gas and radiation. In a finite-volume code, this means the state variables (e.g., gas density $\rho$, velocity $\mathbf{v}$, radiation energy density $E_r$, and flux $\mathbf{F}_r$) in the "[ghost cells](@entry_id:634508)" outside one face of the box are copied from the corresponding active cells on the opposite face. For a vector like $\mathbf{F}_r$, all components are copied directly, ensuring that a photon leaving one side re-enters the other with its direction and energy unchanged in the [comoving frame](@entry_id:266800).

A common technique to account for sources outside the simulation volume is to include a **spatially uniform ionizing background**. This is often constructed from the box-averaged [emissivity](@entry_id:143288), $\bar{\varepsilon}_g$. To avoid double-counting energy, one splits the total [emissivity](@entry_id:143288) into its average and a fluctuating part: $\varepsilon_g(\mathbf{x}) = \bar{\varepsilon}_g + \delta\varepsilon_g(\mathbf{x})$. The simulation then adds $\bar{\varepsilon}_g$ as a uniform [source term](@entry_id:269111) (or solves for the uniform field it generates) and adds only the local fluctuation $\delta\varepsilon_g(\mathbf{x})$ as the spatially varying source. In a simple uniform steady state, this background emissivity generates a background radiation energy density $E_g = \bar{\varepsilon}_g / (c \kappa_g)$ . This procedure ensures both energy conservation and correct boundary conditions for a representative cosmological volume.