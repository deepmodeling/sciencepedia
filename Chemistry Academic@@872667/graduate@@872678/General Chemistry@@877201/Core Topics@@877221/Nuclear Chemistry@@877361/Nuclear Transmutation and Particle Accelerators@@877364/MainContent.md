## Introduction
The ancient alchemical quest to transform one element into another, while impossible by chemical means, has become a routine reality in the realm of modern physics. This feat is accomplished through [nuclear transmutation](@entry_id:153100), a process of altering the very identity of an atomic nucleus using particle accelerators. This technology bridges the gap between theoretical [nuclear physics](@entry_id:136661) and tangible applications that impact fields from medicine to materials science. The ability to control and induce [nuclear reactions](@entry_id:159441) allows us to create life-saving medical isotopes, probe the structure of matter with intense neutron beams, and explore the exotic, short-lived nuclei that forge the elements in stars. This article addresses how the fundamental laws of physics are harnessed to achieve these transformations.

This comprehensive overview will guide you from core concepts to practical implementation. In the first section, "Principles and Mechanisms," we will delve into the energetics of the nucleus, exploring concepts like binding energy, the [liquid-drop model](@entry_id:751355), and the conservation laws that govern all nuclear interactions. Next, "Applications and Interdisciplinary Connections" will showcase how these principles are put to work in [radioisotope](@entry_id:175700) production, [experimental design](@entry_id:142447), and analytical techniques. Finally, "Hands-On Practices" will provide opportunities to apply this knowledge to solve realistic problems in accelerator science. By navigating these sections, you will gain a robust understanding of how we purposefully change the elements.

## Principles and Mechanisms

The artificial transmutation of elements, once the domain of alchemists, is now a routine procedure in modern physics and chemistry, enabled by particle accelerators. These devices provide beams of energetic particles that can induce nuclear reactions, altering the very composition of atomic nuclei. Understanding these processes requires a synthesis of concepts from classical mechanics, electromagnetism, and quantum theory. This chapter elucidates the fundamental principles governing [nuclear stability](@entry_id:143526) and [reaction dynamics](@entry_id:190108), and explores the primary mechanisms by which accelerators are used to effect [nuclear transmutation](@entry_id:153100).

### The Energetics of Nuclear Transmutation

At the heart of any nuclear process is the conversion of mass into energy, governed by Einstein's famous relation, $E = mc^2$. The stability of a nucleus, and the energy released or absorbed during its transformation, is directly related to its mass.

#### Mass Defect and Nuclear Binding Energy

The mass of a stable nucleus is always less than the sum of the masses of its constituent protons and neutrons (collectively known as **nucleons**) in their free state. This difference in mass is called the **[mass defect](@entry_id:139284)**, denoted by $\Delta m$. For a [nuclide](@entry_id:145039) ${}^A_Z X$ with $Z$ protons and $N = A-Z$ neutrons, the mass defect is:

$$ \Delta m = (Z m_p + N m_n) - M_{\text{nuc}}({}^A_Z X) $$

where $m_p$ and $m_n$ are the masses of a free proton and neutron, respectively, and $M_{\text{nuc}}$ is the mass of the nucleus.

This "missing" mass has been converted into energy that binds the nucleons together, known as the **[nuclear binding energy](@entry_id:147209)**, $B$. The binding energy is therefore:

$$ B = (\Delta m) c^2 = \left[ (Z m_p + N m_n) - M_{\text{nuc}}({}^A_Z X) \right] c^2 $$

In practice, high-precision mass measurements are performed on neutral atoms, not bare nuclei. The tabulated **atomic mass**, $M_{\text{atom}}$, includes the mass of $Z$ electrons. We can reformulate the binding energy in terms of atomic masses. By approximating the mass of a [neutral hydrogen](@entry_id:174271) atom ($m_{\text{H}}$) as the sum of a proton and an electron mass ($m_p + m_e$), and neglecting the comparatively minuscule binding energies of atomic electrons (on the order of keV versus MeV for nuclear binding), we can express the total binding energy as [@problem_id:2948366]:

$$ B \approx \left[ Z m_{\text{H}} + N m_n - M_{\text{atom}}({}^A_Z X) \right] c^2 $$

