## Introduction
In the realm of nuclear and particle physics, scattering experiments are the primary tool for probing the fundamental forces of nature. However, interpreting the complex patterns of scattered particles requires a robust theoretical framework. Partial wave analysis provides this essential framework, transforming the intricate three-dimensional scattering problem into a manageable series of one-dimensional problems, each corresponding to a specific angular momentum state. This decomposition is not merely a mathematical convenience; it provides a powerful physical language to describe everything from low-energy interactions to the formation of short-lived resonant states. This article aims to provide a comprehensive graduate-level understanding of partial wave analysis, bridging the gap between textbook formalism and its practical application in modern research.

We will begin our journey in the **Principles and Mechanisms** chapter, deriving the formalism from the Schrödinger equation, defining key concepts like [phase shifts](@entry_id:136717) and the S-matrix, and exploring the analytic structure that reveals the physics of [bound states and resonances](@entry_id:138162). Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the method's power in practice, covering how to calculate observables from potentials, perform a Partial Wave Analysis (PWA) on experimental data, and handle complexities like inelasticity and [coupled channels](@entry_id:204758). We will also explore its surprising connections to fields like Lattice QCD and quantum chemistry. Finally, the **Hands-On Practices** section will offer a chance to apply these concepts through guided computational problems, solidifying your understanding by moving from theory to implementation.

## Principles and Mechanisms

In this chapter, we transition from the conceptual introduction of partial wave analysis to its core principles and underlying mechanisms. The primary objective of partial wave analysis is to deconstruct the complex three-dimensional scattering problem into a set of simpler, one-dimensional radial problems, each corresponding to a definite orbital angular momentum. This decomposition not only simplifies the problem computationally but also provides a profound physical language for interpreting scattering phenomena, from low-energy threshold behavior to high-energy resonances. We will systematically develop the formalism, starting from the Schrödinger equation and culminating in advanced applications relevant to modern nuclear physics.

### The Radial Schrödinger Equation

The foundation of our analysis is the time-independent Schrödinger equation (TISE) for a particle of [reduced mass](@entry_id:152420) $\mu$ scattering from a spherically symmetric central potential $V(r)$, where $r=|\mathbf{r}|$:
$$
-\frac{\hbar^2}{2\mu}\nabla^2\psi(\mathbf{r}) + V(r)\psi(\mathbf{r}) = E\psi(\mathbf{r})
$$
The spherical symmetry of the potential suggests that the solutions can be separated into a radial part and an angular part. This is accomplished by expanding the wavefunction $\psi(\mathbf{r})$ in a basis of spherical harmonics, $Y_{\ell m}(\hat{\mathbf{r}})$, which are the [eigenfunctions](@entry_id:154705) of the orbital [angular momentum operators](@entry_id:153013) $\hat{L}^2$ and $\hat{L}_z$. Each component of this expansion is a **partial wave**, characterized by the [orbital angular momentum quantum number](@entry_id:167573) $\ell$ and its projection $m$.

For a central potential, the Hamiltonian commutes with $\hat{L}^2$ and $\hat{L}_z$, so we can seek solutions that are simultaneous eigenfunctions of these operators. Such a solution takes the form $\psi_{\ell m}(\mathbf{r}) = R_{\ell}(r)Y_{\ell m}(\hat{\mathbf{r}})$. Substituting this into the TISE and using the fact that $\hat{L}^2 Y_{\ell m}(\hat{\mathbf{r}}) = \hbar^2 \ell(\ell+1) Y_{\ell m}(\hat{\mathbf{r}})$, we can separate the variables to obtain an ordinary differential equation for the radial function $R_{\ell}(r)$. For convenience, it is standard to define a **reduced [radial wavefunction](@entry_id:151047)**, $u_{\ell}(r) = r R_{\ell}(r)$. This substitution elegantly simplifies the radial [kinetic energy operator](@entry_id:265633), leading to the **radial Schrödinger equation** :
$$
\frac{d^2u_{\ell}(r)}{dr^2} + \left[k^2 - \frac{\ell(\ell+1)}{r^2} - U(r)\right]u_{\ell}(r) = 0
$$
Here, we have introduced the wave number $k$, defined by the energy $E = \frac{\hbar^2 k^2}{2\mu}$, and the reduced potential $U(r) = \frac{2\mu}{\hbar^2}V(r)$. This equation has the familiar form of a one-dimensional Schrödinger equation, but with an **effective potential** that includes the repulsive **[centrifugal barrier](@entry_id:147153)**, $V_{\text{cent}}(r) = \frac{\hbar^2 \ell(\ell+1)}{2\mu r^2}$. This term represents the classical rotational kinetic energy and plays a crucial role in suppressing the contribution of high-$\ell$ partial waves at low energies.

