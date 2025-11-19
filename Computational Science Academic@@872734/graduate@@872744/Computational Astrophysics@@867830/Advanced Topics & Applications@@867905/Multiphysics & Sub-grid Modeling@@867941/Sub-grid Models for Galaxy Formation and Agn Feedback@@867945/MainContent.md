## Introduction
The formation and evolution of galaxies unfold across an immense range of physical scales, from the vast [cosmic web](@entry_id:162042) down to the accretion disks around individual black holes. This vast [dynamic range](@entry_id:270472) poses a fundamental problem for [computational astrophysics](@entry_id:145768): no single simulation can resolve all relevant physical processes simultaneously. To bridge this gap, astrophysicists rely on [sub-grid models](@entry_id:755588)—physically motivated recipes that encapsulate the net effects of unresolved physics on the scales that can be simulated. These models are the essential engine that allows simulations to connect the microphysics of star formation and black hole growth to the macroscopic properties of galaxies we observe.

This article provides a comprehensive overview of the [sub-grid models](@entry_id:755588) that are foundational to modern galaxy formation theory. Over the next three chapters, you will delve into the core concepts and practicalities of this critical field. The first chapter, **Principles and Mechanisms**, lays the groundwork by defining [sub-grid models](@entry_id:755588) and detailing the physics behind common prescriptions for star formation, [black hole accretion](@entry_id:159859), and feedback. The second chapter, **Applications and Interdisciplinary Connections**, explores how these models are tested, implemented, and used to interpret astronomical observations and [scaling relations](@entry_id:136850), touching on advanced numerical methods and surprising links to fields like control theory. Finally, **Hands-On Practices** will challenge you to apply these principles to solve idealized problems, solidifying your understanding of how these theoretical constructs are put into practice.

## Principles and Mechanisms

The vast dynamic range of galaxy formation, spanning from the cosmological scales of dark matter halos to the parsec scales of individual stars and [black hole accretion](@entry_id:159859) disks, presents a formidable challenge for numerical simulations. Even with state-of-the-art computational resources, it is impossible to resolve all relevant physical processes simultaneously within a large cosmological volume. Consequently, any process that occurs on scales smaller than the [resolution limit](@entry_id:200378) of the simulation—the so-called "sub-grid" scale—must be encapsulated in a physically motivated model. This chapter delves into the fundamental principles and common mechanisms of these essential [sub-grid models](@entry_id:755588), focusing on the formation of stars and the growth and feedback from supermassive black holes.

### The Rationale and Definition of Sub-Grid Models

At its core, a [cosmological hydrodynamics](@entry_id:747918) simulation solves a set of equations for the conservation of mass, momentum, and energy for a compressible, self-gravitating fluid. However, when these equations are averaged or filtered over a finite resolution element (a grid cell or a smoothed particle), new terms arise that represent the effects of unresolved, small-scale physics. For instance, in a Large Eddy Simulation (LES) framework, applying a spatial filter to the fluid equations introduces a **sub-grid stress tensor**, $\tau_{ij} = \overline{\rho u_i u_j} - \bar{\rho}\tilde{u}_i \tilde{u}_j$, which represents the [momentum transport](@entry_id:139628) by unresolved turbulent motions. Similarly, in a Reynolds-Averaged Navier-Stokes (RANS) framework, ensemble averaging introduces analogous **Reynolds stresses**. These terms do not have a [closed form](@entry_id:271343) in terms of the resolved (filtered or averaged) variables.

A **sub-grid model** is a physically motivated parameterization that provides a closure for these unclosed terms. It aims to represent the net effect of unresolved physics—such as turbulence, the structure of the multiphase interstellar medium (ISM), [star formation](@entry_id:160356), and feedback from [active galactic nuclei](@entry_id:158029) (AGN)—on the resolved scales. These models are expressed in terms of the resolved fluid quantities (like density $\rho$, temperature $T$, and velocity $\mathbf{u}$) and a set of calibrated parameters [@problem_id:3537578].

It is critical to distinguish a sub-grid model from a **numerical regularization** mechanism. Numerical regularization, such as the artificial viscosity used in [shock-capturing schemes](@entry_id:754786), is a mathematical device added at the discrete level to ensure the stability and accuracy of the numerical solver. Its form is dictated by the [discretization](@entry_id:145012) algorithm, not by a filtering of the continuum equations, and it is designed to vanish as the resolution increases. In contrast, a sub-grid model represents real physical processes that are simply unresolved. It is not a numerical artifact but an essential component of the physical model being simulated [@problem_id:3537578]. For example, injecting thermal energy to model AGN feedback is a sub-grid physical model, not a form of [artificial viscosity](@entry_id:140376), even though it may have a stabilizing effect on the gas.

