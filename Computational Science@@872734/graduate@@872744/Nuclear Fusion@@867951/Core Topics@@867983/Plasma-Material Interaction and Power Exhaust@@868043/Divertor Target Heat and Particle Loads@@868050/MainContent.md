## Introduction
Successfully confining a fusion plasma is only half the battle; managing the immense power and particle exhaust it produces is an equally critical challenge for the realization of a [fusion reactor](@entry_id:749666). The heat and particle fluxes exiting the core plasma are intense enough to destroy any known material upon direct impact. The primary component designed to intercept this exhaust, cool it, and neutralize it is the divertor. A deep understanding of the physics governing the transport of energy and particles to the divertor targets is therefore not an academic exercise, but a fundamental requirement for designing a durable and efficient fusion power plant.

This article addresses the knowledge gap between the raw power generated in the core and the manageable heat loads required at the material interface. It provides a comprehensive overview of the principles, mechanisms, and applications related to divertor heat and particle loads. You will learn how the global power balance dictates the challenge, how magnetic geometry and [plasma physics](@entry_id:139151) are exploited for mitigation, and how advanced operational regimes are achieved and controlled.

The following chapters will guide you through this complex topic. "Principles and Mechanisms" lays the groundwork, detailing the flow of power from the core to the Scrape-Off Layer and the fundamental physics of [plasma-surface interaction](@entry_id:753483), recycling, and detachment. "Applications and Interdisciplinary Connections" explores how these principles are put into practice through advanced [divertor](@entry_id:748611) designs, operational strategies, and diagnostic techniques. Finally, "Hands-On Practices" offers the opportunity to apply these concepts to solve practical problems related to [divertor](@entry_id:748611) performance and component loading.

## Principles and Mechanisms

The mitigation of plasma exhaust stands as one of the most critical challenges in the development of a magnetic fusion reactor. The immense power flowing out of the core plasma must be handled by material components without causing catastrophic damage or releasing impurities that would contaminate and cool the fusion fuel. The [divertor](@entry_id:748611) is the principal component designed for this task. Understanding the principles and mechanisms that govern the transport of heat and particles from the plasma edge to the divertor targets is therefore paramount. This chapter elucidates these fundamental processes, beginning with the global power flow and progressively delving into the microphysics, control strategies, and operational challenges that define the modern understanding of the plasma-material interface in a [tokamak](@entry_id:160432).

### The Global Power Balance: From Core to Divertor

The journey of exhaust power begins within the core plasma, the region inside the last closed [magnetic flux surface](@entry_id:751622), or **separatrix**. In a steady-state fusion device, the total heating power absorbed by the core plasma, denoted $P_{\mathrm{abs}}$ (from [ohmic heating](@entry_id:190028) and auxiliary systems like neutral beams or [radio-frequency waves](@entry_id:195520)), must be exhausted. Power leaves the core via two primary channels: [electromagnetic radiation](@entry_id:152916) and particle transport.

The first channel is **core radiation**, $P_{\mathrm{rad,core}}$, which consists of [bremsstrahlung](@entry_id:157865) and [line radiation](@entry_id:751334) from both the hydrogenic fuel and any impurity ions present in the core. This power is emitted isotropically and is broadly distributed over the main chamber wall. The remaining power is transported by particles (conduction and convection) across the [separatrix](@entry_id:175112) into the edge region known as the **Scrape-Off Layer (SOL)**. This power crossing the separatrix, $P_{\mathrm{sep}}$, represents the total power that must be handled by the divertor and other plasma-facing components. Applying the principle of energy conservation to the core volume in steady state yields a simple but crucial relationship [@problem_id:3695528]:

$P_{\mathrm{sep}} = P_{\mathrm{abs}} - P_{\mathrm{rad,core}}$

Once in the SOL, the power $P_{\mathrm{sep}}$ flows along open magnetic field lines that are guided into the [divertor](@entry_id:748611). Within the SOL and [divertor](@entry_id:748611) volumes, a portion of this power can be converted into isotropic radiation, primarily through interactions with fuel neutrals and seeded impurities. This radiated power is denoted $P_{\mathrm{SOL,rad}}$. The remaining power is conducted and convected along the field lines until it is deposited on the solid [divertor](@entry_id:748611) target plates as a heat load, $P_{\mathrm{div}}$. Neglecting other [minor loss](@entry_id:269477) channels (such as direct conduction to the main chamber walls), energy conservation within the SOL volume dictates the partitioning of $P_{\mathrm{sep}}$ [@problem_id:3695528]:

$P_{\mathrm{sep}} = P_{\mathrm{div}} + P_{\mathrm{SOL,rad}}$

Consider a hypothetical steady-state discharge where the total [absorbed power](@entry_id:265908) is $P_{\mathrm{abs}} = 25\,\mathrm{MW}$. If bolometric measurements indicate that the core radiates $P_{\mathrm{rad,core}} = 7\,\mathrm{MW}$ and the SOL radiates $P_{\mathrm{SOL,rad}} = 3\,\mathrm{MW}$, the power flow can be tracked. The power entering the SOL is $P_{\mathrm{sep}} = 25\,\mathrm{MW} - 7\,\mathrm{MW} = 18\,\mathrm{MW}$. Of this, $3\,\mathrm{MW}$ is radiated away within the SOL, leaving a total power of $P_{\mathrm{div}} = 18\,\mathrm{MW} - 3\,\mathrm{MW} = 15\,\mathrm{MW}$ to be deposited on the divertor targets [@problem_id:3695528]. This value, $P_{\mathrm{div}}$, represents the total heat load that the [divertor](@entry_id:748611) materials must withstand.

### From Total Power to Surface Heat Flux: The Role of Geometry

The total power $P_{\mathrm{div}}$ is not as critical as the *density* of that power, or **heat flux**, which determines the surface temperature of the material. In the SOL, [thermal transport](@entry_id:198424) is highly anisotropic; thermal conductivity parallel to the magnetic field is many orders of magnitude greater than that perpendicular to it. Consequently, exhaust power flows in a narrow channel along the magnetic field lines. The magnitude of this **[parallel heat flux](@entry_id:753124)**, $q_{\parallel}$, can be extremely high, reaching hundreds of megawatts per square meter in contemporary devices and projected to exceed a gigawatt per square meter in a reactor.

If this intense heat flux were to impinge perpendicularly onto a material surface, no known material could survive. The key principle of modern divertor design is to exploit magnetic geometry to spread this heat load. The [divertor](@entry_id:748611) target is oriented at a very shallow angle to the incoming magnetic field lines. The heat flux deposited on the surface, $q_t$, is the component of the heat [flux vector](@entry_id:273577), $\mathbf{q} = q_{\parallel}\mathbf{\hat{b}}$, normal to the surface, where $\mathbf{\hat{b}}$ is the unit vector along the magnetic field. This is given by $q_t = \mathbf{q} \cdot \mathbf{\hat{n}}$, where $\mathbf{\hat{n}}$ is the unit normal to the target surface.

If we define the **field-line incidence angle**, $\alpha$, as the angle between the magnetic field line and the *plane of the target surface*, the relationship becomes [@problem_id:3695570]:

$q_t = q_{\parallel} \sin(\alpha)$

This simple geometric projection is a powerful tool for heat flux mitigation. By making the angle $\alpha$ very small (typically $1-3$ degrees), the surface heat flux can be dramatically reduced compared to the [parallel heat flux](@entry_id:753124). For instance, if the [parallel heat flux](@entry_id:753124) is $q_{\parallel} = 500\,\mathrm{MW\,m^{-2}}$ and the magnetic field strikes the target at an angle of $\alpha = 2^{\circ}$, the resulting surface heat flux is $q_t = 500 \times \sin(2^{\circ}) \approx 17.45\,\mathrm{MW\,m^{-2}}$ [@problem_id:3695570]. While still a formidable heat load, this is a substantial reduction and brings the challenge closer to the realm of engineering feasibility.

### The Spatial Distribution of Heat: The Scrape-Off Layer Width

The heat flux is not deposited uniformly along the target but is concentrated in a narrow stripe near the **strike point**, where the [separatrix](@entry_id:175112) intersects the target. The characteristic width of this heat deposition profile is a critical parameter. This width is determined by the physics of cross-field transport in the SOL.

We define the **heat flux width**, $\lambda_q$, as the exponential e-folding length of the heat flux profile measured perpendicular to the magnetic field lines. The value of $\lambda_q$ observed at the [divertor](@entry_id:748611) target, $\lambda_{q, \mathrm{targ}}$, is the result of two distinct processes: the establishment of an upstream width and its geometric mapping to the target [@problem_id:3695534].

The fundamental width is set in the main SOL, typically referenced at the outboard midplane, where it is denoted $\lambda_{q, \mathrm{up}}$. This width arises from a competition between the slow, diffusive-like transport of heat radially *across* magnetic field lines and the rapid loss of heat *along* them to the divertor. A simple but insightful model balances these processes, yielding a characteristic width that scales as [@problem_id:3695534]:

$\lambda_{q, \mathrm{up}} \sim \sqrt{D_{\perp} \tau_{\parallel}}$

Here, $D_{\perp}$ is the effective cross-field [thermal diffusivity](@entry_id:144337) (dominated by turbulence), and $\tau_{\parallel}$ is the characteristic time for heat to be lost along the field lines. This parallel loss time depends on the regime: in a **convection-limited** (or sheath-limited) regime, heat is carried by plasma flowing at the sound speed $c_s$ over a [connection length](@entry_id:747697) $L_{\parallel}$, so $\tau_{\parallel} \sim L_{\parallel}/c_s$. In a **conduction-limited** regime, heat transport is dominated by electron conduction with parallel [thermal diffusivity](@entry_id:144337) $\chi_{\parallel}$, giving $\tau_{\parallel} \sim L_{\parallel}^2/\chi_{\parallel}$.

This upstream width is then mapped along the magnetic field lines to the [divertor](@entry_id:748611). Due to the presence of the X-point, the [poloidal magnetic field](@entry_id:753563) weakens and the distance between flux surfaces expands. This **[magnetic flux expansion](@entry_id:751620)**, $f_x$, acts like a geometric magnifying glass, stretching the narrow upstream width $\lambda_{q, \mathrm{up}}$ to a larger width at the target. In the simplest case, $\lambda_{q, \mathrm{targ}} = f_x \lambda_{q, \mathrm{up}}$. In reality, additional physical processes within the cold, dense divertor plasma, such as ion-neutral collisions ([charge exchange](@entry_id:186361)) and plasma drifts, can cause further broadening of the heat flux profile [@problem_id:3695534] [@problem_id:3695516].

### Synthesizing the Challenge: A Divertor Figure of Merit

The concepts of separatrix power, SOL width, and geometric factors can be combined to form a powerful [figure of merit](@entry_id:158816) for assessing the divertor challenge of a given device. A commonly used metric is $P_{\mathrm{sep}}/R$, the power crossing the [separatrix](@entry_id:175112) per unit major radius. This metric normalizes the exhaust power to the size of the machine, providing a basis for comparing different [tokamaks](@entry_id:182005) and extrapolating to future reactors.

We can derive a direct relationship between this metric and the peak surface heat flux on the target, $q_{t,\mathrm{peak}}$. The total power flowing into the outboard SOL is a fraction $f_{\mathrm{out}}$ of $P_{\mathrm{sep}}$. This power is distributed over an effective area at the midplane approximately given by the toroidal circumference ($2\pi R$) times the SOL width ($\lambda_q$). This determines the peak [parallel heat flux](@entry_id:753124) at the midplane. As this flux travels to the divertor, it is reduced by flux expansion ($f_{\exp}$) and finally projected onto the target at an angle $\alpha$. Combining these steps gives [@problem_id:3695525]:

$q_{t,\mathrm{peak}} = \frac{f_{\mathrm{out}} P_{\mathrm{sep}} \sin(\alpha)}{2\pi R \lambda_q f_{\exp}}$

This equation is a powerful summary of the [steady-state heat](@entry_id:163341) load problem. It shows that the peak heat flux increases with the power exhaust ($P_{\mathrm{sep}}$) but can be mitigated by having a large machine size ($R$), a wide SOL ($\lambda_q$), large flux expansion ($f_{\exp}$), and a very shallow target angle ($\alpha$).

Given that divertor target materials have a technological limit on the [steady-state heat](@entry_id:163341) flux they can handle, $q_{t,\lim}$ (typically around $10-20\,\mathrm{MW\,m^{-2}}$), we can rearrange the formula to find the maximum permissible value of the [divertor](@entry_id:748611) challenge metric for a given set of physics and engineering parameters [@problem_id:3695525]:

$\left( \frac{P_{\mathrm{sep}}}{R} \right)_{\max} = \frac{2\pi q_{t,\lim} \lambda_q f_{\exp}}{f_{\mathrm{out}} \sin(\alpha)}$

For a device with $\lambda_q = 5\,\mathrm{mm}$, $f_{\exp}=6$, $\alpha = 2.5^{\circ}$, $f_{\mathrm{out}}=0.6$, and a material limit of $q_{t,\lim}=10\,\mathrm{MW\,m^{-2}}$, the maximum tolerable power handling capability would be $(P_{\mathrm{sep}}/R)_{\max} \approx 72\,\mathrm{MW/m}$ [@problem_id:3695525]. This type of analysis is crucial for designing future reactors like ITER and DEMO, where $P_{\mathrm{sep}}/R$ is expected to be significantly higher than in present-day machines.