Physical wavefunctions must be well-behaved everywhere. The behavior of $u_{\ell}(r)$ near the origin is critical. For any potential $V(r)$ that is less singular than $1/r^2$ at the origin (a condition met by all realistic nuclear potentials), the centrifugal term dominates the [radial equation](@entry_id:138211) as $r \to 0$. The analysis of this limit shows two possible behaviors: a **[regular solution](@entry_id:156590)** that behaves as $u_{\ell}(r) \propto r^{\ell+1}$, and an **irregular solution** that behaves as $u_{\ell}(r) \propto r^{-\ell}$. Since the full wavefunction is $\psi_{\ell m} \propto u_{\ell}(r)/r$, the irregular solution would diverge as $r^{-(\ell+1)}$ at the origin, which is physically unacceptable. Therefore, we impose the **regularity condition**: the physical reduced [radial wavefunction](@entry_id:151047) must vanish at the origin with the leading-order behavior $u_{\ell}(r) \propto r^{\ell+1}$ as $r \to 0$ .

### Phase Shifts and the Scattering Matrix

Having fixed the behavior at the origin, we now turn to the asymptotic region, where $r$ is large. For a short-range potential, which vanishes sufficiently fast for $r \to \infty$ (e.g., faster than $1/r$), the potential term $U(r)$ becomes negligible. The [radial equation](@entry_id:138211) simplifies to the free [radial equation](@entry_id:138211):
$$
\frac{d^2u_{\ell}(r)}{dr^2} + \left[k^2 - \frac{\ell(\ell+1)}{r^2}\right]u_{\ell}(r) = 0
$$
The solutions to this are spherical Bessel functions. The general real solution can be written as a linear combination of these, but it is most instructive to examine its large-$r$ form. In the absence of any potential ($V(r)=0$ for all $r$), the [regular solution](@entry_id:156590) has the asymptotic form $u_{\ell}^{\text{free}}(r) \propto \sin(kr - \ell\pi/2)$. The term $-\ell\pi/2$ is a phase shift originating purely from the centrifugal barrier.

When the short-range potential $V(r)$ is present, it modifies the wavefunction in the interior region, which in turn shifts the phase of the asymptotic solution. The asymptotic form of the physical solution is thus written as:
$$
u_{\ell}(r) \xrightarrow{r\to\infty} C \sin\left(kr - \frac{\ell\pi}{2} + \delta_{\ell}(k)\right)
$$
The quantity $\delta_{\ell}(k)$ is the **[scattering phase shift](@entry_id:146584)**. It represents the central observable for each partial wave and encapsulates the entire effect of the scattering potential $V(r)$ at a given energy and angular momentum. A positive phase shift corresponds to an attractive potential that "pulls in" the wavefunction, advancing its phase. A negative phase shift corresponds to a [repulsive potential](@entry_id:185622) that "pushes out" the wavefunction, delaying its phase.

To connect this to a more general formalism, we can express the asymptotic solution as a superposition of an incoming [spherical wave](@entry_id:175261), $e^{-i(kr - \ell\pi/2)}$, and an [outgoing spherical wave](@entry_id:201591), $e^{+i(kr - \ell\pi/2)}$. The sine function can be rewritten as:
$$
u_{\ell}(r) \propto e^{i\delta_{\ell}}e^{i(kr - \ell\pi/2)} - e^{-i\delta_{\ell}}e^{-i(kr - \ell\pi/2)}
$$
The **[scattering matrix](@entry_id:137017) element**, or **S-matrix element**, $S_{\ell}(k)$, is defined as the ratio of the amplitude of the outgoing wave to the amplitude of the incoming wave, relative to their free-particle relationship. From the expression above, we can identify this as:
$$
S_{\ell}(k) = e^{2i\delta_{\ell}(k)}
$$
For [elastic scattering](@entry_id:152152) from a real potential, probability flux must be conserved. This physical requirement translates into the mathematical condition of **unitarity** for the S-matrix: $|S_{\ell}(k)|=1$. This is automatically satisfied if the phase shift $\delta_{\ell}(k)$ is a real number, as is the case for scattering from real potentials .

