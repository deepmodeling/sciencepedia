## Introduction
Gravitational microlensing has emerged as a cornerstone of modern astrophysics, offering a unique window into the universe of cold, low-mass exoplanets and isolated [compact objects](@entry_id:157611) that are largely invisible to other detection methods. Based on the principles of General Relativity, this phenomenon manifests as the temporary and transient brightening of a background star when a massive object passes nearly in front of it. However, moving from the observation of a simple stellar brightening to a detailed characterization of an unseen planetary system presents a significant challenge, requiring a deep understanding of the underlying physics and sophisticated analytical techniques.

This article provides a comprehensive guide to mastering the [gravitational microlensing](@entry_id:160544) method. We will begin in the **Principles and Mechanisms** chapter by deriving the core theory from first principles, building the mathematical models for light curves, and exploring the higher-order effects that are key to measuring physical properties. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how this theoretical framework is practically applied to discover [free-floating planets](@entry_id:1125298), measure [exoplanet demographics](@entry_id:1124734), and probe the structure of our Milky Way. Finally, the **Hands-On Practices** section will allow you to solidify your knowledge by tackling realistic computational problems, bridging the gap between theory and practical data analysis.

## Principles and Mechanisms

Gravitational [microlensing](@entry_id:160918) is a direct consequence of the deflection of light by mass, as predicted by Einstein's theory of General Relativity. While the preceding chapter introduced the historical context and observational significance of this method, this chapter delves into the fundamental principles and physical mechanisms that govern it. We will begin by establishing the basic [lens equation](@entry_id:161034) from first principles, define the characteristic scales of the phenomenon, and then systematically build a model for the observable light curve. Subsequently, we will explore the higher-order effects that break model degeneracies, address key observational realities, and finally, extend the framework to binary lenses, the primary application for detecting exoplanets.

### The Gravitational Deflection of Light

The foundation of all [gravitational lensing](@entry_id:159000) is the bending of a light ray's path as it passes through a gravitational field. In the [weak-field limit](@entry_id:199592) of General Relativity, a light ray with an impact parameter $b$ passing a [point mass](@entry_id:186768) $M$ is deflected by an angle $\hat{\alpha}$ given by:
$$
\hat{\alpha}(b) = \frac{4GM}{c^2 b}
$$
where $G$ is the [gravitational constant](@entry_id:262704) and $c$ is the speed of light. Notice that this deflection angle is independent of the photon's frequency, a direct consequence of the Equivalence Principle. This implies that, in the geometric optics limit, [gravitational lensing](@entry_id:159000) is an intrinsically **achromatic** phenomenon.

To describe an astronomical lensing event, we employ the **thin-lens approximation**, which assumes that all deflection occurs instantaneously in a single plane containing the lens. Consider an observer, a lens, and a background source that are nearly collinear. We can define a two-dimensional [celestial sphere](@entry_id:158268), or "sky plane," perpendicular to the line of sight. Let $\boldsymbol{\beta}$ be the true [angular position](@entry_id:174053) of the source and $\boldsymbol{\theta}$ be the observed [angular position](@entry_id:174053) of a lensed image, both measured relative to the lens's position. The relationship between these angles is described by the **vector [lens equation](@entry_id:161034)**.

The observed image position $\boldsymbol{\theta}$ is displaced from the true source position $\boldsymbol{\beta}$ by a deflection angle $\boldsymbol{\alpha}$, which is the physical deflection $\hat{\boldsymbol{\alpha}}$ scaled by the geometry of the system. If $D_L$ is the distance to the lens, $D_S$ is the distance to the source, and $D_{LS} = D_S - D_L$ is the distance between them, the [lens equation](@entry_id:161034) is :
$$
\boldsymbol{\beta} = \boldsymbol{\theta} - \boldsymbol{\alpha}(\boldsymbol{\theta}) = \boldsymbol{\theta} - \frac{D_{LS}}{D_S} \hat{\boldsymbol{\alpha}}(D_L\boldsymbol{\theta})
$$
Substituting the GR formula for $\hat{\boldsymbol{\alpha}}$, where the impact parameter is $b = D_L |\boldsymbol{\theta}|$, and noting that the deflection is radially outward from the lens, we arrive at the specific [lens equation](@entry_id:161034) for a [point mass](@entry_id:186768).

### The Einstein Radius: A Fundamental Scale