### Modeling Star Formation

One of the most fundamental sub-grid processes is the conversion of interstellar gas into stars. Since individual stars cannot be resolved, simulations adopt a prescription that links the rate of [star formation](@entry_id:160356) to the properties of the gas in a given resolution element.

A widely used approach is the volumetric star formation law, which is based on the idea that star formation is regulated by gravity. The characteristic timescale for gravitational collapse is the **[free-fall time](@entry_id:261377)**, $t_{\mathrm{ff}}$, which for a uniform sphere of density $\rho$ is given by $t_{\mathrm{ff}} = \sqrt{3\pi/(32G\rho)}$. The sub-grid model posits that a certain fraction of the gas in a cell, denoted by the efficiency parameter $\epsilon_{\mathrm{ff}}$, is converted into stars per [free-fall time](@entry_id:261377). This yields a volumetric [star formation](@entry_id:160356) rate density $\dot{\rho}_\star$ [@problem_id:3537567]:

$$
\dot{\rho}_\star = \epsilon_{\mathrm{ff}} \frac{\rho}{t_{\mathrm{ff}}}
$$

Substituting the expression for $t_{\mathrm{ff}}$, we find that this law predicts a strong dependence on gas density:

$$
\dot{\rho}_\star = \epsilon_{\mathrm{ff}} \rho \left( \frac{32G\rho}{3\pi} \right)^{1/2} \propto \rho^{3/2}
$$

In practice, [star formation](@entry_id:160356) does not occur everywhere. It is confined to the coldest, densest regions of the ISM. To mimic this, [sub-grid models](@entry_id:755588) typically impose a **density threshold**, $n_{\mathrm{H,th}}$, such that the star formation law is only applied to gas cells with a density exceeding this value. This threshold acts as a crucial "gate," determining which gas is eligible to form stars and providing a key parameter for calibrating the overall [star formation](@entry_id:160356) rate of a simulated galaxy [@problem_id:3537567].

This local, volumetric law should be contrasted with the empirical **Schmidt-Kennicutt (SK) relation**, which is an observational correlation between the [star formation](@entry_id:160356) rate *[surface density](@entry_id:161889)* ($\Sigma_{\mathrm{SFR}}$) and the gas *[surface density](@entry_id:161889)* ($\Sigma_{\mathrm{gas}}$) averaged over kiloparsec scales. The SK relation is typically a power law, $\Sigma_{\mathrm{SFR}} \propto \Sigma_{\mathrm{gas}}^N$ with $N \approx 1.4$. In a successful simulation, the SK relation should emerge as a consequence of the interplay between the local sub-grid star formation law and feedback processes, rather than being imposed directly.

### Modeling Supermassive Black Holes and Their Growth

The evolution of massive galaxies is inextricably linked to the [supermassive black holes](@entry_id:157796) (SMBHs) at their centers. Modeling their origin, growth, and feedback is a cornerstone of modern galaxy formation theory.

#### Black Hole Seeding

Cosmological simulations must have a mechanism to introduce the first SMBHs, as their formation pathways are not fully understood and occur at scales far below the [resolution limit](@entry_id:200378). This is accomplished through **black hole seeding** prescriptions. Two common strategies are:

1.  **Halo-Mass-Threshold Seeding**: This is a phenomenological approach where a BH seed of a fixed mass (e.g., $M_{\mathrm{seed}} = 10^5 M_\odot$) is placed at the [gravitational potential](@entry_id:160378) minimum of a dark matter halo once the halo's total mass exceeds a certain threshold (e.g., $M_{\mathrm{h,seed}} = 5 \times 10^{10} M_\odot$). An exclusivity condition prevents seeding in halos that already contain a BH. This method is numerically robust because massive halos are well-resolved, making their identification and potential minimum stable. However, it is not directly tied to the physical conditions of gas collapse [@problem_id:3537634].

