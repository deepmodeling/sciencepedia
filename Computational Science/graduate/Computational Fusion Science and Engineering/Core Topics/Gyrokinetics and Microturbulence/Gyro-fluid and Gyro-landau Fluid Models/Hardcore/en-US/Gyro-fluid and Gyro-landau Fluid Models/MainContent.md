## Introduction
In the quest for controlled nuclear fusion, understanding and predicting the turbulent transport of heat and particles in magnetized plasma is a paramount challenge. While first-principles kinetic models offer the highest fidelity, their computational cost is often prohibitive for [large-scale simulations](@entry_id:189129). At the other extreme, simpler fluid models are computationally efficient but miss crucial kinetic physics. Gyro-fluid and Gyro-Landau Fluid (GLF) models emerge as a powerful intermediate framework, providing a vital bridge between these two descriptions. They are designed to retain essential kinetic effects, such as Finite Larmor Radius corrections and collisionless Landau damping, within a computationally tractable fluid structure, making them indispensable tools for modern fusion science.

This article provides a comprehensive overview of the theory and application of these sophisticated reduced models. We will begin in the **Principles and Mechanisms** chapter by exploring the foundational concepts, including the [gyrokinetic ordering](@entry_id:1125860) that justifies the models and the [moment closure problem](@entry_id:1128123) that defines their central challenge. We will see how GLF models are engineered to capture the physics of Landau damping. Next, the **Applications and Interdisciplinary Connections** chapter will showcase how these models are used to simulate plasma turbulence, predict [transport in tokamaks](@entry_id:1133397), and integrate with other computational tools in large-scale modeling efforts. Finally, the **Hands-On Practices** section will offer concrete problems designed to solidify your understanding of the key concepts, from implementing [closures](@entry_id:747387) to addressing numerical challenges.

## Principles and Mechanisms

The derivation of reduced fluid models from first-principles kinetic theory is a cornerstone of modern theoretical and [computational plasma physics](@entry_id:198820). Gyro-fluid and Gyro-Landau Fluid (GLF) models represent a sophisticated class of such theories, designed to retain essential kinetic effects while offering significant computational advantages over a full kinetic description. This chapter elucidates the fundamental principles and mechanisms that underpin these models, from the initial scale separation that justifies them to the intricate [closures](@entry_id:747387) that grant them their predictive power.

### The Gyrokinetic Ordering and Scale Separation

The dynamics of a magnetized plasma span a vast range of temporal and spatial scales. The fastest motion is the Larmor gyration of charged particles around magnetic field lines, characterized by the cyclotron frequency, $\Omega_s = q_s B / m_s$, where $q_s$ and $m_s$ are the charge and mass of species $s$ and $B$ is the magnetic field strength. In contrast, the turbulent fluctuations and transport processes that are often of primary interest in fusion devices evolve on much slower timescales and have spatial structures that are large compared to the Larmor radius. Gyro-fluid models are built upon a systematic exploitation of this scale separation.

This separation is formalized through the **[gyrokinetic ordering](@entry_id:1125860)**, which introduces a small dimensionless parameter $\epsilon \ll 1$. For ion-scale turbulence, this parameter is defined as the ratio of the characteristic ion gyroradius to the macroscopic equilibrium scale length . A common choice is to use the ion sound Larmor radius, $\rho_s = c_s / \Omega_i$, where $c_s = \sqrt{T_e/m_i}$ is the ion sound speed based on the electron temperature $T_e$, and $\Omega_i$ is the ion cyclotron frequency. The small parameter is then $\epsilon = \rho_s / L$, where $L$ is the characteristic scale length of equilibrium gradients (e.g., density or temperature gradients).

The assumption that $\epsilon \ll 1$ provides a basis for a rigorous [asymptotic expansion](@entry_id:149302). A self-consistent set of orderings emerges, which defines the regime of **low-frequency, drift-wave turbulence**:

*   **Frequency Ordering**: The characteristic frequency of fluctuations, $\omega$, is ordered to be much smaller than the ion [cyclotron frequency](@entry_id:156231): $\omega / \Omega_i \sim \mathcal{O}(\epsilon)$. This low-frequency condition is the fundamental justification for averaging over the fast gyromotion.

