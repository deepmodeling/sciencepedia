## Introduction
Gravitational redshift is a cornerstone prediction of Albert Einstein's theory of general relativity, describing how light loses energy as it climbs out of a gravitational potential well. More than a mere curiosity, this phenomenon is a powerful diagnostic tool, allowing us to probe the most extreme environments in the universe, from the surfaces of neutron stars to the event horizons of black holes. This article bridges the gap between the abstract theory of [curved spacetime](@entry_id:184938) and its concrete application in modern astrophysics. It provides a comprehensive exploration of how measuring the stretching of light reveals the fundamental properties of [compact objects](@entry_id:157611) and tests the very laws of gravity.

The journey begins in the **Principles and Mechanisms** chapter, where we will rigorously derive the mathematical formalism for gravitational redshift from first principles, applying it to the spacetimes of various [compact objects](@entry_id:157611) like black holes and [neutron stars](@entry_id:139683). Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how astronomers use [redshift](@entry_id:159945) to characterize stellar properties, map [orbital dynamics](@entry_id:161870) in strong gravity, and even measure the expansion of the universe, while also exploring its surprising connections to fields like fluid dynamics. Finally, the **Hands-On Practices** section will offer you the chance to apply these concepts, guiding you through calculations that connect the internal structure of stars and the dynamics of [binary systems](@entry_id:161443) to the observable [redshift](@entry_id:159945).

This structure is designed to build a deep, intuitive, and practical understanding of [gravitational redshift](@entry_id:158697), transforming it from a theoretical concept into an applicable scientific instrument.

## Principles and Mechanisms

Gravitational [redshift](@entry_id:159945) is a direct and fundamental consequence of the [principle of equivalence](@entry_id:157518) and the [curvature of spacetime](@entry_id:189480). In essence, it is a manifestation of [gravitational time dilation](@entry_id:162143): clocks in a stronger gravitational field (deeper in a [potential well](@entry_id:152140)) run slower relative to clocks in a weaker field. When electromagnetic radiation travels from a region of stronger to weaker gravity, its frequency appears to decrease—and its wavelength to increase or "redshift"—to an observer in the weaker field. This is necessary to ensure that the total number of wave crests emitted is equal to the number received, preserving the integrity of the event despite the differential passage of time between the emitter and observer. This chapter will rigorously develop the principles governing this phenomenon and explore its mechanisms in the vicinity of various [compact objects](@entry_id:157611).

### The General Formalism of Redshift in a Static Spacetime

Let us consider a [stationary spacetime](@entry_id:755387), which is one that possesses a timelike Killing vector field, typically denoted as $\xi^\mu = (\partial_t)^\mu$. The existence of this symmetry implies that there is a conserved quantity for any particle moving along a geodesic. For a photon with [four-momentum](@entry_id:161888) $p^\mu$, this conserved quantity is its energy as measured by an observer at spatial infinity, $E_\infty$. This is given by the projection of the [four-momentum](@entry_id:161888) onto the Killing vector:

$$ E_\infty = -p_\mu \xi^\mu = -p_t $$

where $p_t = g_{t\nu}p^\nu$ is the time component of the covariant four-momentum.

The energy of this same photon as measured by an arbitrary local observer with four-velocity $U^\mu$ is given by $E_{\text{loc}} = -p_\mu U^\mu$. An observer is considered **static** if their [worldline](@entry_id:199036) follows the [integral curves](@entry_id:161858) of the Killing vector field, meaning their spatial velocity components are zero. For such an observer, the [four-velocity](@entry_id:274008) is of the form $U^\mu = (U^t, 0, 0, 0)$. The [normalization condition](@entry_id:156486) $U_\mu U^\mu = -c^2$ requires that $g_{\mu\nu}U^\mu U^\nu = g_{tt}(U^t)^2 = -c^2$. This allows us to solve for the time component of the static observer's [four-velocity](@entry_id:274008):

$$ U^t = \frac{c}{\sqrt{-g_{tt}}} $$

The local energy measured by this static observer is then:

$$ E_{\text{loc}} = -p_t U^t = E_\infty U^t = E_\infty \frac{c}{\sqrt{-g_{tt}}} $$

The frequency of the photon is directly proportional to its energy, $\nu = E/h$, where $h$ is Planck's constant. The [gravitational redshift](@entry_id:158697) $z$ is defined by the fractional change in wavelength, which is equivalent to the ratio of frequencies:

$$ 1+z = \frac{\lambda_{obs}}{\lambda_{em}} = \frac{\nu_{em}}{\nu_{obs}} = \frac{E_{em}}{E_{obs}} $$