2.  **Gas-Collapse Seeding**: This is a more physically motivated approach that attempts to capture the conditions for the direct collapse of a massive primordial gas cloud into a BH. A gas element is converted into a BH seed if it satisfies a set of local criteria, such as exceeding a density threshold, having a short cooling time, and possessing very low metallicity. While more physically plausible, this method is highly sensitive to the simulation's resolution. For instance, if the physical scale of [gravitational instability](@entry_id:160721), the **Jeans length** $\lambda_J$, is smaller than the [gravitational softening](@entry_id:146273) length $\epsilon$ of the simulation, the collapse can be artificially suppressed by numerical effects. This can delay or even prevent BH seeding. Furthermore, without additional constraints, this method can spuriously create multiple BHs in a single collapsing region [@problem_id:3537634].

#### Accretion Models

Once seeded, a BH grows by accreting surrounding gas. The accretion rate $\dot{M}$ must be estimated from the resolved gas properties. The choice of model depends critically on the assumed physics of the inflow, particularly the role of angular momentum.

*   **Bondi-Hoyle-Lyttleton (BHL) Accretion**: This model describes the [gravitational capture](@entry_id:174700) of gas from a relatively homogeneous, quasi-spherical medium with negligible net angular momentum. The accretion rate is determined by the gas density $\rho_\infty$, sound speed $c_s$, and the bulk velocity of the gas relative to the BH, $v_\infty$. The canonical formula is:
    $$
    \dot{M}_{\mathrm{BHL}} = \alpha \frac{4\pi G^2 M_\bullet^2 \rho_\infty}{(c_s^2 + v_\infty^2)^{3/2}}
    $$
    where $M_\bullet$ is the BH mass and $\alpha$ is a dimensionless factor. This model is computationally inexpensive but may be unrealistic in galactic centers where gas is typically rotationally supported [@problem_id:3537573].

*   **Torque-Limited Accretion**: In reality, gas with angular momentum cannot flow directly onto the BH. It settles into a rotationally supported disk. Inflow can only proceed if torques act to remove angular momentum from the gas, transporting it outwards. Torque-limited models assume that the accretion rate is governed by the efficiency of these torques. In simulations, such torques can be generated by non-axisymmetric gravitational potentials, like stellar bars or [spiral arms](@entry_id:160156) within an unstable gas disk. The thermodynamics of the gas play a key role by controlling the disk's stability (e.g., via the Toomre $Q$ parameter), which in turn determines the strength of the instabilities that drive the torques [@problem_id:3537573].

### Implementing Feedback Mechanisms

Feedback—the injection of energy and momentum from stars and AGN into the surrounding gas—is the critical process that regulates galaxy growth. Its implementation is a central challenge for sub-grid modeling.

#### Stellar Feedback: Radiation Pressure

While [supernovae](@entry_id:161773) are a well-known [stellar feedback](@entry_id:755431) channel, the radiation emitted by young, [massive stars](@entry_id:159884) can also be very effective, especially in dusty environments. The [momentum flux](@entry_id:199796) from a source of luminosity $L$ is $L/c$. When photons are absorbed or scattered by dust grains, they transfer this momentum to the gas.

The total momentum deposition rate, $\dot{p}$, depends on the optical depth of the medium.
*   In the **optically thin** or **single-scattering limit**, each photon is absorbed at most once. The momentum deposited is simply the [momentum flux](@entry_id:199796) of the absorbed photons. For a source of UV photons and a medium with UV optical depth $\tau_{\rm UV}$, this is $\dot{p}_{\rm UV} = (1 - e^{-\tau_{\rm UV}}) \frac{L}{c}$ [@problem_id:3537564].
*   In the **optically thick limit**, the situation is more complex. The absorbed UV photons are re-radiated by dust in the infrared (IR). If the medium is also optically thick to this IR radiation ($\tau_{\rm IR} > 1$), the IR photons become "trapped." They are absorbed and re-emitted multiple times before escaping, depositing their momentum with each absorption. This leads to a significant boost in the total momentum coupled to the gas. A common sub-grid prescription for the total momentum deposition rate combines both effects:
    $$
    \dot{p} \approx \left(1 - e^{-\tau_{\rm UV}}\right) \frac{L}{c} + \tau_{\rm IR} \frac{L}{c}
    $$
    For a very optically thick cloud where $\tau_{\rm UV} \gg 1$ and all initial luminosity is converted to IR, this simplifies to $\dot{p} \approx (1 + \tau_{\rm IR}) \frac{L}{c}$. This shows that in dense, dusty regions, [radiation pressure](@entry_id:143156) can be boosted far beyond the single-scattering limit, providing a powerful feedback mechanism [@problem_id:3537564].

