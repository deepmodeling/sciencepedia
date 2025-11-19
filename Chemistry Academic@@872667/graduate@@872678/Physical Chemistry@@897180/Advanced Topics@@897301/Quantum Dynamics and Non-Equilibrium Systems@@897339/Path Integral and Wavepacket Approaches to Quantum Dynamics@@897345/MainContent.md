## Introduction
Understanding the time evolution of quantum systems is fundamental to modern chemistry and physics, governing processes from chemical reactions to electron transport in materials. However, directly solving the time-dependent Schrödinger equation for complex systems is often intractable. This challenge has driven the development of powerful theoretical and computational frameworks, among which Feynman's [path integral](@entry_id:143176) and time-dependent wavepacket approaches stand as pillars of the field. These methods provide indispensable tools for bridging the gap between fundamental quantum principles and observable phenomena, allowing us to simulate dynamics in regimes where classical mechanics fails, such as [quantum tunneling](@entry_id:142867) and [nonadiabatic transitions](@entry_id:199204).

This article provides a comprehensive exploration of these powerful techniques. The first chapter, **Principles and Mechanisms**, delves into the formal construction of the [path integral](@entry_id:143176), the derivation of semiclassical approximations, and the profound connection to [quantum statistical mechanics](@entry_id:140244) via [imaginary time](@entry_id:138627). The second chapter, **Applications and Interdisciplinary Connections**, showcases how these formalisms are applied to calculate [reaction rates](@entry_id:142655), thermodynamic properties, and interpret spectroscopic experiments, highlighting their impact across various scientific disciplines. Finally, the **Hands-On Practices** section offers a curated set of problems to solidify understanding and develop practical skills in implementing these methods.

## Principles and Mechanisms

### The Path Integral Formulation of Quantum Propagation

The [time evolution](@entry_id:153943) of a quantum state is governed by the time-dependent Schrödinger equation, whose formal solution for a time-independent Hamiltonian $\hat{H}$ is given by the action of the [time-evolution operator](@entry_id:186274), $\hat{U}(t) = \exp(-i\hat{H}t/\hbar)$, on the initial state. The Feynman [path integral](@entry_id:143176) provides a powerful and intuitive representation of this operator's [matrix elements](@entry_id:186505), known as the propagator or kernel, $K(x_f, t; x_i, 0) = \langle x_f | \hat{U}(t) | x_i \rangle$. It reformulates quantum mechanics in a Lagrangian framework, expressing the [propagator](@entry_id:139558) as a sum over all possible paths connecting an initial position $x_i$ to a final position $x_f$ in a time $t$.

#### Operator Splitting and the Short-Time Propagator

The direct evaluation of the exponential operator $\exp(-i\hat{H}t/\hbar)$ is generally intractable, primarily because the Hamiltonian $\hat{H}$ is a sum of the kinetic energy operator, $\hat{T} = \hat{p}^2/(2m)$, and the potential energy operator, $\hat{V} = V(\hat{x})$, which do not commute. The non-commutativity, $[\hat{T}, \hat{V}] \neq 0$, rooted in the fundamental commutation relation $[\hat{x}, \hat{p}] = i\hbar$, prevents a simple separation of the exponential: $\exp(\hat{A}+\hat{B}) \neq \exp(\hat{A})\exp(\hat{B})$ for [non-commuting operators](@entry_id:141460) $\hat{A}$ and $\hat{B}$.

The path integral approach circumvents this difficulty by dividing the total time interval $t$ into $N$ infinitesimally small time steps, $\Delta t = t/N$. For a sufficiently short time step $\Delta t$, one can use an approximation for the short-time [propagator](@entry_id:139558), $\hat{U}(\Delta t)$. The simplest such approximation is the **first-order Trotter splitting**:
$$
\hat{U}(\Delta t) = \exp\left(-\frac{i}{\hbar}(\hat{T}+\hat{V})\Delta t\right) \approx \exp\left(-\frac{i\hat{T}\Delta t}{\hbar}\right) \exp\left(-\frac{i\hat{V}\Delta t}{\hbar}\right)
$$
The accuracy of such splitting schemes can be rigorously analyzed using the Baker-Campbell-Hausdorff (BCH) formula. The [local error](@entry_id:635842) of this first-order scheme, which is the error for a single step, is of order $\mathcal{O}((\Delta t)^2)$ and is proportional to the commutator $[\hat{T}, \hat{V}]$. When these local errors accumulate over the $N = t/\Delta t$ steps required to span a finite time $t$, the resulting **global error** scales as $\mathcal{O}(\Delta t)$.

