## Introduction
Understanding the dynamics of condensed matter—how atoms and molecules move and rearrange over time—is fundamental to fields from materials science to [biophysics](@entry_id:154938). While static structure describes a system's average configuration, it is the dynamics that govern material properties like viscosity, diffusion, and the response to external forces. The primary theoretical tools for bridging the gap between microscopic particle trajectories and these macroscopic dynamic behaviors are time [correlation functions](@entry_id:146839). This article provides a comprehensive exploration of the most important of these: the [intermediate scattering function](@entry_id:159928) (ISF). By studying how [density fluctuations](@entry_id:143540) are correlated in space and time, the ISF offers a powerful lens into the complex dance of particles in liquids, glasses, and soft matter.

This article is structured to build a complete understanding from theory to practice. The journey begins in **Principles and Mechanisms**, where we will rigorously define the coherent and self intermediate scattering functions from their microscopic origins. We will explore their behavior in different regimes, uncovering universal short-time dynamics and the complex, multi-step relaxation characteristic of supercooled liquids approaching the [glass transition](@entry_id:142461). Next, **Applications and Interdisciplinary Connections** will demonstrate the ISF's broad utility, showing how it is used to interpret scattering experiments, validate computational models, and explain phenomena in diverse systems from polymers to [liquid crystals](@entry_id:147648). Finally, **Hands-On Practices** will ground these concepts in practical application, guiding you through the computation and analysis of scattering functions from simulation data. We will begin by delving into the core principles that make the [intermediate scattering function](@entry_id:159928) the central quantity for describing dynamics in condensed matter.

## Principles and Mechanisms

Having established the foundational role of time correlation functions in the Introduction, we now delve into the principles and mechanisms that govern their behavior. This chapter will dissect the [intermediate scattering function](@entry_id:159928), the central quantity for describing dynamics in condensed matter. We will start from its microscopic definition, explore its behavior in simple and complex systems, and develop the conceptual tools necessary to interpret the rich dynamical phenomena observed in liquids and glasses, from collective sound waves to the spatially heterogeneous motion characteristic of the approach to the glass transition.

### Defining Dynamic Correlations: The Intermediate Scattering Function

The dynamics of a many-body system are encoded in how the positions of its constituent particles are correlated in space and time. The most direct way to formalize these correlations begins with the concept of the microscopic particle density.

#### Microscopic Density and Its Fourier Modes

At any instant $t$, the configuration of a system of $N$ particles is given by their positions $\{\mathbf{r}_j(t)\}_{j=1}^N$. The **microscopic particle density** at a point $\mathbf{r}$ in space is defined as a field of delta functions centered on each particle's position:
$$
\rho(\mathbf{r}, t) = \sum_{j=1}^{N} \delta(\mathbf{r} - \mathbf{r}_j(t))
$$
While this representation is exact, it is often more insightful to analyze the system's structure in reciprocal space. The spatial **Fourier transform of the microscopic density**, known as the density mode or density fluctuation, is given by:
$$
\hat{\rho}(\mathbf{k}, t) = \int e^{-i\mathbf{k} \cdot \mathbf{r}} \rho(\mathbf{r}, t) d\mathbf{r} = \sum_{j=1}^{N} e^{-i\mathbf{k} \cdot \mathbf{r}_j(t)}
$$
The wavevector $\mathbf{k}$ acts as a probe. The density mode $\hat{\rho}(\mathbf{k}, t)$ measures the collective structural arrangement of particles on a [characteristic length](@entry_id:265857) scale of $2\pi/|\mathbf{k}|$. In computer simulations employing [periodic boundary conditions](@entry_id:147809) in a cubic box of side length $L$, the allowed wavevectors form a [discrete set](@entry_id:146023), $\mathbf{k} = \frac{2\pi}{L}(n_x, n_y, n_z)$, where $n_x, n_y, n_z$ are integers.

#### The Coherent Intermediate Scattering Function $F(\mathbf{k}, t)$