### Threshold Behavior and Low-Energy Expansions

The behavior of scattering [observables](@entry_id:267133) at low energy ($k \to 0$) is governed by universal laws dictated by the [centrifugal barrier](@entry_id:147153). A rigorous analysis shows that for a short-range potential, the phase shift must vanish at the threshold according to the **Wigner threshold law** :
$$
\delta_{\ell}(k) \xrightarrow{k\to 0} \alpha_{\ell} k^{2\ell+1}
$$
This implies that for low incident momenta, scattering is strongly suppressed in higher partial waves. For example, d-wave ($\ell=2$) scattering is suppressed by a factor of $k^4$ relative to [s-wave](@entry_id:754474) ($\ell=0$) scattering. This is a direct consequence of the increasing strength of the centrifugal barrier with $\ell$, which prevents low-energy particles from penetrating into the region where the nuclear force is active. At very low energies, scattering is almost entirely dominated by the [s-wave](@entry_id:754474).

The coefficient $\alpha_{\ell}$ is related to a **generalized scattering length** $a_{\ell}$. For $\ell=0$, the connection is most famous. The [s-wave](@entry_id:754474) phase shift behaves as $\delta_0(k) \approx -a_0 k$. For low-energy [s-wave scattering](@entry_id:155985), it is conventional to analyze the quantity $k\cot\delta_0(k)$, which can be shown to be an [analytic function](@entry_id:143459) of $k^2$ near $k=0$ for short-range potentials. This allows for a Taylor series in $k^2$, known as the **Effective Range Expansion (ERE)** :
$$
k\cot\delta_{0}(k) = -\frac{1}{a_{0}} + \frac{1}{2}r_{0}k^{2} + P_{0}k^{4} + \mathcal{O}(k^6)
$$
The first two parameters in this expansion have profound physical significance.
-   The **scattering length** $a_0$ is defined by the zero-energy limit: $\lim_{k\to 0} (-k\cot\delta_0(k))^{-1} = a_0$. It represents the effective size of the scattering interaction at zero energy. The low-energy total [cross section](@entry_id:143872) is given by $\sigma_{\text{tot}}(k\to 0) = 4\pi a_0^2$.
-   The **[effective range](@entry_id:160278)** $r_0$ characterizes the energy dependence of the scattering at low energies and is related to the spatial range of the potential.

The ERE is an invaluable tool in nuclear physics, allowing one to parameterize the complicated low-energy interaction with just a few numbers derived from experiment. Its validity is, however, restricted to the low-momentum regime where the de Broglie wavelength is much larger than the potential's range, $R$. Formally, the expansion converges for momenta satisfying $kR \ll 1$, with the [radius of convergence](@entry_id:143138) being determined by the nearest singularity of the S-matrix in the [complex momentum](@entry_id:201607) plane, which is typically at a scale of order $1/R$ .

### Practical Truncation: The Semiclassical Cutoff

In principle, the [partial wave expansion](@entry_id:145788) is an infinite sum over $\ell$. For any practical computation, this sum must be truncated at some maximum value, $\ell_{\max}$. A reliable estimate for this cutoff can be derived from semiclassical arguments . For a particle to be significantly scattered by a potential of range $R$, it must have enough kinetic energy to overcome the repulsive centrifugal barrier at that distance. The condition for the particle to reach the interaction region is approximately that its energy $E = \hbar^2k^2/(2\mu)$ exceeds the height of the centrifugal barrier at $r=R$:
$$
\frac{\hbar^2 k^2}{2\mu} \gtrsim \frac{\hbar^2 \ell(\ell+1)}{2\mu R^2}
$$
For large $\ell$, we can approximate $\ell(\ell+1) \approx \ell^2$. The maximum angular momentum that can contribute, $\ell_{\max}$, corresponds to the point where this becomes an equality:
$$
k^2 R^2 \approx \ell_{\max}^2 \quad \implies \quad \ell_{\max} \approx kR
$$
This simple and powerful result states that the number of contributing partial waves grows linearly with both the momentum and the interaction range. For example, scattering a $100$ MeV nucleon ($k \approx 1 \text{ fm}^{-1}$) from a nucleus with radius $R=5$ fm would require including partial waves up to $\ell_{\max} \approx 5$.

