## Introduction
Scattering experiments are the primary method for investigating the fundamental forces of nature, from the interactions between nucleons to the behavior of electrons in a solid. However, the raw data from these experiments—the number of particles scattered in different directions—does not directly reveal the underlying physics. A robust theoretical framework is required to bridge the gap between experimental observables and the quantum mechanical interactions that govern them. This is the role of scattering theory, with the concept of the phase shift standing as its central pillar. Understanding how a potential alters the phase of a scattered wave allows us to decode the interaction's strength, range, and structure.

This article provides a graduate-level journey into the theory and application of scattering and [phase shifts](@entry_id:136717). We will begin by establishing the core theoretical framework, then explore its profound impact across multiple scientific disciplines, and finally offer opportunities for practical application.
-   **Chapter 1: Principles and Mechanisms** lays the groundwork, defining the scattering amplitude and cross section from the Schrödinger equation. It introduces the powerful method of [partial wave analysis](@entry_id:136738) and shows how the problem is reduced to calculating phase shifts, exploring their behavior at low energies and near resonances.
-   **Chapter 2: Applications and Interdisciplinary Connections** demonstrates the remarkable versatility of [phase shift analysis](@entry_id:158865), showing how it is used to constrain nuclear forces, extract [observables](@entry_id:267133) from finite-volume simulations, design computational tools in materials science, and even reveal universal phenomena in atomic and [few-body systems](@entry_id:749300).
-   **Chapter 3: Hands-On Practices** provides a set of computational problems designed to solidify these theoretical concepts, guiding you through solving the Lippmann-Schwinger equation and extracting [interaction parameters](@entry_id:750714) from scattering data.

We will start by building our understanding from first principles, beginning with the fundamental mechanisms of quantum scattering.

## Principles and Mechanisms

In the study of nuclear systems, scattering experiments are the primary tool for probing the fundamental forces between nucleons and the structure of atomic nuclei. The theoretical framework for interpreting these experiments is [scattering theory](@entry_id:143476). This chapter lays out the core principles and mechanisms of nonrelativistic [potential scattering](@entry_id:185768), progressing from the foundational definitions of scattering [observables](@entry_id:267133) to the more complex phenomena encountered in realistic nuclear systems. We will establish the concepts of the scattering amplitude and [phase shifts](@entry_id:136717), and explore their behavior in various physical contexts, including low-energy interactions, [resonant scattering](@entry_id:185638), and reactions involving identical particles, [coupled channels](@entry_id:204758), long-range forces, and inelasticity.

### The Scattering Amplitude and Cross Section

The central problem in [scattering theory](@entry_id:143476) is to determine the outcome of a collision between an incident particle and a target. In the [center-of-mass frame](@entry_id:158134), this is equivalent to describing the motion of a single particle of [reduced mass](@entry_id:152420) $\mu$ scattering from a fixed potential $V(\mathbf{r})$. The state of the system is described by a wave function $\psi(\mathbf{r})$ that is a stationary solution to the time-independent Schrödinger equation:
$$
\left[-\frac{\hbar^{2}}{2\mu}\nabla^{2}+V(\mathbf{r})\right]\psi(\mathbf{r})=E\,\psi(\mathbf{r})
$$
where $E = \frac{\hbar^2 k^2}{2\mu}$ is the kinetic energy, and $k=|\mathbf{k}|$ is the wave number corresponding to the relative momentum $\hbar\mathbf{k}$.

