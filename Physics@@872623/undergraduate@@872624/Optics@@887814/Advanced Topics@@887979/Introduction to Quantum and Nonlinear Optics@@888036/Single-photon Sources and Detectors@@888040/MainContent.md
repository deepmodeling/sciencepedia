## Introduction
The ability to control and measure light at its most fundamental level—the single photon—is a cornerstone of modern quantum science and technology. From guaranteeing the security of communications to enabling computations that are intractable for classical computers, the individual [quantum of light](@entry_id:173025) is a key resource. However, generating light that consists of a perfect, deterministic stream of single photons, and then detecting each one with perfect efficiency, presents significant physical and engineering challenges. This article provides a comprehensive exploration of the technologies developed to meet this challenge, bridging the gap between fundamental quantum principles and practical device operation.

This journey begins in the **Principles and Mechanisms** chapter, where we will establish the statistical language used to define a [single-photon source](@entry_id:143467) and explore the physical processes used to generate them, such as Spontaneous Parametric Down-Conversion. We will also delve into the working principles and inherent limitations of the detectors designed to register their arrival. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these components are used to test the foundations of quantum mechanics, power [quantum communication](@entry_id:138989) protocols like QKD, and enable new frontiers in metrology and materials science. Finally, the **Hands-On Practices** section will provide you with the opportunity to apply these concepts by modeling realistic devices and analyzing the performance of complete quantum systems. We will start by examining the core principles that distinguish quantum light from its classical counterpart.

## Principles and Mechanisms

The previous chapter introduced the concept of the photon and its central role in the burgeoning field of quantum technologies. Now, we move from the abstract to the practical, examining the principles and mechanisms that govern the generation and detection of single photons. To control and harness quantum phenomena, we must first be able to create light in its most fundamental form—one particle at a time—and then reliably register its arrival. This chapter will first establish the statistical language used to classify light sources, defining what makes a source a "[single-photon source](@entry_id:143467)." We will then explore the primary methods for generating single photons and conclude with an analysis of the real-world devices used to detect them, including their inherent imperfections.

### Characterizing Photon Streams: The Language of Photon Statistics

At a classical level, the brightness or intensity of a light beam seems to be its defining characteristic. In the quantum realm, however, this is insufficient. Two light sources with the same average intensity can have profoundly different microscopic structures, defined by the arrival statistics of their constituent photons. The primary experimental tool for probing these statistics is the **Hanbury Brown and Twiss (HBT) interferometer**. In its modern, photon-counting incarnation, an HBT [interferometer](@entry_id:261784) consists of a 50/50 non-polarizing beam splitter with a [single-photon detector](@entry_id:170664) placed at each of its two output ports. By measuring the correlations between detection events at these two detectors, we can build a detailed picture of the photon stream's temporal character.

This characterization is quantified by the **normalized second-order [temporal coherence](@entry_id:177101) function**, denoted $g^{(2)}(\tau)$. This function represents the conditional probability of detecting a photon at a time $\tau$ after an initial photon has been detected, normalized by the probability of detection for a purely random stream of photons. The value of this function at zero time delay, $g^{(2)}(0)$, is of particular importance as it provides a direct measure of the likelihood of detecting two photons simultaneously, serving as a powerful classifier for light sources. Based on the value of $g^{(2)}(0)$, we can sort light into three fundamental categories.

**Photon Bunching: $g^{(2)}(0) > 1$**

Light is said to be **bunched** if photons have a tendency to arrive in groups or "bunches." The detection of one photon increases the probability of detecting another one immediately after. The archetypal example of bunched light is [thermal light](@entry_id:165211), such as that from a blackbody radiator or a chaotic [gas discharge](@entry_id:198337) lamp. For a single-mode [thermal light](@entry_id:165211) source, quantum theory predicts that $g^{(2)}(0) = 2$. This implies that in an HBT experiment, the rate of simultaneous "coincidence" detections from a thermal source will be exactly twice the rate measured for a random source of the same average intensity [@problem_id:2247277]. This bunching arises from the constructive interference of many independent emitters, leading to large fluctuations in the instantaneous intensity of the light field.

**Poissonian Statistics: $g^{(2)}(0) = 1$**

When photon arrivals are statistically [independent events](@entry_id:275822), the light is said to follow **Poissonian statistics**. In this case, the probability of detecting a photon in any given time interval is constant and independent of when previous photons were detected. This results in $g^{(2)}(\tau) = 1$ for all $\tau$, including zero delay. An ideal, stabilized [single-mode laser](@entry_id:194328) is the canonical example of a source producing **[coherent light](@entry_id:170661)** with Poissonian [photon statistics](@entry_id:175965). A measurement of $g^{(2)}(0) = 1$ indicates that, from a statistical standpoint, the source is indistinguishable from an ideal laser [@problem_id:2254947]. While useful for many applications, such a source is fundamentally classical in its statistical nature and does not emit photons one at a time.

