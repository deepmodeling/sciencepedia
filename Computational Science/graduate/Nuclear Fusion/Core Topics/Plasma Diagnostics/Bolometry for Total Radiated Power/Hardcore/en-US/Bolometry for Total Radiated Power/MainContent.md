## Introduction
In the quest for sustainable [fusion energy](@entry_id:160137), managing the immense power flows within a reactor is a paramount challenge. A significant fraction of the energy used to heat the plasma is inevitably lost through electromagnetic radiation. Quantifying and understanding this energy loss channel is not just an accounting exercise; it is fundamental to achieving stable, high-performance plasma operation and protecting the machine's components from excessive heat loads. The primary diagnostic for this task is [bolometry](@entry_id:746904), a technique for measuring the [total radiated power](@entry_id:756065).

This article addresses the need for a comprehensive understanding of [bolometry](@entry_id:746904), moving beyond a simple definition to explore its physical basis, mathematical complexity, and critical applications. It explains how a collection of simple thermal detectors can be used to create detailed spatial maps of radiation, providing deep insights into plasma behavior. Across three chapters, this article will guide you from the first principles of a single detector to the sophisticated analysis required in modern fusion experiments.

First, the **Principles and Mechanisms** chapter will deconstruct the bolometer, starting with the heat balance that governs its operation. We will explore the [atomic physics](@entry_id:140823) processes that cause a plasma to radiate and formulate the forward and inverse problems that connect this local [emissivity](@entry_id:143288) to detector signals through the powerful technique of tomography. Next, the chapter on **Applications and Interdisciplinary Connections** will highlight why these measurements are indispensable. We will see how [bolometry](@entry_id:746904) is used to close the global power balance, control divertor conditions, prevent disruptions, and how it serves as a bridge to other fields like atomic physics and radiative transfer. Finally, a series of **Hands-On Practices** will allow you to engage directly with core concepts, challenging you to model a detector's [response time](@entry_id:271485), account for environmental effects, and evaluate the quality of a [tomographic reconstruction](@entry_id:199351).

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that underpin [bolometry](@entry_id:746904) as a primary diagnostic for measuring [total radiated power](@entry_id:756065) in fusion plasmas. We will begin with the physics of a single detector element, explore the origins of plasma radiation, and then proceed to the complex task of reconstructing the [spatial distribution](@entry_id:188271) of this radiation from line-integrated measurements. Finally, we will address the practical necessities of calibration and spectral response that transform a bolometer from a simple sensor into a quantitative scientific instrument.

### The Bolometer as a Thermal Detector: The Fundamental Heat Balance

At its core, a **bolometer** is a thermal detector. Its operational principle is elegantly simple: it measures incident radiation by absorbing the energy and converting it into heat, which results in a measurable temperature increase. To understand this quantitatively, we can model a single bolometer element as a thermally isolated body connected to a large heat sink.

Consider a small absorber element, such as a thin foil, with a temperature-dependent resistance. This element is exposed to the plasma radiation and is connected to a heat sink, or base, held at a constant temperature $T_0$. The connection is a thermal link with a defined [thermal conductance](@entry_id:189019), $G$. Under steady-state conditions, the power absorbed by the element, $P_{\mathrm{abs}}$, must be precisely balanced by the power it loses to the heat sink. Assuming the dominant heat loss mechanism is conduction through the thermal link—a standard design goal achieved by operating in high vacuum and minimizing radiative losses to the surroundings—the power lost is given by Newton's law of cooling, which for conduction is $P_{\mathrm{out}} = G (T - T_0)$, where $T$ is the [steady-state temperature](@entry_id:136775) of the element.

The [absorbed power](@entry_id:265908), $P_{\mathrm{abs}}$, is only a fraction of the total power radiated by the plasma, $P_{\mathrm{rad}}$. First, the geometry of the diagnostic, defined by its [aperture](@entry_id:172936) and line of sight, allows only a fraction, $F$, of the total plasma radiation to be incident on the detector. This incident power is $P_{\mathrm{inc}} = F P_{\mathrm{rad}}$. Second, the detector element does not absorb all the power that strikes it. Its efficiency in this regard is characterized by its **absorptance**, $\eta$, which is the fraction of incident power that is absorbed. The absorptance is generally a function of wavelength, but for a total power measurement, we can consider a wavelength-averaged value. Thus, the [absorbed power](@entry_id:265908) is $P_{\mathrm{abs}} = \eta P_{\mathrm{inc}}$.