A significant improvement in accuracy is achieved by using a symmetric decomposition, such as the **second-order Strang splitting**:
$$
\hat{U}(\Delta t) \approx \exp\left(-\frac{i\hat{V}\Delta t}{2\hbar}\right) \exp\left(-\frac{i\hat{T}\Delta t}{\hbar}\right) \exp\left(-\frac{i\hat{V}\Delta t}{2\hbar}\right)
$$
The symmetric construction ensures that the leading error term of order $(\Delta t)^2$ cancels. The leading term in the local error for this scheme is of order $\mathcal{O}((\Delta t)^3)$ and involves a linear combination of the nested [commutators](@entry_id:158878) $[\hat{T},[\hat{T},\hat{V}]]$ and $[\hat{V},[\hat{T},\hat{V}]]$. This higher-order local accuracy translates into a [global error](@entry_id:147874) of $\mathcal{O}((\Delta t)^2)$, a substantial improvement over the first-order scheme. By systematically composing symmetric splittings, one can construct even higher-order methods. For example, a **fourth-order Suzuki scheme** can be built from the second-order product, yielding a [local error](@entry_id:635842) of order $\mathcal{O}((\Delta t)^5)$ and a [global error](@entry_id:147874) of $\mathcal{O}((\Delta t)^4)$ [@problem_id:2658924].