A crucial insight arises when we consider the special case of perfect alignment, where the source lies directly behind the lens on the optical axis ($\boldsymbol{\beta} = 0$). In this configuration, the symmetry of the system causes the lensed image to appear as a perfect ring around the lens position. The angular radius of this ring is known as the **angular Einstein radius**, $\theta_E$. Setting $\boldsymbol{\beta} = 0$ and $|\boldsymbol{\theta}| = \theta_E$ in the [lens equation](@entry_id:161034) yields its definition :
$$
\theta_E = \sqrt{\frac{4GM}{c^2} \frac{D_{LS}}{D_L D_S}}
$$
This angular scale is the [fundamental unit](@entry_id:180485) of measurement in microlensing. The corresponding physical size of the ring in the lens plane, the **physical Einstein radius** $R_E$, is simply given by the [small-angle approximation](@entry_id:145423) $R_E = D_L \theta_E$:
$$
R_E = \sqrt{\frac{4GM}{c^2} \frac{D_L D_{LS}}{D_S}}
$$
The Einstein radius elegantly combines the physical properties of the lens ($M$) with the geometry of the system ($D_L, D_S$), defining the region of strong gravitational influence.

### Regimes of Gravitational Lensing

The magnitude of the angular Einstein radius, $\theta_E$, relative to the [resolving power](@entry_id:170585) of our telescopes, determines the observational manifestation of lensing. This comparison allows us to classify lensing phenomena into three distinct regimes :

1.  **Strong Lensing:** When the lens is extremely massive, such as a galaxy or galaxy cluster, $\theta_E$ is typically on the order of arcseconds. This angular separation is large enough to be resolved by modern ground-based or space-based telescopes, allowing us to see multiple distinct images, arcs, or a full Einstein ring. For example, a lens of mass $10^{12} M_\odot$ at a [cosmological distance](@entry_id:270927) of $D_L = 1$ Gpc lensing a source at $D_S = 2$ Gpc produces an Einstein radius of $\theta_E \approx 2$ arcseconds. The resulting image separations are well above the typical resolution of astronomical instruments, placing this firmly in the [strong lensing](@entry_id:161736) regime.

2.  **Weak Lensing:** This regime occurs when the [gravitational potential](@entry_id:160378) is not strong enough to produce multiple images. Instead, the lensing effect manifests as a slight, coherent distortion in the shapes of background galaxies. The effect on any single galaxy is too small to measure, but by statistically averaging the shapes of thousands of background galaxies, we can map the distribution of the intervening (often dark) matter that causes the distortion.

3.  **Microlensing:** This is the regime where the lens is a stellar-mass object (or smaller), such as a star, planet, or black hole. For a typical Galactic setup—for instance, a $0.5 M_\odot$ star at $D_L = 6$ kpc lensing a source at $D_S = 8$ kpc—the Einstein radius is on the order of milliarcseconds ($\theta_E \approx 1.3$ mas). The resulting image separation ($\sim 2\theta_E$) is far too small to be resolved by any current telescope, as it lies well below the [atmospheric seeing](@entry_id:174600) limit ($\sim 1$ arcsec) and even the [diffraction limit](@entry_id:193662) of space telescopes like Hubble ($\sim 0.05$ arcsec). The observer sees a single, unresolved point of light. However, as the lens, source, and observer move relative to each other, the angular separation changes, causing the total [magnification](@entry_id:140628) of the images to vary with time. What we observe is not multiple images, but a transient, time-variable brightening of the source star. This is the signature of a microlensing event. Even for extremely low-mass objects like [free-floating planets](@entry_id:1125298), where $\theta_E$ might be in the microarcsecond range, the phenomenon is still classified as microlensing because the images remain unresolved and the observable is a transient flux variation.

### The Point-Source Point-Lens (PSPL) Model

The simplest and most fundamental model for a [microlensing](@entry_id:160918) event is the **Point-Source Point-Lens (PSPL)** model. It makes two key assumptions: the lens is a single [point mass](@entry_id:186768), and the background source is an infinitesimally small point of light. It also assumes that the [relative motion](@entry_id:169798) between the lens and source across the sky is uniform and rectilinear.

The geometry of the event is described by three fundamental parameters that are directly fitted from the observed light curve :
1.  **The time of closest approach, $t_0$:** The epoch at which the angular separation between the lens and source is at its minimum. This corresponds to the time of peak [magnification](@entry_id:140628).
2.  **The [impact parameter](@entry_id:165532), $u_0$:** The minimum angular separation between the lens and source, normalized by the Einstein radius ($\theta_0 / \theta_E$). It is a dimensionless quantity that quantifies how close the alignment becomes; $u_0=0$ represents perfect alignment.
3.  **The Einstein timescale, $t_E$:** The time it takes for the source to traverse an angular distance equal to $\theta_E$ at the relative [proper motion](@entry_id:157951) $\mu_{\mathrm{rel}}$. It is defined as $t_E = \theta_E / \mu_{\mathrm{rel}}$ and sets the characteristic duration of the event.

