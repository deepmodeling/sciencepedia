## Introduction
Semi-analytic models (SAMs) represent a cornerstone of modern theoretical cosmology, offering a powerful and computationally efficient framework for understanding how galaxies form and evolve. The universe presents a formidable challenge to simulators: the intricate physics of stars, gas, and black holes must be understood within the vast, evolving cosmic web of dark matter. SAMs address this challenge by ingeniously combining the robust predictions of dark matter [structure formation](@entry_id:158241) with a parameterized, physics-based description of the complex baryonic processes that govern galaxy growth. This approach provides a crucial bridge between fundamental cosmological theory and the rich observational data from large-scale galaxy surveys.

This article will guide you through the theory and practice of semi-analytic modeling. In **Principles and Mechanisms**, we will dissect the fundamental architecture of a SAM, starting from the dark matter [merger trees](@entry_id:751891) that provide the cosmic scaffolding, and building upon it with the essential physics of gas cooling, [star formation](@entry_id:160356), and regulatory feedback. Next, in **Applications and Interdisciplinary Connections**, we will explore how these models are deployed to predict the key statistical properties of the galaxy population, constrain the drivers of galaxy evolution, and connect with advanced observational and statistical techniques. Finally, **Hands-On Practices** will provide you with the opportunity to implement and experiment with core algorithms that form the heart of this powerful modeling technique.

## Principles and Mechanisms

Semi-analytic models (SAMs) represent a powerful computational framework for simulating the formation and evolution of the galaxy population within the broader context of [cosmological structure formation](@entry_id:160031). As a modeling technique, they occupy a crucial middle ground between large-scale hydrodynamical simulations and purely empirical methods. The core philosophy of a SAM is to combine a detailed, physically-grounded understanding of dark matter halo assembly with a parameterized, rule-based description of the complex baryonic processes that govern galaxy growth [@problem_id:3486098]. This chapter will deconstruct the fundamental principles and mechanisms that constitute the architecture of a modern semi-analytic model.

### The Dark Matter Scaffolding

The foundation of any SAM is the dark matter skeleton of the universe as predicted by the standard Lambda Cold Dark Matter ($\Lambda$CDM) paradigm. Within this paradigm, galaxies are not isolated entities but are understood to form and evolve within the deep [gravitational potential](@entry_id:160378) wells of dark matter halos. Therefore, the first step in building a model galaxy population is to accurately describe the population of these host halos across cosmic time.

#### Halo Assembly Histories: From Press-Schechter to Excursion Sets

The statistical properties of the dark matter halo population—such as their abundance as a function of mass (the **[halo mass function](@entry_id:158011)**) and their assembly through mergers—are robustly predicted by $\Lambda$CDM. These assembly histories are encapsulated in **[merger trees](@entry_id:751891)**, which serve as the fundamental input for a SAM. A merger tree for a given halo at [redshift](@entry_id:159945) $z=0$ provides a complete record of its progenitor halos and their mergers at all earlier times. These trees can be extracted directly from cosmological $N$-body simulations or generated statistically using algorithms based on the **Excursion Set Theory**.

The Excursion Set Theory, also known as Extended Press-Schechter (EPS) theory, provides a rigorous mathematical framework for understanding halo formation and resolving a key issue in the original **Press-Schechter (PS) formalism**. The original PS [ansatz](@entry_id:184384) attempted to calculate the fraction of mass in halos above a mass $M$ by simply counting all regions in the initial Gaussian density field whose smoothed overdensity, $\delta$, exceeded the critical threshold for [spherical collapse](@entry_id:161208), $\delta_c$. This simple count was found to systematically underestimate the collapsed mass by a factor of two. This discrepancy, known as the **cloud-in-cloud problem**, arises because the single-scale PS approach fails to account for mass in lower-density regions that are already embedded within larger, collapsed structures.