While the Schrödinger equation admits many solutions, a physical scattering solution is uniquely defined by its asymptotic behavior at large distances from the potential. A [scattering experiment](@entry_id:173304) involves preparing a particle in a momentum eigenstate, which is represented by a plane wave $e^{i\mathbf{k}\cdot\mathbf{r}}$. After interacting with the potential, the particle scatters outwards. This physical picture is encoded in the asymptotic boundary condition for the wave function, which must consist of the incident plane wave plus an [outgoing spherical wave](@entry_id:201591). For an incident wave propagating along the $z$-axis ($e^{ikz}$), the asymptotic form of the physical scattering wave function $\psi_{\mathbf{k}}^{(+)}(\mathbf{r})$ is defined as:
$$
\psi_{\mathbf{k}}^{(+)}(\mathbf{r}) \xrightarrow{r\to\infty} e^{ikz} + f(k, \theta) \frac{e^{ikr}}{r}
$$
This equation serves as the definition of the **[scattering amplitude](@entry_id:146099)**, $f(k, \theta)$. It is the coefficient of the [outgoing spherical wave](@entry_id:201591) and quantifies the amplitude and angular dependence of the scattered wave. The angle $\theta$ is the [scattering angle](@entry_id:171822) between the final direction of propagation $\hat{\mathbf{r}}$ and the incident direction $\hat{\mathbf{z}}$.

The choice of an [outgoing spherical wave](@entry_id:201591) ($e^{ikr}/r$) over an incoming one ($e^{-ikr}/r$) is a crucial physical constraint. In the formal Lippmann-Schwinger framework of scattering, this choice is enforced by the prescription used for the free-particle Green's function, $G_0(E) = (E - H_0)^{-1}$. The physical, outgoing-wave solution corresponds to selecting the **"retarded"** Green's function $G_{0}^{(+)}(E) = (E-H_{0}+i\epsilon)^{-1}$ in the limit $\epsilon \to 0^+$. The alternative choice, $G_{0}^{(-)}(E)$, would describe a time-reversed process with an incoming [spherical wave](@entry_id:175261) converging on the target, which does not correspond to a standard scattering experiment. [@problem_id:3588975]

The primary observable in a [scattering experiment](@entry_id:173304) is the **[differential cross section](@entry_id:159876)**, $d\sigma/d\Omega$, defined as the number of particles scattered into a unit [solid angle](@entry_id:154756) per unit time, divided by the incident flux (number of particles per unit area per unit time). We can derive the relationship between $d\sigma/d\Omega$ and $f(k, \theta)$ by calculating these fluxes using the probability current density, $\mathbf{j} = \frac{\hbar}{2\mu i}(\psi^*\nabla\psi - \psi\nabla\psi^*)$.

For the incident plane wave $\psi_{\text{inc}} = e^{ikz}$, the incident flux is found to be constant and directed along $\hat{\mathbf{z}}$, with magnitude $j_{\text{inc}} = \hbar k / \mu$. For the scattered wave $\psi_{\text{sc}} = f(k, \theta) e^{ikr}/r$, a calculation at large $r$ shows that the [probability current](@entry_id:150949) is purely radial and its magnitude is $j_{\text{sc},r} = (\hbar k / \mu) |f(k, \theta)|^2 / r^2$. The number of particles scattered into a [solid angle](@entry_id:154756) $d\Omega$ is the flux passing through the area element $dA = r^2 d\Omega$, which is $j_{\text{sc},r} r^2 d\Omega$. The scattered flux per unit [solid angle](@entry_id:154756) is therefore $j_{\text{sc},r} r^2 = (\hbar k / \mu) |f(k, \theta)|^2$.

Taking the ratio of the scattered flux per unit [solid angle](@entry_id:154756) to the incident flux gives the celebrated result for the [differential cross section](@entry_id:159876):
$$
\frac{d\sigma}{d\Omega} = \frac{j_{\text{sc},r} r^2}{j_{\text{inc}}} = |f(k, \theta)|^2
$$
This simple relationship underscores the central role of the scattering amplitude: its squared modulus is the direct link between the theoretical wave function and the experimentally measured [angular distribution](@entry_id:193827) of scattered particles. [@problem_id:3588975]

### Partial Wave Expansion and Phase Shifts

