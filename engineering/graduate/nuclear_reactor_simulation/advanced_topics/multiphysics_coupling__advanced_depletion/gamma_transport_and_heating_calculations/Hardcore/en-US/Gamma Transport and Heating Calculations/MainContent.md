## Introduction
The transport of gamma rays and the subsequent deposition of their energy as heat are critical phenomena in the design, operation, and safety analysis of nuclear systems. While a significant portion of energy in a reactor core is released by fission fragments, a substantial fraction emerges as gamma photons, which can travel considerable distances before interacting. This non-local energy deposition creates a complex power distribution that simple assumptions cannot capture, posing a challenge for accurate thermal analysis. This article provides a comprehensive overview of the methods used to address this challenge. The following chapters will guide you from first principles to practical application. "Principles and Mechanisms" will detail the governing Boltzmann transport equation, the fundamental photon-matter interactions, and the physics of energy deposition. "Applications and Interdisciplinary Connections" will explore how these principles are utilized in core reactor physics, shielding design, and safety analysis. Finally, "Hands-On Practices" will offer exercises to reinforce the theoretical concepts and their computational implementation.

## Principles and Mechanisms

The transport of photons through matter and the consequent deposition of their energy are phenomena governed by a combination of fundamental physical laws and the statistical nature of particle interactions. This chapter elucidates the core principles and mechanisms underlying gamma transport and heating, beginning with the governing transport equation, detailing the primary photon-matter interaction processes, defining the physics of energy deposition, and concluding with an introduction to key concepts in computational transport methods.

### The Photon Transport Equation

The behavior of a population of photons in a medium is statistically described by the **angular photon flux**, denoted as $\psi(\mathbf{r}, \mathbf{\Omega}, E)$. This quantity represents the number of photons at a spatial position $\mathbf{r}$, traveling in the direction of the unit vector $\mathbf{\Omega}$, with energy $E$, that cross a unit area perpendicular to $\mathbf{\Omega}$ per unit time, per unit solid angle, and per unit energy. The evolution of this flux in phase space (the space of position, direction, and energy) is described by the **linear Boltzmann transport equation (LBE)**.

For a system in a steady state, where the photon population does not change with time, the LBE expresses a balance between the rates of photon loss and gain within an infinitesimal volume of phase space. The equation is written as:

$$
\mathbf{\Omega}\cdot\nabla \psi(\mathbf{r},\mathbf{\Omega},E) + \Sigma_{t}(\mathbf{r},E)\,\psi(\mathbf{r},\mathbf{\Omega},E) = \int_{0}^{\infty}\mathrm{d}E'\int_{4\pi}\mathrm{d}\mathbf{\Omega}'\,\Sigma_{s}(\mathbf{r};E'\!\to\!E,\mathbf{\Omega}'\cdot\mathbf{\Omega})\,\psi(\mathbf{r},\mathbf{\Omega}',E') + q(\mathbf{r},\mathbf{\Omega},E)
$$

Each term in this equation represents a distinct physical process [@problem_id:4228905]:

1.  **Streaming Loss ($\mathbf{\Omega}\cdot\nabla \psi$):** The term $\mathbf{\Omega}\cdot\nabla \psi$ is the divergence of the angular flux along the direction of motion $\mathbf{\Omega}$. It represents the net rate at which photons stream out of a differential spatial volume $d\mathbf{r}$ for a given direction and energy.

2.  **Collision Loss ($\Sigma_{t}\psi$):** The term $\Sigma_{t}(\mathbf{r},E)\,\psi(\mathbf{r},\mathbf{\Omega},E)$ accounts for the removal of photons from the state $(\mathbf{r}, \mathbf{\Omega}, E)$ due to interactions (collisions) with the atoms of the medium. The **total macroscopic cross section**, $\Sigma_{t}(\mathbf{r},E)$, is the probability of any interaction occurring per unit path length for a photon of energy $E$ at position $\mathbf{r}$.

3.  **Scattering Gain (Integral Term):** This term represents the rate at which photons from all other energies $E'$ and directions $\mathbf{\Omega}'$ are scattered *into* the state $(E, \mathbf{\Omega})$. The kernel of this integral, $\Sigma_{s}(\mathbf{r};E'\!\to\!E,\mathbf{\Omega}'\cdot\mathbf{\Omega})$, is the **double-differential macroscopic scattering cross section**. It quantifies the probability that a photon with initial energy $E'$ and direction $\mathbf{\Omega}'$ will emerge from a scattering event with final energy $E$ and direction $\mathbf{\Omega}$. The integral sums these contributions over all possible initial states.