Dynamics are concerned with how these structural arrangements evolve. The primary tool for this is the [time correlation function](@entry_id:149211) of the density modes. The **coherent [intermediate scattering function](@entry_id:159928) (ISF)**, denoted $F(\mathbf{k}, t)$, is defined as the ensemble-averaged time [autocorrelation](@entry_id:138991) of a density fluctuation:
$$
F(\mathbf{k}, t) = \frac{1}{N} \langle \hat{\rho}(\mathbf{k}, t) \hat{\rho}(-\mathbf{k}, 0) \rangle = \frac{1}{N} \left\langle \sum_{j=1}^{N} \sum_{l=1}^{N} e^{-i\mathbf{k} \cdot \mathbf{r}_j(t)} e^{i\mathbf{k} \cdot \mathbf{r}_l(0)} \right\rangle
$$
The angle brackets $\langle \cdot \rangle$ denote an average over an appropriate [statistical ensemble](@entry_id:145292) (e.g., the canonical ensemble). Since particle positions $\mathbf{r}_j$ are real, it follows that $\hat{\rho}(-\mathbf{k}, t) = \hat{\rho}(\mathbf{k}, t)^*$, where the asterisk denotes [complex conjugation](@entry_id:174690). Thus, the definition can also be written as $F(\mathbf{k}, t) = \frac{1}{N} \langle \hat{\rho}(\mathbf{k}, t) \hat{\rho}(\mathbf{k}, 0)^* \rangle$. This function is directly related to the quantity measured in inelastic neutron and X-ray scattering experiments, making it a crucial link between simulation, theory, and experiment.

The value of the coherent ISF at time $t=0$ gives the **[static structure factor](@entry_id:141682)**, $S(\mathbf{k})$:
$$
S(\mathbf{k}) = F(\mathbf{k}, 0) = \frac{1}{N} \langle |\hat{\rho}(\mathbf{k}, 0)|^2 \rangle
$$
$S(\mathbf{k})$ quantifies the intensity of static [density correlations](@entry_id:157860) at wavevector $\mathbf{k}$. It is common to work with the **normalized coherent ISF**, $\Phi(\mathbf{k},t) = F(\mathbf{k}, t) / S(\mathbf{k})$, which is unity at $t=0$ and describes the subsequent decay of correlations.

#### The Self Intermediate Scattering Function $F_s(\mathbf{k}, t)$

The coherent function $F(\mathbf{k}, t)$ contains correlations between all pairs of particles. It is often useful to isolate the motion of individual particles. This is achieved by the **self [intermediate scattering function](@entry_id:159928)**, $F_s(\mathbf{k}, t)$, which correlates the position of a particle only with its own position at a later time. It is defined by restricting the double summation in the definition of $F(\mathbf{k}, t)$ to terms where $j=l$:
$$
F_s(\mathbf{k}, t) = \frac{1}{N} \left\langle \sum_{j=1}^{N} e^{-i\mathbf{k} \cdot [\mathbf{r}_j(t) - \mathbf{r}_j(0)]} \right\rangle
$$
This function describes how, on average, a single particle's "memory" of its initial position decays over time, as probed on the length scale $2\pi/|\mathbf{k}|$. It is the spatial Fourier transform of the **van Hove self-correlation function** $G_s(\mathbf{r}, t)$, which gives the probability distribution for a particle to have a displacement $\mathbf{r}$ in a time $t$.

#### Self, Distinct, and Coherent Functions

The full coherent ISF can be formally decomposed into contributions from self-correlations ($j=l$) and correlations between distinct particles ($j \neq l$). This leads to the fundamental relation:
$$
F(\mathbf{k}, t) = F_s(\mathbf{k}, t) + F_d(\mathbf{k}, t)
$$
Here, $F_d(\mathbf{k}, t)$ is the **distinct [intermediate scattering function](@entry_id:159928)**, defined as:
$$
F_d(\mathbf{k}, t) = \frac{1}{N} \left\langle \sum_{j \neq l} e^{-i\mathbf{k} \cdot \mathbf{r}_j(t)} e^{i\mathbf{k} \cdot \mathbf{r}_l(0)} \right\rangle
$$
This decomposition is powerful. $F_s(\mathbf{k}, t)$ tracks single-particle motion, such as diffusion, while $F_d(\mathbf{k}, t)$ captures how the motion of one particle is correlated with its neighbors. Collective phenomena, like sound waves, are inherently encoded in the cross-correlations contained within $F_d(\mathbf{k}, t)$.

#### Practical Computation from Trajectories

In [molecular dynamics](@entry_id:147283), these scattering functions are not abstract concepts but are computed directly from the simulated particle trajectories $\{\mathbf{r}_j(t)\}$. For a pair of configurations at times $t=0$ and $t=\Delta t$, the ensemble average $\langle \cdot \rangle$ is replaced by a simple average over the particles in the system.