For a central potential, where $V(\mathbf{r}) = V(r)$, the system has rotational symmetry, and the [orbital angular momentum](@entry_id:191303) is conserved. This symmetry allows for a powerful method called **[partial wave analysis](@entry_id:136738)**. The scattering amplitude $f(k, \theta)$ can be expanded in a basis of Legendre polynomials $P_\ell(\cos\theta)$, where each term corresponds to a definite orbital angular momentum $\ell$:
$$
f(k, \theta) = \sum_{\ell=0}^{\infty} (2\ell+1) f_\ell(k) P_\ell(\cos\theta)
$$
Here, $f_\ell(k)$ is the partial wave amplitude for the $\ell$-th wave. This decomposition is extremely useful because in a [central potential](@entry_id:148563), each partial wave scatters independently.

The independence of each partial wave is captured by the partial wave **S-matrix**, $S_\ell(k)$. For purely elastic scattering, the [conservation of probability](@entry_id:149636) requires that the outgoing flux in each partial wave must equal the incoming flux. This imposes the constraint of [unitarity](@entry_id:138773) on the S-[matrix element](@entry_id:136260): $|S_\ell(k)| = 1$. A complex number with unit modulus can always be written as a pure phase. It is conventional to write this as:
$$
S_\ell(k) = e^{2i\delta_\ell(k)}
$$
This equation defines the **phase shift**, $\delta_\ell(k)$. The phase shift represents the change in phase of the asymptotic [radial wave function](@entry_id:156768) due to the potential, relative to the phase of a [free particle](@entry_id:167619) wave function. The factor of 2 is a convention that simplifies the relationship between the S-matrix, the phase shift, and the partial wave amplitude, which becomes:
$$
f_\ell(k) = \frac{S_\ell(k)-1}{2ik} = \frac{e^{2i\delta_\ell(k)}-1}{2ik} = \frac{e^{i\delta_\ell(k)}\sin\delta_\ell(k)}{k}
$$
The total [cross section](@entry_id:143872), $\sigma_{\text{tot}} = \int (d\sigma/d\Omega) d\Omega$, can also be expressed as a sum over partial waves:
$$
\sigma_{\text{tot}}(k) = \sum_{\ell=0}^{\infty} \sigma_\ell(k) = \frac{4\pi}{k^2} \sum_{\ell=0}^{\infty} (2\ell+1) \sin^2\delta_\ell(k)
$$
Thus, the entire scattering problem for a [central potential](@entry_id:148563) is reduced to calculating the set of phase shifts $\delta_\ell(k)$ for all $\ell$ and all relevant energies.

To see how [phase shifts](@entry_id:136717) are calculated in practice, consider the simple case of $s$-wave ($\ell=0$) scattering from a spherical square-well potential of depth $V_0$ and range $R$. The radial Schrödinger equation for the reduced [radial wave function](@entry_id:156768) $u_0(r) = r\psi_0(r)$ is solved separately for the interior region ($r \lt R$) and the exterior region ($r \gt R$).
- For $r \lt R$, the solution regular at the origin is $u_0^{\text{in}}(r) = A \sin(Kr)$, where $K = \sqrt{2\mu(E+V_0)}/\hbar$.
- For $r \gt R$, the potential is zero, and the solution must reflect the phase shift: $u_0^{\text{out}}(r) = B \sin(kr + \delta_0(k))$.

By enforcing the continuity of the wave function and its derivative at the boundary $r=R$, we can eliminate the constants and find a condition relating the phase shift to the potential parameters. The continuity of the [logarithmic derivative](@entry_id:169238), $u'(r)/u(r)$, at $r=R$ yields the equation:
$$
K \cot(KR) = k \cot(kR + \delta_0(k))
$$
This equation can be solved for the phase shift $\delta_0(k)$. [@problem_id:3588970] This procedure of matching interior and exterior solutions is a general method for computing [phase shifts](@entry_id:136717) for any finite-range potential.

### Low-Energy Scattering and the Effective Range Expansion

