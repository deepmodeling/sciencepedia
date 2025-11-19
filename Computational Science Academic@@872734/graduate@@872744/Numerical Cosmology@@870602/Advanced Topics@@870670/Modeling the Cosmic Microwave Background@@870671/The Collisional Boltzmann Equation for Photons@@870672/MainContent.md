## Introduction
The collisional Boltzmann equation is the cornerstone of theoretical and [numerical cosmology](@entry_id:752779), providing the essential link between the microphysics of particle interactions in the early universe and the large-scale structures we observe today, most notably the anisotropies in the Cosmic Microwave Background (CMB). Understanding how photons propagate and scatter in the [primordial plasma](@entry_id:161751) is fundamental to deciphering the information encoded in the CMB about the universe's initial conditions, composition, and evolution. This article aims to bridge the gap between abstract theory and practical application, detailing how the Boltzmann equation governs the generation and evolution of the [photon distribution function](@entry_id:753416).

This article will guide you through this fundamental framework in three parts. The first chapter, **Principles and Mechanisms**, will dissect the Boltzmann equation itself, exploring the physics of Thomson scattering, the concepts of [optical depth](@entry_id:159017) and the [visibility function](@entry_id:756540), and the mechanisms that generate temperature and polarization anisotropies. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how this theory is put into practice, from the [line-of-sight integral](@entry_id:751289) used in modern computational codes to the deep connections with numerical analysis and [atomic physics](@entry_id:140823). Finally, the **Hands-On Practices** section will provide practical exercises to build an intuitive and computational understanding of these concepts.

## Principles and Mechanisms

The evolution of photon distribution in the cosmos is governed by the interplay between free propagation through an [expanding spacetime](@entry_id:161389) and interactions with matter. The primary interaction mechanism for [cosmic microwave background](@entry_id:146514) (CMB) photons after the era of [electron-positron annihilation](@entry_id:161028) is Compton scattering with free electrons. In the context of the early universe, this process is almost universally approximated as Thomson scattering. This chapter delineates the fundamental principles and mechanisms underpinning the collisional Boltzmann equation for photons in this regime, establishing the theoretical foundation for computing the anisotropies observed in the CMB.

### The Thomson Scattering Regime: Domain of Validity

The Thomson approximation simplifies the more general Compton scattering by assuming that the scattering process is elastic in the rest frame of the electron. This simplification is not universally valid and rests on a set of conditions related to the [energy scales](@entry_id:196201) of the interacting particles. Before delving into the details of the [collision operator](@entry_id:189499), it is crucial to establish the domain of validity for this approximation. We can quantify this domain using a set of [dimensionless parameters](@entry_id:180651) derived from fundamental physical principles [@problem_id:3493998].

First, for the scattering to be nearly elastic, the photon must transfer a negligible fraction of its energy to the electron. This occurs when the photon's momentum is much smaller than the characteristic momentum of the electron, which is on the order of $m_e c$. This implies that the photon's energy, $E_\gamma = h\nu$, must be much smaller than the electron's rest energy, $m_e c^2$. We can define a dimensionless metric for this condition:
$$
M_{\gamma} = \frac{h\nu}{m_e c^2} \ll 1
$$
For a typical CMB photon today, with $\nu \approx 160\,\text{GHz}$, and $m_e c^2 \approx 511\,\text{keV}$, this ratio is of order $10^{-6}$, satisfying the condition comfortably. However, for [high-energy astrophysics](@entry_id:159925) involving X-ray or gamma-ray photons, this approximation fails, and the full quantum-mechanical Compton scattering formalism, including electron recoil, is necessary [@problem_id:3493998].