*   **Perpendicular Wavenumber Ordering**: To retain the influence of the finite size of particle orbits on the turbulence, the perpendicular wavelength, $1/k_\perp$, must be comparable to the gyroradius. This leads to the crucial ordering for **Finite Larmor Radius (FLR) effects**: $k_\perp \rho_s \sim \mathcal{O}(1)$. This distinguishes [gyro-fluid models](@entry_id:1125847) from standard fluid models like MHD, where $k_\perp \rho_s \ll 1$.

*   **Parallel Wavenumber Ordering**: Turbulence in strongly magnetized plasmas is highly anisotropic, with structures elongated along the magnetic field. The parallel wavenumber $k_\parallel$ is assumed to be much smaller than the perpendicular wavenumber, reflecting long parallel wavelengths: $k_\parallel / k_\perp \sim \mathcal{O}(\epsilon)$.

*   **Amplitude and Drift Ordering**: The theory is perturbative, assuming small-amplitude fluctuations. The normalized electrostatic potential is ordered as $e\phi/T_e \sim \mathcal{O}(\epsilon)$. This is consistent with the ordering for the dominant perpendicular drift velocity, the $\mathbf{E}\times\mathbf{B}$ drift $v_E = |\mathbf{E}_\perp \times \mathbf{B}|/B^2$. A straightforward derivation shows that $v_E/c_s \sim (k_\perp \rho_s)(e\phi/T_e) \sim \mathcal{O}(1) \cdot \mathcal{O}(\epsilon) = \mathcal{O}(\epsilon)$, meaning drift velocities are slow compared to thermal speeds .

These orderings allow one to systematically separate the particle's position $\mathbf{r}$ into a slowly evolving **guiding-center** position $\mathbf{R}$ and a rapidly oscillating gyroradius vector $\boldsymbol{\rho}_s$. The dynamics of any physical quantity can then be averaged over the gyro-angle $\theta$ to obtain equations for the guiding-center (or gyro-averaged) quantities. This is accomplished using the **gyroaverage operator**:
$$
\langle g \rangle_{\theta}(\mathbf{R}, v_\perp) = \frac{1}{2\pi} \int_{0}^{2\pi} g\big(\mathbf{R} + \boldsymbol{\rho}_s(\theta)\big)\, d\theta
$$
When this operator acts on a plane-wave perturbation of the form $\delta \phi(\mathbf{r}) = \phi_{\mathbf{k}} \exp(i \mathbf{k}\cdot \mathbf{r})$, it filters the wave's effect on the particle's guiding center. The result introduces a multiplicative factor that depends on the perpendicular wavenumber and the particle's perpendicular velocity $v_\perp$ . Specifically,
$$
\langle \exp(i \mathbf{k}\cdot \mathbf{r}) \rangle_{\theta} = \exp(i \mathbf{k}\cdot \mathbf{R}) \left( \frac{1}{2\pi} \int_{0}^{2\pi} \exp(i \mathbf{k}_\perp \cdot \boldsymbol{\rho}_s(\theta)) d\theta \right) = \exp(i \mathbf{k}\cdot \mathbf{R}) J_0(k_\perp \rho_s)
$$
where $\rho_s = v_\perp / \Omega_s$ is the Larmor radius for a particle with perpendicular speed $v_\perp$, and $J_0$ is the zeroth-order Bessel function of the first kind. This appearance of $J_0(k_\perp \rho_s)$ is the mathematical signature of FLR effects. When deriving fluid models by taking velocity-space moments of the gyro-averaged kinetic equation, these Bessel functions are integrated over the velocity distribution, leading to functions like $\Gamma_0(b_s) = \exp(-b_s)I_0(b_s)$, where $b_s = k_\perp^2 \rho_{\mathrm{th},s}^2$ and $I_0$ is the modified Bessel function . These $\Gamma$ functions encode the FLR effects in the final fluid equations.