For the **self-ISF**, the expression becomes an average over all $N$ particles:
$$
F_s(\mathbf{k}, \Delta t) \approx \frac{1}{N} \sum_{j=1}^{N} e^{-i\mathbf{k} \cdot [\mathbf{r}_j(\Delta t) - \mathbf{r}_j(0)]}
$$
A critical detail in simulations with [periodic boundary conditions](@entry_id:147809) (PBC) is the calculation of the displacement vector $\Delta\mathbf{r}_j = \mathbf{r}_j(\Delta t) - \mathbf{r}_j(0)$. A particle may cross a boundary, leading to a large, unphysical displacement in the raw coordinates. To compute the true physical displacement, one must apply the **[minimum image convention](@entry_id:142070) (MIC)** to $\Delta\mathbf{r}_j$. This ensures that the measured displacement is the shortest possible vector connecting the initial and final positions in the periodically tiled space. Failing to apply the MIC can lead to significant errors in the computed value of $F_s(\mathbf{k}, t)$.

For the **coherent ISF**, we compute the ratio of density modes at the two times. From a single trajectory, the normalized function is estimated as:
$$
\frac{F(\mathbf{k}, \Delta t)}{S(\mathbf{k})} \approx \frac{\hat{\rho}(\mathbf{k}, \Delta t) \hat{\rho}(\mathbf{k}, 0)^*}{|\hat{\rho}(\mathbf{k}, 0)|^2} = \frac{\hat{\rho}(\mathbf{k}, \Delta t)}{\hat{\rho}(\mathbf{k}, 0)}
$$
This direct computation from particle coordinates provides the bridge from microscopic simulation data to experimentally relevant observables.

### Short-Time Dynamics: Ballistic Motion and Initial Decay

The behavior of [correlation functions](@entry_id:146839) at very short times is universal for all classical systems in thermal equilibrium. It is governed not by the complexities of particle interactions but by the fundamental properties of inertia and temperature. For systems described by Hamiltonians that are even under time-reversal (such as Newtonian dynamics without magnetic fields), both $F(\mathbf{k}, t)$ and $F_s(\mathbf{k}, t)$ are [even functions](@entry_id:163605) of time, $F(\mathbf{k}, t) = F(\mathbf{k}, -t)$. Consequently, their Taylor series expansions around $t=0$ contain only even powers of $t$:
$$
F(k,t) = F(k,0) + \frac{1}{2} \ddot{F}(k,0) t^2 + \frac{1}{24} F^{(4)}(k,0) t^4 + \mathcal{O}(t^6)
$$
where the dots denote time derivatives. The odd derivatives at $t=0$ are zero. The second-order term, $\ddot{F}(k,0)$, captures the initial decay of correlations and is determined by the Maxwell-Boltzmann distribution of particle velocities.

#### Short-Time Behavior of the Self-ISF

Let us examine the initial decay of $F_s(k,t)$. Differentiating its definition twice with respect to time and evaluating at $t=0$ yields a general result related to the mean-square velocity:
$$
\ddot{F}_s(k,0) = -\frac{1}{N} \left\langle \sum_{j=1}^{N} (\mathbf{k} \cdot \mathbf{v}_j(0))^2 \right\rangle
$$
In an isotropic system, the average of $(\mathbf{k} \cdot \mathbf{v}_j)^2$ is $\frac{1}{3} k^2 \langle v_j^2 \rangle$. The equipartition theorem states that $\frac{1}{2}m \langle v_j^2 \rangle = \frac{3}{2} k_B T$, so $\langle v_j^2 \rangle = 3k_B T / m$. Combining these gives a universal result:
$$
\ddot{F}_s(k,0) = -\frac{k^2 k_B T}{m}
$$
Therefore, for any classical fluid at short times, the self-ISF decays quadratically as:
$$
F_s(k,t) \approx 1 - \frac{k^2 k_B T}{2m} t^2
$$
This describes the "ballistic" regime, where particles move freely according to their initial thermal velocities before experiencing significant interactions with their neighbors.

#### An Exactly Solvable Model: The Harmonic Oscillator

