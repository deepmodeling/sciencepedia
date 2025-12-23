## Introduction
To harness the power of a star on Earth, we must be able to diagnose the extreme conditions at the heart of a fusion plasma, where temperatures reach hundreds of millions of degrees. Since charged particles are trapped by powerful magnetic fields, they cannot tell us what is happening in the core. Neutrons, however, being electrically neutral, escape the plasma unimpeded, acting as direct messengers from the fusion reactions themselves. The fundamental challenge lies in intercepting these elusive particles and decoding the wealth of information they carry about the plasma's performance, stability, and path toward ignition.

This article provides a comprehensive foundation in the principles and applications of neutron diagnostics. It bridges the gap between the fundamental physics of neutron generation and the practical interpretation of detector signals to assess fusion performance. Over the course of three chapters, you will gain a robust understanding of this [critical field](@entry_id:143575). The journey begins in the "Principles and Mechanisms" chapter, which lays the groundwork by exploring the physics of neutron creation in fusion reactions, their interactions with matter, and the core techniques used for their detection. Following this, the "Applications and Interdisciplinary Connections" chapter demonstrates how these principles are applied to infer key parameters like fusion power and [ion temperature](@entry_id:191275), probe advanced [burning plasma physics](@entry_id:1121944), and inform [fusion engineering](@entry_id:1125401) and technology. Finally, a series of "Hands-On Practices" will allow you to solidify your knowledge by tackling practical problems in diagnostic analysis and design.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and mechanisms that form the bedrock of neutron diagnostics in fusion plasmas. We will journey from the genesis of neutrons in the fiery heart of a [fusion reaction](@entry_id:159555), through their interactions with matter, to the intricate processes by which they are detected and their signals are interpreted. Our focus is on building a robust conceptual and quantitative understanding from first principles, establishing the physical basis for the diagnostic techniques discussed in subsequent chapters.

### Neutron Generation in Fusion Plasmas

The primary motivation for neutron diagnostics is that neutrons are a [direct product](@entry_id:143046) of the very fusion reactions we aim to sustain. Unlike charged particles, neutrons are not confined by the plasma's magnetic fields and thus escape, carrying with them a wealth of information about the conditions at their point of origin.

#### Kinematics of Key Fusion Reactions

The most relevant fusion reactions for current and future energy-producing devices are the Deuterium-Tritium (DT) and Deuterium-Deuterium (DD) reactions. The DT reaction is:

$$
\mathrm{D} + \mathrm{T} \rightarrow {}^4\mathrm{He} (\alpha) + \mathrm{n}
$$

The DD reaction has two branches of nearly equal probability:

$$
\mathrm{D} + \mathrm{D} \rightarrow \mathrm{T} + \mathrm{p} \quad (\text{proton branch})
$$
$$
\mathrm{D} + \mathrm{D} \rightarrow {}^{3}\mathrm{He} + \mathrm{n} \quad (\text{neutron branch})
$$

Each reaction releases a specific amount of energy, known as the **Q-value**, which arises from the conversion of rest mass into kinetic energy. The Q-value is defined as $Q = (m_{\text{reactants}} - m_{\text{products}})c^2$. The approximate Q-values for these reactions are:

-   $Q_{\mathrm{DT}} \approx 17.6 \, \mathrm{MeV}$
-   $Q_{\mathrm{DD} \rightarrow \mathrm{n}} \approx 3.27 \, \mathrm{MeV}$
-   $Q_{\mathrm{DD} \rightarrow \mathrm{p}} \approx 4.03 \, \mathrm{MeV}$

In a fusion plasma, the initial kinetic energy of the reacting ions is typically on the order of tens of keV, which is negligible compared to the MeV-scale Q-values. We can therefore analyze the reaction kinematics by assuming the reactants are essentially at rest. By applying the [conservation of energy and momentum](@entry_id:193044) in the [center-of-mass frame](@entry_id:158134), we can determine the kinetic energies of the products.