### The Moment Hierarchy and the Closure Problem

The transition from a kinetic description (which evolves the distribution function in 6D phase space) to a fluid description (which evolves moments like density, velocity, and pressure in 3D configuration space) is achieved by taking velocity-space moments of the underlying kinetic equation (e.g., the gyrokinetic equation).

This procedure invariably leads to the **closure problem**. Taking the zeroth moment of the kinetic equation yields the continuity equation, which describes the evolution of density (the zeroth moment). However, this equation contains the divergence of the [particle flux](@entry_id:753207), which is related to the flow velocity (the first moment). To find the evolution of the flow velocity, we take the first moment of the kinetic equation. This yields a momentum equation, but it will inevitably contain the divergence of the pressure or stress tensor (the second moment). This continues indefinitely: the evolution equation for the $n$-th moment depends on the $(n+1)$-th moment  .
$$
\frac{\partial M_n}{\partial t} \propto \nabla \cdot M_{n+1}
$$
To obtain a finite, [closed set](@entry_id:136446) of equations, this infinite hierarchy must be truncated. This is done by positing a **[closure relation](@entry_id:747393)**: an expression for a high-order moment in terms of lower-order ones.

The simplest closures involve neglecting high-order moments entirely. For example, assuming the heat flux tensor (the third moment) is zero leads to an adiabatic or [ideal fluid](@entry_id:272764) model. A classic example in magnetized plasma is the Chew–Goldberger–Low (CGL) model, which applies to a collisionless, gyrotropic plasma where heat fluxes are ignored . In this limit, the perpendicular and parallel pressures, $p_\perp$ and $p_\parallel$, evolve according to two separate adiabatic laws:
$$
\frac{d}{dt}\left(\frac{p_\perp}{nB}\right) = 0 \quad \text{and} \quad \frac{d}{dt}\left(\frac{p_\parallel B^2}{n^3}\right) = 0
$$
where $d/dt$ is the [convective derivative](@entry_id:262900). The first invariant is the fluid analogue of the conservation of a single particle's magnetic moment, $\mu$. The second, or "fire-hose," invariant governs the parallel dynamics. While historically important, such ideal [closures](@entry_id:747387) are insufficient for describing modern fusion experiments, as they neglect crucial physical effects.

### Modeling Collisionless Damping: The Essence of Gyro-Landau Fluids

The most significant physical process omitted by simple fluid [closures](@entry_id:747387) is **Landau damping**. This is a purely [collisionless damping](@entry_id:144163) mechanism that arises from resonant energy exchange between a wave and particles moving at or near the wave's phase velocity. From a fluid perspective, this effect originates from **[phase mixing](@entry_id:199798)** due to particle free streaming along magnetic field lines .

Consider the simplest kinetic equation describing this process, the 1D [free-streaming](@entry_id:159506) equation for the perturbed distribution function $g_s$:
$$
\frac{\partial g_s}{\partial t} + v_\parallel \frac{\partial g_s}{\partial z} = 0
$$
In Fourier space ($z \to k_\parallel$), this becomes $\partial_t g_s = -i k_\parallel v_\parallel g_s$, with the solution $g_s(t) = g_s(0) \exp(-i k_\parallel v_\parallel t)$. Any fluid moment, such as the parallel flow $u_{\parallel s} = (1/n_0) \int v_\parallel g_s \, d^3v$, will involve an integral of this solution. The term $\exp(-i k_\parallel v_\parallel t)$ introduces rapid oscillations in the integrand as a function of $v_\parallel$. Due to the Riemann-Lebesgue lemma, this leads to destructive interference and the temporal decay of the moment for any smooth initial condition $g_s(0)$. Fluctuation energy in low-order moments is transferred to ever-finer structures in velocity space (higher-order moments), appearing as a macroscopic damping.

To capture this effect, a fluid model's closure must replicate this kinetic behavior. A simple truncation like setting the [parallel heat flux](@entry_id:753124) $q_\parallel$ to zero fails, as it leads to undamped oscillations. A collisional closure, like Fourier's law, introduces damping with the wrong physical origin and mathematical character. The breakthrough of **Gyro-Landau Fluid (GLF) models** was the development of closures that approximate the full kinetic response  .

