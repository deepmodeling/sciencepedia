## Introduction
Scanning Tunneling Microscopy (STM) and its spectroscopic counterpart, Scanning Tunneling Spectroscopy (STS), have revolutionized our ability to see and probe the world at its most fundamental level. By harnessing the quantum mechanical phenomenon of [electron tunneling](@entry_id:272729), these techniques can image individual atoms on a surface and map their electronic properties with unprecedented spatial and [energy resolution](@entry_id:180330). However, interpreting the rich data provided by an STM requires a deep understanding of the intricate physics governing the [tunnel junction](@entry_id:1133481) and the various factors that influence the measurement. This article aims to bridge the gap between principle and practice, providing a comprehensive guide to this powerful nanoscale methodology.

The journey will begin in the "Principles and Mechanisms" chapter, which lays the theoretical groundwork by exploring quantum tunneling, the Tersoff-Hamann model, and the key operational modes of the microscope. Following this, the "Applications and Interdisciplinary Connections" chapter will showcase the vast scientific impact of STM and STS, from characterizing material properties and visualizing quantum effects to probing magnetism and chemical reactions. Finally, the "Hands-On Practices" section offers a series of problems designed to solidify understanding of the practical challenges and data interpretation nuances encountered in real-world experiments.

## Principles and Mechanisms

This chapter delineates the fundamental physical principles and mechanisms that govern the operation of Scanning Tunneling Microscopy (STM) and Scanning Tunneling Spectroscopy (STS). We will begin with the quantum mechanical basis for electron tunneling, build a quantitative model for the tunneling current, explore the primary modes of instrument operation, and finally, address a series of advanced topics and refinements crucial for the accurate interpretation of experimental data.

### The Quantum Mechanical Basis of Tunneling

The operation of the STM is a direct manifestation of a quintessentially quantum mechanical phenomenon: **electron tunneling**. Classically, an electron with energy $E$ cannot exist in a region where the potential energy $V(x)$ is greater than $E$. However, quantum mechanics predicts a non-zero probability for the electron to traverse such a "classically forbidden" region. In the context of STM, this region is the vacuum gap separating a conductive tip and a sample surface.

#### The Tunneling Probability and WKB Approximation

We can model the vacuum gap, to a first approximation, as a one-dimensional rectangular potential barrier of width $z$ (the tip-sample distance) and height $\phi$ (the effective work function or barrier height) relative to the energy of the tunneling electron. For an electron with energy $E  \phi$, the time-independent Schrödinger equation inside the barrier ($0  x  z$) is:

$$
-\frac{\hbar^2}{2m} \frac{d^2\psi(x)}{dx^2} + \phi \psi(x) = E \psi(x)
$$

Rearranging this gives:

$$
\frac{d^2\psi(x)}{dx^2} = \frac{2m(\phi-E)}{\hbar^2} \psi(x) = \kappa^2 \psi(x)
$$

where we have defined the **inverse decay length**, $\kappa$:

$$
\kappa = \sqrt{\frac{2m(\phi-E)}{\hbar^2}}
$$

The general solution to this equation is a linear combination of exponentially decaying and growing functions, $\psi(x) = A e^{-\kappa x} + B e^{\kappa x}$. For a particle incident from the left, the physically relevant solution inside the barrier is a decaying wave, $\psi(x) \propto e^{-\kappa x}$.

The probability that an electron will successfully tunnel through the barrier is given by the **[transmission probability](@entry_id:137943)**, $T$. For a barrier that is wide compared to the electron's decay length (i.e., $\kappa z \gg 1$), the **Wentzel-Kramers-Brillouin (WKB) approximation** provides an excellent and generalizable result. The WKB method shows that the wavefunction amplitude decays exponentially within the barrier, $\psi(z) \propto \exp(-\int_0^z \kappa(x) dx)$. Since the [transmission probability](@entry_id:137943) is proportional to the squared magnitude of the wavefunction, $|\psi(z)|^2$, we find:

$$
T \propto \left| \exp\left(-\int_0^z \kappa(x) dx\right) \right|^2 = \exp\left(-2\int_0^z \kappa(x) dx\right)
$$

For our simple rectangular barrier, $\kappa$ is constant, and the integral becomes $\kappa z$. Thus, the transmission probability simplifies to:

$$
T \propto \exp(-2\kappa z)
$$

The tunneling current, $I$, which is the net flow of electrons per unit time, is directly proportional to this transmission probability. Therefore, the current exhibits a dramatic exponential dependence on the tip-sample distance:

$$
I \propto \exp(-2\kappa z)
$$

This extreme sensitivity is the cornerstone of STM's remarkable vertical resolution. The factor of 2 in the exponent arises directly from the fact that current is a [probability flux](@entry_id:907649), which scales with the square of the wavefunction's amplitude .

To appreciate the magnitude of this sensitivity, consider a typical metal-vacuum-metal junction with a barrier height of $\phi \approx 4.0 \, \text{eV}$. The inverse decay length is approximately $\kappa \approx 1.0 \, \text{\AA}^{-1}$. An increase in the tip-sample distance of just $1 \, \text{\AA}$ ($0.1 \, \text{nm}$) would decrease the current by a factor of $\exp(-2 \times 1.0 \, \text{\AA}^{-1} \times 1 \, \text{\AA}) = \exp(-2) \approx 0.135$, which is nearly an [order of magnitude](@entry_id:264888) reduction in current .

This exponential relationship also makes the STM exquisitely sensitive to [mechanical vibrations](@entry_id:167420). Any small, unwanted fluctuation in the tip-sample distance, $\delta z(t)$, will be amplified into a large fluctuation in the tunneling current. The fractional change in current is given by the [logarithmic derivative](@entry_id:169238):

$$
\frac{\delta I}{I} \approx \frac{d(\ln I)}{dz} \delta z = (-2\kappa) \delta z
$$

For a typical barrier, $|-2\kappa|$ is on the order of $20 \, \text{nm}^{-1}$. This means a vibration causing a minuscule $1 \, \text{pm}$ RMS displacement of the tip would induce a substantial current noise of about $2\%$ RMS. Consequently, heroic efforts in mechanical [vibration isolation](@entry_id:275967) are essential for the stable operation of an STM. For instance, to limit junction displacement noise to $1.0 \, \text{pm}$ RMS from a typical floor vibration of $5.0 \, \text{nm}$ peak amplitude at $60 \, \text{Hz}$, a passive isolation system would need a [transmissibility](@entry_id:756124) of less than $3 \times 10^{-4}$ .

### Tunneling Current and Spectroscopic Information

While the WKB model captures the dominant distance dependence, a more [complete theory](@entry_id:155100) is needed to understand how STM and STS probe the electronic properties of a material. This is provided by the **Bardeen transfer Hamiltonian formalism**, first applied to STM by Tersoff and Hamann.

#### The Bardeen Formalism and Local Density of States (LDOS)

Within this framework, the net tunneling current is calculated using Fermi's Golden Rule. It is expressed as an integral over all energies, accounting for the density of available initial states, the density of available final states, and the [tunneling probability](@entry_id:150336) between them. At a finite temperature $T$ and with a bias voltage $V$ applied to the sample (relative to the tip), the current $I$ is given by:

$$
I(V) \propto \int_{-\infty}^{\infty} \rho_s(\mathbf{r}_0, E) \rho_t(E-eV) |M|^2 [f(E-eV) - f(E)] dE
$$

Here, several key terms appear:
- $\rho_s(\mathbf{r}_0, E)$ is the **sample's Local Density of States (LDOS)** at the position of the tip apex $\mathbf{r}_0$ and at energy $E$ relative to the sample's Fermi level ($E_F^s$). It is formally defined as $\rho_s(\mathbf{r}, E) \equiv \sum_n |\psi_n(\mathbf{r})|^2 \delta(E - E_n)$, where $\psi_n$ are the sample's electronic wavefunctions. The LDOS is a measure of the number of electronic states per unit energy and unit volume at a specific point in space.
- $\rho_t(E-eV)$ is the DOS of the tip.
- $|M|^2$ is the tunneling [matrix element](@entry_id:136260), which includes the exponential decay factor $\exp(-2\kappa z)$. For simplicity in this expression, its energy dependence is often absorbed into the LDOS terms.
- $f(E)$ is the Fermi-Dirac distribution, $f(E) = [1 + \exp(E/k_B T)]^{-1}$ (assuming the chemical potential is at $E=0$). The term $[f(E-eV) - f(E)]$ ensures that tunneling only occurs from occupied states on one side to unoccupied states on the other.