**Photon Antibunching: $g^{(2)}(0)  1$**

The most intriguing case is **[photon antibunching](@entry_id:165214)**, where $g^{(2)}(0)  1$. This inequality signifies that the detection of one photon makes the immediate detection of a second photon *less* likely than for a random stream. This behavior has no classical analogue; it is a purely quantum mechanical effect. The physical interpretation is that the emission of one photon temporarily depletes the source, introducing a "dead time" during which it cannot emit another. This is the definitive signature of a [non-classical light](@entry_id:190601) source, and any source exhibiting [antibunching](@entry_id:194774) is, to some degree, a [single-photon source](@entry_id:143467).

### The Ideal Single-Photon Source

The ultimate limit of antibunched light is an **ideal [single-photon source](@entry_id:143467)**, a device that emits photons strictly one by one in a deterministic sequence. For such a source, the concept of detecting two photons "simultaneously" is physically impossible. If a single photon enters an HBT [interferometer](@entry_id:261784), it must make a choice at the [beam splitter](@entry_id:145251): it is either transmitted to one detector or reflected to the other. It cannot be in both places at once. Consequently, the rate of coincidence counts must be zero. This leads to the unambiguous criterion for an ideal [single-photon source](@entry_id:143467):

$g^{(2)}(0) = 0$

This result can be formalized using the quantum mechanical description of light. The state of a light field containing exactly one photon is represented by the Fock state $|1\rangle$. The [second-order coherence function](@entry_id:175172) can be expressed in terms of the photon [number operator](@entry_id:153568), $\hat{n} = \hat{a}^\dagger \hat{a}$, where $\hat{a}$ and $\hat{a}^\dagger$ are the [annihilation and creation operators](@entry_id:194608), respectively:

$g^{(2)}(0) = \frac{\langle \hat{n}(\hat{n}-1) \rangle}{\langle \hat{n} \rangle^2}$

For the single-photon state $|1\rangle$, the expectation value of the [number operator](@entry_id:153568) is $\langle \hat{n} \rangle = \langle 1 | \hat{n} | 1 \rangle = 1$. The operator in the numerator, $\hat{n}(\hat{n}-1)$, effectively counts pairs of photons. Acting on the state $|1\rangle$, we find $\hat{n}(\hat{n}-1)|1\rangle = 1(1-1)|1\rangle = 0$. Therefore, the [expectation value](@entry_id:150961) $\langle \hat{n}(\hat{n}-1) \rangle$ is zero, which confirms that $g^{(2)}(0) = 0$ for an ideal [single-photon source](@entry_id:143467) [@problem_id:2247318]. The experimental observation of $g^{(2)}(0)  1$ is the gold standard for verifying that a source produces single photons.

### Generating Single Photons: Principles and Processes

Creating light that satisfies the stringent condition of [antibunching](@entry_id:194774) requires careful engineering at the quantum level. Two main strategies have emerged as the leading methods for single-photon generation.

#### Isolated Quantum Emitters

The most intuitive way to generate single photons is to isolate a single quantum system that can only emit one photon at a time. Examples include a single trapped atom, an ion, a fluorescent molecule, or a semiconductor quantum dot. Such a system can be modeled as a **two-level system** with a ground state $|g\rangle$ and an excited state $|e\rangle$. An external energy source (e.g., a laser pulse) excites the system from $|g\rangle$ to $|e\rangle$. The system then spontaneously decays back to the ground state, emitting a single photon in the process. Once in the ground state, it is incapable of emitting another photon until it is re-excited. This forced "refractory period" is the physical origin of [photon antibunching](@entry_id:165214) in these sources.

#### Heralded Single-Photon Sources via SPDC

A more flexible and widely used method for single-photon generation is **Spontaneous Parametric Down-Conversion (SPDC)**. In this nonlinear optical process, a high-energy "pump" photon ($p$) propagates through a suitable [nonlinear crystal](@entry_id:178123) and has a small probability of being annihilated to create a pair of lower-energy photons, conventionally named the "signal" ($s$) and "idler" ($i$). This process is governed by strict conservation laws.

**Energy conservation** dictates that the sum of the signal and idler photon energies must equal the pump [photon energy](@entry_id:139314), which implies $\omega_p = \omega_s + \omega_i$, or in terms of wavelength, $\frac{1}{\lambda_p} = \frac{1}{\lambda_s} + \frac{1}{\lambda_i}$.