If we consider a photon emitted by a static source at position 'e' and received by a static observer at position 'o', their locally measured energies are $E_{em}$ and $E_{obs}$, respectively. Using our derived relation between local and "at-infinity" energy, we have:

$$ E_{em} = \frac{E_\infty c}{\sqrt{-g_{tt}(r_e)}} \quad \text{and} \quad E_{obs} = \frac{E_\infty c}{\sqrt{-g_{tt}(r_o)}} $$

Substituting these into the [redshift](@entry_id:159945) definition, the conserved energy $E_\infty$ cancels, yielding the master formula for gravitational redshift between two static points in a [stationary spacetime](@entry_id:755387):

$$ 1+z = \frac{\sqrt{-g_{tt}(r_o)}}{\sqrt{-g_{tt}(r_e)}} $$

This powerful equation forms the basis for calculating gravitational redshift in a wide variety of astrophysical scenarios. Typically, the observer is assumed to be at a very large distance from the gravitational source ($r_o \to \infty$), where spacetime is asymptotically flat. In this limit, the metric approaches the Minkowski metric, and $g_{tt}(r_o \to \infty) \to -c^2$. The formula then simplifies to:

$$ 1+z = \frac{c}{\sqrt{-g_{tt}(r_e)}} $$

This demonstrates that the observed redshift is determined entirely by the time component of the metric at the point of emission.

### Redshift in Schwarzschild Spacetime

The simplest and most common application of this formalism is to the spacetime outside a static, spherically symmetric, uncharged body of mass $M$. This is described by the Schwarzschild metric, where the time component is:

$$ g_{tt}(r) = -c^2 \left(1 - \frac{2GM}{c^2r}\right) = -c^2 \left(1 - \frac{R_s}{r}\right) $$

where $R_s = 2GM/c^2$ is the Schwarzschild radius. For a photon emitted from a radius $r=R$ and observed at infinity, the redshift is:

$$ 1+z = \frac{c}{\sqrt{- \left(-c^2 \left(1 - \frac{2GM}{c^2R}\right)\right)}} = \frac{1}{\sqrt{1 - \frac{2GM}{c^2R}}} $$

Thus, the [redshift](@entry_id:159945) parameter $z$ is:

$$ z = \left(1 - \frac{2GM}{c^2R}\right)^{-1/2} - 1 $$

This is the classic formula for gravitational redshift from a compact object. Note that as the emission radius $R$ approaches the Schwarzschild radius $R_s$, the redshift approaches infinity.

An alternative and physically insightful derivation of this same result can be found by considering the [conservation of energy](@entry_id:140514). Imagine a particle-antiparticle pair, each with rest mass $m$, at rest at a radius $R$. Their total energy, as measured by a local static observer, is $2mc^2$. However, their contribution to the total conserved energy of the system (the energy at infinity) is reduced by the gravitational potential. This conserved energy is $E_{\text{total}, \infty} = 2mc^2 \sqrt{1 - 2GM/c^2R}$. If the pair annihilates into two photons, this total energy is conserved. If one photon travels towards the black hole and one travels outwards to a distant observer, the outward photon carries an energy $E_{\text{photon}, \infty} = mc^2 \sqrt{1 - 2GM/c^2R}$ to infinity. The energy of the photon at the point of emission, as measured locally, was simply $E_{\text{photon}, R} = mc^2$. The [redshift](@entry_id:159945) is the ratio of these energies (or frequencies), which again yields $1+z = E_{R}/E_{\infty} = (1-2GM/c^2R)^{-1/2}$ [@problem_id:216849].

While [redshift](@entry_id:159945) is often discussed as a phenomenon measured over vast distances, it is fundamentally a local effect. The [gravitational potential](@entry_id:160378) varies continuously with position, meaning there is a differential [redshift](@entry_id:159945) even between infinitesimally separated points. Consider a small, rigid rod of [proper length](@entry_id:180234) $L$ held radially in a Schwarzschild spacetime, with its inner end at radius $r$. The [proper length](@entry_id:180234) is related to the coordinate separation $dr$ by $L = \int \sqrt{g_{rr}} dr \approx \sqrt{g_{rr}} dr$. A photon traveling from the inner end to the outer end will experience a small [redshift](@entry_id:159945). By applying a first-order Taylor expansion to the [redshift](@entry_id:159945) formula, one can show that this differential [redshift](@entry_id:159945) $z_{diff}$ is approximately [@problem_id:216944]:

$$ z_{diff} \approx \frac{g L}{c^2} = \frac{R_s L}{2r^2 \sqrt{1 - R_s/r}} $$

Here, $g$ represents the local gravitational acceleration. This result beautifully connects the relativistic concept of [redshift](@entry_id:159945) to the more intuitive Newtonian idea of gravitational force, demonstrating that the magnitude of the redshift over a small distance is a direct measure of the local field strength.

### Redshift from Stellar Models

The Schwarzschild solution describes the vacuum spacetime outside a spherical mass. To understand [redshift](@entry_id:159945) from photons originating within a star, we must use an interior solution that accounts for the distribution of matter and pressure.

A simple but instructive model is that of an incompressible fluid star, where the density $\rho$ is constant. The spacetime inside such a star ($r \le R$) is described by the interior Schwarzschild metric. For a photon emitted from the very center of the star ($r=0$) and observed at infinity, we must match the interior metric at $r=0$ with the exterior metric at $r \to \infty$. The relevant component of the interior metric is:

$$ -g_{tt}(r) = c^2 \left[ \frac{3}{2} \sqrt{1 - \frac{2GM}{Rc^2}} - \frac{1}{2} \sqrt{1 - \frac{2GM r^2}{R^3 c^2}} \right]^2 $$

Evaluating this at the center ($r=0$) and applying the general redshift formula gives the [redshift](@entry_id:159945) for a photon originating from the core [@problem_id:216766]:

$$ z_{center} = \frac{2}{3 \sqrt{1 - 2GM/Rc^2} - 1} - 1 = \frac{3\left(1 - \sqrt{1 - \frac{2GM}{Rc^2}}\right)}{3\sqrt{1 - \frac{2GM}{Rc^2}} - 1} $$

This result depends sensitively on the star's **compactness**, the dimensionless ratio $X = 2GM/Rc^2$. This compactness cannot be arbitrarily large. A fundamental result in general relativity, **Buchdahl's theorem**, places a limit on the maximum compactness of any static, spherically symmetric fluid star under reasonable physical assumptions (namely, that the energy density does not increase outwards). The limit is found by requiring that the pressure inside the star remain finite. For the incompressible fluid model, the pressure at the center would become infinite if the denominator in the pressure equation, $3\sqrt{1-X} - 1$, becomes zero. This leads to the famous Buchdahl limit:

$$ \frac{2GM}{Rc^2} \le \frac{8}{9} $$

This constraint on the maximum possible compactness of any static star implies a corresponding limit on the maximum observable surface [redshift](@entry_id:159945). Substituting $X_{max} = 8/9$ into the standard surface [redshift](@entry_id:159945) formula gives [@problem_id:216751]:

$$ z_{max} = \left(1 - \frac{8}{9}\right)^{-1/2} - 1 = (1/9)^{-1/2} - 1 = 3 - 1 = 2 $$

Thus, no static, spherically symmetric object satisfying the conditions of Buchdahl's theorem can have a surface [redshift](@entry_id:159945) greater than 2. This represents a profound connection between the internal structure of stars and an external observable.

More sophisticated models can include effects such as pressure anisotropy, where the radial pressure differs from the tangential pressure ($p_r \neq p_t$). Such conditions may arise in stars with strong magnetic fields or those composed of exotic matter. The redshift in these cases is modified, as the metric component $g_{tt}$ depends on the specific equation of state. For a hypothetical model parameterized by an anisotropy constant $\lambda$, the surface redshift might take the form $z = (1-u)^{-(1-2\lambda)/2} - 1$, where $u$ is the compactness [@problem_id:216882]. This illustrates that gravitational redshift can, in principle, be a valuable tool for probing the internal physics of [compact objects](@entry_id:157611).

### Effects of Rotation, Charge, and Asphericity

Real astrophysical objects are not always uncharged, non-rotating spheres. These additional properties alter the [spacetime geometry](@entry_id:139497) and, consequently, the [gravitational redshift](@entry_id:158697).

For a charged, non-rotating black hole described by the Reissner-Nordström metric, the term $g_{tt}$ is modified by the charge $Q$. The presence of charge adds a repulsive gravitational effect, weakening the [potential well](@entry_id:152140) compared to a Schwarzschild black hole of the same mass. This results in a lower gravitational redshift for a photon emitted from the same coordinate radius.

Rotation has a more complex and significant impact. The spacetime around a rotating object is described by the Kerr metric. A key feature of the Kerr metric is its dependence on the polar angle $\theta$, even for the time component $g_{tt}$, due to the rotation-induced oblateness of the spacetime itself. In Boyer-Lindquist coordinates, the function $\rho^2 = r^2 + a^2\cos^2\theta$ appears in the denominator of the potential term, where $a$ is the spin parameter.