By equating the power absorbed with the power lost at steady state ($P_{\mathrm{abs}} = P_{\mathrm{out}}$), we arrive at the fundamental heat balance equation for a bolometer :

$G (T - T_0) = \eta F P_{\mathrm{rad}}$

This equation establishes the direct proportionality between the [total radiated power](@entry_id:756065) of the plasma, $P_{\mathrm{rad}}$, and the measured temperature rise of the detector, $(T - T_0)$. By measuring this temperature change (often indirectly, via a change in [electrical resistance](@entry_id:138948)), and with prior knowledge of the [thermal conductance](@entry_id:189019) $G$, absorptance $\eta$, and geometry factor $F$, one can determine the absolute value of the [total radiated power](@entry_id:756065).

### The Source of Radiation: Plasma Emissivity and its Mechanisms

Having established how a bolometer measures power, we now turn our attention to the source of this power: the plasma itself. The [total radiated power](@entry_id:756065), $P_{\mathrm{rad}}$, is a macroscopic quantity representing the sum of all microscopic emission processes occurring throughout the plasma volume. It is formally defined as the integral of the local **emissivity**, $\varepsilon(\mathbf{r})$, over the entire plasma volume $V$:

$P_{\mathrm{rad}} = \int_V \varepsilon(\mathbf{r}) dV$

The local [emissivity](@entry_id:143288), $\varepsilon(\mathbf{r})$, with units of power per unit volume (e.g., $\mathrm{W/m^3}$), arises from several fundamental atomic physics processes. In a typical high-temperature fusion plasma, the dominant contributors to radiation are bremsstrahlung, [line radiation](@entry_id:751334), and recombination radiation .

#### Bremsstrahlung (Free-Free Radiation)

**Bremsstrahlung**, German for "[braking radiation](@entry_id:267482)," is produced when free electrons are deflected, and thus accelerated, by the electrostatic fields of ions. This process occurs for all ion species in the plasma. The [power density](@entry_id:194407) of bremsstrahlung, $p_{\mathrm{ff}}$, can be shown to scale with the electron density $n_e$, the density $n_i$ and charge $Z_i$ of each ion species, and the [electron temperature](@entry_id:180280) $T_e$. The scaling is given by :

$p_{\mathrm{ff}} \propto n_e \sqrt{T_e} \sum_i n_i Z_i^2$

This dependence on the sum of $n_i Z_i^2$ makes it convenient to introduce the **effective ion charge**, $Z_{\mathrm{eff}}$, a key parameter characterizing plasma purity:

$Z_{\mathrm{eff}} = \frac{\sum_i n_i Z_i^2}{n_e}$

Substituting this definition, the bremsstrahlung [power density](@entry_id:194407) simplifies to a clear scaling relationship:

$p_{\mathrm{ff}} \propto n_e^2 Z_{\mathrm{eff}} \sqrt{T_e}$

This shows that bremsstrahlung increases with density, temperature (albeit weakly), and plasma impurity content as captured by $Z_{\mathrm{eff}}$. In the very hot, clean core of a tokamak (e.g., $T_e > 5 \, \mathrm{keV}$), where light impurities like carbon and oxygen are fully stripped of their electrons, bremsstrahlung is often the dominant radiation mechanism .

#### Line Radiation (Bound-Bound Radiation)

**Line radiation** is emitted when a bound electron in an impurity ion transitions from a higher energy level to a lower one. For this to occur, the ion must first be excited, which in a fusion plasma happens predominantly through collisions with free electrons. In the **[coronal equilibrium](@entry_id:188784)** model, valid for low-density, high-temperature plasmas, the rate of electron-impact excitation is balanced by the rate of spontaneous [radiative decay](@entry_id:159878).

This leads to a power density for a specific ion in charge state $k$ that is proportional to the product of the electron density and the ion density, $p_{\mathrm{line}, k} \propto n_e n_k$. Summing over all impurity species and charge states, the total line [radiation power](@entry_id:267187) density is :

