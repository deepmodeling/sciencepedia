## Introduction
Radio Frequency (RF) waves are a critical tool in modern fusion energy research, providing essential mechanisms for heating plasmas to fusion temperatures and driving electrical currents for stable confinement. Accurately modeling the propagation of these waves through the complex, magnetized plasma environment is a significant computational challenge. While full-wave simulations based on Maxwell's equations offer a complete description, their computational cost is often prohibitive. The ray tracing method, based on the geometric optics approximation, provides a powerful, efficient, and physically intuitive alternative for scenarios where the wave properties vary slowly. This article provides a comprehensive overview of ray tracing for RF wave propagation. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, deriving the ray equations from the eikonal ansatz and the Hamiltonian formulation. Building on this foundation, the second chapter, **Applications and Interdisciplinary Connections**, will explore how ray tracing is used to design and analyze practical heating and current drive systems and demonstrate its conceptual links to other scientific fields. Finally, **Hands-On Practices** will offer practical exercises to solidify understanding of the computational implementation. We begin by examining the fundamental principles that allow us to reduce a complex wave problem to the tractable task of tracing rays.

## Principles and Mechanisms

The propagation of radio frequency (RF) waves through the complex, inhomogeneous, and anisotropic medium of a magnetized fusion plasma is a cornerstone of strategies for plasma heating, current drive, and diagnostic measurements. While a complete description requires solving Maxwell's equations coupled with a kinetic plasma model—a computationally formidable task known as a "full-wave" simulation—a powerful and widely used simplification is available when the wave's properties change slowly over the scale of a single wavelength. This is the domain of **geometric optics**, a method that reduces wave propagation to the tracing of rays. This chapter elucidates the fundamental principles and mechanisms underpinning the geometric optics approximation and its computational implementation via ray tracing.

### The Geometric Optics Approximation and the Eikonal Ansatz

The foundation of geometric optics lies in a crucial assumption about scale separation. Consider a time-harmonic electromagnetic wave of angular frequency $\omega$ propagating in a plasma whose properties, such as electron density $n_e(\mathbf{r})$ and magnetic field $\mathbf{B}_0(\mathbf{r})$, vary on a characteristic spatial scale $L$. The geometric optics approximation is valid when the local wavelength of the wave, $\lambda$, is much smaller than this scale length $L$. Mathematically, if we define the local wavevector as $\mathbf{k}(\mathbf{r})$, with magnitude $k = |\mathbf{k}| = 2\pi/\lambda$, the fundamental condition for the validity of geometric optics is:

$$
kL \gg 1
$$

This condition implies that over the distance of one wavelength, the plasma appears nearly homogeneous. This insight motivates seeking a solution to the wave equation of the form of a locally plane wave, known as the **eikonal ansatz** or **WKB (Wentzel-Kramers-Brillouin) approximation** [@problem_id:4038232]:

$$
\mathbf{E}(\mathbf{r}) = \mathcal{E}(\mathbf{r}) e^{iS(\mathbf{r})}
$$

Here, $S(\mathbf{r})$ is a rapidly varying real phase function, called the **eikonal**, and $\mathcal{E}(\mathbf{r})$ is a slowly varying complex vector that contains the wave's amplitude and polarization. The "slowness" of $\mathcal{E}(\mathbf{r})$ and the "rapidity" of $S(\mathbf{r})$ are direct consequences of the scale separation $kL \gg 1$. The gradient of the eikonal defines the local wavevector [@problem_id:4038228]:

$$
\mathbf{k}(\mathbf{r}) = \nabla S(\mathbf{r})
$$