### Parallel Transport and Plasma-Surface Interaction

To understand how to control the parameters in our [divertor](@entry_id:748611) model, especially temperature and [particle flux](@entry_id:753207), we must look closer at the physics along the magnetic field lines and at the ultimate boundary with the material surface.

#### The Plasma-Wall Boundary: Sheath and Bohm Criterion

The interface between the quasi-neutral bulk plasma and the solid target is mediated by a thin, non-neutral boundary layer called the **[plasma sheath](@entry_id:201017)**. It forms because electrons, being much lighter and hotter than ions, have a much higher [thermal velocity](@entry_id:755900) and would otherwise strike the surface at a far greater rate. This initial electron flux charges the surface negatively with respect to the plasma. The resulting strong electric field in the sheath acts to repel most of the electrons while accelerating ions into the target, establishing a steady state where the ion and electron currents to an electrically floating surface are equal. The thickness of this [space-charge layer](@entry_id:271625) is on the order of a few **Debye lengths** [@problem_id:3695555].

For a stable, monotonic potential drop to form in the sheath, the ions must enter the sheath from the upstream quasi-neutral "presheath" with a minimum velocity. This fundamental constraint is known as the **Bohm criterion**. It states that the ion flow speed at the sheath entrance, $u_i$, must be at least equal to the local **ion-acoustic speed**, $c_s$. For a plasma with [electron temperature](@entry_id:180280) $T_e$ and [ion temperature](@entry_id:191275) $T_i$, this speed is given by [@problem_id:3695555]:

$u_{i} \ge c_{s} = \sqrt{\frac{k_{B}(T_{e} + \gamma_{i} T_{i})}{m_{i}}}$

where $k_B$ is the Boltzmann constant, $m_i$ is the ion mass, and $\gamma_i$ is the ion [polytropic index](@entry_id:137268) (typically between 1 and 3). This means that the plasma must be accelerated throughout the presheath to become supersonic (relative to $c_s$) at the sheath edge. The Bohm criterion imposes a critical boundary condition on all fluid models of the SOL: it fixes the [particle flux](@entry_id:753207) onto the target, $\Gamma_t$, to be at least $\Gamma_t = n_t c_s$, where $n_t$ is the plasma density at the target. This, in turn, sets a lower bound on the convective heat flux to the target, which is proportional to $\Gamma_t T_t$.

#### Particle Recycling and Flux Amplification

The [particle flux](@entry_id:753207) to the divertor target is not simply the flux of particles that has crossed the separatrix from the core. It is dominated by a process known as **particle recycling**. When plasma ions strike the target, they are neutralized and can be re-emitted back into the plasma. This outgoing flux of neutral atoms consists of two components: **prompt reflection**, where incident ions [backscatter](@entry_id:746639) ballistically from surface atoms, and **re-emission**, a slower process where ions are implanted in the material and later outgas [@problem_id:3695557].

The efficiency of this process is quantified by the **[recycling coefficient](@entry_id:754164)**, $R$, defined as the ratio of the total neutral flux leaving the surface to the incident ion flux, $\Gamma_t$. These recycled neutrals travel a short distance before they are re-ionized by the plasma, creating a localized source of new plasma particles near the target.

In steady state, the ion flux arriving at the target must equal the sum of the flux entering the SOL from upstream, $\Gamma_{\mathrm{up}}$, plus the integrated source of ions from the ionization of recycled neutrals. A simple [particle balance](@entry_id:753197) model for the [divertor](@entry_id:748611) leg reveals a profound consequence of this process [@problem_id:3695557]:

$\Gamma_t = \frac{\Gamma_{\mathrm{up}}}{1 - R}$

This is the **[flux amplification](@entry_id:749479)** formula. It shows that as the [recycling coefficient](@entry_id:754164) $R$ approaches 1, the [particle flux](@entry_id:753207) at the target can become enormously amplified, often exceeding the upstream flux from the core by one or two orders of magnitude. This **high-recycling regime** is characteristic of standard [divertor](@entry_id:748611) operation and leads to a very high [plasma density](@entry_id:202836) near the target, which is a key prerequisite for achieving [divertor detachment](@entry_id:748613).

### The Path to Heat Load Mitigation: Divertor Detachment