At very low energies, where the de Broglie wavelength of the incident particle is much larger than the range of the interaction ($kR \ll 1$), scattering is dominated by the $s$-wave ($\ell=0$). The behavior of the phase shift in this limit is universal for any short-range interaction. Based on the analyticity of the S-matrix, it can be shown that the function $k\cot\delta_0(k)$ has a convergent [power series expansion](@entry_id:273325) in $k^2$:
$$
k\cot\delta_0(k) = -\frac{1}{a} + \frac{1}{2}r_e k^2 + \mathcal{O}(k^4)
$$
This is the **[effective range expansion](@entry_id:137491) (ERE)**. It provides a model-independent description of [low-energy scattering](@entry_id:156179) using just two parameters:
1.  The **[scattering length](@entry_id:142881)**, $a$, defined as $a = -\lim_{k\to 0} \frac{\tan\delta_0(k)}{k}$. For small [phase shifts](@entry_id:136717), this is approximately $a \approx -\lim_{k\to 0} \frac{\delta_0(k)}{k}$.
2.  The **[effective range](@entry_id:160278)**, $r_e$, which characterizes the first correction in energy. It is formally defined by $r_e = 2 \lim_{k\to 0} \frac{\partial}{\partial(k^2)}\left[k\cot\delta_0(k) + \frac{1}{a}\right]$.

The ERE is valid as long as the momentum is small compared to the scale set by the interaction range ($kR \ll 1$) and there are no [long-range forces](@entry_id:181779) like the Coulomb interaction. [@problem_id:3588985]

The scattering length $a$ has a profound physical significance. In the zero-energy limit, the $s$-wave [cross section](@entry_id:143872) approaches a constant value $\sigma_0(k\to 0) = 4\pi a^2$. Geometrically, $|a|$ can be interpreted as the apparent "radius" of the scattering center at zero energy. The sign of $a$ provides information about the potential's ability to form a bound state. A large, positive [scattering length](@entry_id:142881) indicates the presence of a shallow [bound state](@entry_id:136872), while a large, negative scattering length indicates a "[virtual state](@entry_id:161219)," which is a nearly bound state.

A new $s$-wave [bound state](@entry_id:136872) appears at exactly zero binding energy when the [scattering length](@entry_id:142881) diverges to infinity ($a \to \pm\infty$). This corresponds to the condition $k\cot\delta_0(k) \to 0$ as $k \to 0$. For the square-well potential, this threshold condition occurs when $K_0 R = (2n+1)\pi/2$, where $K_0 = \sqrt{2\mu V_0}/\hbar$. This allows us to calculate the specific critical depths $V_0^{(n)}$ at which new [bound states](@entry_id:136502) emerge, linking scattering data directly to the bound spectrum of the system. [@problem_id:3588970]

### Resonances and Higher Partial Waves

While [low-energy scattering](@entry_id:156179) is dominated by the $s$-wave, as energy increases, higher partial waves ($\ell \ge 1$) become important. For these waves, the radial Schrödinger equation includes an additional repulsive term, the **centrifugal barrier**:
$$
U_{\text{eff}}(r) = V(r) + \frac{\hbar^2 \ell(\ell+1)}{2\mu r^2}
$$
This effective potential shapes the scattering dynamics for higher angular momenta. The centrifugal term dominates at large $r$, suppressing the wave function near the origin at low energies. This suppression is quantified by the **Wigner threshold law**, which states that for [short-range forces](@entry_id:142823), the phase shift vanishes as $\delta_\ell(k) \propto k^{2\ell+1}$ for $k \to 0$. This, in turn, implies that the partial cross section vanishes rapidly: $\sigma_\ell(k) \propto k^{4\ell}$. Consequently, at low energies, cross sections are always dominated by the lowest possible partial waves. [@problem_id:3588999]

If the [nuclear potential](@entry_id:752727) $V(r)$ is sufficiently attractive at short range, the effective potential $U_{\text{eff}}(r)$ can form a "pocket" with a barrier at larger $r$. This potential shape can temporarily trap a particle in a **quasibound state** at a positive energy, leading to a phenomenon known as a **shape resonance**. [@problem_id:3588999]