$p_{\mathrm{line}} = \sum_k n_e n_k L_k(T_e)$

Here, $L_k(T_e)$ is the **cooling [rate coefficient](@entry_id:183300)** for the ion of charge state $k$. It encapsulates all the [atomic physics](@entry_id:140823) of that ion and is a strong, non-[monotonic function](@entry_id:140815) of [electron temperature](@entry_id:180280). For any given element, [line radiation](@entry_id:751334) is most efficient at temperatures where the ion is only partially stripped, possessing a complex [electron shell structure](@entry_id:156047). At very high temperatures, light- and medium-Z impurities become fully ionized and cease to produce [line radiation](@entry_id:751334). However, in the cooler plasma edge and pedestal regions ($T_e \sim 50 - 500 \, \mathrm{eV}$), even trace amounts of impurities, particularly medium- to high-Z elements like tungsten, can make [line radiation](@entry_id:751334) the overwhelmingly dominant contribution to local emissivity .

#### Recombination Radiation (Free-Bound Radiation)

**Recombination radiation** is emitted when a free electron is captured by an ion into a bound state. This process is essentially the inverse of [photoionization](@entry_id:157870). The rate of recombination, and thus its radiative power, is strongly enhanced at low electron temperatures and high electron densities. Its [emissivity](@entry_id:143288) scales roughly as $\varepsilon_{fb} \propto n_e^2 T_e^{-1/2}$ or even more strongly with inverse temperature for certain recombination processes. Consequently, recombination radiation is typically negligible in the hot plasma core but becomes a very significant, often dominant, contributor in cold, dense plasma regions, such as a **detached divertor** where temperatures can be as low as $1-2 \, \mathrm{eV}$ .

The [total radiated power](@entry_id:756065), $P_{\mathrm{rad}}$, is the [volume integral](@entry_id:265381) of the sum of these local emissivities. It is a common misconception that the hottest region radiates the most. In fact, due to the extreme efficiency of line and recombination radiation, the relatively small volumes of the plasma edge and divertor often generate a substantial fraction, if not the majority, of the [total radiated power](@entry_id:756065) .

### From Local Emissivity to Detector Signal: The Forward Problem

A single bolometer channel does not measure the local [emissivity](@entry_id:143288) $\varepsilon(\mathbf{r})$ at a point, nor does it measure the total $P_{\mathrm{rad}}$ directly. It measures the power incident upon its [aperture](@entry_id:172936), which corresponds to the radiation emitted along its **Line Of Sight (LOS)**. This gives rise to a chord-integrated measurement. The fundamental task of modeling the diagnostic is to formulate this relationship, known as the **forward problem**.

Assuming the plasma is **optically thin**—meaning that photons emitted within the plasma escape without being reabsorbed—the radiance along a given LOS is simply the integral of the local emissivity along that path. The signal $S$ recorded by a single bolometer channel can be expressed as a [linear functional](@entry_id:144884) of the emissivity :

$S = \int_{\mathrm{LOS}} \varepsilon(\mathbf{r}) W(\mathbf{r}) dl$

Here, the integral is taken along the path length $l$ of the LOS. The function $W(\mathbf{r})$ is a weighting function that accounts for the complete geometric and instrumental response. It includes factors like the detector's field of view, [vignetting](@entry_id:174163), and any spatial variations in sensitivity. The assumption of an optically thin plasma is crucial; if reabsorption is significant (optically thick), the simple [line integral](@entry_id:138107) breaks down, and the modeling becomes a far more complex [radiative transfer](@entry_id:158448) problem .

A more rigorous formulation starts from first principles of [radiometry](@entry_id:174998). The power radiated from a differential volume element $dV$ at position $\mathbf{r}$ is $\varepsilon(\mathbf{r})dV$. For an isotropic emitter, this power is distributed over $4\pi$ steradians. The power collected by a detector with aperture area $A_{\mathrm{ap}}$ at a distance $R$ is proportional to the solid angle subtended by the aperture, $d\Omega = A_{\mathrm{ap}} \cos\theta / R^2$. Integrating over the entire plasma volume visible to the detector gives the total incident power. This more detailed approach is necessary for accurately modeling detectors with extended fields of view .

### Reconstructing the Source: The Inverse Problem and Tomography