While the $t^2$ term is universal, higher-order terms in the expansion depend on the forces, i.e., the [potential energy landscape](@entry_id:143655). This can be seen clearly in an exactly solvable model, such as a single particle in a three-dimensional isotropic [harmonic potential](@entry_id:169618), $U(\mathbf{r}) = \frac{1}{2} m \omega^2 \mathbf{r}^2$. The particle's motion is deterministic and oscillatory. By solving the equation of motion and averaging over canonical [initial conditions](@entry_id:152863), one can derive the exact self-ISF:
$$
F_s(k,t) = \exp\left(-\frac{k^2 k_B T}{m\omega^2} (1 - \cos(\omega t))\right)
$$
Expanding this expression for small $t$ gives:
$$
F_s(k,t) = 1 - \frac{k^2 k_B T}{2m}t^2 + \left(\frac{k^2 k_B T\omega^2}{24m} + \frac{k^4 (k_B T)^2}{8m^2}\right)t^4 + \mathcal{O}(t^6)
$$
As expected, the $t^2$ coefficient matches the universal result. The $t^4$ coefficient, however, contains terms involving the potential (through $\omega^2$) and higher powers of $k$. This demonstrates the general principle that the sequence of time derivatives of $F_s(k,t)$ at $t=0$, known as frequency moments, probe progressively finer details of the dynamics: the second moment probes thermal velocities, the fourth moment probes forces, and so on.

#### Short-Time Behavior of the Coherent-ISF: De Gennes Narrowing

A similar analysis for the coherent function $F(k,t)$ reveals a remarkable connection between [statics](@entry_id:165270) and dynamics. A careful derivation shows that the second moment of the coherent function is identical to that of the self function:
$$
\ddot{F}(k,0) = - \frac{k^2 k_B T}{m}
$$
However, the initial decay of the *normalized* function $\Phi(k,t) = F(k,t)/S(k)$ is what matters. Its second derivative is:
$$
\ddot{\Phi}(k,0) = \frac{\ddot{F}(k,0)}{S(k)} = -\frac{k^2 k_B T}{m S(k)}
$$
This leads to a characteristic frequency $\omega_k$ defined by the [short-time expansion](@entry_id:180364) $F(k,t) = S(k)(1 - \frac{1}{2}\omega_k^2 t^2 + \dots)$. The result is:
$$
\omega_k^2 = - \ddot{\Phi}(k,0) = \frac{k^2 k_B T}{m S(k)}
$$
This is the celebrated **de Gennes narrowing** relation. It states that the initial rate of decay of collective [density fluctuations](@entry_id:143540) is *inversely* proportional to the [static structure factor](@entry_id:141682) $S(k)$. At wavevectors corresponding to peaks in $S(k)$ (e.g., the first sharp diffraction peak in a liquid, which reflects the typical nearest-neighbor distance), the static structure is highly correlated. The de Gennes relation tells us that these highly ordered structures are dynamically slow to relax. This is a profound insight: static correlations impose kinetic constraints on the system's dynamics.

### Long-Time Dynamics and Deviations from Simple Behavior

Beyond the initial ballistic regime, particle interactions become dominant, leading to more complex and system-dependent dynamics.

#### The Gaussian Approximation for the Self-ISF

A powerful and widely used approximation connects the self-ISF to another key dynamical quantity: the **[mean-squared displacement](@entry_id:159665) (MSD)**, $\langle \Delta r^2(t) \rangle = \langle |\mathbf{r}_j(t) - \mathbf{r}_j(0)|^2 \rangle$. If we assume that over a time $t$, the particle displacement vector $\Delta \mathbf{r}(t)$ is a random variable drawn from a three-dimensional Gaussian distribution with [zero mean](@entry_id:271600), then $F_s(k,t)$ takes a simple exponential form. This assumption leads to the **Gaussian approximation**:
$$
F_s(k,t) \approx \exp\left(-\frac{k^2 \langle \Delta r^2(t) \rangle}{6}\right)
$$
This relation can be derived from first principles under the assumption of isotropic Gaussian statistics for the displacement vector. This approximation is exact for a [free particle](@entry_id:167619) undergoing Brownian motion and holds generally in the limits of small $k$ or short times $t$. It provides an intuitive link: the faster the MSD grows, the more rapidly the self-ISF decays.

#### Probing Collective Modes: Sound Waves

While the self-ISF tracks individual particle motion, the coherent ISF, $F(k,t)$, reveals collective dynamics. In the long-wavelength (small $k$) limit, [density fluctuations](@entry_id:143540) in a fluid do not simply decay; they propagate as sound waves. This propagating nature should manifest as oscillations in the time-dependence of $F(k,t)$. For a sound mode with [dispersion relation](@entry_id:138513) $\omega(k) \approx c_s k$, where $c_s$ is the sound speed, the correlation function is expected to oscillate with a frequency close to $\omega(k)$.