4.  **Fixed Source Gain ($q$):** The term $q(\mathbf{r},\mathbf{\Omega},E)$ represents an external or **fixed source** of photons. This includes photons produced from processes other than scattering, such as those emitted during radioactive decay, nuclear fission, or secondary particle reactions.

A quantity of great practical importance is the **scalar photon flux**, $\phi(\mathbf{r}, E)$, which is the angular flux integrated over all directions:
$$
\phi(\mathbf{r},E) = \int_{4\pi}\psi(\mathbf{r},\mathbf{\Omega},E)\,\mathrm{d}\mathbf{\Omega}
$$
The scalar flux represents the total number of photons of energy $E$ entering a infinitesimally small sphere at position $\mathbf{r}$ from all directions, per unit time, per unit area of the sphere's cross section, and per unit energy. It is the central quantity used in calculating reaction rates and heating.

### Fundamental Photon-Matter Interactions

The macroscopic cross sections that appear in the LBE are derived from the underlying physics of individual photon-atom interactions. The probability of an interaction is quantified by the **microscopic cross section**, $\sigma$, which represents an effective target area presented by a single atom and has units of area (e.g., barns, where $1 \text{ barn} = 10^{-24} \text{ cm}^2$). The macroscopic cross section, $\Sigma$, is obtained by multiplying the microscopic cross section by the atomic number density $N$ (atoms per unit volume) of the material: $\Sigma = N\sigma$.

For the photon energies relevant to nuclear reactors, typically ranging from tens of keV to around 10 MeV, three interaction processes dominate [@problem_id:4228872]:

#### Photoelectric Effect

The photoelectric effect is the absorption of a photon by an atom, resulting in the ejection of a bound electron. This process is forbidden for a free electron due to the impossibility of simultaneously conserving energy and momentum. The presence of the nucleus, which absorbs recoil momentum, is essential. The ejected electron, called a photoelectron, emerges with a kinetic energy $T_e$ equal to the incident photon energy $E_\gamma$ minus the electron's initial binding energy $B_i$: $T_e = E_\gamma - B_i$.

This interaction is most probable for tightly bound electrons and therefore exhibits a very strong dependence on the atomic number $Z$ of the material and the photon energy $E$. The microscopic cross section, $\sigma_{\mathrm{pe}}$, scales approximately as:
$$
\sigma_{\mathrm{pe}} \propto \frac{Z^{4-5}}{E^{3-3.5}}
$$
This scaling shows that the photoelectric effect is dominant for low-energy photons and high-$Z$ materials. A key feature of the photoelectric cross section is the presence of **absorption edges**. An edge is a sharp, discontinuous increase in the cross section that occurs when the photon energy becomes just high enough to eject an electron from a new, more tightly bound atomic shell (e.g., the K-shell, L-shell). For instance, when the photon energy surpasses the K-shell binding energy $B_K$, the two K-shell electrons become available for interaction, opening a major new reaction channel. This causes a sudden jump in $\sigma_{\mathrm{pe}}$ and, consequently, in the local gamma heating rate for photons with energies just above the edge compared to those just below it [@problem_id:4228914].

#### Compton Scattering

Compton scattering is the inelastic scattering of a photon by a charged particle, typically an atomic electron. For photon energies much greater than the electron's binding energy (e.g., above 100 keV), the electron can be treated as effectively free and at rest. In this process, the photon transfers a portion of its energy to the electron, which recoils, and a new photon of lower energy emerges at a different angle.