Even for a static source, the redshift depends on its latitude. Let us compare a source at the pole ($\theta=0$) with one at the equator ($\theta=\pi/2$), both at the same coordinate radius $r$. At the pole, $\rho^2 = r^2+a^2$, while at the equator, $\rho^2 = r^2$. This leads to different [redshift](@entry_id:159945) values [@problem_id:216852]:

$$ z_{pole} = \left(1 - \frac{2GMr}{c^2(r^2+a^2)}\right)^{-1/2} - 1 $$
$$ z_{eq} = \left(1 - \frac{2GM}{c^2r}\right)^{-1/2} - 1 $$

The difference $\Delta z = z_{pole} - z_{eq}$ is negative, meaning the [redshift](@entry_id:159945) is greater at the equator than at the pole for the same coordinate radius $r$. This is because the spacetime is "squashed" by the rotation, making the gravitational potential well effectively deeper at the equator. This effect is not limited to black holes. Any rotating body, such as a star or white dwarf, becomes oblate and develops a [mass quadrupole moment](@entry_id:158661) ($J_2$). In a [weak-field approximation](@entry_id:182220), this leads to a latitude-dependent surface [redshift](@entry_id:159945). The difference in redshift between the equator and the pole can be shown to be proportional to the star's compactness, its [ellipticity](@entry_id:199972) $\epsilon_s$, and a factor related to its internal structure [@problem_id:217000], providing a potential method for measuring the shape and internal makeup of distant stars.

### Combining Gravitational and Doppler Shifts

In the most general astrophysical scenarios, the light source is not static but in motion relative to the local spacetime fabric. An orbiting star, for example, experiences both [gravitational redshift](@entry_id:158697) due to the central object's potential and a special relativistic Doppler shift due to its own motion. The total observed [redshift](@entry_id:159945) is a combination of these two effects.

The total redshift is still given by $1+z = \nu_{em}/\nu_{obs}$, but now we must carefully evaluate the emitted and observed frequencies using the four-velocities of both the emitter and the observer. The observed frequency for a distant static observer is $\nu_{obs} = -p_t/h$. The emitted frequency, in the rest frame of the moving source with four-velocity $U^\mu_{em}$, is $\nu_{em} = -p_\mu U^\mu_{em} / h$.

Consider a particle with orbital speed $v$ in a circular orbit at radius $r_0$ around a Reissner-Nordström black hole. The local stationary frame is defined by Zero Angular Momentum Observers (ZAMOs). The particle moves with speed $v$ relative to these ZAMOs. The total [redshift](@entry_id:159945) measured by a distant observer is the product of two factors: (1) the purely gravitational redshift between the ZAMO at $r_0$ and the distant observer, and (2) the special relativistic Doppler shift (transverse and longitudinal) between the moving particle and the local ZAMO, captured by the Lorentz factor $\gamma = (1-v^2/c^2)^{-1/2}$. The combined result for a photon emitted radially outward is [@problem_id:216748]:

$$ 1+z = \frac{\gamma}{\sqrt{f(r_0)}} = \frac{1}{\sqrt{\left(1-\frac{v^2}{c^2}\right)\left(1-\frac{2GM}{c^2r_0}+\frac{GQ^2}{c^4r_0^2}\right)}} $$

This expression elegantly combines the kinematic effect of motion (in the numerator via $\gamma$) and the gravitational effect of the potential (in the denominator via $\sqrt{f(r_0)}$).

When the observer is also in motion, or when the photon is emitted at an arbitrary angle, the calculation becomes more intricate, involving the photon's conserved angular momentum $L$ as well as its energy $E$. For instance, for a photon emitted at an angle $\alpha$ from a stationary source and observed by a body in a [stable circular orbit](@entry_id:172394), the redshift depends on the source radius $r_S$, the emission angle $\alpha$, the observer's orbital radius, and the black hole's parameters. The observed frequency becomes $\nu_{obs} \propto (E - \Omega L)$, where $\Omega$ is the observer's [angular velocity](@entry_id:192539). This leads to a complex expression for [redshift](@entry_id:159945) that encodes detailed information about the geometry of the photon's path and the dynamics of both the source and observer [@problem_id:216953]. Analyzing such combined redshifts is a crucial technique in modern astrophysics for mapping spacetime geometry and measuring the parameters of [compact objects](@entry_id:157611).