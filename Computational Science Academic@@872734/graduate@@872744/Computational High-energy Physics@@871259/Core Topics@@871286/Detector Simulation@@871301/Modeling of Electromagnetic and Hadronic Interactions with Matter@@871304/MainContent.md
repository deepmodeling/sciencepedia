## Introduction
Understanding the journey of a high-energy particle through matter is fundamental to modern physics. Every [particle detector](@entry_id:265221), every analysis of cosmic rays, and every radiation shielding design relies on predicting how particles will interact, lose energy, and create secondary particles as they traverse a medium. The challenge lies in translating the complex, probabilistic rules of the quantum world into robust, computationally tractable models that can describe macroscopic phenomena. This article bridges that gap by providing a comprehensive overview of the physics and computational methods used to model electromagnetic and hadronic interactions.

The first chapter, "Principles and Mechanisms," establishes the theoretical foundation, beginning with the core concept of the interaction [cross section](@entry_id:143872) and progressing through the distinct energy loss mechanisms for heavy charged particles, electrons, photons, and hadrons. It culminates in a discussion of the collective behavior of particle cascades, contrasting the properties of compact electromagnetic showers with complex hadronic ones. The second chapter, "Applications and Interdisciplinary Connections," explores how these principles are put into practice, detailing their central role in the design of [particle detectors](@entry_id:273214) like calorimeters, the analysis of astrophysical air showers, and the engineering of accelerator components. Finally, "Hands-On Practices" provides opportunities to engage directly with the material through guided computational problems. We begin our exploration with the fundamental principles that govern this intricate dance between particle and matter.

## Principles and Mechanisms

The journey of a particle through matter is a complex narrative of successive interactions, each governed by the fundamental forces of nature. Modeling this journey requires a framework that is both physically rigorous and computationally tractable. This chapter lays out the core principles and mechanisms that govern these interactions, starting from the elementary concept of a cross section and building up to the intricate dynamics of particle showers and their simulation.

### Fundamental Concepts of Particle Interactions

At the heart of all particle interactions lies the concept of the **[cross section](@entry_id:143872)**, a probabilistic measure of the likelihood of an interaction. This concept provides the essential link between the microscopic quantum world and the macroscopic phenomena of particle attenuation and energy loss.

#### Cross Sections and the Attenuation of Particle Beams

Imagine a monoenergetic, collimated beam of particles with intensity $I$ (particles per unit area per unit time) incident upon a thin slab of material. The fundamental quantity that governs the interaction probability is the **microscopic [cross section](@entry_id:143872)**, denoted by $\sigma$. This quantity has the dimensions of area and can be interpreted as the effective target area that a single atom or nucleus presents to an incident particle for a specific type of interaction. If the particle's trajectory passes through this area, an interaction occurs. The value of $\sigma$ depends on the type and energy of the incident particle, the nature of the target, and the specific interaction channel (e.g., elastic scattering, absorption).

In a material with a [number density](@entry_id:268986) of $n$ targets per unit volume, the total [effective area](@entry_id:197911) per unit volume is $n\sigma$. This product defines the **macroscopic cross section**, $\Sigma$:

$$
\Sigma = n\sigma
$$

The macroscopic [cross section](@entry_id:143872) has dimensions of inverse length and represents the probability of an interaction occurring per unit path length traveled by a particle in the medium. The reciprocal of the macroscopic [cross section](@entry_id:143872) defines another crucial quantity, the **mean free path**, $\lambda$:

$$
\lambda = \frac{1}{\Sigma} = \frac{1}{n\sigma}
$$

The mean free path is the average distance a particle travels between interactions in the medium.

These definitions allow us to derive the fundamental law of particle beam attenuation. Consider the change in beam intensity, $dI$, as it traverses an infinitesimally thin slab of thickness $dx$. The number of particles removed from the beam is proportional to the incident intensity $I(x)$ and the thickness $dx$. The constant of proportionality is the macroscopic cross section $\Sigma$. This leads to the differential equation:

$$
dI = -I(x) \Sigma \, dx
$$

Solving this equation with the initial condition $I(x=0) = I_0$ yields the celebrated **exponential attenuation law**, also known as the Beer-Lambert law:

$$
I(x) = I_0 \exp(-x/\lambda)
$$