With these definitions, the normalized angular separation $u$ at any time $t$ is given by the Pythagorean theorem :
$$
u(t) = \sqrt{u_0^2 + \left(\frac{t - t_0}{t_E}\right)^2}
$$
The total magnification $A$ is a direct function of this instantaneous separation $u$. Solving the [lens equation](@entry_id:161034) for the two image positions and summing their magnifications yields:
$$
A(u) = \frac{u^2 + 2}{u\sqrt{u^2 + 4}}
$$
The observed light curve, $A(t) = A(u(t))$, is characteristically symmetric about the [peak time](@entry_id:262671) $t_0$. This symmetry has a profound physical origin: the gravitational potential of the [point-mass lens](@entry_id:183660) is axisymmetric, meaning the magnification depends only on the magnitude of the separation ($u$), not its direction. Combined with the assumption of uniform [rectilinear motion](@entry_id:165142), which makes $u(t)$ an [even function](@entry_id:164802) of $(t-t_0)$, the resulting light curve $A(t)$ must be perfectly symmetric .

### The Mass-Timescale Relation and the Microlensing Degeneracy

One of the primary goals of [microlensing](@entry_id:160918) is to measure the properties of the lens, particularly its mass. From the definition of $\theta_E$, we can see that for a fixed geometry, $\theta_E \propto \sqrt{M}$. The event timescale is $t_E = \theta_E / \mu_{\mathrm{rel}}$, so it follows that $t_E \propto \sqrt{M}$ as well. This fundamental scaling implies that, all else being equal, lower-mass lenses produce shorter-duration events .

However, a simple measurement of $t_E$ from a PSPL light curve is insufficient to determine the lens mass uniquely. The timescale is a degenerate combination of three unknown physical quantities: the lens mass ($M$), its distance ($D_L$), and the relative transverse velocity ($v_t = D_L \mu_{\mathrm{rel}}$):
$$
t_E = \frac{\theta_E}{\mu_{\mathrm{rel}}} = \frac{\sqrt{\frac{4GM}{c^2} \frac{D_{LS}}{D_L D_S}}}{\frac{v_t}{D_L}}
$$
This is the central **microlensing degeneracy**. Measuring a single value, $t_E$, provides only one constraint on a multi-dimensional parameter space. A short event could be caused by a low-mass lens, a fast-moving lens, or a lens that is very close to the observer or the source. To determine the mass, we must find ways to break this degeneracy by measuring additional information.

### Probing the Physics: Higher-Order Effects

Deviations from the simple PSPL model are not imperfections; they are invaluable sources of information that allow us to measure additional physical parameters and break the [microlensing](@entry_id:160918) degeneracy.

#### Finite-Source Effects

Real sources are not points of light but have a finite physical and [angular size](@entry_id:195896). We define the **finite-source parameter**, $\rho$, as the ratio of the source's angular radius, $\theta_*$, to the Einstein radius :
$$
\rho = \frac{\theta_*}{\theta_E}
$$
When the source is large enough that $\rho$ is non-negligible, the point-source approximation breaks down. The observed magnification is no longer the value at a single point but an average over the entire face of the source star. This has two critical consequences:
1.  **Suppression of Peak Magnification:** The infinite [magnification](@entry_id:140628) predicted for a [point source](@entry_id:196698) at $u=0$ is resolved. The flux is averaged over a disk of radius $\rho$, leading to a finite peak magnification that, for a central transit, scales as $A_{\max} \sim \rho^{-1}$. Consequently, surveys are biased against detecting very low-mass lenses (which have small $\theta_E$, leading to large $\rho$) lensing large giant stars, as the resulting low-[magnification](@entry_id:140628) events may not pass detection thresholds .
2.  **Smoothing of Sharp Features:** Any sharp features in the light curve, such as the approach to a caustic (which we will discuss later), are smoothed out. The smoothing occurs over the time it takes for the source to move its own radius, a timescale given by $t_* = \theta_*/\mu_{\mathrm{rel}} = \rho t_E$.