A computational experiment can make this connection explicit. By simulating a system where a propagating [density wave](@entry_id:199750) is superimposed on random thermal motion, one can compute $F(k,t)$ from the particle trajectories. The temporal Fourier transform of the resulting $F(k,t)$ will exhibit a peak at a non-zero frequency $\omega_{\text{peak}}$. This peak corresponds to the sound mode, and its frequency allows for the estimation of an effective sound speed $c_{\text{eff}} = \omega_{\text{peak}}/k$. This demonstrates how macroscopic hydrodynamic behavior emerges from the underlying microscopic correlations captured by the ISF.

#### Dynamics in Liquids vs. Glasses

The long-time limit of the ISF provides a fundamental dynamic distinction between a liquid and a glass.
In an **ergodic liquid**, particles are free to explore the entire phase space over long times. Any initial structural configuration eventually decorrelates completely. As a result, for any $k \neq 0$:
$$
\lim_{t \to \infty} F(k,t) = 0 \quad \text{and} \quad \lim_{t \to \infty} F_s(k,t) = 0
$$
In contrast, a **structural glass** is a non-ergodic state where particles are kinetically arrested. They become trapped in "cages" formed by their neighbors for times exceeding typical experimental or simulation timescales. While particles vibrate within these cages, they do not diffuse freely. Consequently, the memory of the initial positions never fully decays. This is captured by a non-zero long-time limit of the self-ISF:
$$
\lim_{t \to \infty} F_s(k,t) = f_k > 0
$$
The quantity $f_k$ is known as the **[non-ergodicity parameter](@entry_id:161461)** or the **Debye-Waller factor**. It represents the height of the plateau in $F_s(k,t)$ and serves as an order parameter for the [glass transition](@entry_id:142461), being zero in the liquid phase and non-zero in the glass phase.

### The Rich Dynamics of Supercooled Liquids and Glasses

The transition from a simple liquid to an arrested glass is not abrupt but occurs over a vast range of temperatures in a regime known as the supercooled liquid state. Here, the dynamics become extraordinarily complex and are characterized by several key phenomena.

#### Two-Step Relaxation and Caging

Upon cooling a liquid below its [melting point](@entry_id:176987), the decay of the self-ISF, $F_s(k,t)$, develops a characteristic **[two-step relaxation](@entry_id:756266)** profile, particularly for wavevectors near the main peak of $S(k)$. This can be understood through the **[caging effect](@entry_id:159704)**.
- At very short times, particles exhibit ballistic motion, leading to an initial fast decay of $F_s(k,t)$.
- At intermediate times, a particle becomes trapped in a cage formed by its neighbors. Its motion is confined, leading to a temporary slowing down of relaxation and the formation of a **plateau** in $F_s(k,t)$. The dynamics associated with this rattling motion inside the cage is termed **$\beta$-relaxation**.
- At much longer times, the cage structure itself rearranges, allowing the particle to escape and diffuse. This final, slow decay of the ISF from the plateau to zero is called **$\alpha$-relaxation**. The timescale of this process, $\tau_{\alpha}$, is the [structural relaxation](@entry_id:263707) time, which grows dramatically upon cooling.

This entire process can be modeled phenomenologically by constructing an MSD, $\langle \Delta r^2(t) \rangle$, that incorporates these three regimes (ballistic, caged, and diffusive) and then using the Gaussian approximation to compute the corresponding $F_s(k,t)$. From such a model, one can precisely define and extract the plateau height $f_k^{(\beta)}$, the $\beta$-relaxation time, and the $\alpha$-relaxation time, providing a quantitative framework for analyzing [two-step relaxation](@entry_id:756266).

#### Non-Gaussian Dynamics and Dynamical Heterogeneity

In simple liquids, the Gaussian approximation for $F_s(k,t)$ works reasonably well. However, in supercooled liquids, it often fails spectacularly, especially at intermediate times corresponding to the end of the $\beta$-relaxation plateau. This failure is not a mere technicality; it is a profound signature of **dynamical heterogeneity**. This term refers to the emergence of spatial regions with vastly different local dynamics: some regions consist of "fast" or mobile particles, while others consist of "slow" or immobile particles, even though the system is structurally homogeneous on average.