For a two-body reaction $1 + 2 \rightarrow 3 + 4$ with negligible initial kinetic energy, energy conservation gives $E_{k,3} + E_{k,4} \approx Q$. Momentum conservation requires that the products move in opposite directions with equal-magnitude momenta, $\vec{p}_3 = -\vec{p}_4$. Since kinetic energy can be expressed non-relativistically as $E_k = p^2 / (2m)$, the condition $p_3^2 = p_4^2$ leads to $m_3 E_{k,3} = m_4 E_{k,4}$. Solving these two [simultaneous equations](@entry_id:193238) yields the energy of particle 3:

$$
E_{k,3} = Q \left( \frac{m_4}{m_3 + m_4} \right)
$$

This crucial result shows that the energy is partitioned inversely to the masses of the products. Applying this to the neutron-producing reactions :

-   **DT Reaction**: The products are a neutron ($m_n \approx 1 \, \mathrm{u}$) and an alpha particle ($m_{\alpha} \approx 4 \, \mathrm{u}$). The neutron receives:
    $$
    E_n = Q_{\mathrm{DT}} \left( \frac{m_{\alpha}}{m_n + m_{\alpha}} \right) \approx 17.6 \, \mathrm{MeV} \left( \frac{4}{1+4} \right) = 14.08 \, \mathrm{MeV} \approx 14.1 \, \mathrm{MeV}
    $$
-   **DD Reaction (neutron branch)**: The products are a neutron ($m_n \approx 1 \, \mathrm{u}$) and a Helium-3 nucleus ($m_{{}^3\mathrm{He}} \approx 3 \, \mathrm{u}$). The neutron receives:
    $$
    E_n = Q_{\mathrm{DD} \rightarrow \mathrm{n}} \left( \frac{m_{{}^3\mathrm{He}}}{m_n + m_{{}^3\mathrm{He}}} \right) \approx 3.27 \, \mathrm{MeV} \left( \frac{3}{1+3} \right) \approx 2.45 \, \mathrm{MeV}
    $$

These two characteristic energies, $14.1 \, \mathrm{MeV}$ for DT and $2.45 \, \mathrm{MeV}$ for DD, are the primary signatures that neutron diagnostics seek to measure.

### Neutron Interactions with Matter

As neutrons traverse the plasma, vacuum vessel, shielding, and finally the detector itself, they interact with the nuclei of the materials they encounter. Understanding these interactions is fundamental to designing diagnostics and interpreting their signals.

#### Fundamental Concepts of Neutron Transport

The probability of a neutron interacting with matter is quantified by the **microscopic cross section**, denoted $\sigma(E)$. It represents the effective "target area" a single nucleus presents to an incident neutron of energy $E$ for a specific type of interaction. Its unit is typically the barn, where $1 \, \text{barn} = 10^{-28} \, \mathrm{m}^2$.

In a bulk material with a uniform number density of nuclei $N$ (atoms per unit volume), the collective effect is described by the **macroscopic cross section**, $\Sigma(E)$, defined as:

$$
\Sigma(E) = N \sigma(E)
$$

$\Sigma(E)$ has units of inverse length (e.g., $\mathrm{m}^{-1}$) and represents the probability of an interaction occurring per unit path length traveled by the neutron. The average distance a neutron travels before an interaction is the **mean free path**, $\lambda(E)$, which is simply the reciprocal of the [macroscopic cross section](@entry_id:1127564):

$$
\lambda(E) = \frac{1}{\Sigma(E)}
$$

These concepts lead to the fundamental law of attenuation for a collimated, monoenergetic beam of neutrons. The intensity of the uncollided beam, $I(x)$, decreases exponentially with [penetration depth](@entry_id:136478) $x$ according to the Beer-Lambert law :