The forward problem maps the known emissivity distribution to the expected detector signals. The diagnostic challenge, however, is the reverse: to determine the unknown [emissivity](@entry_id:143288) distribution $\varepsilon(\mathbf{r})$ from a set of measured chord signals $s_i$. This is a classic **inverse problem**.

A single chord measurement provides only one number, which is an integral of the emissivity over many points in space. It is therefore impossible to determine the local value of emissivity from one measurement. To reconstruct the spatial distribution of $\varepsilon(\mathbf{r})$, we must combine measurements from many chords viewing the plasma cross-section from different angles. This technique is known as **tomography**.

#### The Abel Transform: A Special Case

In the special case of an axisymmetric plasma with circular concentric flux surfaces, where the emissivity is only a function of the minor radius, $\varepsilon(\mathbf{r}) = \varepsilon(r)$, the tomographic problem simplifies considerably. The chord-integrated signal for a LOS with an [impact parameter](@entry_id:165532) $b$ (its closest approach to the magnetic axis) becomes a function $I(b)$. Through a geometric transformation of the [line integral](@entry_id:138107), this relationship can be shown to be the **Abel transform**  :

$I(b) = 2 \int_{b}^{a} \frac{\varepsilon(r) r}{\sqrt{r^2 - b^2}} dr$

where $a$ is the minor radius of the plasma boundary. Crucially, the Abel transform has a known mathematical inverse, the **inverse Abel transform**. This allows for the direct reconstruction of the radial [emissivity](@entry_id:143288) profile $\varepsilon(r)$ from a set of chordal measurements $I(b)$ covering a range of impact parameters.

#### General Tomographic Inversion and Regularization

For general, non-axisymmetric [emissivity](@entry_id:143288) distributions, the reconstruction is more complex. The standard approach is to discretize the problem. The plasma cross-section is divided into a grid of cells or voxels (pixels), indexed by $j=1, \ldots, M$, within which the [emissivity](@entry_id:143288) is assumed to be constant, $\varepsilon_j$. A set of $N$ bolometer measurements, $s_i$, can then be represented as a system of linear equations :

$\mathbf{s} = \mathbf{A} \boldsymbol{\varepsilon}$

Here, $\mathbf{s}$ is the vector of $N$ measurements, $\boldsymbol{\varepsilon}$ is the vector of $M$ unknown pixel emissivities, and $\mathbf{A}$ is the $N \times M$ **geometry matrix**. Each element $A_{ij}$ of this matrix represents the contribution of the emissivity in pixel $j$ to the signal in channel $i$. It is calculated by integrating the contribution of pixel $j$ to channel $i$ based on the full radiometric model, incorporating the geometry of the LOS, the solid angle, and the instrument response :

$A_{ij} = \int_{V_j} \chi_i(\mathbf{r}) \frac{A_{\mathrm{ap},i}\cos\theta(\mathbf{r})}{4\pi R(\mathbf{r})^2} \eta_i dV$

where the integral is over the volume of pixel $j$, and the terms represent visibility, solid angle, and efficiency for channel $i$.

Solving this system for $\boldsymbol{\varepsilon}$ is often an **[ill-posed problem](@entry_id:148238)**. Due to the limited number of views and the inherent smoothing of the line-integration process, the matrix $\mathbf{A}$ is typically ill-conditioned. A direct inversion ($\boldsymbol{\varepsilon} = \mathbf{A}^{-1}\mathbf{s}$) would be extremely sensitive to [measurement noise](@entry_id:275238), producing reconstructions with large, unphysical oscillations. To overcome this, **regularization** techniques are employed. A common method is Tikhonov regularization, which seeks a solution that balances two competing objectives: fitting the data (minimizing the [residual norm](@entry_id:136782) $\|\mathbf{A}\boldsymbol{\varepsilon} - \mathbf{s}\|_2$) and maintaining solution smoothness (minimizing a regularization [seminorm](@entry_id:264573) $\|\mathbf{L}\boldsymbol{\varepsilon}\|_2$, where $\mathbf{L}$ is a smoothing operator like a discrete Laplacian).

