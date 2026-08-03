## Introduction
The [radial velocity](@entry_id:159824) (RV) method is a cornerstone technique in exoplanetology, responsible for many of the earliest and most significant discoveries of worlds beyond our solar system. Its power lies in its ability to detect planets by measuring their gravitational influence on their host stars, providing crucial information about their mass and orbits. However, extracting these subtle signals—often on the order of meters per second—from stellar light requires a deep understanding of physics, sophisticated [mathematical modeling](@entry_id:262517), and rigorous data analysis to distinguish true planets from astrophysical impostors. This article provides a comprehensive guide to the RV method. We will begin in "Principles and Mechanisms" by exploring the physical origin of the signal via the Doppler effect and constructing the complete Keplerian model that describes a star's reflex motion. Next, in "Applications and Interdisciplinary Connections," we will delve into the practical analysis pipeline, from detecting signals with periodograms to vetting candidates and the powerful synergies gained by combining RV with [transit photometry](@entry_id:1133356) and [astrometry](@entry_id:157753). Finally, "Hands-On Practices" will offer applied exercises to solidify these concepts, from deriving signal amplitudes to diagnosing false positives in real-world scenarios. This structured journey will equip you with the foundational knowledge to model, analyze, and interpret [radial velocity](@entry_id:159824) data.

## Principles and Mechanisms

The detection and characterization of exoplanets via the [radial velocity](@entry_id:159824) (RV) method is a testament to the power of applying fundamental physical principles to minute astronomical signals. The entire technique rests upon two pillars: the Doppler effect, which translates motion into an observable spectral shift, and Newtonian dynamics, which describes the predictable gravitational dance of a star and its companions. This chapter details the principles and mechanisms that form the foundation of RV modeling, beginning with the physical origin of the signal and culminating in the mathematical framework used to decode it.

### The Physical Basis of the Radial Velocity Signal

The [radial velocity method](@entry_id:261713) does not measure velocity directly. Instead, it measures the Doppler shift of light emitted by a star. When a light source moves relative to an observer, the observed wavelength of its light is shifted. This phenomenon is a direct consequence of the principles of Special Relativity.

Consider a spectral line emitted by a star with a known rest-frame wavelength $\lambda_0$. When this starlight is measured by an observer at the Solar System Barycenter, its wavelength will be observed as $\lambda_{\mathrm{obs}}$. If the star's motion is purely along the line of sight, the exact relativistic relationship between its [radial velocity](@entry_id:159824), $v_r$, and these wavelengths is given by:

$$
v_r = c \frac{\lambda_{\mathrm{obs}}^2 - \lambda_0^2}{\lambda_{\mathrm{obs}}^2 + \lambda_0^2}
$$

Here, $c$ is the speed of light. This formula is derived directly from the Lorentz transformation of the [wave four-vector](@entry_id:194373) . It is crucial to adhere to the standard astronomical sign convention:
-   A **redshift** ($\lambda_{\mathrm{obs}} > \lambda_0$), where [spectral lines](@entry_id:157575) shift to longer wavelengths, corresponds to a source receding from the observer. In this case, the formula yields a **positive [radial velocity](@entry_id:159824)** ($v_r > 0$).
-   A **blueshift** ($\lambda_{\mathrm{obs}}  \lambda_0$), where [spectral lines](@entry_id:157575) shift to shorter wavelengths, corresponds to a source approaching the observer. This yields a **negative radial velocity** ($v_r  0$).

For the vast majority of stellar reflex motions caused by orbiting exoplanets, the velocities are non-relativistic ($v_r \ll c$). In this limit, the exact formula can be approximated by the more familiar classical Doppler equation:

$$
v_r \approx c \frac{\lambda_{\mathrm{obs}} - \lambda_0}{\lambda_0} = c z
$$

where $z$ is the [redshift](@entry_id:159945). While this approximation is often sufficient, the exact relativistic formula provides the rigorous physical underpinning of the measurement. The observed RV signal is, therefore, the [scalar projection](@entry_id:148823) of the star's velocity vector onto the observer's line of sight . Any component of motion perpendicular to this line of sight (transverse velocity) does not produce a Doppler shift and is invisible to this technique.