A resonance manifests in several distinct ways:
-   **Phase Shift**: The phase shift $\delta_\ell(E)$ for the resonant partial wave rapidly increases by approximately $\pi$ as the energy $E$ passes through the [resonance energy](@entry_id:147349) $E_r$. At the peak of the resonance, the phase shift is approximately $\pi/2$ (modulo $\pi$). [@problem_id:3588999]
-   **Cross Section**: This rapid change in $\delta_\ell$ causes the term $\sin^2\delta_\ell$ to reach its maximum value of 1. This produces a distinct, symmetric peak in the partial-wave [cross section](@entry_id:143872) $\sigma_\ell$, typically of the Breit-Wigner form, which is also visible in the total [cross section](@entry_id:143872). [@problem_id:3588999]
-   **Time Delay**: The trapping of the particle in the [potential well](@entry_id:152140) means it spends more time in the interaction region than it would if it were moving freely. This is quantified by the **Wigner time delay**, $\tau_\ell(E) = 2\hbar \frac{d\delta_\ell}{dE}$. Near a resonance, the phase shift is rapidly increasing, so its [energy derivative](@entry_id:268961) is large and positive. This results in a large, positive peak in the time delay at the [resonance energy](@entry_id:147349). The height and width of this peak are related to the lifetime of the quasibound state; a narrow resonance corresponds to a long-lived state and a large [peak time](@entry_id:262671) delay. For an isolated resonance of width $\Gamma$, the [peak time](@entry_id:262671) delay is $\tau_\ell(E_r) = 4\hbar/\Gamma$. This enhancement can be orders of magnitude larger than the time delay from non-resonant background scattering. [@problem_id:3588986] [@problem_id:3588999]

### Advanced Topics in Elastic Scattering

Real-world [nuclear scattering](@entry_id:172564) often involves additional complexities. Here we address several important cases.

#### Scattering of Identical Particles

When the projectile and target particles are identical, quantum mechanics requires the total wave function of the system to have a definite symmetry under [particle exchange](@entry_id:154910): symmetric for **bosons** and antisymmetric for **fermions**. Since the total [wave function](@entry_id:148272) is a product of a spatial part and a spin part, this requirement constrains the allowed spatial symmetries.

In the [center-of-mass frame](@entry_id:158134), exchanging the two particles is equivalent to inverting the relative [coordinate vector](@entry_id:153319), which corresponds to the transformation $\theta \to \pi - \theta$. A spatial [wave function](@entry_id:148272) built from only even-$\ell$ partial waves is symmetric under exchange, while one built from only odd-$\ell$ partial waves is antisymmetric. This leads to strict selection rules:
-   For **spinless identical bosons**, the spin state is symmetric, so the spatial state must also be symmetric. Only **even** values of $\ell$ can contribute to the scattering sum.
-   For **identical spin-1/2 fermions**, if they are in a spin-[triplet state](@entry_id:156705) ($S=1$, symmetric spin), the spatial state must be antisymmetric, so only **odd** $\ell$ contribute. If they are in a [spin-singlet state](@entry_id:153133) ($S=0$, antisymmetric spin), the spatial state must be symmetric, and only **even** $\ell$ contribute.

The [scattering amplitude](@entry_id:146099) must also be symmetrized. For a spatially symmetric final state (e.g., spinless bosons), the amplitude is $f_{\text{symm}}(\theta) = f(\theta) + f(\pi-\theta)$, leading to a cross section $d\sigma/d\Omega = |f(\theta) + f(\pi-\theta)|^2$. The interference term can lead to dramatic effects, such as constructive interference at $\theta=\pi/2$, where the cross section can be four times that for [distinguishable particles](@entry_id:153111). For an unpolarized beam of spin-1/2 fermions, the scattering is an incoherent statistical average: $3/4$ of the time the particles are in a [triplet state](@entry_id:156705) (odd $\ell$) and $1/4$ of the time they are in a [singlet state](@entry_id:154728) (even $\ell$). The measured [cross section](@entry_id:143872) is a weighted sum of the cross sections from these two channels. [@problem_id:3589009]