This law states that the intensity of a monoenergetic beam decreases exponentially as it penetrates the material. The underlying assumption of independent, random interaction events implies that the number of interactions over a given path length follows a Poisson distribution. Consequently, the distribution of free paths—the distance a particle travels to its first interaction—is an [exponential distribution](@entry_id:273894) with a mean value of $\lambda$. This statistical foundation is a cornerstone of particle transport modeling [@problem_id:3522969].

#### The Optical Theorem: Linking Scattering and Total Interaction Rate

The total interaction probability is composed of different processes. The **total [cross section](@entry_id:143872)** ($\sigma_{\text{tot}}$) is the sum of the **elastic cross section** ($\sigma_{\text{el}}$) and the **inelastic cross section** ($\sigma_{\text{inel}}$).

$$
\sigma_{\text{tot}} = \sigma_{\text{el}} + \sigma_{\text{inel}}
$$

Elastic scattering changes the particle's direction but preserves its internal state and kinetic energy (in the [center-of-mass frame](@entry_id:158134)). Inelastic processes include all other possibilities, such as absorption of the particle or the creation of new particles. In the language of quantum scattering theory, the asymptotic wavefunction for an elastic scattering process is described by an incident [plane wave](@entry_id:263752) and an [outgoing spherical wave](@entry_id:201591): $\psi(\mathbf{r}) \sim e^{ikz} + f(\theta)\frac{e^{ikr}}{r}$. The quantity $f(\theta)$ is the **scattering amplitude**, and the differential elastic [cross section](@entry_id:143872) is given by $|f(\theta)|^2$. The total elastic [cross section](@entry_id:143872) is the integral over all solid angles: $\sigma_{\text{el}} = \int |f(\theta)|^2 \, d\Omega$.

A profound and non-trivial result from quantum mechanics, known as the **Optical Theorem**, provides a direct link between the total [cross section](@entry_id:143872) and the scattering amplitude in the forward direction ($\theta=0$). For [short-range interactions](@entry_id:145678), it states:

$$
\sigma_{\text{tot}} = \frac{4\pi}{k} \text{Im}[f(0)]
$$

Here, $k$ is the wave number of the incident particle and $\text{Im}[f(0)]$ is the imaginary part of the [forward scattering amplitude](@entry_id:154109). This theorem is a direct consequence of the conservation of probability (or the unitarity of the S-matrix). It expresses the fact that any particle removed from the forward-going beam, whether by scattering to other angles or by inelastic absorption, must manifest as a reduction in the amplitude of the forward-propagating wave. This manifests as a non-zero imaginary part of the [forward scattering amplitude](@entry_id:154109) [@problem_id:3523048].

It is important to note that for charged particles, the long-range Coulomb interaction complicates this picture. The standard formulation of the [optical theorem](@entry_id:140058) assumes [short-range forces](@entry_id:142823). To apply it to hadron-nucleus scattering, for example, one must use a more sophisticated formalism involving Coulomb-distorted waves to properly isolate the short-range nuclear scattering amplitude [@problem_id:3523048].

### Electromagnetic Interactions

Electromagnetic interactions are ubiquitous for charged particles and photons traversing matter. The nature of these interactions, however, depends critically on the type of particle and its energy.

#### Interactions of Heavy Charged Particles

For charged particles significantly heavier than an electron (such as muons, [pions](@entry_id:147923), protons, and heavier ions), the dominant energy loss mechanism at energies up to hundreds of GeV is [ionization](@entry_id:136315) and excitation of the atoms in the medium. This rate of energy loss per unit path length, $-dE/dx$, is known as the **[stopping power](@entry_id:159202)**.

The quintessential description of this process is the **Bethe-Bloch formula**. For a heavy particle with charge $ze$ and velocity $\beta c = v$, traversing a medium with atomic number $Z$, atomic mass $A$, and density $\rho$, the mean energy loss is given by:

$$
- \frac{dE}{dx} = K \frac{z^2 Z}{A} \frac{\rho}{\beta^2} \left[ \frac{1}{2} \ln\left(\frac{2 m_e c^2 \beta^2 \gamma^2 T_{\text{max}}}{I^2}\right) - \beta^2 - \frac{\delta(\beta\gamma)}{2} - \frac{C}{Z} \right]
$$

where $K = 4 \pi N_A r_e^2 m_e c^2$ is a collection of physical constants, $\gamma = (1-\beta^2)^{-1/2}$ is the Lorentz factor, and $m_e$ is the electron mass [@problem_id:3522992]. Let's dissect the physical meaning of each term:

*   **Overall Scaling**: The [stopping power](@entry_id:159202) is proportional to the square of the projectile's charge ($z^2$) and the electron density of the medium (proportional to $Z\rho/A$). The $1/\beta^2$ factor signifies that a faster particle spends less time near any given atom, transferring less impulse and thus losing less energy per unit distance.

*   **Logarithmic Term**: This term arises from integrating the [energy transfer](@entry_id:174809) over all possible impact parameters, from distant, gentle collisions to close, violent ones. It is bounded by two scales: the **[mean excitation energy](@entry_id:160327)** ($I$), which represents the average energy required to ionize an atom in the medium, and the maximum possible kinetic energy transferred to an electron in a single collision, $T_{\text{max}}$. This term is responsible for the characteristic "[relativistic rise](@entry_id:157811)" of the [stopping power](@entry_id:159202), as it increases with $\ln(\gamma^2)$.

*   **Correction Terms**: The basic formula is refined by three crucial corrections:
    1.  The $-\beta^2$ term is a relativistic kinematic correction that moderates the logarithmic rise.
    2.  The **[shell correction](@entry_id:754768)** ($-C/Z$) becomes important at low energies, when the projectile's velocity is comparable to the orbital velocities of the inner-shell (K, L) electrons. These tightly bound electrons are less likely to be excited, reducing the [stopping power](@entry_id:159202) relative to the simple theory which assumes they are free.
    3.  The **[density effect correction](@entry_id:748309)** ($-\delta(\beta\gamma)/2$) is significant at very high energies. The projectile's electric field polarizes the medium, which shields the field felt by atoms far from the particle's path. This reduces the contribution of distant collisions and causes the [relativistic rise](@entry_id:157811) to saturate, reaching a "Fermi plateau".

In addition to losing energy, charged particles are deflected by the Coulomb fields of the nuclei. While a single large-angle scatter is possible, the trajectory is typically dominated by the cumulative effect of a vast number of small-angle deflections. This process is known as **Multiple Coulomb Scattering (MCS)**. The [central limit theorem](@entry_id:143108) suggests that the distribution of the total projected deflection angle after traversing a certain thickness should be approximately Gaussian. However, the underlying Rutherford [scattering cross section](@entry_id:150101) has a long power-law tail ($\propto \theta^{-4}$), which gives rise to significant non-Gaussian tails in the distribution, corresponding to rare, larger-angle scatters.

A widely used empirical formula that captures the width of the central Gaussian core of the projected scattering angle distribution is the **Highland parametrization**:

$$
\theta_0 \approx \frac{13.6\,\mathrm{MeV}}{\beta p} z \sqrt{\frac{x}{X_0}}\left[1+0.038\ln\left(\frac{x}{X_0}\right)\right]
$$

This formula shows that the RMS scattering angle $\theta_0$ is inversely proportional to the particle's momentum $p$ (stiffer particles deflect less) and grows with the square root of the thickness $x$ measured in units of radiation length $X_0$ (a characteristic of a [random walk process](@entry_id:171699)) [@problem_id:3522983].

#### Interactions of Electrons and Positrons

While electrons also lose energy through ionization, their small mass means that another process, radiative energy loss or **bremsstrahlung**, becomes critically important at much lower energies compared to heavy particles. Bremsstrahlung is the emission of photons (X-rays) by an electron as it is deflected and accelerated in the Coulomb field of an atomic nucleus.

At high energies ($E \gg m_e c^2$), the average rate of radiative energy loss is approximately proportional to the electron's own energy:

$$
\left( -\frac{dE}{dx} \right)_{\text{rad}} \approx \frac{E}{X_0}
$$

This relation defines one of the most important parameters in high-energy physics, the **radiation length ($X_0$)**. It is the mean distance over which a high-energy electron loses all but $1/e$ of its energy to bremsstrahlung. It is a material-dependent property that scales roughly as $X_0 \propto A / (\rho Z^2)$.

The total energy loss for an electron is the sum of collisional and radiative losses. Since collisional loss is only logarithmically dependent on energy, while radiative loss is linearly dependent, there must be an energy at which the two are equal. This is the **[critical energy](@entry_id:158905) ($E_c$)**:

$$
\left( -\frac{dE}{dx} \right)_{\text{rad}} \bigg|_{E=E_c} = \left( -\frac{dE}{dx} \right)_{\text{coll}}
$$