By measuring both $\rho$ and $t_E$ from a detailed light curve fit, we can measure the source crossing time $t_*$. If the [angular size](@entry_id:195896) of the source star $\theta_*$ can be independently estimated (e.g., from its color and magnitude), we can determine the Einstein radius via $\theta_E = \theta_*/\rho$. This measurement of a second physical scale is a crucial step in breaking the mass-distance-velocity degeneracy.

#### Microlensing Parallax

The assumption of uniform [rectilinear motion](@entry_id:165142) is an approximation because the observer (on Earth) is accelerating as it orbits the Sun. This motion induces a **[microlensing parallax](@entry_id:158437)** effect, causing the observed trajectory of the source relative to the lens to deviate from a straight line. This distortion introduces asymmetries into the otherwise symmetric PSPL light curve.

The effect is quantified by the **[microlensing parallax](@entry_id:158437) vector**, $\boldsymbol{\pi}_E$, a dimensionless vector defined as :
$$
\boldsymbol{\pi}_E = \frac{\pi_{\mathrm{rel}}}{\theta_E} \hat{\boldsymbol{n}}
$$
where $\pi_{\mathrm{rel}} = \mathrm{AU}(1/D_L - 1/D_S)$ is the relative parallax between the lens and source, and $\hat{\boldsymbol{n}}$ is the [unit vector](@entry_id:150575) in the direction of relative [proper motion](@entry_id:157951). The full trajectory is then perturbed by a term proportional to $\boldsymbol{\pi}_E$ and the Earth's known projected [position vector](@entry_id:168381).

By meticulously fitting the full, distorted light curve over a significant fraction of a year, one can measure the two components of $\boldsymbol{\pi}_E$. The component parallel to the Earth's acceleration at $t_0$ creates an antisymmetric distortion, while the perpendicular component creates a symmetric one; this difference allows both to be disentangled. Measuring $\pi_E = |\boldsymbol{\pi}_E|$ provides another physical constraint on the system. With both $\theta_E$ (from finite-source effects) and $\pi_E$ measured, one can solve for the lens mass $M$ and distance $D_L$ directly:
$$
M = \frac{c^2 \mathrm{AU}}{4G} \frac{\theta_E}{\pi_E} \quad , \quad D_L = \frac{\mathrm{AU}}{\pi_E \theta_E + \pi_S}
$$
where $\pi_S = \mathrm{AU}/D_S$ is the parallax of the source.

### Confronting Reality: Observational Considerations

Real-world observations must contend with further complexities that affect the interpretation of light curves.

#### Blended Light

Microlensing surveys often monitor dense stellar fields, like the Galactic bulge. A single photometric measurement may contain light not only from the lensed source but also from other unresolved stars that happen to fall within the same patch of sky. This additional, unmagnified flux is called **blend flux**, $F_b$.

The total observed flux is $F_{\mathrm{obs}}(t) = F_s A(t) + F_b$, where $F_s$ is the intrinsic source flux. The baseline flux is $F_{\mathrm{base}} = F_s + F_b$. The observed [magnification](@entry_id:140628) is therefore diluted :
$$
A_{\mathrm{obs}}(t) = \frac{F_s A(t) + F_b}{F_s + F_b} = f_s A(t) + (1-f_s)
$$
where $f_s = F_s / (F_s + F_b)$ is the **blending parameter**, representing the fraction of baseline light from the source. This shows that blending linearly scales and shifts the true magnification. While the symmetric shape is preserved, the amplitude is reduced. If blending is ignored (i.e., one assumes $f_s=1$), the reduced observed magnification would be misinterpreted as a larger impact parameter $u_0$, leading to incorrect conclusions. For a high-[magnification](@entry_id:140628) event with true [impact parameter](@entry_id:165532) $u_0$, an erroneous fit with $f_s=1$ would infer an impact parameter $u_0' \approx u_0 / f_s$.

#### Achromaticity and Its Violations

As a consequence of the Equivalence Principle, pure [gravitational lensing](@entry_id:159000) is achromatic. However, observed microlensing events can exhibit chromaticity (color changes) for several reasons :

1.  **Blending:** If the source star and the unresolved blend stars have different colors, the color of the combined light will change as the event progresses. As the source is magnified, its color dominates the blend, so the observed color shifts towards that of the source near the peak of the event.
2.  **Finite-Source Effects:** The surface brightness of a star is not uniform across its disk; this is known as **[limb darkening](@entry_id:157740)**. The degree of limb darkening is wavelength-dependent. As the highly non-uniform magnification pattern of a [caustic](@entry_id:164959) sweeps across the stellar disk, it differentially magnifies regions of different intrinsic color, producing a measurable chromatic signal.
3.  **Diffraction:** In the [wave optics](@entry_id:271428) limit, when the wavelength of light becomes comparable to the [gravitational radius](@entry_id:1125749) of the lens ($R_S = 2GM/c^2$), diffraction effects become important and the magnification itself becomes frequency-dependent. This is a source of true, intrinsic chromaticity, though it is only relevant for extremely low-mass lenses observed at very long radio wavelengths.