The Excursion Set Theory elegantly solves this problem by reframing it as a "[first-passage time](@entry_id:268196)" problem for a random walk [@problem_id:3486119]. Imagine tracking the density overdensity $\delta(S)$ for a given mass element as we smooth the field over progressively smaller scales (corresponding to increasing variance, $S$). For a sharp-$k$ space filter, this trajectory $\delta(S)$ executes a Markovian random walk. A mass element is considered to have collapsed into a halo of mass $M$ at the moment its trajectory first crosses the collapse barrier $\delta_c$ at the corresponding variance $S(M)$. This "first-crossing" condition correctly assigns every mass element to the largest halo to which it belongs, thereby resolving the cloud-in-cloud ambiguity. Using a mathematical tool known as the reflection principle, it can be shown that the total fraction of trajectories that have crossed the barrier by a given "time" $S$ is exactly twice the fraction that happen to be above the barrier at that instant. This provides a formal derivation for the ad-hoc factor of 2 in the original PS formula and yields a correctly normalized [halo mass function](@entry_id:158011).

#### The Internal Structure of Halos: The NFW Profile

Once the assembly history of halos is established, we must define their internal structure, as this sets the gravitational potential in which the [baryons](@entry_id:193732) evolve. High-resolution $N$-body simulations have revealed that virialized dark matter halos, regardless of their mass or formation time, exhibit a nearly universal density profile. This is most famously described by the **Navarro-Frenk-White (NFW) profile** [@problem_id:3486144].

The NFW [density profile](@entry_id:194142) is given by:
$$
\rho(r) = \frac{\rho_s}{\left(r/r_s\right)\left(1+r/r_s\right)^{2}}
$$
where $r_s$ is a characteristic **scale radius** and $\rho_s$ is a corresponding **scale density**. This profile features a shallow inner cusp, $\rho(r) \propto r^{-1}$, and a steep outer slope, $\rho(r) \propto r^{-3}$. The profile is fully specified by two parameters. These are often expressed in terms of the halo's virial mass, $M_{\rm vir}$, and its **concentration**, $c \equiv R_{\rm vir}/r_s$, where $R_{\rm vir}$ is the halo's virial radius.

The cumulative mass profile $M(r)$ for an NFW halo can be found by integrating the density profile over a spherical volume:
$$
M(r) = 4\pi \rho_s r_s^3 \left[ \ln\left(1+\frac{r}{r_s}\right) - \frac{r/r_s}{1+r/r_s} \right]
$$
This relation allows us to connect the profile parameters ($\rho_s, r_s$) to the halo's overall properties ($M_{\rm vir}, c$). Furthermore, the mass profile determines the **[circular velocity](@entry_id:161552) curve**, $V_c(r) = \sqrt{G M(r)/r}$, which characterizes the depth of the [potential well](@entry_id:152140) at any radius. A notable feature of the NFW profile is that the [circular velocity](@entry_id:161552) reaches a maximum value, $V_{\max}$, at a radius of approximately $r_{\max} \approx 2.163 \, r_s$ [@problem_id:3486144]. These properties—the gravitational potential and the characteristic velocities—are critical inputs for modeling the behavior of baryonic gas.

### The Baryonic Components: From Accretion to Stars

With the dark matter scaffolding in place, the "semi-analytic" part of the modeling begins. The core challenge is to model the complex, multi-scale physics of [baryons](@entry_id:193732)—gas, stars, and black holes. The fundamental justification for the semi-analytic approach lies in two key insights: the **separation of scales** and the **hierarchy of uncertainties** [@problem_id:3486145].

The evolution of a galaxy involves processes occurring on vastly different timescales. For instance, in a massive halo, the time it takes for hot gas to radiatively cool can be much longer than the dynamical time of the halo itself. A calculation for a typical Milky Way-like halo ($M_{\rm vir} \sim 10^{12} M_{\odot}$) reveals that the cooling time can be tens of gigayears, while the dynamical time is only around one gigayear [@problem_id:3486145]. This condition, $t_{\rm cool} \gg t_{\rm dyn}$, implies that the halo's hot gas atmosphere can be treated as a quasi-static reservoir that evolves slowly. This [separation of timescales](@entry_id:191220) justifies abstracting the complex fluid dynamics into a set of budget equations for integrated quantities.