This formulation is exceptionally useful as it relies directly on experimentally tabulated atomic masses. A more revealing metric for comparing [nuclear stability](@entry_id:143526) is the **[binding energy per nucleon](@entry_id:141434)**, $B/A$. Let us compute this for iron-56 (${}^{56}\text{Fe}$), a [nuclide](@entry_id:145039) of particular significance. Given $Z=26$, $N=30$, and the relevant atomic masses ($m_{\text{H}} = 1.007825\,\text{u}$, $m_n = 1.008665\,\text{u}$, $M_{\text{atom}}({}^{56}\text{Fe}) = 55.934936\,\text{u}$) and the conversion factor $1\,\text{u} \cdot c^2 = 931.494\,\text{MeV}$, the mass defect is calculated to be $\Delta m \approx 0.52846\,\text{u}$. This corresponds to a total binding energy of $B \approx 492.26\,\text{MeV}$, yielding a [binding energy per nucleon](@entry_id:141434) of:

$$ \frac{B}{A} \approx \frac{492.26\,\text{MeV}}{56} \approx 8.790\,\frac{\text{MeV}}{\text{nucleon}} $$

This value is among the highest for any [nuclide](@entry_id:145039), a fact of profound consequence.

#### The Binding Energy Curve and the Nature of Nuclear Forces

When the [binding energy per nucleon](@entry_id:141434) is plotted against the [mass number](@entry_id:142580) $A$ for all stable and long-lived nuclides, a characteristic curve emerges. It rises steeply for [light nuclei](@entry_id:751275), peaks near $A \approx 56-62$ in the iron-nickel region, and then slowly decreases for heavier nuclei. This shape is a direct manifestation of the fundamental properties of the [nuclear forces](@entry_id:143248) [@problem_id:2948379]. The semi-classical **[liquid-drop model](@entry_id:751355)** of the nucleus provides a powerful framework for understanding this behavior by modeling the nucleus as a droplet of [incompressible fluid](@entry_id:262924) governed by competing effects:

1.  **Volume Term:** The [strong nuclear force](@entry_id:159198) is attractive and **short-ranged**. Crucially, it exhibits **saturation**, meaning each nucleon interacts strongly with only a finite number of its nearest neighbors. Consequently, the primary contribution to the binding energy is proportional to the total number of nucleons, i.e., to the nuclear volume. This term, scaling as $A$, is responsible for the bulk of the binding energy and explains why $B/A$ is approximately constant ($\approx 8$ MeV) for medium-to-heavy nuclei. If the strong force were long-ranged and non-saturating, the binding energy would scale as $A^2$, which is contrary to experimental evidence [@problem_id:2948379] [@problem_id:2948366].

2.  **Surface Term:** Nucleons on the surface of the "droplet" have fewer neighbors than those in the interior. They are less tightly bound, which reduces the total binding energy. This effect is analogous to surface tension in a liquid. The magnitude of this reduction is proportional to the surface area of the nucleus. Since the [nuclear radius](@entry_id:161146) scales as $R \approx r_0 A^{1/3}$, the surface area scales as $A^{2/3}$, and this term contributes a negative correction proportional to $-A^{2/3}$. This term is most significant for [light nuclei](@entry_id:751275), where a larger fraction of nucleons are on the surface, and it is a primary reason for the initial rise of the $B/A$ curve.

3.  **Coulomb Term:** The [electrostatic repulsion](@entry_id:162128) between protons is a long-range force. Every proton repels every other proton, leading to a destabilizing effect that reduces the binding energy. For a uniform charge distribution within a sphere of radius $R \propto A^{1/3}$, the total [electrostatic self-energy](@entry_id:177518) is proportional to $Z^2/R$, which scales as $-Z^2/A^{1/3}$. As $Z$ (and $A$) increases, this repulsive term becomes increasingly important, causing the gradual decline of the $B/A$ curve for heavy nuclei.

4.  **Asymmetry Term:** The Pauli exclusion principle dictates that protons and neutrons, as distinct fermions, occupy separate sets of quantized energy levels. The total energy is minimized when the number of protons and neutrons is approximately equal ($N \approx Z$). Any significant deviation from this balance, such as a large neutron excess, forces nucleons into higher energy states, reducing the binding. This quantum statistical effect contributes a negative correction term, typically modeled as $-(N-Z)^2/A$.

The peak of the [binding energy curve](@entry_id:147007) near ${}^{56}\text{Fe}$ represents the optimal trade-off: these nuclei are large enough to minimize surface effects and maximize the volume-based strong force attraction, but not so large that Coulomb repulsion becomes overwhelmingly dominant [@problem_id:2948366]. This peak divides the nuclear landscape into two regions of potential energy release. Nuclei lighter than iron can release energy by **fusion** (combining to form heavier, more tightly bound nuclei), while nuclei heavier than iron can release energy by **fission** (splitting into lighter, more tightly bound fragments). This explains the energetic favorability of accelerator-driven transmutation schemes that convert heavy, long-lived radioactive waste into more stable, lighter fission products.