### The Keplerian Model of Stellar Reflex Motion

In a star-planet system, the planet does not simply orbit a stationary star. Rather, both bodies orbit their common center of mass, or **[barycenter](@entry_id:170655)**. Because the star is far more massive than the planet, the barycenter lies very close to the star's center, often deep within its interior. Nonetheless, the star executes a small, periodic "reflex" orbit around this point. It is the velocity of the star in this reflex orbit that we measure.

According to Newtonian gravity, the solution to this [two-body problem](@entry_id:158716) is that both bodies trace out Keplerian ellipses. Our goal is to construct a model that predicts the star's radial velocity, $v_r(t)$, as a function of time. This requires a precise mapping from the [uniform flow](@entry_id:272775) of time to the star's non-uniform motion in its [elliptical orbit](@entry_id:174908).

#### From Time to Position: The Orbital Anomalies

A key challenge in describing elliptical motion is that an orbiting body moves fastest when it is closest to the barycenter (at **periastron**) and slowest when it is farthest away (at **apoastron**). This is a direct consequence of the [conservation of angular momentum](@entry_id:153076), famously encapsulated in **Kepler's second law**: the line joining the star and the [barycenter](@entry_id:170655) sweeps out equal areas in equal intervals of time. Since time flows uniformly but the star's orbital speed does not, we need a special set of angular variables, known as **anomalies**, to connect them.

The **Mean Anomaly ($M$)** is a fictitious angle designed to increase linearly with time. It represents the [angular position](@entry_id:174053) of a body that *would* be moving at a constant average speed around a circle. Its definition arises directly from the [area law](@entry_id:145931) . The fraction of an orbit's total area swept out since periastron is proportional to the elapsed time. The mean anomaly is defined as this fraction multiplied by $2\pi$. Therefore, $M$ increases uniformly with time:
$$
M(t) = \frac{2\pi}{P}(t - T_0) = n(t - T_0)
$$
where $P$ is the [orbital period](@entry_id:182572), $T_0$ is the time of periastron passage, and $n = 2\pi/P$ is the **mean motion**, or average angular speed.

The **True Anomaly ($\nu$ or $f$)** is the actual, physical angle of the star in its orbital plane, measured from the direction of periastron. This is the geometric quantity that ultimately determines the star's velocity projection.

To connect the time-linear $M$ to the geometrically meaningful $\nu$, we use an intermediate variable: the **Eccentric Anomaly ($E$)**. Geometrically, $E$ is defined with respect to an **auxiliary circle** of radius $a$ (the [semi-major axis](@entry_id:164167)) that circumscribes the ellipse. For a given position of the star on its ellipse, one can project this position onto the auxiliary circle. The [eccentric anomaly](@entry_id:164775) is the angle of this projected point as measured from the circle's center .

These three anomalies are linked by two fundamental equations of celestial mechanics  :
1.  **Kepler's Equation**, which relates the mean and eccentric anomalies:
    $$
    M = E - e \sin E
    $$
    Here, $e$ is the orbital **eccentricity**, which defines the shape of the ellipse ($e=0$ for a circle, $0  e  1$ for an ellipse). This equation is transcendental and must be solved numerically for $E$ given a time (which gives $M$) and the [eccentricity](@entry_id:266900).

2.  The relation between the eccentric and true anomalies:
    $$
    \tan\left(\frac{\nu}{2}\right) = \sqrt{\frac{1 + e}{1 - e}} \tan\left(\frac{E}{2}\right)
    $$
This chain of transformations, $t \rightarrow M \rightarrow E \rightarrow \nu$, provides the instantaneous [angular position](@entry_id:174053) $\nu(t)$ of the star in its orbit at any given time $t$.

### The Complete Single-Planet RV Model