$$
I(x) = I(0) \exp\left(-\int_0^x \Sigma(E, x') dx'\right)
$$

For a homogeneous material where $\Sigma(E)$ is constant, this simplifies to $I(x) = I(0) e^{-\Sigma(E)x}$.

#### A Taxonomy of Neutron Interactions

The total cross section, $\sigma_{\text{tot}}(E)$, is the sum of the partial cross sections for all possible interaction channels. For fusion-energy neutrons, the most important interactions are:

-   **Elastic Scattering ($\sigma_{\text{el}}$)**: The neutron collides with a nucleus, conserving total kinetic energy. The neutron changes direction and transfers some of its energy to the recoiling nucleus. For high-energy neutrons scattering off heavy nuclei (like iron or lead in shielding), the scattering is strongly peaked in the forward direction, and the energy loss per collision is small. This is the primary interaction mechanism for neutrons in organic [scintillators](@entry_id:159846), where scattering off light hydrogen nuclei (protons) leads to large energy transfers and is the basis of detection.

-   **Inelastic Scattering ($\sigma_{\text{inel}}$)**: The neutron collision excites the target nucleus to a higher energy level. The kinetic energy of the system is not conserved; the scattered neutron emerges with a reduced energy, the difference having been absorbed by the nucleus (which later de-excites, typically by emitting gamma rays). For fast neutrons (e.g., $14.1 \, \mathrm{MeV}$) interacting with medium-to-heavy nuclei, [inelastic scattering](@entry_id:138624) is a very important process and is a primary mechanism for slowing neutrons down in energy .

-   **Radiative Capture ($\sigma_{\gamma}$)**: The neutron is absorbed by the nucleus, forming a [compound nucleus](@entry_id:159470) in an excited state, which then de-excites by emitting one or more gamma rays. The cross section for this process, often denoted as $(n, \gamma)$, is generally very large for low-energy (thermal) neutrons but becomes very small for fast neutrons in the MeV range.

-   **Fission ($\sigma_{\text{fis}}$)**: For certain heavy nuclei (fissile materials like $^{235}\mathrm{U}$ or $^{239}\mathrm{Pu}$), absorption of a neutron can cause the nucleus to split into two smaller fragments, releasing a tremendous amount of energy and more neutrons. While negligible in most structural materials, this process is exploited in specific detector types.

The total probability of any interaction is governed by the total [macroscopic cross section](@entry_id:1127564) $\Sigma_{\text{tot}} = \sum_j \Sigma_j$. If an interaction occurs, the probability that it is of a specific type $j$ is given by the ratio $\Sigma_j / \Sigma_{\text{tot}}$. In the context of a collimator made of iron at $14.1 \, \mathrm{MeV}$, scattering (both elastic and inelastic) accounts for over $99\%$ of interactions, while capture is negligible.

### Principles of Neutron Detection

The detection of any particle relies on converting its presence and properties (energy, time-of-arrival) into a measurable signal, typically an electronic pulse. Since neutrons are electrically neutral, they do not directly cause ionization. Their detection is therefore a two-step process: first, a neutron interaction must convert its kinetic energy into one or more energetic charged particles; second, these charged particles deposit their energy in the detector medium, creating the signal.

#### General Formalism of Detector Response

Let us consider a neutron field incident upon a detector. The rate of neutrons arriving at the detector with energy between $E$ and $E+dE$ is given by the differential rate $\phi(E) dE$, where $\phi(E)$ has units of $\mathrm{s}^{-1}\mathrm{eV}^{-1}$.

The **intrinsic detection efficiency**, $\epsilon(E)$, is the probability that an incident neutron of energy $E$ will produce a registered count. A count is typically registered if the resulting electronic pulse has an amplitude $s$ that exceeds a certain threshold, $s_{\text{th}}$.

The **detector response function**, $R(s|E)$, provides a complete probabilistic description of the detector's behavior. It is defined such that $R(s|E)ds$ is the probability that an incident neutron of energy $E$ will produce a pulse of amplitude between $s$ and $s+ds$. With this definition, the efficiency is the integral of the response function over all amplitudes that exceed the threshold :

$$
\epsilon(E) = \int_{s_{\text{th}}}^{\infty} R(s|E) ds
$$

The total expected count rate, $C$, is then found by integrating the product of the incident rate and the efficiency over all possible energies:

$$
C = \int_0^{\infty} \phi(E) \epsilon(E) dE
$$

This fundamental equation connects the physical quantity of interest, $\phi(E)$, to the measured observable, $C$. A key task in neutron diagnostics is to characterize $\epsilon(E)$ and $R(s|E)$ in order to invert this equation and infer properties of the neutron source from the measured data.

#### Detection via Charged Particle Conversion

##### Fission Chambers: High-Energy Signatures

A **fission chamber** is a gas-filled detector that uses the neutron-induced fission reaction as the conversion mechanism. A typical design consists of concentric electrodes, with the inner surface coated with a thin layer of a fissile material such as $^{235}\mathrm{U}$.

When a fast neutron (e.g., $2.5 \, \mathrm{MeV}$ or $14.1 \, \mathrm{MeV}$) induces fission in a $^{235}\mathrm{U}$ nucleus, the nucleus splits into two heavy, highly-charged fragments. These fragments share a massive amount of kinetic energy, approximately $170 \, \mathrm{MeV}$ total. Typically, one fragment escapes the coating and enters the detector gas. This single particle, with a kinetic energy of around $85 \, \mathrm{MeV}$, is a heavy ion that loses its energy very rapidly through intense ionization of the gas. The number of ion pairs created is enormous—on the order of $3 \times 10^6$.

In contrast, background gamma rays interact with the low-density gas primarily through Compton scattering, producing energetic electrons. These electrons have a much lower rate of energy loss ([stopping power](@entry_id:159202)) and deposit far less energy in the gas, creating a pulse corresponding to perhaps $10^4-10^5$ ion pairs at most.

This enormous difference in energy deposition is the key to the fission chamber's utility . By setting the pulse-height threshold $s_{\text{th}}$ at a level well above the maximum possible signal from a gamma ray, but far below the signal from a fission fragment, the detector can be made to count neutron-induced fission events with high efficiency while remaining almost completely insensitive to the intense gamma-ray background present in a fusion environment.

##### Organic Scintillators: Recoil Protons and Pulse Shape Discrimination

**Organic [scintillators](@entry_id:159846)** are materials (liquid or plastic) rich in hydrogen and carbon that produce flashes of light (scintillation) when traversed by charged particles. For fast neutron detection, the dominant interaction is [elastic scattering](@entry_id:152152) on hydrogen nuclei (protons). The incident neutron transfers a significant portion of its kinetic energy to a recoil proton, which then excites the scintillator molecules as it slows down. These excited molecules de-excite by emitting light, which is collected by a photosensor (e.g., a [photomultiplier tube](@entry_id:906129)).

A remarkable property of many organic [scintillators](@entry_id:159846) is that the time profile of the light emission depends on the type of exciting particle. This enables **Pulse Shape Discrimination (PSD)**, a powerful technique for distinguishing neutron events from gamma-ray events . The physical basis for PSD lies in the different **Linear Energy Transfer (LET)**, or [stopping power](@entry_id:159202) ($dE/dx$), of the recoil particles.

-   **Neutron Events**: A recoil proton is a relatively heavy particle that creates a very dense track of ionization (high LET). This high density of excited molecules enhances interactions between them, particularly the formation of long-lived molecular states (triplet states). The delayed de-excitation of these states produces a significant "slow" component in the light pulse, with a decay time of hundreds of nanoseconds.
-   **Gamma-Ray Events**: A Compton-scattered electron is a light particle that creates a sparse ionization track (low LET). Inter-molecular interactions are rare, and de-excitation is dominated by prompt fluorescence from short-lived states (singlet states). This results in a predominantly "fast" light pulse, with a decay time of a few nanoseconds.

By analyzing the shape of the electronic pulse from the photosensor—specifically, by comparing the amount of light in the "tail" of the pulse to the total light—one can effectively distinguish the high-LET neutron events from the low-LET gamma-ray events.

### Advanced Topics in Neutron Measurement and Interpretation

Building upon these fundamentals, we can now explore the more subtle and quantitative aspects of neutron diagnostics that are essential for high-fidelity measurements in a complex fusion environment.

#### The Scintillator Light Yield: Birks' Law and Quenching

The relationship between the energy deposited by a charged particle, $E$, and the amount of scintillation light produced, $L$, is not perfectly linear. This nonlinearity, known as **quenching**, is particularly pronounced for high-LET particles like recoil protons. The phenomenon is well-described by the semi-empirical **Birks' law** , which states that the [light yield](@entry_id:901101) per unit path length, $dL/dx$, is a saturating function of the stopping power, $dE/dx$:

$$
\frac{dL}{dx} = S \frac{dE/dx}{1 + k_B \frac{dE}{dx}}
$$

Here, $S$ is the scintillation efficiency in the limit of low LET, and $k_B$ is the Birks constant, which quantifies the degree of quenching. For recoil protons, where $dE/dx$ is large (especially at lower energies), the denominator becomes significantly greater than one, "quenching" the light output. For electrons, $dE/dx$ is small, and the response is nearly linear ($dL/dx \approx S \, dE/dx$).

By integrating Birks' law over the particle's track, one can derive the total light output $L(E_p)$ for a proton of initial energy $E_p$. The result is a non-linear function. This has a critical consequence: if a scintillator's energy scale is calibrated using a gamma-ray source (which produces electrons), applying this linear calibration to interpret the light from recoil protons will lead to a systematic underestimation of the proton's energy, and therefore the incident neutron's energy. Accurate neutron spectrometry with [scintillators](@entry_id:159846) requires a careful, non-linear calibration of the light response for recoil ions.

#### Disentangling Signal from Background

A successful neutron measurement hinges on the ability to distinguish the desired signal—direct, uncollided fusion neutrons—from a variety of background sources. The primary backgrounds in a fusion experiment are :

1.  **Prompt Gamma Rays**: Produced by nuclear reactions in the plasma and surrounding structures, these arrive at the detector almost instantaneously (at the speed of light).
2.  **Scattered (Room-Return) Neutrons**: These are fusion neutrons that have scattered off the walls of the experimental hall or other structures. Their path length is longer and their energy is lower, so they arrive later and with a broad energy distribution.
3.  **Cosmic Rays**: High-energy particles, primarily muons, that are uncorrelated in time with the fusion event.

A comprehensive discrimination strategy employs multiple, orthogonal techniques:

-   **Time-of-Flight (TOF)**: By using a timing signal ($t_0$) from the fusion event, one can measure the neutron's travel time to a detector at a known distance $L$. Since velocity depends on energy ($E_k = \frac{1}{2}mv^2$), TOF is equivalent to an energy measurement. A $14.1 \, \mathrm{MeV}$ neutron travels significantly slower ($\approx 0.17c$) than a gamma ray ($c$). A narrow TOF gate can thus select the direct $14.1 \, \mathrm{MeV}$ neutrons while rejecting the much earlier prompt gammas and the much later scattered neutrons.
-   **Pulse Shape Discrimination (PSD)**: As discussed previously, this technique is used in organic [scintillators](@entry_id:159846) to reject gamma-ray and cosmic-ray muon events (low LET) that may happen to fall within the TOF gate of interest.
-   **Pulse Height Thresholding**: Setting a minimum signal amplitude rejects low-energy background events, such as low-energy scattered neutrons and [electronic noise](@entry_id:894877).
-   **Shadow Cones**: To accurately subtract the background of scattered neutrons, which is correlated with the fusion source, a shadow cone of dense material can be placed between the source and detector. This blocks the direct line-of-sight flux, allowing a clean measurement of the scattered component alone, which can then be subtracted from the `open` (unblocked) measurement.

By combining these methods, a clean measurement of the direct neutron flux can be achieved.

#### Interpreting Neutron Energy Spectra

A high-resolution measurement of the neutron energy spectrum reveals more than just a single peak. The detailed shape of the spectrum provides a window into the plasma's kinetic state . The main features are:

-   **The Primary Peak**: For a thermal plasma, the neutrons born from DT fusion do not all have exactly $14.1 \, \mathrm{MeV}$. The thermal motion of the reacting D and T ions causes a **Doppler broadening** of the emission line. The width of this peak is directly related to the ion temperature, with the full-width at half-maximum (FWHM) scaling as $\Delta E_{\text{FWHM}} \propto \sqrt{T_i}$.
-   **The Down-Scattered Continuum**: Primary neutrons can elastically scatter off deuterium, tritium, or impurity ions within the plasma before they escape. Each scattering event reduces the neutron's energy, populating a continuum at energies below the primary peak. The intensity and shape of this continuum are related to the plasma's density and size, encapsulated in the areal density $\rho R$.
-   **The High-Energy Tail**: A faint but important feature is a tail of neutrons with energies extending well above $14.1 \, \mathrm{MeV}$. This is the signature of secondary fusion reactions involving energetic **knock-on ions**. For example, a $14.1 \, \mathrm{MeV}$ neutron can elastically scatter off a [deuteron](@entry_id:161402), transferring several MeV of energy to it. If this fast [deuteron](@entry_id:161402) then fuses with a thermal [triton](@entry_id:159385), the additional kinetic energy of the reactants boosts the energy of the emitted neutron, creating the high-energy tail.

#### From Neutron Rate to Fusion Power

The ultimate goal of many diagnostic efforts is to determine the total fusion power, $P_{\text{fus}}$, produced by the plasma. Neutron measurements are the most direct way to achieve this.

The **total fusion power** is the total rate of energy released by fusion reactions. For DT, this is $P_{\text{fus}} = \dot{N}_{\text{reac}} \cdot Q_{\mathrm{DT}}$, where $\dot{N}_{\text{reac}}$ is the reaction rate. The **prompt neutron power**, $P_n$, is the portion of this power carried away by the escaping neutrons, $P_n = \dot{N}_{\text{reac}} \cdot E_n$. The remaining power, $P_{\alpha} = \dot{N}_{\text{reac}} \cdot E_{\alpha}$, is carried by the alpha particles. Because the alphas are charged, they are confined by the magnetic field and deposit their energy in the plasma, a process called **[alpha heating](@entry_id:193741)**.

Since each DT reaction produces one neutron, the measured total neutron production rate, $\dot{N}_n$, is equal to the reaction rate, $\dot{N}_{\text{reac}}$. Therefore, an absolutely calibrated measurement of $\dot{N}_n$ allows for a direct inference of the total fusion power :

$$
P_{\text{fus}} = \dot{N}_n \cdot Q_{\mathrm{DT}} = \dot{N}_n \cdot (17.6 \, \mathrm{MeV})
$$

A crucial aspect of modern fusion analysis is performing consistency checks. By using independent measurements of [plasma density](@entry_id:202836) and temperature profiles, one can calculate the expected thermonuclear reaction rate. Comparing this calculated rate to the measured $\dot{N}_n$ helps to validate the measurements and identify the contribution of non-thermal neutron sources, such as those from energetic [neutral beam injection](@entry_id:204293).

#### Absolute Calibration: Grounding Measurements in Reality

A quantitative measurement of $\dot{N}_n$ requires an **absolute calibration** of the detector system. This process relates the detector's raw output (counts) to the physical quantity of interest (incident neutron flux) in a traceable manner. A standard method involves using a compact neutron generator with a known, calibrated yield $Y$ (neutrons per second), traceable to a national [metrology](@entry_id:149309) institute .

The procedure involves several key steps:
1.  **Calculate Incident Flux**: The generator is placed at a known distance $r$ from the detector. The number of neutrons incident on the detector's active area $S$ is calculated from the source yield and the geometric solid angle, $\Omega = S/r^2$. The incident rate is $\phi_{\text{inc}} = Y \cdot (\Omega / 4\pi)$.
2.  **Measure Net Count Rate**: The detector's count rate is measured. To isolate the counts from direct, unscattered neutrons, a background measurement is performed using a shadow cone and subtracted from the total.
3.  **Correct for Inefficiencies**: The measured rates must be corrected for instrumental effects, most notably **detector [dead time](@entry_id:273487)**—the brief period after an event during which the detector is unable to process another.
4.  **Calculate Efficiency**: The absolute efficiency is then the ratio of the corrected net count rate to the calculated incident flux: $\epsilon_{\text{abs}} = R_{\text{net, corrected}} / \phi_{\text{inc}}$.
5.  **Uncertainty Analysis**: A rigorous calibration includes a full propagation of uncertainties. The dominant sources of uncertainty are often systematic, such as the uncertainty in the source yield itself (typically 1-2%) and its angular emission [isotropy](@entry_id:159159), rather than counting statistics or geometric measurements.

This meticulous process ensures that the neutron rates measured on a fusion device are not just relative indicators but accurate, physical quantities that can be used to reliably determine fusion performance.