Let us derive the explicit coordinate-space representation of the short-time [propagator](@entry_id:139558) using a symmetric splitting, which is fundamental to most numerical and theoretical applications of [path integrals](@entry_id:142585) [@problem_id:2658901]. We use the alternative symmetric form $\hat{U}(\Delta t) \approx \exp(-\frac{i\hat{T}\Delta t}{2\hbar}) \exp(-\frac{i\hat{V}\Delta t}{\hbar}) \exp(-\frac{i\hat{T}\Delta t}{2\hbar})$. The [propagator](@entry_id:139558) is $K(x', \Delta t; x, 0) = \langle x'|\hat{U}(\Delta t)|x\rangle$. We insert a [completeness relation](@entry_id:139077) $\int dy |y\rangle\langle y| = \hat{1}$ to evaluate the matrix element:
$$
K(x', \Delta t; x, 0) \approx \int dy \left\langle x' \left| \exp\left(-\frac{i\hat{T}\Delta t}{2\hbar}\right) \right| y \right\rangle \left\langle y \left| \exp\left(-\frac{i\hat{V}\Delta t}{\hbar}\right) \right| x \right\rangle
$$
Since $\hat{V}$ is diagonal in the [position basis](@entry_id:183995), $\langle y|\exp(-i\hat{V}\Delta t/\hbar)|x\rangle = \exp(-iV(x)\Delta t/\hbar) \delta(y-x)$. The integral collapses, yielding a product of a free-[particle propagator](@entry_id:195036) and a potential-dependent phase factor. This is the result for an asymmetric splitting.

For the symmetric splitting, we must insert two completeness relations. A more direct route is the [stationary phase approximation](@entry_id:196626). The [path integral](@entry_id:143176) for a short time step can be written as an integral over an intermediate point $x_1$ at time $\Delta t/2$. The symmetric splitting leads to an action where the potential is evaluated at the midpoint in time. For the path segment from $(x,0)$ to $(x', \Delta t)$, the [stationary phase approximation](@entry_id:196626) shows that the path is dominated by the classical trajectory. For a short step, this is a straight line, and the dominant intermediate point is the spatial midpoint $x_1 \approx (x+x')/2$. The action contribution from the potential is then approximately $V((x+x')/2)\Delta t$. This is known as the **[midpoint rule](@entry_id:177487)**. Combining this with the kinetic energy term, which corresponds to free-particle propagation, we arrive at the expression for the symmetric short-time [propagator](@entry_id:139558):
$$
K(x', \Delta t; x, 0) \approx \sqrt{\frac{m}{2\pi i\hbar \Delta t}} \exp\left\{ \frac{i}{\hbar} \left[ \frac{m(x'-x)^{2}}{2\Delta t} - V\left(\frac{x+x'}{2}\right)\Delta t \right] \right\}
$$
This form is not only more accurate but also preserves [time-reversal symmetry](@entry_id:138094) at the discrete level, a crucial property for many physical systems.

#### Constructing the Full Path Integral

With an accurate expression for the short-time [propagator](@entry_id:139558), we can construct the propagator for a finite time $t$ by chaining $N$ short steps together. We partition the time interval $[t_i, t_f]$ into $N$ slices of duration $\Delta t = (t_f - t_i)/N$. The full [evolution operator](@entry_id:182628) is the product $\hat{U}(t_f, t_i) = \hat{U}(t_N, t_{N-1}) \cdots \hat{U}(t_1, t_0)$. To find its matrix elements, we insert a [resolution of the identity](@entry_id:150115), $\int dx_k |x_k\rangle\langle x_k| = \hat{1}$, at each intermediate time slice $t_k$ ($k=1, \dots, N-1$):
$$
K(x_f, t_f; x_i, t_i) = \int dx_1 \cdots \int dx_{N-1} \prod_{k=1}^{N} \langle x_k | \hat{U}(t_k, t_{k-1}) | x_{k-1} \rangle
$$
where $x_0 \equiv x_i$ and $x_N \equiv x_f$. Each term in the product is a short-time propagator. To maintain second-order global accuracy for a potentially time-dependent Hamiltonian $\hat{H}(t) = \hat{T} + \hat{V}(t)$, we must use a scheme that is locally accurate to third order. This involves two midpoint rules: one for the [operator splitting](@entry_id:634210) (Strang splitting) and one for the time-integration of the potential. This leads to a short-time kernel where the potential is evaluated at the midpoint in time, $t_{k-1/2} = t_{k-1} + \Delta t/2$, and its effect is split between the endpoints in space, $x_{k-1}$ and $x_k$ [@problem_id:2658884]. The final discretized path integral is an $(N-1)$-fold integral over all intermediate positions:
$$
K_N(x_f, t_f; x_i, t_i) = \left(\frac{m}{2\pi i \hbar \Delta t}\right)^{N/2} \int \left(\prod_{j=1}^{N-1} dx_j\right) \exp\left\{ \frac{i}{\hbar} \sum_{k=1}^{N} \mathcal{L}_{k} \right\}
$$
The term in the exponent is the sum of the discrete **Lagrangian**, $\mathcal{L}_k = \frac{m(x_k - x_{k-1})^2}{2\Delta t} - \frac{\Delta t}{2} \left[ V(x_k, t_{k-1/2}) + V(x_{k-1}, t_{k-1/2}) \right]$. In the limit $N \to \infty$, this sum becomes the classical action integral, $S[x(t)] = \int_{t_i}^{t_f} L(x(t), \dot{x}(t), t) dt$, and the integration measure becomes a sum over all paths, $\mathcal{D}x(t)$.

### The Semiclassical Limit and Wavepacket Dynamics

#### The Van Vleck Propagator and Classical Trajectories

The [path integral formalism](@entry_id:138631) provides a natural bridge between quantum and classical mechanics. In the **semiclassical limit**, where the action $S$ is large compared to $\hbar$, the phase factor $\exp(iS/\hbar)$ oscillates extremely rapidly. The integral over paths is therefore dominated by contributions from paths where the phase is stationary, i.e., where the action is at an extremum. This is precisely the content of Hamilton's Principle of Least Action, which defines the classical path.

The [stationary phase approximation](@entry_id:196626) to the path integral leads to the **semiclassical** or **Van Vleck [propagator](@entry_id:139558)**, which expresses the kernel as a sum over all classical trajectories connecting the initial and final points:
$$
K_{\text{sc}}(\mathbf{x}_f, \mathbf{x}_i; t) \approx \sum_{\text{cl. paths } j} A_j \exp\left(\frac{i}{\hbar} S_j(\mathbf{x}_f, \mathbf{x}_i; t)\right)
$$
The phase is given by the classical action $S_j$ along the $j$-th path. The pre-exponential factor $A_j$ accounts for the Gaussian fluctuations of quantum paths around the classical one. For a multidimensional system, this prefactor is determined by the stability of the classical trajectory. It can be expressed in terms of the **[monodromy matrix](@entry_id:273265)**, $\mathbf{M}(t)$, which linearizes the mapping of phase-space deviations from the initial time to the final time. The explicit form of the [propagator](@entry_id:139558) is [@problem_id:2658891]:
$$
K(\mathbf{x}_f, \mathbf{x}_i; t) \approx \sum_{\text{cl}} \frac{1}{(2\pi i \hbar)^{d/2}} \frac{1}{\sqrt{|\det \mathbf{B}|}} \exp\left[ \frac{i}{\hbar}S_{\text{cl}}(\mathbf{x}_f, \mathbf{x}_i; t) - i \frac{\pi}{2} \nu \right]
$$
Here, $d$ is the number of dimensions, and $\mathbf{B} = \partial\mathbf{x}_f / \partial\mathbf{p}_i$ is the upper-right block of the [monodromy matrix](@entry_id:273265), which measures how an initial spread in momentum affects the final position. The prefactor's magnitude, $1/\sqrt{|\det\mathbf{B}|}$, is large when a family of trajectories focuses ($\det \mathbf{B} \to 0$) and small when they diverge. A point where $\det \mathbf{B} = 0$ is known as a **[caustic](@entry_id:164959)**, where the [semiclassical approximation](@entry_id:147497) diverges. The **Maslov index** $\nu$ is an integer that counts the number of times the trajectory has passed through [caustics](@entry_id:158966), adding a phase shift of $-\pi/2$ for each passage.

#### Dynamics of Gaussian Wavepackets

An ideal case study for [semiclassical dynamics](@entry_id:140913) is the evolution of a **Gaussian wavepacket**, which represents a quantum state that is maximally localized in phase space, satisfying the minimum uncertainty relation $\sigma_x \sigma_p = \hbar/2$. For a Hamiltonian that is at most quadratic in position and momentum, such as the quantum harmonic oscillator, a remarkable property holds: an initial Gaussian wavepacket remains Gaussian for all time.

Consider a [harmonic oscillator](@entry_id:155622) with Hamiltonian $\hat{H} = \frac{\hat{p}^2}{2m} + \frac{1}{2}m\omega^2\hat{x}^2$. If we prepare an initial wavepacket centered at $(x_0, p_0)$ with position standard deviation $\sigma_0$, its subsequent evolution can be solved exactly [@problem_id:2658897]. The centroid of the wavepacket, $\langle \hat{x} \rangle(t)$, follows the classical trajectory of a particle with [initial conditions](@entry_id:152863) $(x_0, p_0)$:
$$
\langle \hat{x} \rangle(t) = x_0 \cos(\omega t) + \frac{p_0}{m\omega} \sin(\omega t)
$$
The quantum nature of the system manifests in the evolution of the wavepacket's width, or position standard deviation $\sigma_x(t)$. It does not remain constant but oscillates in time, a phenomenon known as "breathing":
$$
\sigma_x(t) = \sqrt{\sigma_0^2 \cos^2(\omega t) + \frac{\hbar^2}{4m^2\omega^2\sigma_0^2} \sin^2(\omega t)}
$$
This exact solution beautifully illustrates the correspondence principle: the expectation values of the [quantum operators](@entry_id:137703) follow classical mechanics, while the [quantum fluctuations](@entry_id:144386) (the wavepacket's shape) evolve according to a quantum-mechanical law.

#### Tunneling and Complex Classical Paths

The semiclassical picture appears to fail for classically forbidden processes, such as [quantum tunneling](@entry_id:142867), where no real classical trajectory connects the initial and final points. However, the framework can be extended by allowing paths to propagate in complex-valued space and time.

Consider tunneling through a symmetric double-well potential. A wavepacket initially localized in one well has zero probability of being found in the other well according to classical mechanics (at energies below the barrier height). In the semiclassical path integral, there are no real stationary paths that cross the barrier. However, there exists a pair of **[complex conjugate](@entry_id:174888) classical paths** that solve the boundary-value problem. Their actions are complex conjugates, $S_{\pm} = S_R \pm i S_E$, where the imaginary part $S_E$ is positive and related to the integral of $\sqrt{2m(V(x)-E)}$ across the barrier.

The propagator for tunneling is given by the coherent sum of the contributions from these two paths. This interference leads to an amplitude in the forbidden region that is exponentially suppressed by the factor $e^{-S_E/\hbar}$, but which is also oscillatory, proportional to $\cos(S_R/\hbar + \phi)$, where $\phi$ is a phase. This gives rise to a faint, time-oscillatory probability density in the other well, known as a **tunneling precursor**, appearing at very short times, long before any significant [population transfer](@entry_id:170564) occurs [@problem_id:2658855]. This demonstrates that even quintessentially quantum phenomena like tunneling can be understood through the lens of (complexified) classical mechanics.

### Path Integrals in Imaginary Time: Quantum Statistical Mechanics

#### The Quantum-Classical Isomorphism and the Ring Polymer

A profound connection exists between quantum dynamics and statistical mechanics. The quantum [time-evolution operator](@entry_id:186274), $e^{-i\hat{H}t/\hbar}$, is formally equivalent to the Boltzmann operator of statistical mechanics, $e^{-\beta\hat{H}}$, upon the substitution of real time $t$ with imaginary time $\tau = i t$, where $t = -i\beta\hbar$. Here, $\beta = 1/(k_B T)$ is the inverse temperature. This allows us to compute quantum statistical properties, such as the partition function $Z = \text{Tr}(e^{-\beta\hat{H}})$, using path integral techniques.

The imaginary-time [path integral](@entry_id:143176) for the partition function involves a sum over all paths that are periodic in imaginary time with period $\beta\hbar$. Discretizing this [path integral](@entry_id:143176) with $P$ time slices (often called **beads**) leads to a remarkable result known as the **[quantum-classical isomorphism](@entry_id:201443)**. A single quantum particle is mapped onto a classical system of $P$ beads connected by harmonic springs, forming a closed necklace or **ring polymer**. The [effective potential energy](@entry_id:171609) of this classical polymer is:
$$
U_{\text{RP}}(\{q_j\}) = \sum_{j=1}^{P} \left[ \frac{1}{2} m \omega_P^2 (q_j - q_{j+1})^2 + V(q_j) \right]
$$
with the cyclic condition $q_{P+1} \equiv q_1$. The physical potential $V(q)$ is sampled at each bead, while the quantum kinetic energy has manifested as a harmonic interaction between adjacent beads. The spring constant depends on the "discretization frequency" $\omega_P = P/(\beta\hbar)$.

The internal structure of this polymer can be analyzed by a normal-mode transformation, which diagonalizes the harmonic coupling. For a free particle ($V(q)=0$), the normal modes are discrete Fourier modes. The frequencies of these internal vibrations of the ring polymer are given by [@problem_id:2658886]:
$$
\omega_k = 2\omega_P \sin\left(\frac{\pi k}{P}\right) = \frac{2P}{\beta\hbar} \sin\left(\frac{\pi k}{P}\right) \quad \text{for } k = 0, 1, \dots, P-1
$$
The $k=0$ mode has zero frequency and corresponds to the free translation of the polymer's center of mass. The non-zero frequency modes ($k>0$) represent the quantum fluctuations or "[delocalization](@entry_id:183327)" of the particle.

#### Instanton Theory of Quantum Reaction Rates

Imaginary-time [path integrals](@entry_id:142585) provide a powerful framework for calculating [chemical reaction rates](@entry_id:147315), especially at low temperatures where [quantum tunneling](@entry_id:142867) is significant. In this context, the rate is related to the imaginary part of the free energy, which can be computed via a [saddle-point approximation](@entry_id:144800) to the path integral.

The saddle points are paths that extremize the Euclidean (imaginary-time) action. For a reaction proceeding over a potential barrier, two types of saddle points are of primary importance:
1.  A trivial path, $x(\tau)=0$, where the particle stays atop the potential barrier for all [imaginary time](@entry_id:138627) $\tau$. This path corresponds to classical [thermal activation](@entry_id:201301) and is the basis for **Transition State Theory (TST)**.
2.  A non-trivial periodic path that traverses the potential barrier in imaginary time. This path is known as an **[instanton](@entry_id:137722)** and describes the [quantum tunneling](@entry_id:142867) process.

The competition between these two pathways is temperature-dependent. For a potential with a barrier-top (imaginary) frequency of $\omega_b$, there exists a **[crossover temperature](@entry_id:181193)**, $T_c = \hbar\omega_b / (2\pi k_B)$.
-   For $T > T_c$, the dominant mechanism is [thermal activation](@entry_id:201301). The trivial path at the barrier top is the relevant saddle point, and the rate is well-described by quantum-corrected TST.
-   For $T  T_c$, the trivial path becomes unstable. A new saddle point, the instanton, emerges and dominates the path integral. The rate is then governed by tunneling, with $k \propto e^{-S_{\text{inst}}/\hbar}$, where $S_{\text{inst}}$ is the action of the instanton path. As temperature decreases, the tunneling contribution provided by [instanton theory](@entry_id:182167) far exceeds the prediction of classical TST [@problem_id:2658856].

### Alternative Representations and Computational Challenges

#### Coherent State Path Integrals

The coordinate-space representation is not the only useful basis for [path integrals](@entry_id:142585). For systems dominated by oscillatory motion, such as [molecular vibrations](@entry_id:140827) or quantized electromagnetic fields, the **[coherent state](@entry_id:154869)** basis is often more natural. A canonical coherent state $|\alpha\rangle$, labeled by a complex number $\alpha$, is an [eigenstate](@entry_id:202009) of the [annihilation operator](@entry_id:149476), $\hat{a}|\alpha\rangle = \alpha|\alpha\rangle$. It can be generated by applying the displacement operator $\hat{D}(\alpha) = \exp(\alpha\hat{a}^\dagger - \alpha^*\hat{a})$ to the vacuum state: $|\alpha\rangle = \hat{D}(\alpha)|0\rangle$.

Coherent states are normalized but not orthogonal; their overlap is given by $\langle\beta|\alpha\rangle = \exp(-\frac{1}{2}|\alpha|^2 - \frac{1}{2}|\beta|^2 + \beta^*\alpha)$. They form an **overcomplete** set, resolving the identity as $\int \frac{d^2\alpha}{\pi} |\alpha\rangle\langle\alpha| = \hat{I}$, where the integration is over the entire complex plane.

Constructing a [path integral](@entry_id:143176) using this basis leads to the **coherent-state [path integral](@entry_id:143176)**. The resulting action contains a special "kinetic" or **symplectic term** that does not appear in the coordinate-space version. For a normally ordered Hamiltonian $H(\hat{a}^\dagger, \hat{a})$, the action for the [path integral](@entry_id:143176) over complex fields $\alpha(t)$ is:
$$
S[\alpha^*, \alpha] = \int_0^T \left[ i\hbar \alpha^*(t) \frac{d\alpha(t)}{dt} - H(\alpha^*(t), \alpha(t)) \right] dt
$$
This symplectic term, $i\hbar \alpha^*\dot{\alpha}$, arises directly from the [non-orthogonality](@entry_id:192553) of the coherent state basis at infinitesimal time steps apart. It is crucial for generating the correct quantum dynamics and has deep connections to the concept of geometric phase (Berry phase) [@problem_id:2658887].

#### The Dynamical Sign Problem

While the path integral provides a profound theoretical framework, its numerical evaluation for real-time quantum dynamics is notoriously difficult. This challenge is known as the **dynamical [sign problem](@entry_id:155213)**. In a Monte Carlo evaluation of a real-time path integral, one typically samples paths from a positive probability distribution $p_0[x]$ and computes [observables](@entry_id:267133) by reweighting each path with the oscillatory phase factor $e^{i\phi_t[x]}$, where $\phi_t[x] = S[x]/\hbar$ is the phase accumulated over time $t$. An expectation value is then a ratio of two such averages: $\langle A \rangle = \langle A e^{i\phi_t} \rangle_0 / \langle e^{i\phi_t} \rangle_0$.

The denominator, $\langle e^{i\phi_t} \rangle_0$, represents the average phase factor over all sampled paths. The phase $\phi_t$ is a sum of increments from each time step. By the [central limit theorem](@entry_id:143108), for long times, $\phi_t$ becomes a normally distributed random variable with a variance that grows linearly with time, $\mathrm{Var}_0(\phi_t) \sim v t$, where $v$ is a phase "diffusion" constant. The average of the phase factor is the characteristic function of this Gaussian distribution, which decays exponentially:
$$
|\langle e^{i\phi_t} \rangle_0| \approx e^{-\frac{1}{2}\mathrm{Var}_0(\phi_t)} \sim e^{-vt/2}
$$
As time $t$ increases, the average phase factor, which is the "signal," decays exponentially to zero due to massive destructive interference between paths. The variance of the Monte Carlo estimator for the ratio is inversely proportional to the square of this decaying signal, and therefore grows exponentially: $\mathrm{Var}(\hat{A}) \sim \frac{1}{N}e^{vt}$. To maintain a constant signal-to-noise ratio, the number of Monte Carlo samples $N$ must grow exponentially with time, rendering the method computationally intractable for all but the shortest time scales [@problem_id:2658869]. This exponential degradation of signal-to-noise is a fundamental obstacle in the simulation of real-time [quantum dynamics](@entry_id:138183) for [many-body systems](@entry_id:144006).