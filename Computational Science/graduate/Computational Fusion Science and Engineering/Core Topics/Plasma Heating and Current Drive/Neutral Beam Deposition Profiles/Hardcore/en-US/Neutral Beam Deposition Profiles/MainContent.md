## Introduction
Neutral Beam Injection (NBI) is a cornerstone technique for achieving and sustaining the extreme conditions required for nuclear fusion. Its success, however, is not merely a matter of injecting power; it depends critically on *where* and *how* that power is deposited within the plasma. This spatial distribution, known as the [neutral beam deposition](@entry_id:1128677) profile, dictates the effectiveness of heating, the efficiency of [current drive](@entry_id:186346), and the ability to control plasma stability. A simplistic view of NBI as a bulk heat source is insufficient for modern fusion science, which demands precise control over the plasma state. This article addresses this need by providing a comprehensive, multi-faceted examination of the physics and application of [neutral beam deposition](@entry_id:1128677).

We will embark on a structured exploration beginning with the **Principles and Mechanisms** that govern the transformation of a neutral atom beam into a population of confined fast ions. This includes a deep dive into the [atomic physics](@entry_id:140823) of [beam attenuation](@entry_id:1121488) and the critical role of magnetic geometry. Next, in **Applications and Interdisciplinary Connections**, we will see how these principles are leveraged to use NBI as a sophisticated actuator for heating, fueling, driving [plasma rotation](@entry_id:753506) and current, and stabilizing the plasma against destructive instabilities. Finally, the **Hands-On Practices** section will challenge you to apply this theoretical knowledge to solve practical, quantitative problems encountered in fusion research and engineering. This journey will equip you with a robust understanding of [neutral beam deposition](@entry_id:1128677), from first-principles physics to advanced computational modeling and control applications.

## Principles and Mechanisms

The process of [neutral beam deposition](@entry_id:1128677) is the foundation upon which [neutral beam injection](@entry_id:204293) (NBI) for heating, [current drive](@entry_id:186346), and [plasma control](@entry_id:753487) is built. It describes the transformation of a beam of high-energy, electrically neutral atoms into a population of energetic, or "fast," ions within the plasma. This transformation is not instantaneous; it occurs progressively as the [neutral beam](@entry_id:752451) traverses the plasma, leading to a spatially distributed source of fast ions. The precise location and characteristics of this source profile are critical for the effectiveness of NBI and are governed by a combination of [atomic physics](@entry_id:140823), beam parameters, and the magnetic geometry of the confinement device. This chapter elucidates the fundamental principles and mechanisms that determine the [neutral beam deposition](@entry_id:1128677) profile.

### Fundamental Attenuation Processes

A neutral atom, being electrically uncharged, travels in a straight line, unaffected by the strong magnetic fields used for plasma confinement. Its journey through the plasma is terminated only when it undergoes a collision that strips it of its electron, converting it into an ion. Once ionized, the particle is subject to the Lorentz force and becomes confined by the magnetic field, where it subsequently transfers its substantial kinetic energy to the background plasma particles through collisions. The primary atomic processes that lead to the ionization of beam neutrals are electron-impact ionization, ion-impact ionization, and charge exchange.

Let us consider a monoenergetic beam of fast neutral atoms, denoted $A^0$, traversing a plasma composed of electrons and various ion species $B^+$.

**Electron-Impact Ionization** is the process whereby a plasma electron collides with a beam neutral and ionizes it:
$$
A^0 + e^- \to A^+ + e^- + e^-
$$
In this reaction, the original fast neutral becomes a fast ion, retaining nearly all of its initial momentum and energy. A new, low-energy electron is liberated, thereby increasing the total number of electrons and ions in the plasma.