A crucial simplification, known as the **Tersoff-Hamann model**, assumes a simple metallic tip with a constant DOS ($\rho_t$ is constant) and a spherically symmetric, **[s-wave](@entry_id:754474)** apex wavefunction. Under these conditions, the tunneling [matrix element](@entry_id:136260) becomes independent of the specific character of the sample wavefunctions, and the tunneling current at low temperature ($T \to 0$) and small bias voltage $V$ simplifies significantly. At $T=0$, the Fermi-Dirac functions become [step functions](@entry_id:159192), and the integral is restricted to the energy window between the tip and sample Fermi levels, i.e., from $0$ to $eV$. The current becomes:

$$
I(\mathbf{r}_0, V) \propto \int_{0}^{eV} \rho_s(\mathbf{r}_0, E) dE
$$

This expression reveals that the tunneling current is proportional to the integrated LDOS of the sample over the energy range made accessible by the bias voltage.

#### Scanning Tunneling Spectroscopy (STS)

The true power of this relationship is unleashed when we consider the differential conductance, $dI/dV$. By applying the Leibniz integral rule to the expression above, we find a remarkably direct relationship:

$$
\frac{dI}{dV}(\mathbf{r}_0, V) \propto \rho_s(\mathbf{r}_0, E_F^s + eV)
$$

This result is the central principle of **Scanning Tunneling Spectroscopy (STS)**: the differential conductance measured at a bias voltage $V$ is directly proportional to the sample's Local Density of States at the position of the tip and at an energy $eV$ above the sample's Fermi level . By sweeping the bias voltage and measuring $dI/dV$ (typically with a [lock-in amplifier](@entry_id:268975)), one can map out the electronic spectrum of the sample surface with atomic-scale spatial resolution.

### Modes of Operation and Image Interpretation

An STM can be operated in two primary imaging modes, which represent different trade-offs between speed, safety, and the physical quantity being measured.

#### Constant-Current Mode

In **[constant-current mode](@entry_id:184685)**, a feedback loop actively adjusts the vertical position of the tip, $z$, to maintain a constant tunneling current setpoint, $I_0$, as the tip is scanned laterally across the surface ($\mathbf{r}$). The recorded image is a map of the required tip height, $z(\mathbf{r})$. This is the most common mode of operation.

Because the feedback loop continuously compensates for height variations, this mode is highly tolerant to thermal drift and can safely navigate surfaces with significant topography (hills and valleys) without crashing the tip. However, its imaging speed is fundamentally limited by the mechanical [response time](@entry_id:271485) of the [piezoelectric scanner](@entry_id:193262) and the bandwidth of the feedback electronics . For a typical feedback loop with a bandwidth of $f_b = 1 \, \text{kHz}$, the time constant is $\tau \approx 1/(2\pi f_b) \approx 0.16 \, \text{ms}$. To ensure accurate height measurement at each pixel, one must wait for the feedback to settle, typically for about $5\tau$, limiting the pixel acquisition rate to around $1.3 \times 10^3 \, \text{s}^{-1}$.

In this mode, the measured topography is not purely geometric. By holding the current constant ($I_0 \propto \rho_s(\mathbf{r}, E_F) \exp[-2\kappa z(\mathbf{r})]$), the recorded height $z(\mathbf{r})$ must vary to compensate for changes in the LDOS. Solving for $z(\mathbf{r})$ reveals:

$$
z(\mathbf{r}) = z_0 - \frac{1}{2\kappa} \ln\left( \frac{\rho_s(\mathbf{r}, E_F)}{\rho_{\text{ref}}} \right)
$$

This shows that the apparent height is logarithmically dependent on the [local density of states](@entry_id:136852). Regions with higher LDOS will appear as depressions in the constant-current image, as the tip must retract to keep the current constant. This phenomenon is known as **electronic corrugation**. For instance, a surface with a sinusoidal LDOS modulation of $\rho_s \propto [1 + 0.12 \cos(\mathbf{G}\cdot\mathbf{r})]$ would produce an apparent topographic corrugation of about $11 \, \text{pm}$ for a typical barrier height of $4.6 \, \text{eV}$, even if the surface is geometrically flat .

#### Constant-Height Mode

In **constant-height mode**, the feedback loop is turned off, and the tip is scanned at a fixed average height above the surface. The measured quantity is the variation in the tunneling current, $I(\mathbf{r})$. According to the Tersoff-Hamann model, this current map is a direct image of the sample's LDOS at the Fermi level, $I(\mathbf{r}) \propto \rho_s(\mathbf{r}, E_F)$.

The primary advantage of this mode is speed. Since it is not limited by the mechanical feedback loop, imaging can be performed at rates limited only by the bandwidth of the [current amplifier](@entry_id:274238) and data acquisition system, which can be orders of magnitude faster than in [constant-current mode](@entry_id:184685). However, this mode is only suitable for atomically flat surfaces and in ultra-stable, low-drift environments. Any significant topographic feature could cause a catastrophic tip crash, and any vertical drift will appear as a large, unwanted gradient in the current map .

### Advanced Spectroscopic Principles and Artifacts

The relation $dI/dV \propto \rho_s$ is an idealization. In practice, several other physical effects can influence the measured spectra and must be understood for accurate data interpretation.

#### Energy Dependence of the Tunneling Process

The simple STS model assumes the [tunneling probability](@entry_id:150336) is constant over the bias window. However, the WKB [transmission probability](@entry_id:137943) $T(E) \propto \exp(-2\kappa z)$ contains the energy-dependent term $\kappa = \sqrt{2m(\phi-E)/\hbar^2}$. As the energy $E$ of a tunneling electron increases, the effective barrier it faces, $\phi-E$, decreases, and its transmission probability increases. Furthermore, applying a finite bias $V$ distorts the [potential barrier](@entry_id:147595) from a rectangle to a trapezoid, which can be approximated by an effective barrier height $\bar{\phi} \approx \phi - e|V|/2$ for small biases .

The full expression for the differential conductance more accurately includes this energy-dependent transmission factor, $T(E, V)$. The measured $dI/dV$ spectrum is therefore not purely the sample LDOS, but a product:

$$
\frac{dI}{dV}(V) \propto \rho_s(E_F+eV) \cdot T(E_F+eV, V)
$$

This transmission function $T(E,V)$ typically acts as a smooth, exponentially increasing background that can distort the true shape and intensity of features in $\rho_s$. A common technique to mitigate this is to normalize the differential conductance, for example by dividing by the total conductance $I/V$. Under the simplifying assumption that the kernel $K(E,z)$ is energy-independent, the **normalized differential conductance** becomes  :