### The Realm of Binary Lenses and Exoplanets

The most powerful application of microlensing is the detection of exoplanets. The presence of a planetary companion orbiting the primary lens star turns the single [point mass](@entry_id:186768) into a [binary lens](@entry_id:160834). This dramatically alters the lensing behavior, producing complex caustic structures that can lead to strong, short-lived anomalies in the light curve.

#### The Binary Lens Equation and Caustics

The [lens equation](@entry_id:161034) for a [binary system](@entry_id:159110) is the sum of the deflections from each component. Using complex notation, where $z = \theta_x/\theta_E + i\theta_y/\theta_E$ is the normalized image position and $\zeta$ is the normalized source position, the binary [lens equation](@entry_id:161034) is written as :
$$
\zeta = z - \sum_{j=1}^{2} \frac{\varepsilon_j}{\bar{z} - \bar{z}_j}
$$
Here, $\bar{z}$ is the [complex conjugate](@entry_id:174888), $z_j$ are the positions of the two masses, and $\varepsilon_j = M_j / M_{\mathrm{tot}}$ are their mass fractions. The system is described by the **[mass ratio](@entry_id:167674)**, $q = M_2/M_1$, and the projected **separation**, $s$, in units of the total system's Einstein radius $\theta_E$.

This mapping is no longer simple. There now exist [closed curves](@entry_id:264519) in the lens plane, called **[critical curves](@entry_id:203397)**, where the [magnification](@entry_id:140628) of an image formally diverges. The mapping of these [critical curves](@entry_id:203397) onto the source plane creates a set of **caustics**. When the source crosses a caustic, the number of images changes (typically by two), and the light curve exhibits a sharp, intense spike in magnification.

#### Planetary Perturbations

In the planetary regime ($q \ll 1$), the lens system consists of a dominant star and a small perturbing planet. The [caustics](@entry_id:158966) generated by such a system generally fall into two categories :
1.  **Central Caustic:** A small, [astroid](@entry_id:162907)-shaped caustic located near the primary star. It is a perturbation of the point caustic that would exist for the star alone. Its linear size scales with the [mass ratio](@entry_id:167674) as $\sim q$.
2.  **Planetary Caustics:** One or two caustics located further out, near the projected position of the planet. These arise from the planet's own lensing effect, perturbed by the shear from the host star. The size of these caustics is set by the planet's own Einstein radius, which scales as $\sqrt{q}$, making them significantly larger than the central caustic.

Because the source moves at a constant rate, the duration of an anomaly caused by a [caustic crossing](@entry_id:1122154) is proportional to the [caustic](@entry_id:164959)'s width. Anomalies from central [caustics](@entry_id:158966) have durations $\Delta t \sim q t_E$, while those from planetary [caustics](@entry_id:158966) have durations $\Delta t \sim \sqrt{q} t_E$. Since $q \ll 1$ for a planet, both types of anomalies are very short-lived compared to the overall event timescale $t_E$, appearing as brief, sharp deviations from a smooth PSPL curve.

#### The Close-Wide Degeneracy

A persistent challenge in interpreting planetary microlensing signals is the **close-wide degeneracy**. For a high-[magnification](@entry_id:140628) event, where the source trajectory passes near the central caustic, the shape of the resulting light curve anomaly is approximately invariant under the transformation $s \leftrightarrow 1/s$ . This means that a planet on a "close" projected orbit with separation $s  1$ can produce a nearly identical signal to a planet on a "wide" orbit with separation $1/s > 1$.

This degeneracy arises because, for $q \ll 1$, the [morphology](@entry_id:273085) of the central caustic depends primarily on the combination $|s-1/s|$. While the orientation of the [caustic](@entry_id:164959) is different (elongated along the binary axis for wide companions, perpendicular for close ones), this can be difficult to distinguish with a single source track. The degeneracy is most severe in idealized events where finite-source effects, planetary orbital motion, and parallax effects are negligible. Each of these second-order effects evolves differently for a close versus a wide orbit, and their detection is often key to resolving the ambiguity and correctly identifying the planet's true projected separation.