Finally, when calculating the total cross section for identical particles, one must account for the fact that detecting a particle at angle $\theta$ is physically indistinguishable from detecting the other particle at $\theta$. To avoid double-counting each scattering event, an extra factor of $1/2$ is included when integrating the [differential cross section](@entry_id:159876). [@problem_id:3589009]

#### Coupled-Channel Scattering

If the interaction potential is not purely central, it may not conserve [orbital angular momentum](@entry_id:191303) $\ell$, though it may still conserve [total angular momentum](@entry_id:155748) $J$. A prime example in nuclear physics is the **tensor force** in the [nucleon-nucleon interaction](@entry_id:162177), which couples different $\ell$ states. In the case of total angular momentum $J=1$ and [total spin](@entry_id:153335) $S=1$, the [tensor force](@entry_id:161961) couples the $L=0$ ($^3S_1$) and $L=2$ ($^3D_1$) channels.

In this scenario, scattering can cause a transition between the two channels, and the S-matrix becomes a $2\times2$ matrix in the basis of these two states. The fundamental principles of [probability conservation](@entry_id:149166) (unitarity, $S^\dagger S = I$) and [time-reversal invariance](@entry_id:152159) (symmetry, $S=S^T$) still hold for this S-matrix. A general $2\times2$ unitary, symmetric matrix can be parameterized by three real numbers. The standard convention in [nuclear physics](@entry_id:136661) (the Stapp or "eigenphase" parameterization) is to use two **eigenphase shifts**, $\delta_S$ and $\delta_D$, and one real **mixing angle**, $\epsilon_1$. The S-matrix is constructed by diagonalizing it with a [rotation matrix](@entry_id:140302) defined by the mixing angle:
$$
S(k) = R(\epsilon_1) \begin{pmatrix} e^{2i\delta_S} & 0 \\ 0 & e^{2i\delta_D} \end{pmatrix} R(\epsilon_1)^T, \quad \text{where} \quad R(\epsilon_1) = \begin{pmatrix} \cos\epsilon_1 & \sin\epsilon_1 \\ -\sin\epsilon_1 & \cos\epsilon_1 \end{pmatrix}
$$
The eigenphase shifts represent the [phase shifts](@entry_id:136717) of the two eigenstates of the S-matrix, which are mixtures of the original $S$ and $D$ waves. The mixing angle $\epsilon_1(k)$ quantifies the strength of the coupling induced by the tensor force at a given energy. When the coupling vanishes, $\epsilon_1 \to 0$, and the S-matrix becomes diagonal, correctly recovering the uncoupled case. [@problem_id:3589022]

#### Scattering with Long-Range Forces

When a long-range force like the Coulomb interaction is present in addition to a short-range [nuclear force](@entry_id:154226), as in nucleus-nucleus scattering, the standard formalism must be modified. The asymptotic form of the wave function is no longer a [plane wave](@entry_id:263752) plus a [spherical wave](@entry_id:175261) because the Coulomb potential distorts the waves even at infinite distances. The wave function acquires a logarithmic, coordinate-dependent phase term.

The key results are as follows:
-   The strength of the Coulomb interaction is characterized by the dimensionless **Sommerfeld parameter**, $\eta = \frac{Z_1 Z_2 e^2 \mu}{\hbar^2 k}$, where $Z_1$ and $Z_2$ are the charges of the colliding particles.
-   The pure Coulomb potential itself produces a phase shift, known as the **Coulomb phase shift**, $\sigma_\ell(\eta) = \arg \Gamma(\ell+1+i\eta)$.
-   The total S-matrix for the combined Coulomb-plus-[nuclear potential](@entry_id:752727) factorizes into a product of the Coulomb S-matrix and a nuclear S-matrix: $S_\ell^{(C+N)}(k) = e^{2i\sigma_\ell(\eta)} e^{2i\delta_\ell^N(k)}$. Here, $\delta_\ell^N(k)$ is the additional **nuclear phase shift** caused by the short-range potential $V_N(r)$ in the presence of the Coulomb field.