Second, the electrons themselves are assumed to be non-relativistic. This has two components: their thermal motion and their collective bulk motion. The characteristic thermal kinetic energy of an electron in a plasma at temperature $T_e$ is of order $k_B T_e$. For the electrons to be non-relativistic, this energy must be much smaller than their rest energy. This gives us a second metric:
$$
M_{T} = \frac{k_B T_e}{m_e c^2} \ll 1
$$
For example, in a hot galaxy cluster with $T_e \approx 10^8\,\text{K}$ ($k_B T_e \approx 8.6\,\text{keV}$), this ratio is about $0.017$. While small, it is not negligible, and energy exchange in this "trans-relativistic" regime can become important. Additionally, the bulk velocity of the [baryon-photon fluid](@entry_id:159479), $v_b$, must be small compared to the speed of light, $v_b \ll c$. This is generally true for the linear perturbations considered in cosmology [@problem_id:3493998].

Finally, while the energy exchange per scattering may be small, the cumulative effect over many scatterings can be significant. The mean fractional energy change per collision is proportional to $M_T$. The total effect can be estimated by the **Comptonization parameter**, $y$, which is the product of the total optical depth (a proxy for the number of scatterings) and the fractional energy exchange per scattering.
$$
y \approx \tau \left( \frac{k_B T_e}{m_e c^2} \right)
$$
For the spectrum of the CMB to remain nearly a perfect blackbody, this parameter must be small, $y \ll 1$. When this condition is violated, such as for photons passing through the hot gas in galaxy clusters, the resulting spectral distortion is known as the thermal Sunyaev-Zel'dovich effect [@problem_id:3493998] [@problem_id:3494013].

Throughout most of this chapter, we will operate within the Thomson limit where these conditions hold, allowing for significant simplification of the [collision operator](@entry_id:189499).

### The Collisional Boltzmann Equation

The evolution of the [photon distribution function](@entry_id:753416) in phase space, $f(x^\mu, p^\mu)$, is described by the Boltzmann equation, which can be written schematically as:
$$
\frac{df}{d\eta} = C[f]
$$
Here, $\eta$ is [conformal time](@entry_id:263727), the [total derivative](@entry_id:137587) on the left-hand side is the Liouville operator representing the free streaming of photons in a perturbed spacetime, and $C[f]$ is the [collision operator](@entry_id:189499) representing interactions.

The Thomson [collision operator](@entry_id:189499) is most simply expressed in the instantaneous rest frame of the scattering electron. However, since the electron fluid moves with a bulk velocity $\mathbf{v}_b$ with respect to the cosmological rest frame, a Lorentz transformation is required. To first order in perturbations, the photon temperature anisotropy seen in the electron frame, $\Theta^{(e)}$, is related to the anisotropy in the cosmological frame, $\Theta$, by a simple Doppler shift [@problem_id:3493988]:
$$
\Theta^{(e)}(\hat{\mathbf{n}}) = \Theta(\hat{\mathbf{n}}) - \hat{\mathbf{n}} \cdot \mathbf{v}_b
$$
This relation follows directly from the Lorentz invariance of the [distribution function](@entry_id:145626) $f$ and the transformation of photon energy between frames. This term is the source of the "Doppler effect" in CMB anisotropies.