The [critical energy](@entry_id:158905) marks the transition between two distinct regimes of electron behavior. For $E \ll E_c$, [ionization](@entry_id:136315) dominates, and the electron behaves much like a heavy charged particle. For $E \gg E_c$, bremsstrahlung dominates, and the electron's energy decreases exponentially with distance, on average [@problem_id:3522987].

#### Interactions of Photons

Unlike charged particles, photons are neutral and interact with matter through discrete, "all-or-nothing" events that remove the photon from the beam entirely. The total attenuation coefficient for photons is the sum of contributions from three main processes, each dominating in a different energy range [@problem_id:3523027]:

1.  **Photoelectric Effect**: At low energies (keV to hundreds of keV), a photon is absorbed by a bound atomic electron, ejecting it from the atom. The cross section for this process is strongly dependent on the [atomic number](@entry_id:139400) of the medium, scaling approximately as $\sigma_{\text{pe}} \propto Z^5$, and decreases rapidly with increasing photon energy, roughly as $E^{-7/2}$. The strong $Z$ dependence makes high-Z materials like lead excellent shields for low-energy X-rays.

2.  **Compton Scattering**: In the intermediate energy range (hundreds of keV to several MeV), the dominant process is [incoherent scattering](@entry_id:190180) off a quasi-free atomic electron. The photon transfers some of its energy to the electron and continues in a different direction with lower energy. Since every electron in the atom can participate, the [cross section](@entry_id:143872) scales linearly with the number of electrons, $\sigma_{\text{C}} \propto Z$. The cross section, described by the Klein-Nishina formula, decreases with increasing energy.

3.  **Pair Production**: Above a [threshold energy](@entry_id:271447) of $E_{\gamma} = 2m_e c^2 \approx 1.022 \text{ MeV}$, a photon can convert into an electron-positron pair in the strong Coulomb field of a nucleus. This process becomes dominant at high energies (above ~10 MeV). The [cross section](@entry_id:143872) scales with the square of the nuclear charge, $\sigma_{\text{pp}} \propto Z^2$, and rises from the threshold, eventually leveling off at very high energies. Notably, the high-energy [mean free path](@entry_id:139563) for [pair production](@entry_id:154125) is directly related to the radiation length, $\lambda_{\text{pair}} \approx \frac{9}{7} X_0$, establishing $X_0$ as the fundamental length scale for high-energy electromagnetic interactions for both electrons and photons [@problem_id:3522987].

### Hadronic and Electroweak Interactions

While electromagnetic interactions govern the behavior of a wide range of particles, the interactions of hadrons (protons, neutrons, [pions](@entry_id:147923), etc.) are dominated by the [strong nuclear force](@entry_id:159198).

#### General Characteristics of Hadronic Interactions

Inelastic hadronic interactions are characterized by a mean free path known as the **nuclear interaction length ($\lambda_I$)**. This is the average distance a high-energy [hadron](@entry_id:198809) travels before undergoing a non-[elastic collision](@entry_id:170575) with a nucleus. In most materials, $\lambda_I$ is significantly larger than the radiation length $X_0$. For example, in lead, $\lambda_I \approx 17.1$ cm, whereas $X_0 \approx 0.56$ cm. This disparity in length scales is a key principle in the design of [particle detectors](@entry_id:273214), allowing for the separation of electromagnetic and hadronic components of a [particle shower](@entry_id:753216) [@problem_id:3522989].

#### High-Energy Muon Energy Loss

Muons are leptons and do not participate in the strong interaction. However, being 207 times heavier than electrons, their [critical energy](@entry_id:158905) is much higher. Consequently, ionization remains the dominant energy loss mechanism up to several hundred GeV. At TeV energies and beyond, radiative processes become significant. The total [stopping power](@entry_id:159202) for a high-energy muon is often modeled as:

$$
-\frac{dE}{dX} = a(E) + b(E)E
$$

where $X$ is the mass thickness (in g/cm$^2$), $a(E)$ represents the nearly constant ionization loss, and $b(E)E$ represents the sum of three radiative processes [@problem_id:3523008]:
1.  **Bremsstrahlung**: Similar to electrons, but suppressed by a factor of $(m_e/m_{\mu})^2$.
2.  **Direct Pair Production**: The muon's virtual photon field creates an $e^+e^-$ pair in the field of a nucleus. This is a dominant radiative process for muons at TeV energies.
3.  **Photonuclear Interactions**: The muon interacts with a nucleus via the exchange of a virtual photon, which then interacts hadronically. This process becomes increasingly important at multi-TeV energies.