When the eikonal ansatz is substituted into the governing wave equation (derived from Maxwell's equations), the derivatives of the slow amplitude $\mathcal{E}(\mathbf{r})$ are smaller than terms involving the large phase gradient $\mathbf{k}$ by a factor of order $1/(kL)$. By neglecting these smaller terms, we arrive at a leading-order algebraic equation for the field. This equation is non-trivial only if the determinant of its coefficient matrix vanishes, which yields the **local dispersion relation**: an equation of the form $D(\omega, \mathbf{k}, \mathbf{r}) = 0$. This relation constrains the possible wavevectors $\mathbf{k}$ that can exist at a given frequency $\omega$ and position $\mathbf{r}$.

A practical measure of accuracy for the geometric optics approximation can be formulated based on the small parameter $\eta \sim 1/(kL)$. For instance, requiring that the first-order correction to the wave amplitude be no more than 5% implies a condition $\eta \le 0.05$, which translates to a minimum required wavenumber of $k_{\min} = 20/L$ [@problem_id:4038265]. This highlights that shorter wavelengths and more gradual plasma gradients favor the accuracy of ray tracing.

Furthermore, the approximation implicitly assumes that wave damping is weak. If the wave is heavily damped, its amplitude changes significantly over a single wavelength, violating the "slowly varying amplitude" assumption. This introduces a second condition for validity: the wave frequency must be much larger than any effective collision or damping frequency $\nu$ [@problem_id:4038232].

$$
\omega \gg \nu
$$

### The Hamiltonian Formulation of Ray Tracing

The local dispersion relation $D(\omega, \mathbf{k}, \mathbf{r}) = 0$ is the central equation of motion in geometric optics. It can be viewed as a constraint surface in the phase space of $(\mathbf{r}, \mathbf{k})$. The path that a wave packet, or ray, follows through this phase space is governed by a set of equations formally identical to Hamilton's equations in classical mechanics, where the frequency $\omega(\mathbf{r}, \mathbf{k})$ serves as the Hamiltonian. The **ray equations** are [@problem_id:4038253]:

$$
\frac{d\mathbf{r}}{dt} = \frac{\partial \omega}{\partial \mathbf{k}} \equiv \mathbf{v}_g \quad ; \quad \frac{d\mathbf{k}}{dt} = -\frac{\partial \omega}{\partial \mathbf{r}}
$$

The first equation defines the ray's trajectory in real space; the velocity of the ray is the **group velocity** $\mathbf{v}_g$, which describes the transport of wave energy. The second equation describes how the wavevector $\mathbf{k}$ evolves—or "refracts"—as the ray propagates through the inhomogeneous medium. Integrating this system of ordinary differential equations yields the ray path $\mathbf{r}(t)$ and the evolution of the wavevector $\mathbf{k}(t)$ along it.

This Hamiltonian framework provides deep insights into conserved quantities. Because $\omega$ does not explicitly depend on time, it is a conserved quantity along the ray: $\frac{d\omega}{dt} = 0$. This reflects the conservation of wave energy in a time-invariant medium. Furthermore, if the plasma equilibrium is symmetric with respect to a spatial coordinate (e.g., invariant under translation in the $y$-direction), then $\partial \omega / \partial y = 0$. According to the ray equations, this implies $\frac{dk_y}{dt} = 0$, meaning the corresponding component of the wavevector is a constant of motion. This is a direct manifestation of Noether's theorem, linking symmetry to conservation laws [@problem_id:4038253].

As a concrete example, consider the **Ordinary (O-mode)** wave in a cold, unmagnetized or perpendicularly magnetized plasma. Its dispersion relation is $\omega^2 = c^2 k^2 + \omega_{pe}^2(\mathbf{r})$, where $\omega_{pe}$ is the electron plasma frequency. The Hamiltonian is $\omega(\mathbf{r}, \mathbf{k}) = \sqrt{c^2(k_x^2 + k_y^2 + k_z^2) + \omega_{pe}^2(\mathbf{r})}$. The ray equations are readily found:

$$
\frac{d\mathbf{r}}{dt} = \frac{c^2 \mathbf{k}}{\omega} \quad ; \quad \frac{d\mathbf{k}}{dt} = -\frac{1}{2\omega} \nabla(\omega_{pe}^2)
$$

These equations show that the ray refracts away from regions of higher plasma density, as $\nabla(\omega_{pe}^2)$ points in the direction of increasing density. A numerical implementation can integrate these equations to trace the ray's path and verify the conservation of $\omega$ and any symmetry-related components of $\mathbf{k}$ [@problem_id:4038253].

### The Plasma Dielectric Tensor

To apply the ray tracing formalism, one must first obtain the dispersion relation $\omega(\mathbf{r}, \mathbf{k})$. This is derived from the specific properties of the plasma medium, which are encapsulated in the **dielectric tensor** $\boldsymbol{\varepsilon}$. Starting from the linearized momentum equation for cold, collisionless plasma species (electrons and ions) in a magnetic field $\mathbf{B}_0$, one can derive the plasma's current response to a wave's electric field. This leads to the dielectric tensor, which relates the displacement field $\mathbf{D}$ to the electric field $\mathbf{E}$ via $\mathbf{D} = \varepsilon_0 \boldsymbol{\varepsilon} \cdot \mathbf{E}$.

In a coordinate system where the magnetic field $\mathbf{B}_0$ is aligned with the $z$-axis, the dielectric tensor takes a characteristic gyrotropic form. It is commonly expressed in terms of the **Stix parameters** $S$ (Sum), $D$ (Difference), and $P$ (Plasma) [@problem_id:4038235]:

$$
\boldsymbol{\varepsilon} = \begin{pmatrix} S  -iD  0 \\ iD  S  0 \\ 0  0  P \end{pmatrix}
$$

These parameters are functions of the wave frequency $\omega$ and the fundamental frequencies of the plasma species $s$ (electrons and ions):

-   **Plasma Frequency:** $\omega_{ps}^2 = \frac{n_s q_s^2}{\varepsilon_0 m_s}$, related to collective charge oscillations.
-   **Cyclotron Frequency:** $\Omega_s = \frac{q_s B_0}{m_s}$, the frequency of gyration around magnetic field lines. Note that $\Omega_s$ is a signed quantity depending on the charge $q_s$.

The Stix parameters are given by sums over all plasma species:

$$
S = 1 - \sum_s \frac{\omega_{ps}^2}{\omega^2 - \Omega_s^2} \quad ; \quad D = \sum_s \frac{\Omega_s}{\omega} \frac{\omega_{ps}^2}{\omega^2 - \Omega_s^2} \quad ; \quad P = 1 - \sum_s \frac{\omega_{ps}^2}{\omega^2}
$$

The general dispersion relation for electromagnetic waves is then found by solving $\det[ \mathbf{k}\mathbf{k} - k^2\mathbf{I} + \frac{\omega^2}{c^2}\boldsymbol{\varepsilon} ] = 0$. This equation, together with the definitions of $S$, $D$, and $P$, forms the complete basis for ray tracing in a cold magnetized plasma.

### Wave Polarization and Birefringence: The Refractive Index Surface

The dispersion relation derived from the Stix tensor is a biquadratic equation for the refractive index magnitude $n = ck/\omega$. This means that for any given direction of propagation $\hat{\mathbf{k}} = \mathbf{k}/k$, there are generally two distinct solutions for $n^2$, corresponding to two different wave modes that can propagate with different speeds and polarizations. This property is known as **birefringence**.

A powerful way to visualize this anisotropic, birefringent nature is through the **refractive index surface**. This is a surface in "index space" (a 3D space with coordinates $(n_x, n_y, n_z)$) formed by plotting the vector $\mathbf{n} = n(\hat{\mathbf{k}}) \hat{\mathbf{k}}$ for all possible propagation directions $\hat{\mathbf{k}}$ [@problem_id:4064632]. Due to the two solutions for $n$, this surface consists of two distinct sheets. Each sheet corresponds to a particular wave mode with a well-defined (and generally elliptical) polarization.

The character of these modes is most easily understood in limiting cases:
-   **Parallel Propagation ($\mathbf{k} \parallel \mathbf{B}_0$):** The two modes become the right-hand circularly polarized (RHCP) wave and the left-hand circularly polarized (LHCP) wave.
-   **Perpendicular Propagation ($\mathbf{k} \perp \mathbf{B}_0$):** The two modes are the linearly polarized **Ordinary (O) wave**, with its electric field parallel to $\mathbf{B}_0$, and the elliptically polarized **Extraordinary (X) wave**, with its electric field in the plane perpendicular to $\mathbf{B}_0$.

The shape and topology of these two sheets dictate the propagation and accessibility of RF waves in a fusion device.

### Breakdown of Geometric Optics: Critical Regions and Phenomena

The elegance of ray tracing lies in its reduction of a complex wave problem to a set of simple ODEs. However, this approximation is not universally valid. It breaks down in regions where its fundamental assumption, $kL \gg 1$, is violated, or where other rapid changes occur. Understanding these limitations is critical for the correct application and interpretation of ray tracing results.

#### Cutoffs

A **cutoff** is a surface in the plasma where the refractive index for a wave mode goes to zero ($n \to 0$), which implies the wavenumber also vanishes ($k \to 0$). As a ray approaches a cutoff, its wavelength $\lambda = 2\pi/k$ diverges to infinity, catastrophically violating the condition $\lambda \ll L$. Physically, the wave can no longer propagate and is reflected. For the O-mode, the cutoff occurs where the parameter $P=0$, or $\omega = \omega_{pe}$. A classic analysis using WKB theory matched to an Airy function solution across this turning point shows that for a lossless plasma, the power reflection coefficient is exactly unity [@problem_id:4038244]. This means all incident wave energy is reflected from the cutoff surface.

#### Resonances

In stark contrast to a cutoff, a **resonance** is a surface where the refractive index for a wave mode tends to infinity ($n \to \infty$, $k \to \infty$). Examples include cyclotron resonances, where the wave frequency matches a harmonic of a species' gyrofrequency ($\omega = n\Omega_s$), and hybrid resonances. Naively, one might think that since $k \to \infty$, the condition $kL \gg 1$ becomes even better satisfied. However, the geometric optics approximation fails for a different reason. As a ray approaches a resonance, its group velocity component normal to the resonant surface slows to zero. The ray spends a very long time in the vicinity of the resonance. In any realistic plasma, even a tiny amount of dissipation (modeled by a small imaginary part in the dielectric tensor) will cause the wave to be completely absorbed during this extended interaction time [@problem_id:4038236]. Mathematically, dissipation makes the wavevector complex, $\mathbf{k} = \operatorname{Re}(\mathbf{k}) + i\operatorname{Im}(\mathbf{k})$. The imaginary part $\operatorname{Im}(\mathbf{k})$ becomes very large at the resonance, leading to strong spatial damping of the wave amplitude according to $e^{-\int \operatorname{Im}(\mathbf{k}) \cdot d\mathbf{s}}$. Thus, resonances are regions of strong absorption, not reflection.

#### Mode Conversion

Simple ray tracing treats the two wave modes (the two sheets of the refractive index surface) as independent. This assumption, known as **adiabatic following**, holds when the eigenvalues (the refractive indices) of the two modes are well-separated. The criterion for adiabaticity is that the rate of change of the polarization eigenvectors along the ray, quantified by a coupling coefficient $\mathcal{C}(s) = \langle \mathbf{e}_- | d\mathbf{e}_+ / ds \rangle$, must be much smaller than the difference in wavenumbers, $\Delta k = k_+ - k_-$ [@problem_id:4038240].

However, if the plasma parameters vary such that the two sheets of the refractive index surface approach each other or cross, the eigenvalues become degenerate or nearly degenerate ($\Delta k \approx 0$). In this "mode conversion zone," the adiabatic approximation breaks down, and energy can be transferred from one mode to another. To model this, one must abandon simple ray tracing and solve a system of coupled-mode equations [@problem_id:4038223]. The probability of such a non-adiabatic transition is given by the **Landau-Zener formula**, which for a linear crossing of eigenvalues takes the form:

$$
P_{\mathrm{conv}} \simeq \exp\left(-2\pi \frac{|\mathcal{C}(s_0)|^2}{|d(\Delta k)/ds|_{s_0}}\right)
$$

where $s_0$ is the location of the degeneracy. This shows that conversion is significant when the coupling $\mathcal{C}$ is large or when the eigenvalues cross slowly.

### Applicability to Fusion Plasmas: A Practical Perspective

The principles outlined above have direct implications for modeling RF waves in tokamaks. Two of the most important wave schemes are Electron Cyclotron (EC) waves and Lower Hybrid (LH) waves.

-   **Electron Cyclotron (EC) Waves:** These waves operate at very high frequencies (e.g., 100-170 GHz), resulting in very short wavelengths ($\lambda \sim$ millimeters). In the hot, dense core of a tokamak where density scale lengths are on the order of tens of centimeters, the condition $kL \gg 1$ is exceptionally well satisfied. Consequently, ray tracing is a highly accurate and reliable tool for modeling EC wave propagation and absorption, provided the ray path avoids cutoffs [@problem_id:4038265].

-   **Lower Hybrid (LH) Waves:** These waves have lower frequencies (e.g., 1-8 GHz) but are launched such that they excite a "slow wave" branch with a very large refractive index and a correspondingly short wavelength in the plasma core. Therefore, ray tracing is also often applicable deep inside the plasma. However, LH waves must be launched from the low-density edge and propagate through regions of steep gradients where the geometric optics approximation can be marginal. Furthermore, their propagation is often characterized by multiple reflections from the plasma edge and complex spectral evolution, making their modeling a more challenging application of ray tracing.

In summary, ray tracing provides a physically intuitive and computationally efficient framework for modeling RF wave propagation. Its successful application requires not only solving the Hamiltonian ray equations but also a keen awareness of its limitations—cutoffs, resonances, and mode conversion zones—where the simple picture of rays propagating independently breaks down and must be augmented by more complete physical models.