This abstraction is further motivated by the hierarchy of uncertainties. While the gravitational dynamics of dark matter are well understood and can be simulated with high precision, the "subgrid" physics of [star formation](@entry_id:160356) and feedback is exceptionally complex and poorly constrained from first principles. SAMs embrace this reality by encapsulating this uncertain physics into parameterized, analytic recipes. This approach allows for efficient exploration of the vast [parameter space](@entry_id:178581) and enables the generation of large, statistical galaxy catalogs for comparison with observational surveys [@problem_id:3486145].

The architectural result is a system of coupled ordinary differential equations that track the flow of mass and metals between different baryonic reservoirs: hot halo gas, cold disk gas, stars in the disk and bulge, and an ejected component [@problem_id:3486075]. The following sections detail the principal modules that govern these flows.

#### Gas Accretion and Heating

As dark matter halos grow through accretion and mergers, they pull in baryonic gas from the surrounding [intergalactic medium](@entry_id:157642). In the standard picture for massive halos, this infalling gas passes through a strong **virial shock** near the halo's virial radius. This shock heats the gas to the halo's **virial temperature**, $T_{\rm vir}$, creating a hot, quasi-hydrostatic atmosphere that fills the halo.

The virial temperature is a direct measure of the depth of the halo's gravitational potential well. Assuming the hot gas is in hydrostatic equilibrium within an approximately isothermal potential, we can derive a fundamental relationship connecting the gas temperature to the halo's [circular velocity](@entry_id:161552), $V_c$. The balance between the outward pressure gradient and the inward gravitational force leads to the relation [@problem_id:3486091]:
$$
T_{\rm vir} = \frac{\mu m_p V_c^2}{2 k_B}
$$
where $\mu$ is the mean molecular weight of the gas, $m_p$ is the proton mass, and $k_B$ is the Boltzmann constant. This equation sets the initial thermal state of gas accreted into massive halos and is a cornerstone of all subsequent cooling calculations.

#### Radiative Cooling

Stars form from cold, dense gas, not from the hot, diffuse atmosphere at the virial temperature. Therefore, a critical step in galaxy formation is the [radiative cooling](@entry_id:754014) of this hot gas. The rate of cooling is governed by the gas's density, temperature, and chemical composition (metallicity). The local **cooling time**, $t_{\rm cool}(r)$, is defined as the ratio of the thermal energy density to the radiative loss rate per unit volume. For a hot plasma, this can be expressed as [@problem_id:3486156]:
$$
t_{\rm cool}(r) \propto \frac{T(r)}{\rho_g(r) \Lambda(T,Z)}
$$
where $T(r)$ is the temperature profile, $\rho_g(r)$ is the gas [density profile](@entry_id:194142), and $\Lambda(T,Z)$ is the **cooling function**, which encapsulates the microphysics of atomic radiation processes. This relation highlights two key dependencies:
1.  **Density:** Cooling is a two-body process, so its rate scales with density squared, making the cooling time inversely proportional to density ($t_{\rm cool} \propto 1/\rho_g$). Gas cools much faster in the dense central regions of halos.
2.  **Metallicity:** At the temperatures found in massive halos ($T > 10^6$ K), cooling is dominated by [line emission](@entry_id:161645) from [heavy elements](@entry_id:272514) (metals). The cooling function $\Lambda(T,Z)$ is therefore a strong increasing function of metallicity, $Z$. Higher metallicity gas cools much more efficiently, reducing its cooling time.