**Charge Exchange** is a process in which an electron is transferred from the fast beam neutral to a slower plasma ion:
$$
A^0_{\text{fast}} + B^+_{\text{slow}} \to A^+_{\text{fast}} + B^0_{\text{slow}}
$$
Here, the fast neutral is converted into a fast ion, while the plasma ion is neutralized. This process conserves the total number of ions but is a powerful mechanism for converting beam neutrals into confined fast ions. The resulting slow neutral is no longer confined by the magnetic field and may escape the plasma, representing a potential energy loss channel.

A third key process is **Ion-Impact Ionization**, where a plasma ion collides with and ionizes a beam neutral:
$$
A^0 + B^+ \to A^+ + B^+ + e^-
$$
Similar to electron-impact ionization, this reaction creates a new fast ion and a free electron, increasing the [plasma density](@entry_id:202836). Its importance relative to the other channels depends on the beam energy and the charge and mass of the plasma ions.

The likelihood of any of these reactions occurring is quantified by the **microscopic cross-section**, $\sigma(E)$, which represents an effective target area for the collision. This cross-section is a strong function of the relative kinetic energy of the colliding particles, $E = \frac{1}{2}\mu v_{\text{rel}}^2$, where $\mu$ is the [reduced mass](@entry_id:152420) of the projectile-target pair and $v_{\text{rel}}$ is their relative speed. To determine the total reaction frequency, $\nu$, for a single beam neutral moving through a plasma, we must average the product of the cross-section and relative speed over the velocity distributions of the target plasma species. For a target species $s$ with density $n_s$, the reaction frequency is given by :
$$
\nu_s = n_s \langle \sigma_s(E) v_{\text{rel}} \rangle_s = n_s \int f_s(\mathbf{v}_s) \sigma_s\left(\frac{1}{2}\mu_{sA} |\mathbf{v}_{\text{b}} - \mathbf{v}_s|^2\right) |\mathbf{v}_{\text{b}} - \mathbf{v}_s| \, \mathrm{d}^3\mathbf{v}_s
$$
where $\mathbf{v}_{\text{b}}$ is the beam velocity and $f_s(\mathbf{v}_s)$ is the normalized [velocity distribution function](@entry_id:201683) of the target species.

The energy dependence of these cross-sections is crucial. In the energy range typical for NBI systems (in the range of tens to hundreds of keV), the [cross-sections](@entry_id:168295) for charge exchange and ion-impact ionization generally decrease with increasing beam energy $E_b$. For instance, the charge-exchange cross-section $\sigma_{\text{cx}}$ often scales approximately as $E_b^{-1}$ or more steeply at high energies. In contrast, the effective reaction rate for electron-impact ionization in a hot plasma (where electron thermal speeds far exceed the beam speed) is primarily determined by the electron temperature, not the beam energy. The [attenuation coefficient](@entry_id:920164) for electron-impact ionization, $\alpha_{ei}$, which is proportional to $\nu_e / v_b$, consequently scales as $1/v_b \propto E_b^{-1/2}$. Because this decrease is slower than that for charge exchange, electron-impact ionization becomes the dominant attenuation channel at higher beam energies, a key consideration for achieving core deposition in large, hot fusion devices .

### The Beer-Lambert Law and Deposition Profiles

The collective effect of all attenuation processes can be described by the Beer-Lambert law. The total attenuation coefficient, $\alpha_{\text{eff}}$, is the sum of the contributions from each independent collision channel with each target species $k$:
$$
\alpha_{\text{eff}} = \sum_k \frac{\nu_k}{v_b} = \sum_k n_k \frac{\langle \sigma_k v_{\text{rel}} \rangle_k}{v_b} \approx \sum_k n_k \sigma_{\text{eff},k}
$$
The approximation holds when the target thermal motion is negligible compared to the beam speed, where $\sigma_{\text{eff},k}$ is the effective cross-section at the beam energy.