The ultimate goal of divertor physics is to reduce the peak heat and particle loads on the targets to manageable levels. The most promising solution is to operate the [divertor](@entry_id:748611) in a **detached** state. This involves intentionally creating a cold, dense plasma region in front of the target that can dissipate the majority of the exhaust power through volumetric processes before it reaches the surface.

#### The Conduction-Limited SOL: The Two-Point Model

The foundation for understanding detachment lies in the **two-point model**, which describes [heat transport](@entry_id:199637) in a **conduction-limited SOL**. This model considers a 1D flux tube connecting an upstream location ("u") with a target location ("t"). Assuming power flows primarily via electron heat conduction governed by the classical **Spitzer-Härm** law ($q_{\parallel} \propto -T_e^{5/2} dT_e/ds$) and is conserved along the flux tube, one can integrate the heat transport equation. This yields a powerful relationship between the upstream temperature $T_u$, the target temperature $T_t$, the [parallel heat flux](@entry_id:753124) $q_{\parallel}$, and the [connection length](@entry_id:747697) $L$ [@problem_id:3695510]:

$T_u^{7/2} - T_t^{7/2} = \frac{7}{2} \frac{q_{\parallel} L}{\kappa_0}$

Here, $\kappa_0$ is the Spitzer-Härm conductivity coefficient. This equation shows that a large temperature gradient can be sustained along the SOL, allowing for a hot upstream plasma (e.g., $T_u \sim 100\,\mathrm{eV}$) to connect to a much colder target plasma ($T_t \sim 10\,\mathrm{eV}$). This large temperature drop is a hallmark of the high-recycling regime.

#### Radiative Power Dissipation: Impurity Seeding

The two-point model assumes $q_{\parallel}$ is constant. To actually reduce the heat flux reaching the target, this power must be dissipated volumetrically. The most effective way to do this is by introducing a small amount of a non-fuel gas, or **impurity**, into the divertor region. This technique is called **[impurity seeding](@entry_id:750578)** [@problem_id:3695552].

Low-Z impurities like nitrogen or neon, when introduced into the cold divertor plasma, are not fully ionized. Their remaining bound electrons can be excited by collisions with plasma electrons. The subsequent de-excitation emits photons, radiating power away. Under **[coronal equilibrium](@entry_id:188784)**, where electron-impact excitation is balanced by spontaneous [radiative decay](@entry_id:159878), the volumetric [radiated power](@entry_id:274253) density is given by:

$p_{\mathrm{rad}} = n_e n_z L_z(T_e)$

where $n_z$ is the impurity density and $L_z(T_e)$ is the **coronal power loss function**. This function is highly dependent on the impurity species and the [electron temperature](@entry_id:180280), typically exhibiting strong peaks at specific temperatures where certain atomic shells are most effectively excited [@problem_id:3695552]. By choosing an impurity that radiates strongly at the typical divertor temperatures ($5-20\,\mathrm{eV}$), a small impurity fraction ($f_z = n_z/n_e$) can radiate a very large fraction of the incoming power. For example, in a [divertor](@entry_id:748611) plasma with $n_e=5 \times 10^{19}\,\mathrm{m}^{-3}$ and $T_e=8\,\mathrm{eV}$, a nitrogen fraction of just $f_z \approx 0.013$ can be sufficient to radiate $5\,\mathrm{MW}$ of power in a volume of $1\,\mathrm{m}^3$ [@problem_id:3695552]. The primary challenge of [impurity seeding](@entry_id:750578) is to confine the impurities to the divertor region, as their penetration into the hot core plasma can cause significant energy loss and fuel dilution, degrading fusion performance [@problem_id:3695552].

#### The Detached State

**Divertor detachment** is the operational regime achieved when volumetric power and momentum losses become so strong that the plasma effectively "detaches" from the target. It is characterized by a simultaneous, drastic reduction in both the temperature and the [particle flux](@entry_id:753207) at the target plate [@problem_id:3695556].

The process begins by increasing the upstream density or [impurity seeding](@entry_id:750578), which enhances the recycling and radiation in the divertor. The intense volumetric power losses, primarily from impurity and hydrogenic radiation, consume the [parallel heat flux](@entry_id:753124), causing the target temperature to plummet to below $5\,\mathrm{eV}$, and often as low as $1\,\mathrm{eV}$. At these low temperatures, the ionization rate of hydrogen drops sharply, and **[volumetric recombination](@entry_id:756563)** (where an ion and electron recombine to form a neutral atom) becomes a significant particle sink. This recombination, coupled with momentum loss from ion-neutral collisions ([charge exchange](@entry_id:186361)), breaks the [flux amplification](@entry_id:749479) cycle, leading to a "roll-over" and sharp drop in the ion flux $\Gamma_t$ arriving at the target. This combination of reduced temperature and [particle flux](@entry_id:753207) leads to a dramatic decrease in the target heat load, achieving the primary goal of divertor operation.