**Momentum conservation** (also known as [phase matching](@entry_id:161268)) requires that the vector sum of the signal and idler momenta equals the pump [photon momentum](@entry_id:169903): $\mathbf{k}_p = \mathbf{k}_s + \mathbf{k}_i$.

These conservation laws create powerful correlations between the two generated photons. For instance, in a non-collinear SPDC setup, where the [signal and idler photons](@entry_id:185729) emerge at different angles relative to the pump beam, their emission angles and wavelengths are inextricably linked. The conservation of momentum perpendicular to the pump direction implies that $k_s \sin\theta_s = k_i \sin\theta_i$, where $k_j = 2\pi n_j / \lambda_j$ is the magnitude of the [wavevector](@entry_id:178620) in the crystal. This relationship allows for the precise prediction of one photon's properties based on the measurement of its twin [@problem_id:2254952].

This intrinsic pairing is the foundation of the **[heralded single-photon source](@entry_id:196153)**. While the generation of a pair in SPDC is a random, probabilistic event, the photons themselves are created simultaneously. By placing a detector in the path of the idler photon, a "click" at this detector heralds the existence of its corresponding signal photon. Conditioned on this herald event, the signal channel contains a single photon with high certainty.

However, the "certainty" of this heralding is compromised by real-world imperfections. The **heralding efficiency**, defined as the probability that a signal photon is truly available at the output given a herald event, is a critical [figure of merit](@entry_id:158816). It is degraded by several factors: inefficient collection of the signal or idler photons ($\eta_{cs}$, $\eta_{ci}$), and imperfections in the heralding detector itself, such as a [quantum efficiency](@entry_id:142245) less than one ($\eta_{di}$) and the occurrence of false clicks known as **dark counts** ($p_d$). A careful [probabilistic analysis](@entry_id:261281) reveals that the heralding efficiency is a complex function of all these parameters, and a herald click does not offer an absolute guarantee of a signal photon's presence [@problem_id:2254944].

### Characterizing Real-World Sources

In practice, no [single-photon source](@entry_id:143467) is perfect. Its quality is assessed not just by its efficiency but by the quantum purity and indistinguishability of its output photons.

#### Purity and Background Contamination

A common issue in experimental setups is the contamination of the single-photon stream with unwanted background light, such as scattered light from the pump laser. Since this background is typically coherent ($g^{(2)}_{bg}(0) = 1$), it degrades the measured [antibunching](@entry_id:194774). If a [single-photon source](@entry_id:143467) with intensity $I_m$ and $g^{(2)}_m(0) = 0$ is mixed with a coherent background of intensity $I_b$, the measured [second-order coherence](@entry_id:180621) of the combined field becomes:

$g^{(2)}(0) = 1 - \left(\frac{I_m}{I_m + I_b}\right)^2$

This expression shows that any amount of background light will raise the measured $g^{(2)}(0)$ above the ideal value of zero [@problem_id:2247287]. Therefore, measuring a small but non-zero $g^{(2)}(0)$ is typical in experiments and can be used to quantify the signal-to-background ratio of the source.

#### Photon Indistinguishability and the Hong-Ou-Mandel Effect

For many quantum information protocols, it is not enough for photons to be emitted one at a time; they must also be **indistinguishable**. This means they must be identical in all degrees of freedom: wavelength, polarization, spatial mode, and temporal profile. The definitive test for photon indistinguishability is the **Hong-Ou-Mandel (HOM) effect**.

In a HOM [interferometer](@entry_id:261784), two photons are sent into the two separate input ports of a 50/50 beam splitter. Classically, one would expect the photons to exit independently, leading to a 50% chance of a [coincidence detection](@entry_id:189579). Quantum mechanics, however, predicts a startling result. If the two photons are perfectly indistinguishable and arrive simultaneously, they will always exit the beam splitter together, in the same output port. This [two-photon interference](@entry_id:166442) effect leads to a complete suppression of coincidence counts.

The degree of this suppression, often called the **HOM visibility**, is a direct measure of the photons' indistinguishability. If the photons are partially distinguishable—for example, due to a mismatch in their [polarization states](@entry_id:175130)—the interference will be incomplete, and the minimum coincidence rate will be non-zero. The probability of coincidence for two photons in internal states $|\phi_a\rangle$ and $|\phi_b\rangle$ is proportional to $1 - |\langle \phi_a | \phi_b \rangle|^2$, where $|\langle \phi_a | \phi_b \rangle|^2$ is the fidelity of their states. For example, if one photon is horizontally polarized and the other is polarized at an angle $\theta$ relative to it, the normalized minimum coincidence rate is $\sin^2(\theta)$. By measuring the depth of this "HOM dip," one can precisely quantify the degree of distinguishability between photons from one or more sources [@problem_id:2234153].