An alternative, classical perspective yields the same result. The classical angular momentum is $L = pb = (\hbar k)b$, where $b$ is the [impact parameter](@entry_id:165532). For interaction to occur, the [impact parameter](@entry_id:165532) must be smaller than the range, $b \lesssim R$. The semiclassical correspondence relates $L$ to $\ell$ via $L \approx \hbar\ell$ for large $\ell$. Combining these gives $\hbar\ell \approx \hbar k b$. The maximum $\ell$ corresponds to the maximum impact parameter, $b_{\max} \approx R$, leading directly to $\ell_{\max} \approx kR$ .

### The Analytic S-Matrix and Scattering Phenomena

A deeper understanding of scattering emerges when the S-matrix element $S_{\ell}(k)$ is viewed as an [analytic function](@entry_id:143459) of a [complex momentum](@entry_id:201607) variable $k$. The locations of the poles of $S_{\ell}(k)$ in the complex $k$-plane have a one-to-one correspondence with the discrete and resonant spectrum of the system .

-   **Bound States**: A pole on the positive [imaginary axis](@entry_id:262618), at $k = i\kappa$ with $\kappa > 0$, corresponds to a physical **[bound state](@entry_id:136872)**. At this imaginary momentum, the outgoing wave $e^{ikr}$ becomes a decaying exponential $e^{-\kappa r}$. A pole in the S-matrix signifies a solution that exists with only an outgoing wave component, which for $k=i\kappa$ is a purely decaying, square-integrable wavefunction with a negative energy $E = -\frac{\hbar^2\kappa^2}{2\mu}$. A near-threshold [s-wave](@entry_id:754474) bound state ($\kappa \to 0^+$) is associated with a large, positive scattering length $a_0 \approx 1/\kappa$.

-   **Virtual States**: A pole on the negative [imaginary axis](@entry_id:262618), at $k = -i\kappa$ with $\kappa > 0$, on the "unphysical" Riemann sheet, corresponds to a **[virtual state](@entry_id:161219)**. This is not a normalizable state, as its wavefunction would grow exponentially as $e^{+\kappa r}$. However, its proximity to the origin can dramatically influence [low-energy scattering](@entry_id:156179). A near-threshold s-wave [virtual state](@entry_id:161219) is associated with a large, negative [scattering length](@entry_id:142881) $a_0 \approx -1/\kappa$, leading to a large low-energy [cross section](@entry_id:143872) even without a bound state . The deuteron is a bound state, while the "di-neutron" is a [virtual state](@entry_id:161219).

-   **Resonances**: A pair of poles located symmetrically in the lower half of the unphysical sheet, at $k = \pm k_r - ik_i$ (with $k_r, k_i > 0$), corresponds to a **resonance**. A resonance is a metastable, or quasi-bound, state. The real part of the pole position determines the [resonance energy](@entry_id:147349), $E_r \approx \frac{\hbar^2 k_r^2}{2\mu}$, while the imaginary part determines its lifetime, $\tau = 1/\Gamma$, where the width is $\Gamma \approx \frac{2\hbar^2 k_r k_i}{\mu}$. Near the [resonance energy](@entry_id:147349), the phase shift $\delta_{\ell}(E)$ rises rapidly through $\pi/2$, causing a characteristic Breit-Wigner peak in the partial [cross section](@entry_id:143872).

The lifetime of a resonance can be directly probed via the **Wigner-Smith time delay**, defined as $\tau_{\ell}(E) = 2\hbar \frac{d\delta_{\ell}}{dE}$ . This quantity represents the excess time a particle wavepacket spends in the interaction region compared to free propagation. Near a narrow resonance, the phase shift changes rapidly, leading to a large, positive peak in the time delay. The maximum delay at the [resonance energy](@entry_id:147349) $E_r$ is directly related to the [resonance width](@entry_id:186927): $\tau_{\ell}(E_r) \approx 4\hbar/\Gamma$. This beautifully connects a purely geometric property of the phase shift function to the physical lifetime of the resonant state.

### Advanced Mechanisms and Formalisms

The basic framework of partial wave analysis can be extended to handle more complex and realistic scenarios prevalent in nuclear physics.

#### The Lippmann-Schwinger Equation