Operationally, detachment is identified by several key signatures [@problem_id:3695556]:
-   A roll-over and decrease in the [ion saturation current](@entry_id:196456) measured by **Langmuir probes** embedded in the target, which is proportional to $\Gamma_t$.
-   An increase in the [total radiated power](@entry_id:756065) measured by **bolometer** arrays viewing the divertor.
-   The appearance of specific **spectroscopic** signatures indicating high recombination rates (e.g., a shift in the Balmer series [line emission](@entry_id:161645) ratio).
-   A significant drop in the measured [plasma pressure](@entry_id:753503) near the target compared to upstream, indicating strong momentum loss.

### Multi-dimensional Effects and Transients

While 1D models provide immense insight, real divertor plasmas are fully three-dimensional and are subject to transient events.

#### Asymmetries from Plasma Drifts

The heat and particle loads are rarely symmetric between the various [divertor](@entry_id:748611) strike points (inboard vs. outboard, top vs. bottom). These asymmetries are primarily driven by **plasma drifts**.

The **top/bottom asymmetry** is mainly caused by the charge-dependent **$\nabla B$ and curvature drifts**. In a standard tokamak magnetic field geometry, these drifts drive ions vertically (e.g., downwards) and electrons in the opposite direction. This creates a vertical current that must be closed by parallel currents flowing to the targets, leading to an enhancement of particle and heat fluxes on the divertor target in the direction of the ion $\nabla B$ drift. Reversing the main [toroidal magnetic field](@entry_id:756057) reverses the drift direction and, consequently, the top/bottom asymmetry [@problem_id:3695516].

The **inboard/outboard asymmetry** is more complex and is strongly influenced by the charge-independent **$\mathbf{E}\times\mathbf{B}$ drift**. The vertical drifts and other effects create a poloidally varying electrostatic potential in the SOL. The resulting poloidal electric field, when crossed with the [toroidal magnetic field](@entry_id:756057), drives a radial $\mathbf{E}\times\mathbf{B}$ drift. This drift can convect plasma across flux surfaces, preferentially loading either the inboard or outboard targets and creating a strong in/out asymmetry in the [divertor](@entry_id:748611) loads [@problem_id:3695516].

#### Transient Heat Loads: Edge Localized Modes (ELMs)

In the high-confinement mode (H-mode) of operation, the plasma edge develops a steep pressure gradient, or "pedestal," which is subject to periodic magnetohydrodynamic (MHD) instabilities known as **Edge Localized Modes (ELMs)**. Each ELM event involves the rapid, impulsive expulsion of a significant amount of energy ($E_{\mathrm{ELM}}$) and particles from the plasma edge into the SOL [@problem_id:3695519].

This burst of energy travels down the SOL and strikes the divertor targets over a very short duration, $\Delta t$ (typically $0.1-1\,\mathrm{ms}$), and over a specific **wetted area**, $A_{\mathrm{wet}}$. The resulting transient heat flux can be estimated from [energy conservation](@entry_id:146975) as [@problem_id:3695519]:

$q_{\mathrm{ELM}} = \frac{f_{\mathrm{div}} E_{\mathrm{ELM}}}{A_{\mathrm{wet}} \Delta t}$

where $f_{\mathrm{div}}$ is the fraction of ELM energy reaching the divertors. Given that $E_{\mathrm{ELM}}$ can be on the order of $10^4 - 10^5\,\mathrm{J}$ in current machines and the deposition time is very short, the resulting transient heat fluxes can be enormous. For example, an ELM with $E_{\mathrm{ELM}} = 50\,\mathrm{kJ}$ depositing half its energy over $1\,\mathrm{ms}$ onto an area of $0.5\,\mathrm{m}^2$ would produce a transient heat flux of $q_{\mathrm{ELM}} = 50\,\mathrm{MW\,m^{-2}}$ [@problem_id:3695519]. For future reactors like ITER, unmitigated ELMs are projected to cause heat loads well in excess of material limits, leading to rapid erosion and component failure. The control and mitigation of ELMs, or operation in ELM-free regimes, is therefore a research area of the highest priority, standing alongside the challenge of handling steady-state power exhaust.