The distribution of particle displacements, $G_s(r,t)$, is no longer a simple Gaussian. Instead, it often develops an exponential tail, indicating a higher-than-expected probability of large displacements coming from the minority of mobile particles. The primary tool for quantifying this deviation is the **non-Gaussian parameter**, $\alpha_2(t)$, defined in three dimensions as:
$$
\alpha_2(t) = \frac{3 \langle \Delta r^4(t) \rangle}{5 \langle \Delta r^2(t) \rangle^2} - 1
$$
This parameter is constructed such that $\alpha_2(t) = 0$ for a perfectly Gaussian displacement distribution. A positive value indicates a "fat-tailed" distribution consistent with dynamical heterogeneity. In supercooled liquids, $\alpha_2(t)$ is typically small at very short and very long times but exhibits a prominent peak at an intermediate timescale, $t \approx \tau_{\alpha}$, signaling the moment of maximum heterogeneity. A simple yet powerful model for understanding the origin of non-Gaussianity is to consider a mixture of two populations of particles diffusing at different rates, which naturally leads to a non-zero $\alpha_2(t)$.

#### Correcting for Non-Gaussianity: Expansions of the ISF

To develop a more accurate theoretical description of the ISF beyond the Gaussian approximation, one can employ systematic expansions that incorporate [higher-order moments](@entry_id:266936) of the displacement.

One approach is a direct Taylor [series expansion](@entry_id:142878) of $F_s(k,t)$ in powers of the wavevector $k$. Truncating at the fourth order yields:
$$
F_s(k,t) \approx 1 - \frac{k^2}{6} \langle \Delta r^2(t) \rangle + \frac{k^4}{120} \langle \Delta r^4(t) \rangle
$$
This expansion correctly captures the initial deviation from Gaussian behavior at small $k$, as it involves the fourth moment of the displacement, $\langle \Delta r^4(t) \rangle$.

A more powerful and often more rapidly converging approach is the **[cumulant expansion](@entry_id:141980)** of the logarithm of the ISF. To fourth order in $q$, this gives:
$$
\ln F_s(k,t) \approx -\frac{k^2}{6} \langle \Delta r^2(t) \rangle + \frac{k^4}{120} \langle \Delta r^4(t) \rangle_c
$$
The coefficient of the $k^4$ term involves the **connected fourth-order radial moment**, $\langle \Delta r^4(t) \rangle_c = \langle \Delta r^4(t) \rangle - \frac{5}{3} \langle \Delta r^2(t) \rangle^2$, which is directly related to the non-Gaussian parameter $\alpha_2(t)$. This expansion effectively resums parts of the direct Taylor series into an exponential form, providing a better approximation at larger values of $k$. Comparing these improved approximations to exact results in simple models of heterogeneity demonstrates that including the fourth-order correction can significantly improve accuracy, especially when $\alpha_2(t)$ is large.

#### Probing Spatially Correlated Dynamics: Four-Point Functions

The non-Gaussian parameter $\alpha_2(t)$ quantifies the breadth of the mobility distribution but does not, by itself, reveal the spatial organization of the fast and slow particles. To probe these spatial correlations, one must turn to higher-order, **four-point correlation functions**.

The key quantities are the **four-point dynamical susceptibility**, $\chi_4(t)$, and the **four-point spatial correlation function**, $G_4(r,t)$. Conceptually, $\chi_4(t)$ measures the volume of dynamically correlated particles, while $G_4(r,t)$ describes how the mobility at one point in space is correlated with mobility at a distance $r$. The integral of $G_4(r,t)$ over all space yields $\chi_4(t)$.

A central finding in the study of glasses is that $\chi_4(t)$ exhibits a peak at a time $t^{\star}$ that closely tracks the [structural relaxation](@entry_id:263707) time $\tau_{\alpha}$. The height of this peak, $\chi_4^{\text{peak}}$, grows as the liquid is cooled, indicating an increasing number of particles moving cooperatively. The decay of the spatial function $G_4(r, t^{\star})$ defines a **[dynamic correlation](@entry_id:195235) length**, $\xi(t^{\star})$. The peak susceptibility is proportional to the volume of these correlated regions, $\chi_4^{\text{peak}} \sim \xi^3$. This explains a crucial finite-size effect: in simulations, $\chi_4^{\text{peak}}$ will grow with the system size $L$ as long as $L  \xi$, but will saturate to a constant value once the simulation box becomes large enough to contain the entire correlated domain, i.e., when $L \gg \xi$. These four-point observables provide the most direct evidence for the existence of growing domains of correlated motion that underlie the dramatic slowing down of dynamics in supercooled liquids.