#### Refinements to Nuclear Stability: Shell Effects

The [liquid-drop model](@entry_id:751355) treats the nucleus as a continuous fluid, but in reality, nucleons occupy discrete quantum energy levels, much like electrons in an atom. When a shell of proton or neutron energy levels is completely filled, the nucleus exhibits exceptionally high stability. The numbers of nucleons corresponding to these shell closures are known as **[magic numbers](@entry_id:154251)** ($2, 8, 20, 28, 50, 82, 126$).

These quantum shell effects introduce non-smooth, localized corrections to the binding energy predicted by the smooth [liquid-drop model](@entry_id:751355). A magic nucleus has an anomalously high binding energy compared to its neighbors. These deviations can be precisely measured at accelerator facilities using devices like Penning-trap mass spectrometers. While one could subtract a theoretical LDM prediction from the measured mass to find the [shell correction](@entry_id:754768), a model-independent method is often preferred.

The presence of a shell closure at a neutron number $N$ manifests as a sharp drop in the **neutron [separation energy](@entry_id:754696)**, $S_n(Z,N) = B(Z,N) - B(Z,N-1)$, just after the magic number. To create a more robust metric that is insensitive to nucleon pairing effects (which cause an even-odd staggering in binding energies), one can use a quantity related to the second derivative of the binding energy surface. The **empirical two-neutron shell gap**, defined as $\delta_{2n}(Z,N) \equiv S_{2n}(Z,N) - S_{2n}(Z,N+2)$, where $S_{2n}(Z,N) = B(Z,N) - B(Z,N-2)$ is the two-neutron [separation energy](@entry_id:754696), serves this purpose. This metric shows a large positive peak at a magic number $N$, providing a clear, quantitative signature of shell structure directly from experimental mass data [@problem_id:2948316].

### Kinetics and Dynamics of Nuclear Reactions

While [nuclear stability](@entry_id:143526) determines the overall energetics, the actual occurrence of a reaction depends on kinetics and dynamics, including the energy of the collision and the presence of any potential barriers.

#### Reaction Energetics: The Q-value

The net energy released or absorbed in a nuclear reaction is quantified by the **Q-value**. For a generic reaction $a + X \rightarrow b + Y$, the Q-value is the difference between the total initial and final rest energies:

$$ Q = \left( (m_a + m_X) - (m_b + m_Y) \right) c^2 $$

Using atomic masses, this becomes $Q = \left[ M_{\text{atom}}(a) + M_{\text{atom}}(X) - M_{\text{atom}}(b) - M_{\text{atom}}(Y) \right] c^2$.

-   If $Q > 0$, the reaction is **exoergic** (or exothermic), releasing energy. The total mass of the products is less than that of the reactants.
-   If $Q  0$, the reaction is **endoergic** (or endothermic), requiring a net input of energy to proceed. The total mass of the products is greater than that of the reactants.

For example, consider the transmutation of nitrogen-14 by a proton beam, ${}^{14}\text{N}(p,\alpha){}^{11}\text{C}$. Using the precise atomic masses for ${}^1\text{H}$, ${}^{14}\text{N}$, ${}^{4}\text{He}$, and ${}^{11}\text{C}$, the change in mass is found to be $\Delta m \approx -0.003138\,\text{u}$. This corresponds to a Q-value of $Q \approx -2.923\,\text{MeV}$ [@problem_id:2948375]. Since the Q-value is negative, this reaction is endoergic and will not occur unless sufficient energy is supplied by the incoming proton.

#### Overcoming Barriers: Threshold Energy and the Coulomb Barrier

For a reaction to proceed, the interacting particles must have sufficient energy to overcome two types of barriers: kinematic and electrostatic.

**Kinematic Threshold Energy:** For an endoergic reaction ($Q0$) involving a projectile striking a stationary target, not all of the projectile's laboratory kinetic energy, $E_{\text{lab}}$, is available to create the additional rest mass of the products. A portion of the initial energy must be conserved as the kinetic energy of the center of mass of the system. The minimum projectile kinetic energy required for the reaction to be possible is the **kinematic [threshold energy](@entry_id:271447)**, $E_{\text{th}}$. At this threshold, the reaction products are created with zero [relative velocity](@entry_id:178060) (i.e., at rest in the [center-of-mass frame](@entry_id:158134)). A non-relativistic derivation shows that the [threshold energy](@entry_id:271447) is related to the Q-value by [@problem_id:2948384]:

$$ E_{\text{th}} = -Q \left( 1 + \frac{m_{\text{projectile}}}{M_{\text{target}}} \right) $$

Note that $E_{\text{th}} > |Q|$. The additional energy is required to ensure momentum is conserved. For proton-induced $(p,n)$ reactions on a series of tin isotopes, the Q-values are all negative, ranging from $-5.20\,\text{MeV}$ for ${}^{112}\text{Sn}$ to $-4.10\,\text{MeV}$ for ${}^{120}\text{Sn}$. The corresponding threshold energies range from $E_{\text{th}} \approx 5.247\,\text{MeV}$ for ${}^{112}\text{Sn}$ down to $E_{\text{th}} \approx 4.134\,\text{MeV}$ for ${}^{120}\text{Sn}$. To ensure all these reaction channels are open on a mixed-isotope target, the proton beam energy must exceed the highest of these thresholds, i.e., $E_{\text{beam}} \ge 5.247\,\text{MeV}$ [@problem_id:2948384].

**The Coulomb Barrier:** When the projectile is a charged particle (like a proton or alpha particle), it experiences [electrostatic repulsion](@entry_id:162128) from the positively charged target nucleus. This creates a potential energy barrier, the **Coulomb barrier**, that the projectile must overcome to get close enough for the short-range strong nuclear force to initiate a reaction.

Using a simple classical model of two touching, uniformly charged spheres, the height of the Coulomb barrier, $V_C$, is the [electrostatic potential energy](@entry_id:204009) at the point of contact. The interaction distance is the sum of the [nuclear radii](@entry_id:752728), $d = R_1 + R_2$. Using the empirical radius formula $R_i = r_0 A_i^{1/3}$, the barrier height is:

$$ V_C = \frac{1}{4\pi\varepsilon_0} \frac{Z_1 Z_2 e^2}{R_1 + R_2} $$

For the reaction of a proton ($Z_1=1$) on a heavy target like bismuth-209 ($Z_2=83$, $A_2=209$), with $r_0 = 1.2\,\text{fm}$, the barrier height is estimated to be $V_C \approx 14.4\,\text{MeV}$ [@problem_id:2948348]. For a heavy target, the center-of-mass correction is small, so the required laboratory energy is approximately equal to the barrier height.

It is important to note that due to **[quantum tunneling](@entry_id:142867)**, there is a non-zero probability for a projectile with energy less than $V_C$ to penetrate the barrier. Therefore, reaction cross sections become measurable at energies below the classical barrier height, though they rise exponentially as the energy approaches and surpasses $V_C$.

**Electron Screening in Solid Targets:** In accelerator experiments performed on solid-state targets, the host material's cloud of mobile conduction electrons partially screens the positive charge of the target nucleus. This has the effect of lowering the Coulomb barrier experienced by the incoming projectile. This **[electron screening](@entry_id:145060)** can be modeled as an effective increase in the collision energy, $E \rightarrow E_{\text{eff}} = E + U_e$, where $U_e$ is the screening potential. This seemingly small shift has a profound impact because reaction cross sections at low energies are exponentially sensitive to energy. The [screening effect](@entry_id:143615) enhances the measured cross section, $\sigma_{\text{meas}}$, relative to the bare-nucleus [cross section](@entry_id:143872), $\sigma_{\text{bare}}$. To leading order, the enhancement factor is given by $f_{\text{scr}}(E) \approx \exp(\pi \eta(E) U_e / E)$, where $\eta(E)$ is the Sommerfeld parameter. Extracting the astrophysically-relevant bare-nucleus cross section from experimental data requires correcting for this enhancement: $\sigma_{\text{bare}}(E) \approx \sigma_{\text{meas}}(E) \exp(-\pi \eta(E) U_e / E)$ [@problem_id:2948370].

### Fundamental Rules: Conservation Laws in Nuclear Reactions

Energetic possibility is a necessary but not sufficient condition for a nuclear reaction to occur. All reactions must strictly adhere to a set of fundamental conservation laws. These laws act as selection rules, determining which reaction channels are "allowed" and which are "forbidden".

Consider a proton-neutron entrance channel prepared in an accelerator experiment with a total [center-of-mass energy](@entry_id:265852) of $2012.0\,\text{MeV}$ [@problem_id:2948337]. The following conservation laws must be checked for any proposed final state (exit channel):