$$
G_N(V) = \frac{dI/dV}{I/V} = \frac{e V \rho_{s}(eV)}{\int_{0}^{eV} \rho_{s}(E') dE'}
$$

This quantity represents the LDOS at energy $eV$ normalized by its running average up to that energy. This normalization can effectively remove the strong distance dependence and suppress the smooth energy-dependent background, thus providing a better representation of the intrinsic LDOS features.

#### Finite Temperature Effects

All real experiments are performed at a finite temperature $T$, which causes thermal broadening of spectral features. At finite $T$, the sharp step of the Fermi-Dirac distribution is smeared over an energy range of a few $k_B T$. As a result, the measured differential conductance is not the true LDOS, but rather a convolution of the LDOS with a thermal broadening function. This can be derived by differentiating the finite-temperature current integral, which yields:

$$
\frac{dI}{dV}(V) \propto \int_{-\infty}^{\infty} \rho_s(E) \left[-\frac{df(E-eV)}{dE}\right] dE
$$

The measured spectrum is a convolution of $\rho_s(E)$ with the broadening kernel $K_T(E) = -df(E)/dE$. This kernel is a symmetric, bell-shaped function, $\frac{1}{4k_B T} \text{sech}^2\left(\frac{E}{2k_B T}\right)$, peaked at $E=0$. An intrinsically sharp feature in the LDOS, like a delta function $\delta(E-E_0)$, will be measured as a peak with this sech-squared lineshape. The full width at half maximum (FWHM) of this thermal broadening is exactly $2 \ln(3+2\sqrt{2}) k_B T \approx 3.53 k_B T$. At a typical low temperature of $T=5\,\text{K}$, this corresponds to an intrinsic energy broadening of about $1.52\,\text{meV}$, setting a fundamental limit on the achievable spectroscopic resolution .

#### Tip Orbital Effects: Beyond the [s-wave](@entry_id:754474) Approximation

The Tersoff-Hamann model's assumption of an [s-wave](@entry_id:754474) tip is a powerful simplification, but it fails to describe many experimental observations. Real STM tips can have apex states with higher angular momentum, such as **p-like** or **d-like** character. According to **Chen's derivative rule**, a tip orbital with a specific symmetry selectively probes the corresponding spatial derivative of the sample's wavefunction at the tip's location.
- An **[s-wave](@entry_id:754474) tip** ($l=0$) measures the wavefunction amplitude itself: $I \propto |\psi_s(\mathbf{r}_0)|^2$.
- A **$p_z$-wave tip** ($l=1$, aligned along the surface normal) measures the vertical gradient: $I \propto |\partial\psi_s/\partial z|^2$.
- A **$d_{z^2}$-wave tip** ($l=2$) measures a combination of second derivatives: $I \propto |(2\partial^2/\partial z^2 - \partial^2/\partial x^2 - \partial^2/\partial y^2)\psi_s|^2$.

This has profound consequences for [image contrast](@entry_id:903016). For example, when imaging a surface state with $d_{z^2}$ character, which has maximum amplitude on-axis, a $p_z$ tip will also show maximum intensity on top of the atom. A $d_{z^2}$ tip, however, will show a dramatically enhanced and sharpened on-top maximum, because both the vertical and lateral second-derivative terms in its operator contribute constructively at the orbital's center . Understanding the tip state is therefore critical for interpreting sub-atomic and chemical contrast.

#### Spectroscopy on Semiconductors: Tip-Induced Band Bending

When performing STS on a semiconductor, an additional complication arises: **Tip-Induced Band Bending (TIBB)**. The electric field from the biased tip penetrates the semiconductor and repels or attracts mobile carriers, creating a **[space-charge region](@entry_id:136997)** near the surface. This causes the semiconductor's energy bands (conduction and valence bands) to bend relative to their positions in the neutral bulk.

For example, above a p-type semiconductor, a positive sample bias will repel holes from the surface, creating a negatively charged **depletion region** of ionized acceptors. The electrostatic potential $\phi(z)$ in this region is governed by the **Poisson equation**:

$$
\nabla^2 \phi = -\frac{\rho}{\varepsilon_s}
$$

In the 1D depletion approximation for a uniformly doped sample, the charge density $\rho = -qN_A$ is constant, and solving the equation with appropriate boundary conditions yields a parabolic potential profile. If a fraction $\eta$ of the applied bias $V$ drops across the semiconductor, the potential is given by :

$$
\phi(z) = \frac{qN_A}{2\varepsilon_s} \left( z - \sqrt{\frac{2\varepsilon_s \eta V}{qN_A}} \right)^2
$$

This band bending means that the energy of a spectral feature measured by STS does not directly correspond to its energy in the flat-band condition. The applied voltage $V$ is partitioned between the vacuum gap and the semiconductor, and careful modeling is required to deconvolve the intrinsic electronic structure from the effects of TIBB.