The choice of the [regularization parameter](@entry_id:162917), $\lambda$, which controls this balance, is critical. The **L-curve criterion** is a widely used heuristic for this purpose . It involves plotting the logarithm of the [residual norm](@entry_id:136782) versus the logarithm of the solution [seminorm](@entry_id:264573) for a range of $\lambda$ values. This plot typically forms a characteristic 'L' shape. The optimal $\lambda$ is chosen at the "corner" of the curve—the point of maximum curvature—which represents the best compromise between fidelity to the data and the smoothness of the reconstructed [emissivity](@entry_id:143288) profile.

### Practicalities of the Measurement: Calibration and Spectral Response

To be a quantitative diagnostic, a bolometer system must be carefully calibrated, and its non-ideal characteristics must be understood. Two of the most critical aspects are absolute calibration and spectral response.

#### Absolute Calibration

**Absolute calibration** is the process of establishing the relationship between the raw output of the detector (e.g., a voltage signal) and the absolute incident power in physical units (Watts). This is typically performed using a reference radiation source with a known output, such as a **blackbody source** at a precisely controlled temperature $T$ .

When a detector is exposed to this known source, its response is measured. The instrument's absolute sensitivity, $S^{\mathrm{abs}}$, is defined as the change in output signal per unit change in incident power:

$S_V^{\mathrm{abs}} = \frac{dV}{dP_{\mathrm{inc}}}$

The incident power from the blackbody source depends on its [spectral radiance](@entry_id:149918) $L_\lambda(T)$, the instrument's throughput or [etendue](@entry_id:178668) (a product of its area $A$ and solid angle $\Omega$), and the detector's wavelength-dependent efficiency $\eta(\lambda)$. The total incident power is found by integrating over all wavelengths:

$P_{\mathrm{inc}} = \int \eta(\lambda) A \Omega L_\lambda(T) d\lambda$

By measuring $V$ and calculating the theoretical $P_{\mathrm{inc}}$, the absolute sensitivity can be determined. This sensitivity factor is then used to convert the raw signals measured from the plasma into absolute power values.

#### Spectral Response and Effective Absorptance

A core challenge in [bolometry](@entry_id:746904) is that no real detector has a perfectly uniform, or "flat," spectral response. The goal of a bolometer is to measure the total power, $\int \Phi(\lambda) d\lambda$, where $\Phi(\lambda)$ is the incident spectral [power density](@entry_id:194407). However, what it actually measures is proportional to a weighted integral, $\int \eta(\lambda) \Phi(\lambda) d\lambda$. The function $\eta(\lambda)$ is the complete spectral response of the instrument system  .

This system response is a product of the spectral properties of all components in the optical path. For a typical setup including a vacuum window with transmission $T_w(\lambda)$, a filter with transmission $T_f(\lambda)$, and an absorber foil with absorptance $\eta_a(\lambda)$, the total system absorptance is :

$\eta(\lambda) = T_w(\lambda) T_f(\lambda) \eta_a(\lambda)$

The degree to which the measured, weighted integral approximates the true total power depends on the "flatness" of this $\eta(\lambda)$ across the spectral range where the plasma emits. To quantify the overall efficiency for a given plasma spectrum, we define the **effective absorptance**, $\eta_{\mathrm{eff}}$, as the ratio of the total [absorbed power](@entry_id:265908) to the total incident power:

$\eta_{\mathrm{eff}} = \frac{P_{\mathrm{abs}}}{P_{\mathrm{inc}}} = \frac{\int \eta(\lambda) \Phi(\lambda) d\lambda}{\int \Phi(\lambda) d\lambda}$

This effective absorptance is a single number that represents the spectrally-averaged efficiency of the detector for a specific incident plasma spectrum. Its value is sensitive to both the instrument's design and the plasma's [radiative properties](@entry_id:150127). For example, if a change in the window material blocks a spectral band where the plasma was radiating strongly, the effective absorptance could change significantly, underscoring the importance of accurately characterizing both the instrument and the plasma spectrum for high-fidelity power measurements .

In summary, the reliable measurement of [total radiated power](@entry_id:756065) via [bolometry](@entry_id:746904) rests on a chain of principles: the fundamental heat balance of the detector, a thorough understanding of the plasma's emission physics, the mathematical framework of tomographic inversion to recover local emissivity, and a meticulous approach to calibration and characterization of the instrument's real-world response.