In SAMs, the cooling rate is typically calculated by defining a **cooling radius**, $r_{\rm cool}$. This is the radius within which the gas has had sufficient time to cool since it was last shock-heated. It is found by solving the equation $t_{\rm cool}(r_{\rm cool}) = t_{\rm avail}$, where $t_{\rm avail}$ is a characteristic timescale for the halo, such as its dynamical time or age. All the gas mass inside this radius is assumed to cool and accrete onto the central galaxy, providing fuel for [star formation](@entry_id:160356). If the cooling is very efficient such that $r_{\rm cool}$ exceeds the virial radius, the galaxy enters a **rapid cooling regime**, where gas inflow is limited only by the [free-fall time](@entry_id:261377) from the edge of the halo [@problem_id:3486156].

### Regulating Galaxy Growth: The Role of Feedback

Early models that included only gas accretion and cooling suffered from a significant flaw: the **overcooling problem**. They predicted that gas would cool far too efficiently, converting most of the baryons in the universe into stars at early times. This resulted in the formation of galaxies that were far more massive and star-filled than observed. The resolution to this crisis lies in **feedback**—energetic processes that regulate or halt gas cooling and star formation. Feedback mechanisms are broadly categorized by their energy source: [supernovae](@entry_id:161773) from massive stars, and accretion onto supermassive black holes.

#### Stellar Feedback from Supernovae

In lower-mass galaxies (like the Milky Way and smaller), the dominant feedback mechanism is energy and momentum injection from **[supernovae](@entry_id:161773) (SNe)**. Massive stars end their short lives in powerful explosions, which collectively can drive large-scale galactic winds. These winds can heat the surrounding interstellar medium (ISM) and eject gas from the galaxy, or even from the halo entirely.

In SAMs, the strength of this feedback is quantified by the **mass-loading factor**, $\eta$, defined as the ratio of the mass outflow rate to the [star formation](@entry_id:160356) rate: $\eta \equiv \dot{M}_{\rm out} / \dot{M}_{\star}$. A simple but powerful constraint on this process comes from [energy conservation](@entry_id:146975) [@problem_id:3486117]. The kinetic power of the outflow, $\frac{1}{2}\dot{M}_{\rm out}V_{\rm esc}^2$, cannot exceed the energy supplied by [supernovae](@entry_id:161773), which is proportional to the star formation rate. This leads to a maximum physically allowed mass-loading factor:
$$
\eta_{\max} = \frac{2 \epsilon_{\rm SN} E_{\rm SN}}{V_{\rm esc}^2}
$$
where $E_{\rm SN}$ is the total energy released by SNe per unit mass of stars formed, $\epsilon_{\rm SN}$ is the efficiency with which this energy couples to the ISM, and $V_{\rm esc}$ is the [escape velocity](@entry_id:157685) of the galaxy or halo. This equation immediately shows that $\eta_{\max} \propto V_{\rm esc}^{-2}$. It is much easier to drive powerful winds from the shallow potential wells of low-mass galaxies.

Many SAMs adopt a parameterization for the mass-loading factor that reflects this scaling, such as $\eta \propto V_c^{-2}$. However, a detailed [energy budget](@entry_id:201027) analysis reveals a significant tension: to match observations, the required values of $\eta$ are often so large that they would require more than 100% of the available SN energy. For instance, a common [model parameterization](@entry_id:752079) can require nearly 8 times the available energy budget, even assuming a generous coupling efficiency of $\epsilon_{\rm SN}=0.01$ [@problem_id:3486117]. This "energy crisis" for [stellar feedback](@entry_id:755431) suggests that simple energy-driven wind models are incomplete and that other factors, such as momentum injection or cosmic ray pressure, may play a crucial role.

#### Active Galactic Nucleus (AGN) Feedback

While SN feedback is effective in low-mass galaxies, it is insufficient to quench star formation in massive halos ($M_{\rm vir} \gtrsim 10^{12} M_{\odot}$). In these systems, the [gravitational potential](@entry_id:160378) well is too deep for SN-driven winds to escape, and a different mechanism is required to solve the overcooling problem. This role is filled by feedback from **Active Galactic Nuclei (AGN)**, powered by accretion onto the central [supermassive black hole](@entry_id:159956) (SMBH).