With the ability to calculate the true anomaly $\nu(t)$, we can now construct the full model for the observed radial velocity. The [instantaneous velocity](@entry_id:167797) of the star projected onto the line of sight depends not only on its position in the orbit ($\nu$) but also on the orientation of that orbit in three-dimensional space. This orientation is described by two angles: the **inclination ($i$)** and the **argument of periastron ($\omega$)**. The inclination is the angle between the orbital plane and the plane of the sky ($i=90^\circ$ for an edge-on orbit, $i=0^\circ$ for a face-on orbit). The argument of periastron is the angle within the orbital plane from the point where the star is moving towards us (the ascending node) to the location of periastron.

The resulting [radial velocity](@entry_id:159824) of the star is given by the canonical Keplerian RV model  :

$$
v_r(t) = \gamma + K \big[ \cos(\nu(t) + \omega) + e \cos\omega \big]
$$

Let us deconstruct this crucial equation:

-   **$\gamma$ (Systemic Velocity)**: This is a constant velocity offset. It represents the [radial velocity](@entry_id:159824) of the entire star-planet system's barycenter with respect to the observer, plus any constant instrumental offset. We will discuss its physical meaning in more detail shortly. For now, it is the baseline of the RV curve.

-   **$K$ (RV Semi-amplitude)**: This parameter, often called simply the "K-amplitude," defines the maximum variation of the star's orbital velocity about the systemic velocity. It scales the size of the RV signal and is given by:
    $$
    K = \frac{2\pi a_\star \sin i}{P \sqrt{1-e^2}}
    $$
    where $a_\star$ is the [semi-major axis](@entry_id:164167) of the star's reflex orbit. The term $\sin i$ is of paramount importance: it shows that the observed amplitude is only a projection of the true velocity. For a face-on orbit ($i=0^\circ$), $\sin i = 0$ and the RV signal vanishes entirely, regardless of the planet's mass.

-   **$\cos(\nu(t) + \omega)$**: This is the primary time-varying component. The angle $\nu(t) + \omega$ represents the star's [angular position](@entry_id:174053) relative to the line of nodes. For a circular orbit ($e=0$), $\nu(t)$ increases linearly with time, and this term produces a pure sinusoidal curve. For an eccentric orbit, the non-uniform evolution of $\nu(t)$ distorts the curve from a simple sine wave.

-   **$e \cos\omega$**: This is a constant term within the brackets, but it is fundamental to the model for eccentric orbits. It is often called the "shape" term. For $e > 0$, the average value of $\cos(\nu(t) + \omega)$ over one orbit is not zero. The addition of the $e\cos\omega$ term precisely cancels this non-zero mean, ensuring that the entire bracketed expression averages to zero over one orbit. This correctly isolates $\gamma$ as the true time-averaged velocity of the system . The argument of periastron, $\omega$, controls the asymmetry of the RV curve; a curve is maximally asymmetric for $\omega = 90^\circ$ or $270^\circ$ and symmetric for $\omega=0^\circ$ or $180^\circ$.

Notably, the **longitude of the ascending node ($\Omega$)**, which describes the orientation of the orbit in the plane of the sky, does not appear in the RV equation. This is because the Doppler shift is sensitive only to motion along the line of sight, making the measurement insensitive to rotations about that line of sight .

### Interpreting the Model Parameters and Observables

By fitting the Keplerian model to a time series of RV data, we can estimate the orbital parameters $P$, $e$, $\omega$, $K$, and $\gamma$. These observables, in turn, allow us to infer the physical properties of the unseen planetary companion.

#### The Mass Function and Minimum Mass ($m_p \sin i$)

The ultimate prize of an RV measurement is often a constraint on the planet's mass. This is achieved through the **[mass function](@entry_id:158970)**, a powerful relation derived by combining the definition of $K$, Kepler's third law, and the barycentric relation ($M_\star a_\star = m_p a_p$) . The derivation yields:

$$
\frac{P K^3 (1-e^2)^{3/2}}{2\pi G} = \frac{(m_p \sin i)^3}{(M_\star + m_p)^2}
$$

where $G$ is the [gravitational constant](@entry_id:262704), $m_p$ is the planet's mass, and $M_\star$ is the star's mass.

This equation is profound. The left-hand side contains only quantities that are directly observable from the RV curve ($P, K, e$) and fundamental constants. The right-hand side contains the physical properties of the system we wish to know. By measuring the RV curve and independently estimating the [stellar mass](@entry_id:157648) $M_\star$ (e.g., from its spectrum), we can solve for the quantity **$m_p \sin i$**.