1.  **Conservation of Total Energy:** The total energy of the final state (rest energy + kinetic energy) must equal the total energy of the initial state. A reaction is kinematically forbidden if the total rest mass of the products exceeds the available [center-of-mass energy](@entry_id:265852). For instance, the reaction $p + n \rightarrow p + p + \pi^{-}$ is forbidden because the products' rest mass ($2016.1\,\text{MeV}$) exceeds the available energy. Conversely, $p + n \rightarrow d + \pi^{0}$ (final rest mass $2010.6\,\text{MeV}$) is energetically allowed.

2.  **Conservation of Linear Momentum:** The total vector momentum of the products must equal that of the reactants. In the [center-of-mass frame](@entry_id:158134), the total momentum is zero by definition, so the products must be emitted in such a way that their vector momenta sum to zero. This law, in conjunction with energy conservation, forbids two-to-one particle reactions like $p+n \rightarrow d$ if there is initial kinetic energy. The single final particle cannot simultaneously be at rest (to conserve momentum) and carry the excess kinetic energy (to conserve energy).

3.  **Conservation of Baryon Number ($B$):** Protons and neutrons are **baryons** (assigned $B=+1$), while [mesons](@entry_id:184535) (like [pions](@entry_id:147923)) and leptons are not ($B=0$). The total [baryon number](@entry_id:157941) must be the same before and after the reaction. For $p+n$ collisions, the initial state has $B=1+1=2$. All valid final states, such as $d+\gamma$ or $p+n+\pi^0$, must also have a total [baryon number](@entry_id:157941) of 2.

4.  **Conservation of Electric Charge ($Q$):** The net electric charge is always conserved. For $p+n$, the initial charge is $+1e$. A final state like $p+p+\pi^-$ has charge $(+1) + (+1) + (-1) = +1$, so charge is conserved.

5.  **Conservation of Lepton Number ($L$):** Leptons (electrons, muons, taus, and their corresponding neutrinos) and antileptons (positrons, etc.) carry lepton number. Electrons and neutrinos have $L_e=+1$; positrons and antineutrinos have $L_e=-1$. The initial $p+n$ state has $L_e=0$. The reaction $p + n \rightarrow p + n + e^{+} + e^{-}$ is allowed because the final state has an electron ($L_e=+1$) and a [positron](@entry_id:149367) ($L_e=-1$), for a total lepton number of $0$. Weak-interaction processes that might violate this on longer timescales are neglected in fast collisions dominated by the strong and electromagnetic forces.

6.  **Conservation of Angular Momentum ($J$) and Parity ($\pi$):** The total angular momentum vector $\mathbf{J}$ and the total parity $\pi$ of the system must be conserved. Parity is a quantum property of the wavefunction under spatial inversion ($\mathbf{r} \rightarrow -\mathbf{r}$), which can be even ($+1$) or odd ($-1$). The total parity of a system is the product of the intrinsic parities of the particles and an [orbital parity](@entry_id:182992) factor $(-1)^L$, where $L$ is the relative [orbital angular momentum](@entry_id:191303). For example, the radiative capture process $p+n \rightarrow d + \gamma$ can proceed from an initial $p+n$ state with $J^\pi = 1^+$ (the triplet S-wave state, $^3S_1$) to the final [deuteron](@entry_id:161402) ground state, which is also $J^\pi = 1^+$. To conserve both angular momentum and parity, the emitted photon ($\gamma$) must carry away the appropriate [quantum numbers](@entry_id:145558). An M1 ([magnetic dipole](@entry_id:275765)) photon accomplishes this, making the reaction channel allowed. Analysis shows that the channels $p+n \rightarrow d+\pi^0$, $d+\gamma$, $p+n+e^+e^-$, and [elastic scattering](@entry_id:152152) ($p+n \rightarrow p+n$) are all allowed, while others like $p+p+\pi^-$ are forbidden by energy conservation [@problem_id:2948337].

### Mechanisms of Transmutation and Particle Production

Particle accelerators are sophisticated tools designed to manipulate charged particles with [electromagnetic fields](@entry_id:272866), accelerate them to high energies, and direct them onto targets to induce transmutations.

#### Guiding Charged Particles: Magnetic Rigidity