Computationally, one cannot simply match the numerical solution to free [spherical waves](@entry_id:200471). Instead, one must match the solution to the known analytic solutions of the pure Coulomb problem: the regular and irregular **Coulomb [wave functions](@entry_id:201714)**, $F_\ell(\eta, kr)$ and $G_\ell(\eta, kr)$. By calculating the logarithmic derivative of the numerical [wave function](@entry_id:148272) at a matching radius $R$ beyond the range of the nuclear force, one can use a matching formula involving $F_\ell$ and $G_\ell$ to extract the desired nuclear phase shift $\delta_\ell^N(k)$. [@problem_id:3589034]

### Inelastic Scattering and the Optical Model

In many [nuclear reactions](@entry_id:159441), the incident particle can excite the target nucleus or induce a reaction, opening **inelastic channels**. In such cases, the total flux in the elastic channel is not conserved; some of it is "absorbed" into other reaction channels.

This loss of flux is described by an elastic S-[matrix element](@entry_id:136260) $S_\ell$ that is no longer unitary, i.e., its modulus is less than one. We introduce the **inelasticity parameter** $\eta_\ell(k)$ to parameterize this:
$$
S_\ell(k) = \eta_\ell(k) e^{2i\delta_\ell(k)}, \quad \text{with} \quad 0  \eta_\ell \le 1
$$
Here, $\eta_\ell=1$ corresponds to purely elastic scattering, while $\eta_\ell  1$ signifies the presence of inelasticity or absorption from the $\ell$-th partial wave.

With this generalized S-matrix, the partial-wave cross sections must be re-derived. The **integrated elastic [cross section](@entry_id:143872)** for the $\ell$-th wave becomes $\sigma_{\text{el}}^{(\ell)} = \frac{\pi}{k^2}(2\ell+1)|1-S_\ell|^2 = \frac{\pi}{k^2}(2\ell+1)[1+\eta_\ell^2 - 2\eta_\ell\cos(2\delta_\ell)]$. The new quantity of interest is the **[reaction cross section](@entry_id:157978)**, which accounts for the total flux lost to all non-elastic channels. It is given by $\sigma_{\text{reac}}^{(\ell)} = \frac{\pi}{k^2}(2\ell+1)(1-|S_\ell|^2) = \frac{\pi}{k^2}(2\ell+1)(1-\eta_\ell^2)$.

The **total cross section** is the sum of the elastic and reaction cross sections, $\sigma_{\text{tot}} = \sigma_{\text{el}} + \sigma_{\text{reac}}$. A fundamental result, the **[optical theorem](@entry_id:140058)**, remains valid even in the presence of absorption. It relates the total cross section to the imaginary part of the [forward scattering amplitude](@entry_id:154109):
$$
\sigma_{\text{tot}} = \frac{4\pi}{k} \text{Im}[f(0)]
$$
Using the generalized form of $S_\ell$, we find the total [cross section](@entry_id:143872) to be $\sigma_{\text{tot}} = \frac{2\pi}{k^2} \sum_{\ell=0}^{\infty} (2\ell+1) [1 - \eta_\ell\cos(2\delta_\ell)]$. One can verify that summing the expressions for the total elastic and total reaction cross sections indeed reproduces this result. [@problem_id:3589000] This framework, where absorption is described by a complex phase shift (or, equivalently, a [complex potential](@entry_id:162103) known as the [optical potential](@entry_id:156352)), is the basis of the highly successful [optical model](@entry_id:161345) of nuclear reactions.