The [critical energy](@entry_id:158905) for muons in materials like rock or iron is around 500 GeV, marking the crossover from an [ionization](@entry_id:136315)-dominated to a radiation-dominated energy loss regime [@problem_id:3523008].

#### High-Energy Hadron-Nucleus Interactions

At very high energies, the quantum nature of the proton and its interactions becomes manifest in uniquely nuclear phenomena like shadowing and diffraction. A key concept is the **[coherence length](@entry_id:140689)**, $l_c$, which is the distance over which a virtual [quantum fluctuation](@entry_id:143477) of the projectile [hadron](@entry_id:198809) can persist. At high energies, $l_c$ can become much larger than the diameter of a nucleus. This means the projectile interacts coherently with multiple nucleons simultaneously.

*   **Nuclear Shadowing**: When the projectile is viewed as a superposition of configurations with different interaction cross sections, the larger-sized (and thus larger-cross-section) components are filtered out by the nucleons on the front face of the nucleus. This "shadows" the nucleons at the back, reducing the total cross section to a value significantly less than the incoherent sum $A\sigma_{pN}$.

*   **Diffractive Dissociation**: The fact that the projectile has a fluctuating internal structure leads to diffraction. In the **Good-Walker picture**, the projectile is a superposition of [eigenstates](@entry_id:149904) of the [scattering matrix](@entry_id:137017). The variance in the interaction strengths of these eigenstates leads to a non-zero probability that the nucleus remains intact but the projectile is excited into a higher-mass state. This process, coherent diffractive [dissociation](@entry_id:144265), is a direct consequence of the fluctuating nature of the hadronic wavefunction [@problem_id:3523012].

### Particle Cascades and Showers

When a high-energy particle strikes a thick block of matter, it initiates a cascade of secondary particles, known as a shower. The properties of the shower depend dramatically on whether it is initiated by an electromagnetic or a hadronic particle.

#### Electromagnetic Showers

Initiated by a high-energy electron or photon, an [electromagnetic shower](@entry_id:157557) is a cascade driven by the alternating processes of [bremsstrahlung](@entry_id:157865) and [pair production](@entry_id:154125). The development of the shower is governed by the two key parameters $X_0$ and $E_c$.

A simple but powerful **Heitler model** captures the essential features. In this model, after one radiation length, every particle doubles its number (an electron radiates a photon; a photon produces a pair), and the energy is shared equally. This multiplication continues until the average energy per particle drops to the [critical energy](@entry_id:158905), $E_c$. At this point, ionization loss takes over, and the cascade rapidly dies out. This simple model correctly predicts two key features of the shower's longitudinal development [@problem_id:3522987]:
*   The number of particles at the shower maximum is proportional to the initial energy: $N_{\text{max}} \approx E_0 / E_c$.
*   The depth of the shower maximum increases only logarithmically with energy: $t_{\text{max}} (\text{in } X_0) \approx \ln(E_0/E_c)$.

Electromagnetic showers are characterized by being relatively short (contained within 25-30 $X_0$), narrow, and with relatively small event-to-event fluctuations.

#### Hadronic Showers

Hadronic showers, initiated by particles like protons or [pions](@entry_id:147923), are far more complex and messy. They are governed by the nuclear interaction length $\lambda_I$. Since $\lambda_I \gg X_0$, hadronic showers are much longer and broader than electromagnetic showers for the same energy.

A crucial feature of hadronic cascades is the large event-to-event fluctuations. In each interaction, a variable number of neutral [pions](@entry_id:147923) ($\pi^0$) are produced. These decay almost instantly into two photons ($\pi^0 \to \gamma\gamma$), which then initiate their own electromagnetic sub-showers. The remaining energy is carried by charged hadrons, which continue the cascade, and by nuclear fragments. A significant fraction of the energy from nuclear breakup is converted into an undetectable form, known as **invisible energy** (e.g., binding energy release, neutrinos, low-energy neutrons).