#### The AGN Feedback Dichotomy: Quasar and Radio Modes

AGN feedback is often implemented using a two-mode model, motivated by observations and accretion disk theory. The [dominant mode](@entry_id:263463) is determined by the BH's accretion rate relative to its theoretical maximum, the **Eddington rate**, $\dot{M}_{\mathrm{Edd}}$. The ratio is known as the **Eddington ratio**, $\lambda \equiv \dot{M}/\dot{M}_{\mathrm{Edd}}$.

1.  **Quasar Mode (or Thermal/Radiative Mode)**: This mode operates at high accretion rates ($\lambda \gtrsim \lambda_{\mathrm{crit}}$, where $\lambda_{\mathrm{crit}} \sim 0.01-0.1$). Accretion is radiatively efficient, proceeding through a geometrically thin, optically thick disk. A fraction of the enormous luminosity couples to the surrounding gas, primarily as isotropic thermal heating or radiation-driven winds. This mode is thought to be responsible for expelling large amounts of gas from galaxies during their most active growth phases, which typically occur in gas-rich, cold, and dense environments like those found during galaxy mergers [@problem_id:3537579].

2.  **Radio Mode (or Kinetic/Jet Mode)**: This mode dominates at low accretion rates ($\lambda \lesssim \lambda_{\mathrm{crit}}$). Accretion is radiatively inefficient, likely occurring via a geometrically thick, optically thin flow (like an Advection-Dominated Accretion Flow, or ADAF). This state is associated with the launching of powerful, collimated [relativistic jets](@entry_id:159463). The feedback energy is coupled mechanically to the gas, inflating large bubbles or cavities in the surrounding medium. This mode is prevalent in massive galaxies residing in the hot, dilute gas of galaxy groups and clusters, where it is thought to be the primary agent that prevents catastrophic cooling and runaway star formation (the "cool-core problem") [@problem_id:3537579].

#### Advanced Feedback Channels: Cosmic Rays

More recent models have begun to incorporate **[cosmic rays](@entry_id:158541) (CRs)** as a distinct feedback channel. In these models, a fraction of the total AGN feedback power, $\dot{E}_{\mathrm{fb}} = \epsilon_f \epsilon_r \dot{M}_{\mathrm{BH}} c^2$, is injected into a CR fluid component, distinct from the thermal gas [@problem_id:3537575]. This CR fluid is characterized by a relativistic [equation of state](@entry_id:141675) ($P_{\mathrm{CR}} = (\gamma_{\mathrm{CR}}-1)e_{\mathrm{CR}}$ with $\gamma_{\mathrm{CR}}=4/3$) and provides an additional source of non-thermal pressure support.

The crucial physics of CR feedback lies in its transport. Unlike thermal energy, which can be quickly radiated away, CRs are long-lived and transport energy differently. Their motion is tied to magnetic field lines, leading to two primary transport mechanisms:
*   **Anisotropic Diffusion**: CRs diffuse rapidly along magnetic field lines (with diffusion coefficient $\kappa_\parallel$) but very slowly across them ($\kappa_\perp \ll \kappa_\parallel$).
*   **Streaming**: CRs can stream down their own pressure gradient along magnetic field lines at a speed limited by the local **Alfvén speed**, $v_A = B/\sqrt{4\pi\rho}$. This streaming is not lossless; the interaction with the background plasma that limits the streaming speed also transfers energy and momentum from the CRs to the thermal gas, resulting in **streaming heating**.

This complex transport allows CRs to carry energy from the galactic center to the [circumgalactic medium](@entry_id:747361), providing a less violent but more persistent form of feedback compared to purely thermal or kinetic injections.

### Numerical Implementation, Convergence, and Calibration

The practical use of [sub-grid models](@entry_id:755588) requires careful attention to numerical consistency and an understanding of how model parameters are constrained.

#### Energy Conservation and Double Counting

A subtle but critical issue arises when a sub-grid model for a multiphase ISM is used alongside explicit feedback injection. Some ISM models use an **effective [equation of state](@entry_id:141675) (EOS)**, where the pressure is augmented to account for unresolved turbulence or a hot gas phase, e.g., $P = (\gamma-1)\rho(u + u_{\mathrm{EOS}})$. Here, $u$ is the resolved specific internal energy and $u_{\mathrm{EOS}}$ is a term representing unresolved pressure support [@problem_id:3537574].