In the electron rest frame, the [collision operator](@entry_id:189499) takes the form of a gain term and a loss term:
$$
C[f_e] = n_e \sigma_T c \left[ -f_e(\hat{\mathbf{n}}_e) + \int_{\Omega'} \frac{d\sigma}{d\Omega'} \frac{1}{ \sigma_T } f_e(\hat{\mathbf{n}}'_e) d\Omega' \right]
$$
Here, $n_e$ is the electron [number density](@entry_id:268986), $\sigma_T$ is the total Thomson [cross section](@entry_id:143872), and $d\sigma/d\Omega'$ is the [differential cross section](@entry_id:159876). The term $a n_e \sigma_T c$ is often written as $\dot{\tau}$, the differential optical depth per unit [conformal time](@entry_id:263727). The first term describes the loss of photons from the beam direction $\hat{\mathbf{n}}_e$ due to scattering, while the integral term describes the gain of photons into the beam from scattering events originating from all other directions $\hat{\mathbf{n}}'_e$.

A fundamental property of this operator is **detailed balance**. If the photon distribution is isotropic, $f_e(\hat{\mathbf{n}}'_e) = f_{iso}$, the gain term simplifies. The integral of the normalized [differential cross section](@entry_id:159876) over all angles is unity, so the gain term becomes $f_{iso}$. The operator then vanishes: $C[f_{iso}] = \dot{\tau}(-f_{iso} + f_{iso}) = 0$. This signifies that collisions do not alter a distribution that is already in [local thermal equilibrium](@entry_id:147993) [@problem_id:3493989].

For a distribution that is not isotropic, the [collision operator](@entry_id:189499) acts to reduce anisotropies. This can be seen clearly through the **[relaxation-time approximation](@entry_id:138429)**, a simplified model of the collision term often used for pedagogical purposes. In this model, the operator is written as:
$$
C[f] = -\dot{\tau} (f - \langle f \rangle_{\hat{n}})
$$
where $\langle f \rangle_{\hat{n}}$ is the angular average of the [distribution function](@entry_id:145626) (the monopole). This form makes it clear that the scattering rate $\dot{\tau}$ drives any anisotropic component of the distribution, $(f - \langle f \rangle_{\hat{n}})$, towards zero. For instance, consider a simple dipole anisotropy in a homogeneous universe, $f(\eta) = f^{(0)}(1 + \Psi(\eta)\mu)$. The Boltzmann equation in this context becomes $\frac{\partial f}{\partial \eta} = C[f]$. Applying the relaxation-time operator yields a simple differential equation for the dipole amplitude $\Psi(\eta)$:
$$
\frac{d\Psi}{d\eta} = -\dot{\tau}(\eta) \Psi(\eta)
$$
The solution, $\Psi(\eta) = \Psi_i \exp(-\int_{\eta_i}^\eta \dot{\tau}(\eta') d\eta')$, demonstrates that collisions exponentially damp anisotropies. The integral in the exponent is the [optical depth](@entry_id:159017) [@problem_id:3494026].

### Optical Depth and the Visibility Function

The damping of anisotropies by scattering naturally leads to the concepts of [optical depth](@entry_id:159017) and the [visibility function](@entry_id:756540), which are central to understanding when and where the CMB anisotropies were imprinted.

The **optical depth**, $\tau(\eta)$, is defined as the integral of the scattering rate from a given [conformal time](@entry_id:263727) $\eta$ to the present time $\eta_0$:
$$
\tau(\eta) \equiv \int_{\eta}^{\eta_0} \dot{\tau}(\eta') d\eta'
$$
From a probabilistic standpoint, $\tau(\eta)$ represents the expected number of scattering events a photon will undergo between time $\eta$ and today. The probability that a photon travels unimpeded from $\eta$ to $\eta_0$ is given by $P_{\text{no-scatter}} = \exp(-\tau(\eta))$, a direct consequence of the Poisson statistics of the scattering process [@problem_id:3494009].

This allows us to define the **[visibility function](@entry_id:756540)**, $g(\eta)$. It represents the probability density that a photon observed today had its last scattering event in the [conformal time](@entry_id:263727) interval $[\eta, \eta+d\eta]$. This is the product of two probabilities: the probability of scattering in the interval $d\eta$, which is $\dot{\tau}(\eta) d\eta$, and the probability of subsequently [free-streaming](@entry_id:159506) to the present, $\exp(-\tau(\eta))$. Therefore:
$$
g(\eta) = \dot{\tau}(\eta) \exp(-\tau(\eta))
$$
Notice that $g(\eta) = -\frac{d}{d\eta}\exp(-\tau(\eta))$. The [visibility function](@entry_id:756540) is sharply peaked around the [epoch of recombination](@entry_id:158245) ($\eta \approx 280$ Mpc), when the universe transitioned from being an opaque plasma to a transparent gas. This peak defines the "[surface of last scattering](@entry_id:266191)." The time at which the [visibility function](@entry_id:756540) peaks can be found by setting its derivative to zero, which yields the condition $\ddot{\tau}(\eta_{peak}) = (\dot{\tau}(\eta_{peak}))^2$. For a specific model of $\dot{\tau}(\eta)$, this equation can be solved to find the precise moment of last scattering [@problem_id:3494009].

### Anisotropy Generation: Intensity and Polarization

While collisions damp anisotropies, they are also essential for generating them. Anisotropies are created when photons, attempting to free-stream, are coupled back to the local properties of the [baryon-photon fluid](@entry_id:159479) via scattering.

#### Parity and the Intensity Hierarchy

The Thomson scattering process has a distinct angular structure. The [differential cross section](@entry_id:159876) for unpolarized light is proportional to $(1+\cos^2\theta_s)$, where $\theta_s$ is the scattering angle. This angular dependence has a profound consequence for the evolution of intensity anisotropies when expanded in Legendre polynomials, $\Theta(\mu) = \sum_\ell \Theta_\ell P_\ell(\mu)$.

The [collision operator](@entry_id:189499) for the $\ell$-th multipole, $\Theta_\ell$, involves an integral over the scattering kernel and the full [angular distribution](@entry_id:193827). After averaging over the azimuthal angle in an axisymmetric system, the effective scattering kernel becomes an even function of both the incoming and outgoing [direction cosines](@entry_id:170591), $\mu$ and $\mu'$. When this even kernel is integrated against an odd Legendre polynomial $P_\ell(\mu)$ (for odd $\ell$), the result is zero. This implies that the scattering-in (source) term for all odd multipoles of the intensity anisotropy is zero [@problem_id:3493970].
$$
C_\ell[\Theta] = -\dot{\tau}(\eta) \Theta_\ell(\eta) \quad \text{for } \ell=1, 3, 5, \dots
$$
Odd multipoles, such as the dipole ($\ell=1$), are therefore only damped by Thomson scattering. They are not regenerated by scattering from other multipoles. In contrast, even multipoles do have a source term from scattering, primarily from the monopole $\Theta_0$. This [parity selection rule](@entry_id:155458) leads to a [decoupling](@entry_id:160890) of the odd and even multipoles in the Boltzmann hierarchy, a crucial feature for both analytical understanding and numerical solution.

#### The Generation of Linear Polarization

Thomson scattering can generate linear polarization if the incident [radiation field](@entry_id:164265) is anisotropic. An isotropic bath of photons will produce no net polarization upon scattering. A dipole anisotropy, which has a hot pole and a cold pole, also produces no net polarization due to the front-back symmetry of the scattering process. The lowest-order anisotropy that can source [linear polarization](@entry_id:273116) is a **quadrupole** ($\ell=2$) [@problem_id:3494036]. Imagine an electron seeing hotter radiation from above and below, and cooler radiation from the sides. When it scatters photons towards an observer, the scattered light will have a net linear polarization.

The state of [linear polarization](@entry_id:273116) is described by the Stokes parameters $Q$ and $U$. These can be decomposed into parity-even **E-modes** and parity-odd **B-modes**. Scalar perturbations, such as density fluctuations in the early universe, are themselves parity-even. The Thomson scattering process is governed by electromagnetism, which conserves parity. Therefore, a parity-even source ([scalar perturbations](@entry_id:160338)) acting through a parity-conserving interaction (Thomson scattering) can only generate parity-even outcomes. This means that [scalar perturbations](@entry_id:160338) can only source **E-modes** of polarization. B-modes are not generated by this mechanism and, like odd intensity multipoles, are only damped by scattering [@problem_id:3494036] [@problem_id:3493970].

This physics is encapsulated in the [evolution equations](@entry_id:268137) for the lowest E- and B-mode multipoles, which take the simplified form:
$$
\frac{dE}{d\eta} = -\dot{\tau}(\eta) E(\eta) + \dot{\tau}(\eta) S_P(\eta)
$$
$$
\frac{dB}{d\eta} = -\dot{\tau}(\eta) B(\eta)
$$
where the polarization source term $S_P(\eta)$ is proportional to the local temperature quadrupole, $\Theta_2(\eta)$. This system shows that E-modes are sourced by the quadrupole and damped by scattering, while B-modes are purely damped. The detection of a primordial B-mode signal would therefore be strong evidence for a different, parity-odd source, such as [primordial gravitational waves](@entry_id:161080) ([tensor perturbations](@entry_id:160430)).

### The Line-of-Sight Integral: A Formal Solution

The principles discussed thus far—free streaming, collisional sources, and the [visibility function](@entry_id:756540)—can be synthesized into a single formal solution for the observed CMB anisotropies. The Boltzmann equation for the temperature perturbation $\Theta(\mathbf{k}, \mu, \eta)$ can be written as a first-order ordinary differential equation along the line of sight:
$$
\frac{d\Theta}{d\eta} + i k \mu \Theta = -\dot{\tau}\Theta + \dot{\tau} S_{tot}
$$
where $S_{tot} = \Theta_0 - \mu v_b + \dots$ includes all source terms. This equation can be formally solved using an integrating factor, yielding the **[line-of-sight integral](@entry_id:751289)** solution for the anisotropy observed today ($\eta_0$) [@problem_id:3493980]:
$$
\Theta(\mathbf{k}, \mu, \eta_0) = \int_0^{\eta_0} S(k, \eta) e^{ik\mu(\eta - \eta_0)} d\eta
$$
Here, the total [source function](@entry_id:161358) $S(k,\eta) = g(\eta)S_{tot}(k,\eta)$ combines the physical sources (like the temperature monopole and Doppler term) with the [visibility function](@entry_id:756540) $g(\eta)$, which ensures that only sources near the [surface of last scattering](@entry_id:266191) contribute significantly. The term $e^{ik\mu(\eta - \eta_0)}$ is a geometric projection factor that accounts for the free streaming of photons from the source location at time $\eta$ to the observer today.

To connect this to observations, we decompose the solution into spherical multipoles $\Theta_\ell(k)$. This is achieved by projecting the solution onto Legendre polynomials, which transforms the plane-wave projection factor into spherical Bessel functions $j_\ell(x)$:
$$
\Theta_\ell(k, \eta_0) = \int_0^{\eta_0} S(k,\eta) j_\ell(k(\eta_0 - \eta)) d\eta
$$
This equation is the cornerstone of modern CMB theory and computation. It expresses the observed anisotropies today as a weighted integral of the physical sources over the history of the universe, with the weights provided by the [visibility function](@entry_id:756540) and geometric projection kernels.

### Advanced Topic: Inhomogeneous Scattering

Our discussion has so far assumed a homogeneous electron density $n_e$. However, in the late universe, structure formation makes $n_e(x)$ inhomogeneous. This adds a new layer of complexity. The collision term for multipoles $\ell \ge 1$ becomes $C_\ell(x) = -\dot{\tau}(x)\Theta_\ell(x)$. While this is a simple product in configuration space, the Fourier [convolution theorem](@entry_id:143495) dictates that in Fourier space it becomes a convolution [@problem_id:3493984]:
$$
\tilde{C}_\ell(\mathbf{k}) = -(\tilde{\dot{\tau}} * \tilde{\Theta}_\ell)(\mathbf{k}) = -\int \frac{d^3k'}{(2\pi)^3} \tilde{\dot{\tau}}(\mathbf{k}') \tilde{\Theta}_\ell(\mathbf{k}-\mathbf{k}')
$$
This means that a single Fourier mode of the photon field at [wavevector](@entry_id:178620) $\mathbf{k}-\mathbf{k}'$ can be coupled to a mode of the electron density at $\mathbf{k}'$, generating a collisional effect at wavevector $\mathbf{k}$. This mode-coupling, induced by inhomogeneous scattering, is a second-order effect and is the source of the kinetic Sunyaev-Zel'dovich (kSZ) effect, where CMB photons scatter off galaxy clusters with a bulk peculiar velocity, generating new temperature anisotropies on small angular scales. This illustrates how the fundamental structure of the collisional Boltzmann equation can be extended to describe a richer set of physical phenomena.