A cornerstone of accelerator technology is the use of magnetic fields to bend and focus beams of charged particles. When a particle with charge $q$ and momentum $\vec{p}$ moves through a magnetic field $\vec{B}$, it experiences a Lorentz force $\vec{F} = q(\vec{v} \times \vec{B})$. If the velocity is perpendicular to a [uniform magnetic field](@entry_id:263817), this force acts as a [centripetal force](@entry_id:166628), causing the particle to follow a circular path.

Equating the Lorentz force to the relativistic [centripetal force](@entry_id:166628) gives $|q|vB = p v / \rho$, where $\rho$ is the bending radius. This simplifies to a fundamental relationship in [accelerator physics](@entry_id:202689) [@problem_id:2948372]:

$$ B \rho = \frac{p}{|q|} $$

The quantity $B\rho$ is known as the **magnetic rigidity** of the particle. It is a measure of a particle's resistance to being deflected by a magnetic field and depends only on the particle's momentum and charge. For a given momentum, particles with higher charge are bent more easily (smaller $\rho$). For a given magnet ($B$), particles with higher momentum have a larger bending radius.

To calculate the required bending radius for a given particle energy, one must first determine the [relativistic momentum](@entry_id:159500). The total energy is $E = K + m_0c^2$ and is related to momentum by $E^2 = (pc)^2 + (m_0c^2)^2$. For a $30\,\text{MeV}$ proton ($m_p c^2 = 938.3\,\text{MeV}$), the momentum-energy product is $pc = \sqrt{K(K+2m_pc^2)} \approx 239.2\,\text{MeV}$. In a typical dipole magnet with a field of $1.5\,\text{T}$, the required bending radius can be calculated:

$$ \rho = \frac{p}{|q|B} = \frac{pc}{ecB} \approx \frac{239.2 \times 10^6\,\text{V}}{(2.998 \times 10^8\,\text{m/s}) \times 1.5\,\text{T}} \approx 0.5318\,\text{m} $$

This calculation is central to the design of cyclotrons, synchrotrons, and the beam transport lines that deliver particles to experimental stations.

#### Principal Reaction Mechanisms for Neutron Production

One of the most important applications of accelerator-driven transmutation is the production of intense neutron beams for research and industrial applications. Several distinct nuclear reaction mechanisms are employed, each dominating in a different energy regime [@problem_id:2948322].

1.  **Deuteron Stripping/Breakup:** At relatively low energies (a few MeV to tens of MeV), a beam of deuterons can be used to produce neutrons. The deuteron ($d$) is a weakly bound system of a proton and a neutron (binding energy $\approx 2.224\,\text{MeV}$). When a [deuteron](@entry_id:161402) strikes a light target nucleus (e.g., lithium or beryllium), the nuclear or Coulomb field of the target can easily break the [deuteron](@entry_id:161402) apart. In a **stripping** reaction (e.g., $d + {^9\text{Be}} \rightarrow {^{10}\text{B}} + n$), the proton is captured by the target, and the neutron continues. In **breakup**, the deuteron simply dissociates into a free proton and neutron. This mechanism is efficient at low energies and produces approximately one neutron per incident deuteron.

2.  **Fission:** While typically associated with nuclear reactors, accelerator-driven fission is also a source of neutrons. A beam of particles (e.g., protons or electrons) can be used to produce photons or low-energy neutrons, which then induce fission in a fissile target like ${}^{235}\text{U}$ or ${}^{238}\text{U}$. Fission of heavy nuclei is highly exoergic and releases multiple neutrons per event (typically 2-3). Neutron-induced fission of nuclides like ${}^{235}\text{U}$ is most efficient at very low (thermal) neutron energies.

3.  **Spallation:** For producing the most intense neutron beams, spallation is the mechanism of choice. This process requires a high-energy proton beam (typically $E_p > 100\,\text{MeV}$, often approaching $1\,\text{GeV}$) striking a heavy, high-Z target (e.g., lead, bismuth, or [tungsten](@entry_id:756218)). The high-energy proton initiates a complex, two-stage process. First, it triggers an **intranuclear cascade**, colliding with individual nucleons inside the target nucleus and ejecting several high-energy "cascade" neutrons. This leaves the residual nucleus in a highly excited state. Second, this excited nucleus de-excites through a process of **[evaporation](@entry_id:137264)**, statistically emitting a large number of lower-energy "[evaporation](@entry_id:137264)" neutrons. The neutron multiplicity (number of neutrons produced per incident proton) is high, ranging from 10 to 30, and increases with proton energy. Spallation neutron sources are at the forefront of materials science, chemistry, and condensed matter physics research.