The kinetic response is inherently nonlocal. A perturbation at one point along a field line affects another point later in time as particles stream between them. In Fourier space, this nonlocality becomes a specific dependence on the wavenumber $k_\parallel$. A minimal closure for the [parallel heat flux](@entry_id:753124) $q_{\parallel s}$ that captures Landau damping must have the form:
$$
\hat{q}_{\parallel s}(k_\parallel) = - \alpha_s n_s v_{\mathrm{th},s} \left( \frac{i k_\parallel}{|k_\parallel|} \right) \hat{T}_{\parallel s}(k_\parallel)
$$
where hats denote Fourier-transformed quantities, $v_{\mathrm{th},s}$ is the [thermal velocity](@entry_id:755900), $T_{\parallel s}$ is the parallel temperature perturbation, and $\alpha_s$ is a dimensionless coefficient. The crucial element is the operator $i k_\parallel / |k_\parallel|$, which in real space corresponds to the Hilbert transform of the parallel gradient. This nonlocal, odd-[parity operator](@entry_id:148434) correctly introduces the dissipation characteristic of linear Landau damping .

The coefficient $\alpha_s$ is not arbitrary; it is rigorously derived by matching the fluid model's response to the exact linear kinetic response in a specific limit. The kinetic response is described by the [plasma dispersion function](@entry_id:201903) $Z(\zeta)$, where $\zeta = \omega / (k_\parallel v_{\mathrm{th},s})$. By using a Padé approximation for the kinetic response function and matching its Taylor series expansion for small $\zeta$, one can systematically determine the closure coefficients. For a common form of the GLF model, this procedure yields a universal constant $\alpha_s = \pi - 2$ . This connection demonstrates that GLF models are not merely phenomenological but are rooted in a systematic approximation of the underlying kinetic theory.

### The Hamiltonian Structure of Ideal Gyro-fluids

While GLF closures introduce necessary dissipation, the underlying dynamics of the gyro-averaged system in the ideal, collisionless, non-dissipative limit possess a beautiful and powerful mathematical structure: they are **Hamiltonian systems**. This structure is most elegantly revealed by expressing the advective dynamics using the **Poisson bracket** .

In the [electrostatic limit](@entry_id:1124352) with a uniform magnetic field $\mathbf{B}$, the perpendicular dynamics of any gyro-fluid moment $M$ are dominated by advection with the $\mathbf{E}\times\mathbf{B}$ drift velocity, $\mathbf{v}_E = (\mathbf{B} \times \nabla \phi) / B^2$. The evolution equation, neglecting parallel dynamics and sources, is:
$$
\frac{\partial M}{\partial t} + \mathbf{v}_E \cdot \nabla M = 0
$$
(Note that for a uniform $\mathbf{B}$, the flow is incompressible, $\nabla \cdot \mathbf{v}_E = 0$, so $\mathbf{v}_E \cdot \nabla M = \nabla \cdot (M\mathbf{v}_E)$.) The advection term can be rewritten using the perpendicular Poisson bracket, defined for two [scalar fields](@entry_id:151443) $f$ and $g$ as:
$$
\{f, g\} \equiv \frac{1}{B} \hat{\mathbf{b}} \cdot (\nabla f \times \nabla g)
$$
A direct calculation shows that $\mathbf{v}_E \cdot \nabla M = \{\phi, M\}$. Thus, the ideal [advection equation](@entry_id:144869) becomes:
$$
\frac{\partial M}{\partial t} + \{\phi, M\} = 0
$$
This form makes the Hamiltonian nature of the system explicit. The electrostatic potential $\phi$ acts as the Hamiltonian for the advection of tracer fields like $M$. This structure has profound implications for the conservation laws of the system.