Because the inclination $i$ is generally unknown for non-transiting systems, we cannot disentangle $m_p$ from $\sin i$. Since the maximum value of $\sin i$ is 1 (for an edge-on orbit), the value $m_p \sin i$ represents a **minimum mass** for the planet. The [true mass](@entry_id:1133457), $m_p$, could be larger if the orbit is inclined. This is the famous "$m \sin i$ ambiguity" inherent to the [radial velocity method](@entry_id:261713).

#### The Systemic Velocity ($\gamma$) and Reference Frames

While $\gamma$ appears as a simple offset in the model, its correct treatment and interpretation are critical for achieving the meter-per-second precision required for exoplanet science. The measured parameter $\gamma$ is a composite of several physical effects :
1.  The true barycentric radial velocity of the star-planet system through space.
2.  An arbitrary **instrumental zero-point offset**, which arises from the spectrograph's internal wavelength calibration.
3.  Quasi-constant astrophysical effects, such as [gravitational redshift](@entry_id:158697) from the star.

When combining data from multiple instruments, each will have its own unique zero-point. Therefore, a separate offset parameter, $\gamma_j$, must be fitted for each instrument $j$ to avoid biasing the shared orbital parameters .

Furthermore, all raw velocity measurements must be corrected for the motion of the observer. The Earth's velocity is substantial (up to $\sim 30$ km/s). To place the measurements in a stable [inertial frame](@entry_id:275504), we correct them to the **Solar System Barycenter (SSB)**. It is critically important to use the SSB and not the Sun as the reference point. The Sun itself orbits the SSB, primarily due to the gravitational pull of Jupiter, with a velocity that can reach approximately 12.5 m/s. If one were to use a simpler heliocentric (Sun-centered) correction, this solar wobble would not be removed. It would remain in the data as a periodic signal with a ~12-year period, capable of mimicking a gas-giant planet or severely biasing the parameters of any detected planets . Accurate barycentric correction is therefore a non-negotiable step in high-precision RV analysis.

### Beyond the Single Planet: Multi-Planet Systems

Many, if not most, stars host multiple planets. The gravitational force on the star is the simple vector sum of the forces from each planet. By the linearity of integration, the star's total RV is the sum of the RV signals that would be induced by each planet. This leads to the common modeling approach of a **linear superposition of Keplerians**:

$$
v_r(t) = \gamma + \sum_{j=1}^{N} K_j \big[ \cos(\nu_j(t) + \omega_j) + e_j \cos\omega_j \big]
$$

where the sum is over $N$ planets. This model, however, relies on a crucial simplifying assumption: that the orbit of each planet is a fixed, non-evolving Keplerian ellipse. In reality, planets exert gravitational forces on each other. These **planet-planet interactions** act as perturbations, causing the [orbital elements](@entry_id:1129191) (like $e_j$ and $\omega_j$) of each planet to change over time, a process known as **[secular evolution](@entry_id:158486)** .

The superposition model is a good approximation if these orbital changes are negligible over the observational time baseline. This is generally true for systems where planets are widely separated and have low masses relative to the star. For such "dynamically cold" systems, secular timescales can be thousands to millions of years, and a simple sum of Keplerians is highly effective .

However, the approximation can fail dramatically in two key scenarios:
1.  **Tightly packed systems**: When planets are close, their mutual gravitational forces are stronger, leading to faster orbital evolution.
2.  **Mean-Motion Resonances (MMRs)**: If the orbital periods of two planets form a simple integer ratio (e.g., 2:1, 3:2), their gravitational interactions can occur at the same location in their orbits, leading to resonant amplification of the perturbations. In such cases, deviations from a simple Keplerian sum can become detectable even over decadal baselines, providing a powerful tool to measure planet-planet interactions and even break the $m \sin i$ degeneracy.

The study of these deviations marks the transition from simple kinematic modeling to the rich field of N-body gravitational dynamics, which is necessary to fully characterize the complex architecture of planetary systems.