### Detecting Single Photons: Devices and Limitations

The ability to generate single photons is only half the story; one must also be able to detect them. A [single-photon detector](@entry_id:170664) is a device that can produce a macroscopic, measurable signal (typically a digital electronic pulse) in response to the absorption of a single light quantum. While many technologies exist, we will focus on their key operational principles and unavoidable imperfections.

#### Key Performance Metrics

- **Quantum Efficiency ($\eta$):** The probability that a photon incident on the detector's active area will generate a detection event.
- **Dark Count Rate:** The rate at which the detector produces spurious counts in complete darkness, caused by thermal effects or other noise sources.
- **Timing Jitter:** The statistical uncertainty in the time delay between a photon's arrival and the output of the electronic pulse.

#### Detector Saturation and Dead Time

A crucial limitation of most single-photon detectors is **[dead time](@entry_id:273487)**, $\tau_d$. After firing, the detector enters a recovery period during which it is insensitive to further incident photons. In a **non-paralyzable** detector, photons arriving during the dead time are simply ignored. This behavior leads to [detector saturation](@entry_id:183023) at high incident photon fluxes. If the average rate of incident photons is $\Phi$, the rate of potential detections is $\lambda = \eta \Phi$. However, the detector is only "live" for a fraction of the time. The average measured count rate, $R_{det}$, can be shown to follow the relation:

$R_{det} = \frac{\eta \Phi}{1 + \eta \Phi \tau_d}$

This equation shows that as the incident flux $\Phi$ becomes very large, the detected count rate approaches a maximum saturation value of $1/\tau_d$ [@problem_id:2254964]. This effect must be accounted for in any experiment involving high count rates.

#### Detector Artifacts: Afterpulsing

Another important imperfection is **afterpulsing**. This occurs when a detection event causes a charge carrier to be trapped within the detector material. This trapped charge can later be released, triggering a secondary, spurious avalanche that is correlated in time with the initial, true detection. This phenomenon can distort correlation measurements. For example, when measuring the $g^{(2)}(\tau)$ of a coherent laser ($g^{(2)}_{true}(\tau) = 1$), afterpulsing will superimpose a decaying exponential peak at small positive delay times $\tau$. The measured [correlation function](@entry_id:137198) will appear as:

$g^{(2)}_{meas}(\tau) = 1 + \frac{p_a}{R \tau_{ap}} \exp\left(-\frac{\tau}{\tau_{ap}}\right)$

Here, $p_a$ is the total probability of an afterpulse, $\tau_{ap}$ is its characteristic decay time, and $R$ is the true photon detection rate [@problem_id:2254958]. It is critical to recognize this feature as a detector artifact, as it could otherwise be mistaken for true [photon bunching](@entry_id:161039) in the light source itself.

#### Physics of Advanced Detectors: The SNSPD

To push the boundaries of detection, new technologies are constantly being developed. The **Superconducting Nanowire Single-Photon Detector (SNSPD)** offers high efficiency, low dark counts, and excellent timing resolution. Its operation is based on a fascinating physical principle. A thin, narrow wire of a superconducting material is cooled to cryogenic temperatures and biased with a DC current $I_b$ that is just below its critical current $I_c$.

According to the **hotspot model**, when a photon is absorbed by the [nanowire](@entry_id:270003), its energy breaks Cooper pairs and creates a small, localized resistive ("normal") region. This hotspot, whose size depends on the [photon energy](@entry_id:139314), expels the [bias current](@entry_id:260952) into the remaining superconducting sections of the wire on either side. If the hotspot is large enough, the [current density](@entry_id:190690) in these side channels will exceed the material's [critical current density](@entry_id:185715), triggering a cascade that forms a resistive barrier across the entire wire. This generates a measurable voltage pulse. This model predicts that the minimum photon energy required for detection, $E_{ph, min}$, depends quadratically on the [bias current](@entry_id:260952) relative to the critical current:

$E_{ph, min} = \alpha w^2 \left(1 - \frac{I_b}{I_c}\right)^2$

where $w$ is the wire width and $\alpha$ is a material-dependent parameter [@problem_id:2254962]. This relationship beautifully illustrates how the detector's sensitivity can be tuned by adjusting the electrical bias, providing a direct link between macroscopic control and microscopic quantum processes.