The **mean free path**, $\lambda$, is the average distance a neutral travels before being ionized, and is defined as the inverse of the [attenuation coefficient](@entry_id:920164), $\lambda = 1/\alpha_{\text{eff}}$. For a plasma with multiple attenuating species, the effective mean free path $\lambda_{\text{eff}}$ is determined by the sum of the individual attenuation coefficients. This leads to the relationship :
$$
\frac{1}{\lambda_{\text{eff}}} = \sum_k \frac{1}{\lambda_k'}
$$
where $\lambda_k' = 1/(n_k \sigma_{\text{eff},k})$ is the mean free path the beam would have in a hypothetical medium composed only of species $k$ at density $n_k$. This shows that the inverse mean free paths, or attenuation rates, are additive.

The attenuation of the [neutral beam](@entry_id:752451) intensity, $I(s)$ (number of particles per unit area per unit time), along its path coordinate $s$ is described by the differential equation:
$$
\frac{dI(s)}{ds} = - \alpha_{\text{eff}}(s) I(s) = - \frac{I(s)}{\lambda_{\text{eff}}(s)}
$$
For a uniform plasma where $\alpha_{\text{eff}}$ is constant, this integrates to the familiar exponential decay: $I(s) = I_0 \exp(-s/\lambda_{\text{eff}})$, where $I_0$ is the initial intensity. In a realistic, non-uniform plasma where the density $n(s)$ varies along the beam path, the solution becomes:
$$
I(s) = I_0 \exp\left( -\int_0^s \alpha_{\text{eff}}(s') ds' \right)
$$
The **deposition profile**, or the rate of fast-ion creation per unit volume, is proportional to the local loss rate of neutrals, $S(s) \propto -dI/ds$.

The integral in the exponent is known as the **[optical depth](@entry_id:159017)**, $\tau(s) = \int_0^s \alpha_{\text{eff}}(s') ds'$. A large [optical depth](@entry_id:159017) ($\tau \gg 1$) implies strong attenuation and that most of the beam is deposited near the plasma edge. A small optical depth ($\tau \ll 1$) implies weak attenuation, allowing the beam to penetrate deep into the plasma core. However, if the total optical depth of the plasma, $\tau_L = \int_0^L \alpha_{\text{eff}}(s) ds$, is too small, a significant fraction of the beam may pass completely through the plasma without being ionized. This unattenuated portion is known as **[shine-through](@entry_id:1131571)**. The [shine-through](@entry_id:1131571) fraction is $\phi_{\text{st}} = I(L)/I_0 = \exp(-\tau_L)$. This fraction carries the full beam power and can cause substantial, localized heat loads on the vessel walls opposite the injector. Calculating this heat load is a critical engineering constraint, requiring integration of the [plasma density profile](@entry_id:193964) along the beam path to find $\tau_L$ and using geometric [view factors](@entry_id:756502) to determine how the [shine-through](@entry_id:1131571) power is distributed onto material surfaces .

### Shaping the Deposition Profile: Geometry and Beam Properties

The spatial distribution of deposited fast ions can be controlled by tailoring both the injection geometry and the properties of the neutral beam itself.

#### Injection Geometry

The straight-line path of the [neutral beam](@entry_id:752451) is a key determinant of the deposition location within the complex [toroidal geometry](@entry_id:756056) of a tokamak or stellarator. By adjusting the launch point and aim vector, injectors can be aimed for **on-axis** or **off-axis** deposition. For a beam launched from position $\mathbf{x}_L$ with aim vector $\hat{\mathbf{u}}$, the point of closest approach to the magnetic axis (at $\mathbf{x}_0$) occurs at a path length $s^* = \hat{\mathbf{u}} \cdot (\mathbf{x}_0 - \mathbf{x}_L)$.

The deposition profile along the beam path is inherently front-loaded due to exponential attenuation. The characteristic deposition length scale is the mean free path, $\lambda$. The interaction between the beam geometry ($s^*$) and the attenuation physics ($\lambda$) determines the final deposition location. If the mean free path is short compared to the distance to the point of closest approach ($\lambda \ll s^*$), most of the beam will be deposited in the outer regions of the plasma, far from the magnetic axis, resulting in off-axis deposition. Conversely, if the mean free path is long ($\lambda \gtrsim s^*$), a significant fraction of the beam can reach the vicinity of the closest approach, enabling on-axis deposition. Therefore, achieving core deposition requires both aiming the beam at the core and ensuring the beam energy is high enough for $\lambda$ to be sufficiently long .

#### Multi-Component Beams

Practical NBI systems are often derived from the acceleration of molecular ions (e.g., $D_2^+, D_3^+$) in addition to atomic ions ($D^+$). When these molecular ions are neutralized, they dissociate, resulting in a [neutral beam](@entry_id:752451) composed of multiple energy components, typically with full ($E$), half ($E/2$), and third ($E/3$) of the primary acceleration energy. As established earlier, the attenuation [cross-sections](@entry_id:168295) are strongly energy-dependent. Lower-energy neutrals have a smaller mean free path. Consequently, a multi-energy beam results in a layered deposition profile: the lowest-energy component (e.g., $E/3$) is deposited most peripherally, while the highest-energy component ($E$) penetrates deepest into the plasma. This effect must be accounted for when modeling heating and current drive profiles. For instance, while lower-energy components are deposited near the edge, they also provide more toroidal momentum per unit of power, since momentum scales as $1/v \propto E^{-1/2}$ for a given power. The overall momentum input profile is a superposition of the contributions from each energy species, each with its own deposition profile and momentum-per-particle weighting .

#### Beam Divergence and Profile Width

An ideal [neutral beam](@entry_id:752451) would be a perfect "pencil beam" with zero cross-sectional area. Real beams, however, have a finite size and **divergence**, or angular spread. This divergence originates in the ion source, where the finite transverse temperature of the ions and the electrostatics of the extraction optics impart a small transverse velocity to the beamlets. This intrinsic angular spread is a key characteristic of the beam's quality.

The concepts of RMS beam size, $\sigma_x$, and RMS angular divergence, $\sigma_\theta$, are combined into a single figure of merit called the **[beam emittance](@entry_id:184476)**, $\epsilon = \sigma_x \sigma_\theta$. According to Liouville's theorem, for a beam subject only to ideal linear focusing forces, the emittance is a conserved quantity. This conservation imposes a fundamental trade-off: one can focus the beam to a smaller spot size ($\sigma_x$) only at the expense of a larger angular spread ($\sigma_\theta$), and vice-versa. A lower emittance source is therefore critical for achieving a small, highly localized deposition spot deep inside the plasma .

The divergence of the beam acts as a broadening mechanism for the deposition profile. Even if attenuation were to deposit all particles at a single point along the beam's central ray, the angular spread would distribute these depositions in a pattern around that point. The overall width of the deposition peak is therefore a competition between two effects: the intrinsic width from the exponential attenuation process and the broadening from [beam divergence](@entry_id:269956). The variance of the final radial deposition profile can be modeled as the sum of the variances from these two independent effects. For a localized region, this can be expressed as :
$$
\sigma_r^2 = \sigma_{\text{attenuation}}^2 + \sigma_{\text{divergence}}^2 \approx \left(\frac{g}{\alpha}\right)^2 + \sigma_{\text{div}}^2
$$
Here, $\alpha$ is the [attenuation coefficient](@entry_id:920164), $g$ is a geometric factor projecting the path length onto the radial coordinate, and $\sigma_{\text{div}}$ is the radial broadening due to divergence. This expression quantitatively shows that a sharp deposition profile requires both strong attenuation ("attenuation focusing," large $\alpha$) and low [beam divergence](@entry_id:269956) (small $\sigma_{\text{div}}$).

### From Neutrals to Fast Ions: Birth Profiles and Orbit Effects

The deposition of a neutral atom marks the birth of a fast ion. The initial state of this ion—its position and velocity—is the starting point for its life in the plasma. This birth profile is not the final effective heating profile, which is further shaped by the ion's subsequent orbital motion.

#### The Birth Profile in Velocity Space

When a neutral is ionized at a position $\mathbf{x}(s)$ along its path, the newly created fast ion instantaneously inherits the neutral's velocity vector, $\mathbf{v} = v_b \hat{\mathbf{b}}(s)$, where $\hat{\mathbf{b}}(s)$ is the unit tangent to the beam trajectory. The ion's subsequent motion is dictated by the local magnetic field, $\mathbf{B}(\mathbf{x}(s))$. A critical parameter governing this motion is the **pitch angle**, $\theta$, the angle between the particle's velocity and the magnetic field. At the moment of birth, the initial pitch angle $\theta_b(s)$ is simply the angle between the beam's direction and the local magnetic field direction. The cosine of this angle, often denoted $\xi$, is given by the dot product of the [unit vectors](@entry_id:165907) :
$$
\xi_0(s) = \cos(\theta_b(s)) = \hat{\mathbf{b}}(s) \cdot \hat{\mathbf{B}}(s)
$$
As the beam traverses the plasma, the direction of the magnetic field lines changes, causing the birth pitch angle $\xi_0(s)$ to vary along the deposition path. Consequently, the spatial deposition profile $S(s)$ is mapped into a source distribution in velocity space, determining the initial population of fast ions with different pitch angles.

#### The Role of Magnetic Geometry and Orbit Broadening

The birth pitch angle determines whether an ion is born onto a **passing orbit** (which circulates toroidally) or a **trapped orbit** (which is confined to a limited range of poloidal angles, bouncing between high-field regions). Ions born with a large pitch angle (i.e., velocity mostly perpendicular to $\mathbf{B}$) are more likely to be trapped.

Trapped particles in a tokamak do not follow flux surfaces. Due to the gradient and curvature of the magnetic field, their guiding centers drift vertically, tracing out a "banana-shaped" path in the poloidal cross-section. The radial width of this **[banana orbit](@entry_id:192144)** can be significant. For a deeply trapped particle, the banana width $\Delta_b$ scales as :
$$
\Delta_b \sim \frac{q}{\sqrt{\varepsilon}} \rho_L
$$
where $q$ is the safety factor, $\varepsilon = r/R_0$ is the inverse aspect ratio, and $\rho_L$ is the ion's Larmor radius. This means that a fast ion born at a single radius $r_0$ is immediately redistributed over a radial range of order $\Delta_b$. This effect constitutes a significant, non-[collisional broadening](@entry_id:158173) of the initial deposition profile. The effective deposition profile, even after just one bounce period, is a convolution of the birth profile with this orbit width.

The magnetic geometry itself has a profound impact on deposition. In an **axisymmetric tokamak**, the toroidal symmetry ensures the conservation of [canonical toroidal momentum](@entry_id:1122015), which helps confine [fast ion orbits](@entry_id:1124850). In a **non-axisymmetric stellarator**, the magnetic field is intrinsically three-dimensional. A straight beam path can intersect a given flux surface multiple times as it traverses the complex field structure. This non-monotonic mapping from path length to flux radius can create deposition profiles with multiple peaks or even hollow profiles, a stark contrast to the typically single-peaked profiles in tokamaks. Furthermore, the lack of axisymmetry in stellarators leads to the non-conservation of canonical toroidal momentum, resulting in classes of orbits that are poorly confined and can be promptly lost from the plasma. This increases the [shine-through](@entry_id:1131571) and can modify the net deposition profile by preferentially removing particles born in certain regions .

In summary, the journey from a neutral beam to a thermalized plasma population is a multi-step process. It begins with atomic collisions that create a birth profile of fast ions, shaped by beam energy, [plasma density](@entry_id:202836), and injection geometry. This birth profile is then immediately modified by the fast-ion's [orbital motion](@entry_id:162856) in the magnetic field, which can significantly broaden and reshape the distribution. Understanding and modeling these principles and mechanisms is paramount for designing and interpreting NBI systems in fusion energy research.