In a non-dissipative system, the Hamiltonian itself (the total energy) is conserved. However, Hamiltonian systems also possess a special class of invariants known as **Casimir invariants**. These are functionals of the system's fields that commute with *any* other functional under the Poisson bracket. For an ideal 2D gyro-fluid system where quantities like a generalized vorticity $q$ and an entropy-like field $s$ are materially advected by the incompressible $\mathbf{E}\times\mathbf{B}$ flow, there exists an infinite family of Casimir invariants :
$$
C_{\mathcal{H}} = \int \mathcal{H}(q, s) \, d^2x
$$
where $\mathcal{H}$ is any arbitrary smooth function. The conservation of these quantities reflects the fact that the incompressible flow merely shuffles the values of $q$ and $s$ around the domain; it does not create or destroy them. The entire fine-grained distribution of $(q,s)$ values is preserved. Specific choices for $\mathcal{H}$, such as $\mathcal{H} = q^2/2$, lead to the conservation of generalized enstrophy, a key feature of 2D turbulence. The existence of these powerful [structural invariants](@entry_id:145830) provides a critical check on numerical implementations and a deep insight into the [nonlinear dynamics](@entry_id:140844) of the system.

### Regimes of Application and Key Dimensionless Parameters

The applicability and behavior of gyro-fluid and GLF models are governed by a set of key [dimensionless parameters](@entry_id:180651) that characterize the plasma regime . Understanding their roles is crucial for interpreting model results.

*   **Plasma Beta ($\beta$)**: Defined as the ratio of plasma pressure to magnetic pressure, $\beta = 2\mu_0 n T / B^2$, this parameter controls the importance of electromagnetic fluctuations. In the **low-$\beta$ limit** ($\beta \to 0$), the plasma cannot significantly perturb the magnetic field. The dynamics become purely **electrostatic**, dominated by drift waves. As $\beta$ increases, the coupling between drift waves and shear-Alfvén waves becomes important. This [electromagnetic coupling](@entry_id:203990) can stabilize certain instabilities, like the Ion Temperature Gradient (ITG) mode, but it can also enable new ones, such as the [kinetic ballooning mode](@entry_id:751024), particularly in regimes of high pressure gradients and magnetic shear.

*   **Collisionality ($\nu$)**: This parameter represents the rate of particle collisions relative to other characteristic frequencies. Gyro-Landau fluid models are designed for the **low-collisionality** limit, where Landau damping dominates parallel dissipation. As collisionality increases, it begins to interfere with the delicate [phase mixing](@entry_id:199798) required for Landau damping, eventually suppressing it. At high collisionality, the physics transitions to a collisional fluid regime, where [parallel transport](@entry_id:160671) is diffusive and new [resistive instabilities](@entry_id:186275) can arise.

*   **Gradient Parameters ($\eta_s$)**: The free energy that drives [microinstabilities](@entry_id:751966) in fusion plasmas comes from the spatial gradients of density and temperature. The parameter $\eta_s = L_n / L_{T_s} = (\mathrm{d}\ln T_s / \mathrm{d}r) / (\mathrm{d}\ln n / \mathrm{d}r)$ measures the relative steepness of the temperature gradient of species $s$ compared to the density gradient. A large value of $\eta_i$ indicates a strong [ion temperature gradient](@entry_id:1126729), which is the primary drive for the **Ion Temperature Gradient (ITG) mode**. In toroidal geometry, there typically exists a critical value, $\eta_{i, \text{crit}}$, above which the ITG mode becomes linearly unstable. GLF models are routinely used to study the nonlinear saturation of these instabilities and the transport they cause.

In summary, gyro-fluid and GLF models are a powerful theoretical and computational tool. They are built upon the rigorous foundation of [gyrokinetic ordering](@entry_id:1125860), which separates fast gyromotion from slow drift dynamics. Their defining feature is the use of sophisticated closure relations, particularly those that model collisionless Landau damping, allowing them to capture essential kinetic physics within a fluid framework. The ideal dynamics possess a rich Hamiltonian structure, leading to powerful conservation laws. The behavior of these models across different plasma regimes is dictated by key physical parameters like $\beta$, $\nu$, and $\eta$, making them versatile instruments for understanding and predicting turbulent transport in magnetized plasmas.