If a feedback event is modeled by both explicitly adding energy $E_{\mathrm{fb}}$ to the resolved internal energy $u$, and also increasing the sub-grid pressure term $u_{\mathrm{EOS}}$ to reflect the creation of a multiphase medium, the same energy has been accounted for twice. This violates [energy conservation](@entry_id:146975). The correct procedure is to ensure that the total injected energy $E_{\mathrm{fb}}$ is partitioned. If a change $\Delta u_{\mathrm{EOS}}$ is attributed to the feedback, the energy added to the resolved component must be reduced accordingly: $E_{\mathrm{fb}}^{\mathrm{net}} = E_{\mathrm{fb}} - m \Delta u_{\mathrm{EOS}}$, where $m$ is the mass of the gas cell. This ensures the total [energy budget](@entry_id:201027) is respected [@problem_id:3537574].

#### Convergence and Parameter Renormalization

The presence of [sub-grid models](@entry_id:755588) complicates the standard notion of numerical convergence.

*   **Strong Convergence** refers to the ideal case where simulation results for a given observable converge to a unique answer as resolution is increased, using a *fixed* set of sub-grid parameters.
*   **Weak Convergence** describes the more common situation where convergence is only achieved if the sub-grid parameters are systematically adjusted with resolution. This adjustment is known as **renormalization** [@problem_id:3537623].

Weak convergence is often necessary because the implementation of sub-grid physics can have an inherent dependence on the resolution scale. For example, consider a thermal feedback model that injects a fixed amount of energy $E_{\mathrm{feed}} \propto \epsilon_f$ into a fixed number of neighboring gas cells, whose total mass is $M_{\mathrm{heat}} \propto m_{\mathrm{gas}}$. The resulting temperature increase is $\Delta T \propto E_{\mathrm{feed}} / M_{\mathrm{heat}} \propto \epsilon_f / m_{\mathrm{gas}}$. If one refines the simulation, $m_{\mathrm{gas}}$ decreases. To achieve the same physical temperature jump $\Delta T$, which might be the desired physical outcome, the parameter $\epsilon_f$ must be scaled down in proportion to $m_{\mathrm{gas}}$. This renormalization, $\epsilon_f(m_{\mathrm{gas}}) \propto m_{\mathrm{gas}}$, is a key strategy for achieving [weak convergence](@entry_id:146650) [@problem_id:3537623].

#### Model Calibration and Parameter Constraints

Sub-grid models contain free parameters (e.g., star formation efficiency $\epsilon_{\mathrm{ff}}$, AGN coupling efficiency $\epsilon_f$, BH accretion boost factor $\beta$) that are not known from first principles. These must be **calibrated** by requiring that the simulation reproduces a set of key astrophysical observations.

Important calibration targets include:
*   The **Stellar-to-Halo Mass Relation (SHMR)**, which connects the [stellar mass](@entry_id:157648) of a galaxy to the mass of its [dark matter halo](@entry_id:157684). This is highly sensitive to the efficiency of [stellar feedback](@entry_id:755431), which regulates star formation in low-mass halos, and AGN feedback, which quenches star formation in massive halos.
*   The **$M_\bullet$-$\sigma$ Relation**, a tight correlation between a galaxy's central SMBH mass ($M_\bullet$) and the velocity dispersion ($\sigma$) of its bulge. This is a primary constraint on models of BH growth and AGN feedback self-regulation.
*   **Galaxy Cluster Entropy Profiles**, which measure the thermal state of the hot gas in clusters. AGN feedback is the leading candidate for injecting the non-[gravitational energy](@entry_id:193726) required to prevent "cool cores" from collapsing, making these profiles powerful probes of the radio-mode feedback history.

Different [observables](@entry_id:267133) have different sensitivities to the sub-grid parameters. A successful calibration effort requires using a combination of observables that can break the degeneracies between parameters. For example, while both the $M_\bullet$-$\sigma$ relation and cluster entropy profiles are sensitive to AGN feedback efficiency, their different dependencies on accretion and coupling physics allow them to be used together to constrain both aspects of the AGN model. Similarly, the SHMR is often the most direct constraint on [stellar feedback](@entry_id:755431) efficiency [@problem_id:3537555]. The process of running large suites of simulations to explore this parameter space and find a model that simultaneously matches multiple observations is a central activity in the field of computational galaxy formation.