AGN feedback is typically implemented in two distinct modes, triggered by different physical conditions [@problem_id:3486114]:

1.  **Quasar Mode (or Bright/Radiative Mode):** This mode is associated with luminous quasars and is fueled by rapid, near-Eddington accretion of **cold gas** onto the SMBH. Such high accretion rates are typically triggered by violent dynamical events, like major galaxy mergers or disk instabilities, which cause large amounts of gas to lose angular momentum and funnel towards the galactic center. The immense radiative pressure from the accretion disk is thought to drive powerful, wide-angle winds that sweep through the galaxy's ISM, expelling the cold gas reservoir and thereby shutting down [star formation](@entry_id:160356).

2.  **Radio Mode (or Maintenance/Kinetic Mode):** This mode operates in massive halos that host a stable, quasi-static hot atmosphere (the regime where $t_{\rm cool} \gg t_{\rm dyn}$). Accretion onto the SMBH in this mode is not from cold gas flows but from the slow, quasi-spherical settling of the surrounding **hot halo gas**, often modeled by a Bondi-like accretion process. This accretion occurs at very low Eddington ratios ($\lambda_{\rm Edd} \ll 10^{-2}$). At such low rates, the accretion flow is believed to become radiatively inefficient and instead launch powerful, collimated [relativistic jets](@entry_id:159463). These jets inflate large bubbles or cavities in the hot halo gas, injecting energy that offsets [radiative cooling](@entry_id:754014) losses. This "maintenance" heating prevents the hot atmosphere from cooling and forming new stars, thus keeping massive galaxies "red and dead" [@problem_id:3486121].

The establishment of this radio mode is contingent on the ability of the halo to sustain a hot atmosphere. This requires that the energy input from gravitational accretion shocks is sufficient to balance or exceed the [radiative cooling](@entry_id:754014) losses, a condition that is met in massive halos where accretion shocks are strong [@problem_id:3486121].

### The Complete Picture: A Modular Architecture

In summary, a semi-analytic model is a modular computational framework built upon a dark matter merger tree. It evolves the baryonic content of galaxies by solving a system of coupled differential equations that describe the flow of mass and metals between various reservoirs [@problem_id:3486075]. The key modules and information flows include:

-   **Merger Trees:** Provide the halo mass growth history, $\dot{M}_{\rm vir}$, and merger events.
-   **Gas Accretion:** Infalling gas (proportional to $f_b \dot{M}_{\rm vir}$) is shock-heated and added to the **hot gas** reservoir.
-   **Cooling:** Gas cools from the hot reservoir at a rate $\dot{M}_{\rm cool}$ determined by the cooling radius, transferring mass and metals to the **cold gas** disk.
-   **Star Formation:** Cold gas is converted into **stars** at a rate $\dot{M}_{\star}$, typically modeled with a Kennicutt-Schmidt-style law ($\dot{M}_{\star} \propto M_{\rm cold}/t_{\rm dyn}$).
-   **Stellar Feedback:** Star formation drives winds that reheat or eject cold gas, with a mass-loading factor $\eta$ that depends on the halo's potential well depth. This moves gas from the cold reservoir back to the hot reservoir or into an **ejected** reservoir.
-   **AGN Feedback:** Accretion onto the central SMBH, triggered by either cold gas instabilities (quasar mode) or hot halo accretion (radio mode), injects energy that removes cold gas or prevents hot gas from cooling.
-   **Chemical Enrichment:** Stars produce metals, which are returned to the cold and hot gas reservoirs via [stellar evolution](@entry_id:150430) and feedback winds, affecting subsequent cooling rates.
-   **Morphology:** Major mergers can destroy disks and form stellar bulges, transferring stars from the disk component to the bulge component.

By coupling these physically motivated, parameterized recipes, SAMs can efficiently model the [co-evolution](@entry_id:151915) of dark matter halos and their resident galaxies, providing a powerful tool for interpreting large-scale galaxy surveys and testing our theoretical understanding of galaxy formation.