An alternative, more formal approach to [scattering theory](@entry_id:143476) is through integral equations. The central object is the transition operator, or T-matrix, which is related to the S-matrix. The T-matrix satisfies the **Lippmann-Schwinger equation**. In a momentum-space partial-wave basis, this becomes a one-dimensional [integral equation](@entry_id:165305) for the half-off-shell T-[matrix element](@entry_id:136260) $T_{\ell}(p,k;E)$ (where $k=\sqrt{2\mu E}$ is the on-shell momentum) :
$$
T_{\ell}(p,p';E) = V_{\ell}(p,p') + \int_0^{\infty} dq\,q^2 \frac{V_{\ell}(p,q)T_{\ell}(q,p';E)}{E - \frac{q^2}{2\mu} + i0^+}
$$
Here, $V_{\ell}(p,p')$ is the partial-wave [matrix element](@entry_id:136260) of the potential. The key feature of this equation is the energy denominator, which becomes singular when the intermediate momentum $q$ goes "on-shell," i.e., when $q^2/(2\mu) = E$. The infinitesimal term $+i0^+$ provides the prescription for handling this singularity, corresponding to purely outgoing scattered waves. Using the Sokhotski–Plemelj theorem, this [propagator](@entry_id:139558) can be decomposed:
$$
\frac{1}{x+i0^+} = \mathcal{P}\left(\frac{1}{x}\right) - i\pi\delta(x)
$$
The [principal value](@entry_id:192761) part, $\mathcal{P}$, gives the reaction matrix (K-matrix), while the delta-function term ensures the [unitarity](@entry_id:138773) of the S-matrix by relating the imaginary part of the [forward scattering amplitude](@entry_id:154109) to the total [cross section](@entry_id:143872) (the [optical theorem](@entry_id:140058)). This formalism is the starting point for many modern numerical calculations of the NN interaction.

#### Inelasticity and the Optical Model

In many [nuclear reactions](@entry_id:159441), such as nucleon-nucleus scattering, there is a significant probability that the collision will lead to states other than the initial elastic one (e.g., excitation of the nucleus). These are **inelastic channels**. To model this loss of flux from the elastic channel, one introduces a complex **[optical potential](@entry_id:156352)**, $V(r) = V_R(r) + iW(r)$, where the absorptive part is conventionally negative, $W(r) \le 0$ .

With a [complex potential](@entry_id:162103), the Hamiltonian is no longer Hermitian, and probability flux is not conserved in the elastic channel. This manifests as a non-unitary S-matrix, $|S_{\ell}(k)| \le 1$. We parametrize this by introducing the **inelasticity parameter** $\eta_{\ell}(k)$:
$$
S_{\ell}(k) = \eta_{\ell}(k) e^{2i\delta_{\ell}(k)}, \quad \text{where } 0 \le \eta_{\ell} \le 1
$$
Here, $\delta_{\ell}$ remains a real phase shift. A value of $\eta_{\ell}=1$ corresponds to purely [elastic scattering](@entry_id:152152), while $\eta_{\ell}=0$ represents total absorption for that partial wave. The total cross section for each partial wave, $\sigma_{\ell}$, now splits into two parts: an elastic part and a reaction (or absorption) part. These are given by:
$$
\sigma_{\ell}^{\text{el}} = \frac{\pi}{k^2}(2\ell+1)|1-S_{\ell}|^2 = \frac{\pi}{k^2}(2\ell+1)(1 + \eta_{\ell}^2 - 2\eta_{\ell}\cos(2\delta_{\ell}))
$$
$$
\sigma_{\ell}^{\text{reac}} = \frac{\pi}{k^2}(2\ell+1)(1-|S_{\ell}|^2) = \frac{\pi}{k^2}(2\ell+1)(1-\eta_{\ell}^2)
$$
The total [reaction cross section](@entry_id:157978) is simply the sum of the flux lost from all partial waves. For instance, if [s-wave scattering](@entry_id:155985) at $k=0.80 \text{ fm}^{-1}$ is characterized by an inelasticity $\eta_0=0.60$, the [s-wave](@entry_id:754474) [reaction cross section](@entry_id:157978) is $\sigma_0^{\text{reac}} = \frac{\pi}{(0.80)^2}(1 - 0.60^2) = \pi \text{ fm}^2 \approx 0.0314 \text{ barns}$ .

#### Scattering of Charged Particles

When scattering charged particles, such as proton-proton scattering, the long-range Coulomb potential $V_C(r) \propto 1/r$ fundamentally alters the [asymptotic behavior](@entry_id:160836) of the wavefunctions. They are no longer sine waves, but are distorted even at infinite distance. The concept of a phase shift relative to a [free particle](@entry_id:167619) becomes ill-defined.

The solution is to redefine the "free" solutions as the solutions to the pure Coulomb problem. These are the regular and irregular **Coulomb functions**, $F_{\ell}(\eta, \rho)$ and $G_{\ell}(\eta, \rho)$, where $\rho=kr$ and $\eta = \frac{\mu\alpha}{\hbar^2 k}$ is the dimensionless Sommerfeld parameter . The asymptotic form of the full solution (including a short-range [nuclear potential](@entry_id:752727) $V_N(r)$) is then written as a linear combination of these Coulomb functions:
$$
u_{\ell}(r) \xrightarrow{r\to\infty} C \left[\cos\delta_{\ell}^{N} F_{\ell}(\eta, kr) + \sin\delta_{\ell}^{N} G_{\ell}(\eta, kr)\right]
$$
This defines the **Coulomb-modified nuclear phase shift** $\delta_{\ell}^{N}$, which represents the additional phase shift due to the short-range nuclear force *on top of* the known Coulomb scattering. The total S-matrix neatly factorizes into a Coulomb part and a nuclear part:
$$
S_{\ell}^{\text{tot}} = e^{2i\sigma_{\ell}(\eta)} e^{2i\delta_{\ell}^{N}}
$$
where $\sigma_{\ell}(\eta) = \arg\Gamma(\ell+1+i\eta)$ is the pure Coulomb phase shift. This separation allows one to isolate the effects of the short-range nuclear interaction, which is typically the object of study.

#### Coupled Channels and Non-Central Forces

The nuclear force is not purely central. The most prominent non-central component is the **tensor force**, which depends on the orientation of the nucleon spins relative to their separation vector. The tensor operator, $S_{12}$, couples states of the same total angular momentum $J$ and parity, but with orbital angular momenta $L$ differing by two, i.e., $L=J\pm1$.

This means $L$ is no longer a [good quantum number](@entry_id:263156), and a single partial wave is insufficient. We must instead consider a set of **[coupled channels](@entry_id:204758)**. The canonical example in [nucleon-nucleon scattering](@entry_id:159513) is the coupling of the ${}^3S_1$ ($L=0$) and ${}^3D_1$ ($L=2$) channels for total angular momentum $J=1$ and spin $S=1$ . The wavefunction is now a vector in the channel space:
$$
\boldsymbol{\Psi}(\mathbf{r}) = \frac{u(r)}{r}|{}^3S_1\rangle + \frac{w(r)}{r}|{}^3D_1\rangle
$$
Projecting the TISE onto this channel basis results in a system of coupled radial Schrödinger equations:
$$
\frac{d^2}{dr^2}
\begin{pmatrix} u(r) \\ w(r) \end{pmatrix}
-
\frac{1}{r^2}
\begin{pmatrix} 0  0 \\ 0  6 \end{pmatrix}
\begin{pmatrix} u(r) \\ w(r) \end{pmatrix}
+
\left[k^2 - U_C(r)\right]
\begin{pmatrix} u(r) \\ w(r) \end{pmatrix}
- U_T(r) \mathbf{S}_{12}
\begin{pmatrix} u(r) \\ w(r) \end{pmatrix}
= 0
$$
where $U_C$ and $U_T$ are the reduced central and tensor potentials. The coupling is mediated by the matrix of the tensor operator in this basis:
$$
\mathbf{S}_{12} = \begin{pmatrix} \langle {}^3S_1 | S_{12} | {}^3S_1 \rangle  \langle {}^3S_1 | S_{12} | {}^3D_1 \rangle \\ \langle {}^3D_1 | S_{12} | {}^3S_1 \rangle  \langle {}^3D_1 | S_{12} | {}^3D_1 \rangle \end{pmatrix} = \begin{pmatrix} 0  2\sqrt{2} \\ 2\sqrt{2}  -2 \end{pmatrix}
$$
The off-diagonal elements are responsible for mixing the [s-wave](@entry_id:754474) and d-wave components. Solving this system of coupled differential equations is a cornerstone of [computational nuclear physics](@entry_id:747629), revealing, for example, the d-state component of the [deuteron bound state](@entry_id:160543).