The interaction occurs with individual electrons. Since a neutral atom of atomic number $Z$ has $Z$ electrons, the atomic Compton scattering cross section, $\sigma_C$, is approximately proportional to $Z$:
$$
\sigma_C(E,Z) \approx Z \cdot \sigma_e(E)
$$
where $\sigma_e(E)$ is the scattering cross section for a single electron. This process is dominant at intermediate energies (roughly 0.5 MeV to 5 MeV) for most materials. The physics of this interaction is precisely described by Quantum Electrodynamics (QED). The relationship between the incident photon energy $E$, the scattered photon energy $E'$, and the scattering angle $\theta$ is given by the Compton formula [@problem_id:4228906]:
$$
E' = \frac{E}{1 + \frac{E}{m_e c^2}(1 - \cos\theta)}
$$
where $m_e c^2 \approx 0.511$ MeV is the rest mass energy of the electron. The differential cross section for unpolarized photons is given by the **Klein-Nishina formula**:
$$
\frac{\mathrm{d}\sigma}{\mathrm{d}\Omega} = \frac{r_e^2}{2}\left(\frac{E'}{E}\right)^2\left(\frac{E'}{E} + \frac{E}{E'} - \sin^2\theta\right)
$$
where $r_e$ is the classical electron radius. In the low-energy limit ($E \ll m_e c^2$), scattering becomes nearly elastic ($E' \approx E$), and the Klein-Nishina formula reduces to the classical Thomson scattering cross section.

#### Pair Production

If a photon's energy exceeds twice the rest mass energy of an electron ($2m_e c^2 \approx 1.022$ MeV), it can be converted into matter in the form of an electron-positron pair. This process must occur in the field of a charged particle, typically a nucleus, to conserve momentum. The minimum or **threshold energy** for pair production is therefore $1.022$ MeV; below this energy, the cross section is zero.

The cross section for pair production, $\sigma_{\mathrm{pp}}$, rises from zero at the threshold and increases with energy, typically logarithmically, throughout the MeV range. It is strongly dependent on the strength of the nuclear Coulomb field, scaling approximately with the square of the atomic number:
$$
\sigma_{\mathrm{pp}} \propto Z^2
$$
Pair production is the dominant interaction mechanism for high-energy photons (above ~5-10 MeV, depending on the material) and in high-$Z$ materials.

### Gamma Heating and Energy Deposition

Gamma heating is the process by which energy from a photon field is deposited into a material, increasing its internal energy. A careful distinction must be made between the energy *transferred* from photons to charged particles and the energy that is ultimately *deposited* locally as heat.

#### The Physics of Energy Deposition

The initial transfer of energy from uncharged photons to charged particles (electrons and positrons) is quantified by **KERMA**, an acronym for **K**inetic **E**nergy **R**eleased in **MA**tter. The volumetric rate of this energy transfer is calculated by integrating the photon energy fluence rate, $E\phi(\mathbf{r},E)$, with the appropriate energy-transfer cross section. To simplify this, a **kerma factor** is often defined as $k_\gamma(E) = E \Sigma_{\text{tr}}(E)$, where $\Sigma_{\text{tr}}(E)$ is the macroscopic energy-transfer cross section [@problem_id:4228890].

However, not all kinetic energy transferred to an electron is deposited locally through collisions. A high-energy electron can also lose energy by radiating secondary photons (bremsstrahlung) as it decelerates in the field of nuclei. These radiative losses do not contribute to local heating. To correctly calculate heating, one must use the **macroscopic energy-absorption cross section**, $\Sigma_{\text{en}}(E)$, which is constructed by subtracting the energy lost to radiation from the total energy transferred. The volumetric heating rate, $Q_\gamma(\mathbf{r})$, is then given by the integral of the photon energy fluence rate weighted by this cross section [@problem_id:4228905]:
$$
Q_\gamma(\mathbf{r}) = \int_{0}^{\infty} E \Sigma_{\text{en}}(\mathbf{r},E) \phi(\mathbf{r},E) \,dE
$$

The way energy is deposited depends on the initial interaction type. In the photoelectric effect, the photon's full energy (minus the electron binding energy) is given to a single electron. In Compton scattering, only a fraction of the energy is transferred. For pair production, the process is more complex. The initial photon energy $E_\gamma$ is partitioned into the rest mass of the electron-positron pair ($2m_ec^2$) and their combined kinetic energy ($K_{e^-} + K_{e^+}$). This kinetic energy is deposited locally as the particles slow down. However, the $2m_ec^2$ of rest mass energy is only converted back to radiation when the positron annihilates with an electron, producing two $0.511$ MeV annihilation photons. These secondary photons must be transported, and they contribute to heating only if and where they are subsequently absorbed. The rest mass energy is therefore not deposited as heat at the site of the pair production event [@problem_id:4228873].

#### Charged Particle Equilibrium (CPE)

The formalism above, which equates local heating to the energy transferred to charged particles (specifically, the collision KERMA based on $\Sigma_{\text{en}}$), relies on a crucial assumption: **Charged Particle Equilibrium (CPE)**. CPE exists at a point if, for every charged particle of a given type and energy that leaves an infinitesimal volume around that point, another identical particle enters it. This implies that the net transport of energy by charged particles into or out of the volume is zero.

CPE is a good approximation in a homogeneous medium provided that the characteristic distance over which the photon field changes is much larger than the range of the secondary electrons it produces [@problem_id:4228861]. However, CPE breaks down severely in two common situations:
1.  **Near Material Interfaces:** At an interface between a high-$Z$ material (e.g., UO$_2$ fuel) and a low-$Z$ material (e.g., water), the rate of electron production is much higher in the high-$Z$ material. This creates a net flux of electrons from the high-$Z$ side to the low-$Z$ side. As a result, the actual absorbed dose (heating) is lower than the local KERMA on the high-$Z$ side and higher than the local KERMA on the low-$Z$ side.
2.  **In Cavities:** In a thin, low-density region (like a helium-filled gap between fuel pellets) surrounded by a dense material, photon interactions within the gas are negligible, so the local KERMA is near zero. However, the absorbed dose is non-zero, as it is produced by electrons streaming into the gap from the surrounding dense walls.

In situations where CPE is not valid, a simple local deposition model is inaccurate, and an explicit transport calculation for the secondary charged particles is required to determine the heating distribution correctly.

### Concepts in Photon Transport Calculation

Solving the LBE analytically is only possible for highly idealized problems. In practice, numerical methods or simplified models are employed.

#### Uncollided Flux and the Buildup Factor

A powerful concept in radiation shielding is the separation of the photon field into two components: uncollided and scattered photons. For a narrow, collimated beam of photons with incident flux $\phi_0$ at $x=0$, the **uncollided flux**, $\phi_u(x)$, decreases exponentially with penetration depth $x$ according to the Beer-Lambert law:
$$
\phi_u(x) = \phi_0 e^{-\Sigma_t x}
$$
where $\Sigma_t$ is the total macroscopic attenuation coefficient. This formula accounts for all photons removed from the beam by any interaction. However, in a broad beam or a thick shield, scattered photons are not lost from the system and contribute significantly to the total flux at depth.

To account for this contribution without solving the full transport equation, the **buildup factor**, $B$, is introduced. It is a dimensionless correction factor defined as the ratio of the true total response (e.g., total flux or total dose) to the response calculated using only the uncollided flux [@problem_id:4228913]:
$$
B(\text{arguments}) = \frac{\text{Total Response}}{\text{Uncollided Response}}
$$
Since the scattered radiation adds to the field, the buildup factor is always greater than or equal to one ($B \ge 1$). Using a pre-calculated energy-absorption buildup factor, $B_{en}$, the volumetric heating rate can be approximated as:
$$
q_\gamma(x) \approx E \Sigma_{\text{en}}(E) B_{en}(x,E) \phi_u(x)
$$
This approach provides a practical and reasonably accurate method for many shielding design problems.

#### The Discrete Ordinates ($S_N$) Method

For more general and accurate solutions, the LBE is often solved numerically using the **discrete ordinates ($S_N$) method**. This method tackles the complexity of the LBE by discretizing its independent variables.
- **Angular Discretization:** The continuous angular domain is replaced by a finite set of discrete directions $\mathbf{\Omega}_m$ with corresponding weights $w_m$. The angular integral in the scattering source is replaced by a weighted sum, known as a quadrature.
- **Spatial Discretization:** The spatial domain is divided into a mesh of cells. The streaming operator is approximated using a finite-difference scheme, such as the **diamond difference** scheme.
- **Iterative Solution:** The resulting system of algebraic equations is typically solved iteratively. In **source iteration**, an initial guess is made for the scalar flux, which is used to compute the scattering source. A "transport sweep" is then performed, solving for the angular flux in each discrete direction cell by cell. The updated angular fluxes are then used to compute a new scalar flux, and the process is repeated until convergence [@problem_id:4228894].

While powerful, the $S_N$ method has characteristic numerical artifacts. The diamond difference scheme, for example, is not guaranteed to produce positive fluxes if the spatial cells are optically thick, which can lead to unphysical solutions. More fundamentally, the discretization of angle leads to the **ray effect**. Because particles are only allowed to stream along the finite set of discrete directions, a highly localized source in a low-scattering medium will produce a scalar flux field with unphysical streaks or "star patterns" aligned with the quadrature directions [@problem_id:4228860]. These artifacts are not a result of spatial discretization and cannot be eliminated by refining the spatial mesh. Ray effects are mitigated by increasing the number of discrete directions (i.e., using a higher-order $S_N$ approximation), or in situations where physical scattering is high, which naturally smooths the angular distribution of photons [@problem_id:4228860].