This leads to a fundamental problem in [calorimetry](@entry_id:145378) known as **non-compensation**. A typical [calorimeter](@entry_id:146979) responds differently to the electromagnetic component (response 'e') than to the hadronic component (response 'h'), with $e/h > 1$. The large fluctuations in the electromagnetic fraction ($f_{em}$) from event to event are the primary source of the poor [energy resolution](@entry_id:180330) of hadronic calorimeters [@problem_id:3522989]. Designing **compensating calorimeters** with $e/h \approx 1$, for instance by using hydrogen-rich active media to enhance the signal from neutrons, is a major challenge in experimental particle physics [@problem_id:3522989].

### Modeling Transport: From Theory to Computation

The ultimate goal of this field is to simulate the complex journey of particles through matter. This is accomplished using sophisticated Monte Carlo programs that stochastically model the physics described above.

#### The Boltzmann Transport Equation

On a formal level, the average behavior of a population of [non-interacting particles](@entry_id:152322) is described by the **linear Boltzmann transport equation (LBTE)**. This is a particle conservation equation in phase space. For a steady-state situation, it balances the rate of change of the angular [particle flux](@entry_id:753207), $\psi(\mathbf{r}, \mathbf{\Omega}, E)$, due to various processes:

$$
\mathbf{\Omega}\cdot\nabla \psi + \Sigma_{a}\psi + \psi \int \!\! \int \Sigma_{s}(E\to E') \, d\Omega' dE' = S + \int \!\! \int \Sigma_{s}(E'\to E) \psi(\mathbf{r}, \mathbf{\Omega}', E') \, d\Omega' dE'
$$

Each term has a clear physical meaning [@problem_id:3522980]:
*   **Loss Terms (Left Side)**:
    1.  $\mathbf{\Omega}\cdot\nabla \psi$: Net loss from a volume element due to particles **streaming** out.
    2.  $\Sigma_{a}\psi$: Loss due to true **absorption** events.
    3.  $\psi \int \!\! \int \Sigma_{s}(E\to E') ...$: Loss due to particles **scattering out** of the direction $\mathbf{\Omega}$ and energy $E$.

*   **Gain Terms (Right Side)**:
    1.  $S$: Gain from an external **source**.
    2.  $\int \!\! \int \Sigma_{s}(E'\to E) \psi' ...$: Gain due to particles **scattering into** the direction $\mathbf{\Omega}$ and energy $E$ from other states.

Solving this integro-differential equation analytically is impossible for all but the simplest cases. Monte Carlo methods provide a powerful numerical technique for stochastically solving the LBTE.

#### Principles of Monte Carlo Transport

Modern transport codes like Geant4, FLUKA, and MCNP use a **condensed-history** Monte Carlo technique. Instead of simulating every single interaction, which would be computationally prohibitive, they group the effects of many "soft" interactions (like small energy losses and small-angle scatterings) and apply them over a finite path segment, or **step**. "Hard" interactions that cause a large, discrete change in the particle's state (like a hadronic [inelastic collision](@entry_id:175807) or high-energy bremsstrahlung) are sampled individually.

The core of any such algorithm is its **step-size control** strategy. A robust strategy must balance computational performance with physical accuracy. The maximum allowable step length, $h$, at any point is determined by the minimum of several constraints [@problem_id:3523035]:
*   The geometric distance to the next boundary.
*   A fraction of relevant physics length scales, such as the radiation length ($X_0$) and the nuclear interaction length ($\lambda_I$), to ensure that the probability of multiple hard interactions in one step is low.
*   Constraints from the desired accuracy of the continuous process models. For example, limiting the step so that the energy loss is a small fraction of the total energy, or so that the accumulated multiple scattering angle remains small enough for the model to be valid.

Once this maximum step length $h$ is determined, the algorithm samples a free path $s_{\text{int}}$ to the next discrete interaction from the [exponential distribution](@entry_id:273894). The actual step taken is $\min(h, s_{\text{int}})$. If the particle takes the full step $h$ without a discrete interaction, the algorithm uses the **[memoryless property](@entry_id:267849)** of the [exponential distribution](@entry_id:273894) to determine the remaining path to the next interaction in the subsequent step. This combination of physics-limited stepping and [exact sampling](@entry_id:749141) of discrete events ensures that the simulation is both efficient and physically unbiased. The global error from such an algorithm has two components: a deterministic bias from the continuous process integrators, which scales with the average step size $\langle h \rangle$, and a statistical uncertainty from the random nature of the processes, whose RMS value accumulates as $\sqrt{N_{\text{steps}}}$ [@problem_id:3523035].