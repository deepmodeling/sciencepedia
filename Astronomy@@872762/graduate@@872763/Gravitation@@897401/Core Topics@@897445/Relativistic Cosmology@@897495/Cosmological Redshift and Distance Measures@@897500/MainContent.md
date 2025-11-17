## Introduction
Our understanding of the universe's vast scale, history, and ultimate fate rests on a single, fundamental challenge: accurately measuring cosmic distances. While straightforward in our static, everyday experience, this task becomes profoundly complex in an expanding cosmos where the very fabric of space is stretching. The key observable that unlocks this cosmic puzzle is the [cosmological redshift](@entry_id:152343)—the systematic stretching of light from distant galaxies. However, translating this redshift into a meaningful distance is not trivial and requires a sophisticated theoretical framework. This article addresses this challenge by providing a comprehensive guide to [cosmological redshift](@entry_id:152343) and the suite of [distance measures](@entry_id:145286) used in [modern cosmology](@entry_id:752086). The following chapters will first delve into the fundamental **Principles and Mechanisms**, explaining what redshift is and defining the crucial concepts of comoving, luminosity, and [angular diameter distance](@entry_id:157817). Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these tools are used to map the universe's expansion, discover [dark energy](@entry_id:161123), and test the limits of General Relativity. Finally, a series of **Hands-On Practices** will allow readers to apply these concepts to realistic cosmological scenarios. We begin by exploring the foundational principles that link the observed redshift of a photon to the dynamic history of the universe itself.

## Principles and Mechanisms

The observation that light from distant galaxies is systematically shifted towards longer wavelengths—the cosmological redshift—is a cornerstone of modern cosmology. It is the primary evidence for the expansion of the universe and serves as the fundamental observable for mapping the cosmos in three spatial dimensions and one temporal dimension. This chapter delves into the principles governing cosmological redshift and the associated measures of distance, which together form the quantitative framework for probing the history, geometry, and composition of the universe.

### The Nature of Cosmological Redshift

At its most fundamental level, cosmological redshift, denoted by the symbol $z$, is an observational quantity derived from spectroscopy. It is defined as the fractional shift in the wavelength of light between its emission and observation. If a spectral line has a known wavelength $\lambda_{\text{rest}}$ as measured in a laboratory frame (the "rest frame" of the emitter), and it is observed at a wavelength $\lambda_{\text{obs}}$, the [redshift](@entry_id:159945) is given by:

$$ z = \frac{\lambda_{\text{obs}} - \lambda_{\text{rest}}}{\lambda_{\text{rest}}} $$

This can be conveniently rewritten as:

$$ 1 + z = \frac{\lambda_{\text{obs}}}{\lambda_{\text{rest}}} $$

For instance, if the Lyman-alpha emission line of hydrogen, with a rest wavelength of $\lambda_{\text{rest}} = 121.6 \text{ nm}$, is observed in a distant galaxy's spectrum at $\lambda_{\text{obs}} = 512.1 \text{ nm}$, the [redshift](@entry_id:159945) of this galaxy would be $z = (512.1/121.6) - 1 \approx 3.21$ [@problem_id:1819953]. A positive value of $z$ indicates a shift to longer wavelengths (a [redshift](@entry_id:159945)), while a hypothetical negative value would indicate a [blueshift](@entry_id:274414).

While this definition is operational, its physical origin within the [standard cosmological model](@entry_id:159833) is not a Doppler effect in the classical sense. Rather, **cosmological redshift** is a direct consequence of the expansion of space itself. The wavelength of a photon traveling through an [expanding universe](@entry_id:161442) is stretched in direct proportion to the growth of the cosmic **[scale factor](@entry_id:157673)**, $a(t)$. If a photon is emitted at a cosmic time $t_e$ when the scale factor is $a(t_e)$ and observed at a later time $t_0$ when the scale factor is $a(t_0)$, the relationship between the wavelengths is:

$$ \frac{\lambda_{\text{obs}}}{\lambda_{\text{rest}}} = \frac{a(t_0)}{a(t_e)} $$

Combining this with the definition of [redshift](@entry_id:159945), we arrive at the fundamental relation:

$$ 1 + z = \frac{a(t_0)}{a(t_e)} $$

By convention, the scale factor today is normalized to unity, $a(t_0) = 1$, which simplifies the relation to $1+z = 1/a(t_e)$. Thus, observing an object at redshift $z$ is equivalent to looking back in time to an epoch when the universe was a factor of $1/(1+z)$ smaller than it is today.

This expansion affects not only the wavelength of light but also the observed rate of time flow. An event that unfolds over an intrinsic time interval $\Delta t_{\text{int}}$ in the source's rest frame will be observed to last for a longer duration, $\Delta t_{\text{obs}}$, due to **[cosmological time dilation](@entry_id:269734)**. The relationship is directly proportional to the stretching of wavelength:

$$ \Delta t_{\text{obs}} = (1+z) \Delta t_{\text{int}} $$

This effect is readily observable. For example, the characteristic brightening and fading time of a Type Ia [supernova](@entry_id:159451) at [redshift](@entry_id:159945) $z = 1.25$ will appear to us to be $1+1.25 = 2.25$ times longer than for a similar supernova in our local vicinity [@problem_id:1862790].

It is crucial to distinguish cosmological redshift from other sources of redshift, such as the kinematic **Doppler redshift** due to peculiar velocities of galaxies relative to the smooth "Hubble flow," and **gravitational redshift** caused by photons climbing out of a gravitational potential well. These effects can be superimposed. For a photon emitted from the surface of a massive object like a [white dwarf](@entry_id:146596) ($z_g$) residing in a distant galaxy ($z_c$), the total observed [redshift](@entry_id:159945) is a composition of these effects. The $(1+z)$ factors, which represent the total stretching, multiply. The total redshift $z_{\text{total}}$ is therefore given by:

$$ 1 + z_{\text{total}} = (1 + z_c)(1 + z_g) $$

where $z_g$ is the gravitational redshift. For a spherical object of mass $M$ and radius $R$, general relativity predicts $1+z_g = (1 - 2GM/Rc^2)^{-1/2}$. Thus, the total measured redshift combines both local physics and global cosmology [@problem_id:1858876].

### Hubble's Law and the Expanding Universe

For nearby galaxies, where the redshift $z$ is small ($z \ll 1$), the cosmological framework simplifies to a more intuitive picture. In this regime, the recession velocity $v$ of a galaxy can be related to its [redshift](@entry_id:159945) through the first-order Doppler approximation, $z \approx v/c$. In the 1920s, Edwin Hubble discovered a linear relationship between the recession velocities of galaxies and their distances $d$:

$$ v = H_0 d $$

This is **Hubble's Law**, and $H_0$ is the **Hubble constant**, representing the rate of expansion of the universe at the present day. Its value is typically expressed in units of (km/s)/Mpc. Combining these two relations gives the low-redshift version of the Hubble-Lemaître law:

$$ c z \approx H_0 d $$

This law is a direct manifestation of a homogeneous and isotropic expansion. The **Cosmological Principle**, which asserts that the universe looks the same in all directions (isotropy) and from all locations (homogeneity) on large scales, has a profound consequence: every observer in any galaxy will see all other galaxies receding from them according to the same Hubble's Law. If an astronomer in the Milky Way observes a galaxy 100 Mpc away receding at 7000 km/s (assuming $H_0 = 70 \text{ (km/s)/Mpc}$), an astronomer in that galaxy would measure the Milky Way receding from them at the very same speed of 7000 km/s, corresponding to the same redshift $z \approx 0.0233$ [@problem_id:1862778]. There is no "center" to the expansion; it is an expansion of space itself.

### A Rigorous Definition of Cosmological Distance

While Hubble's Law provides a simple picture for the local universe, the relationship between distance and [redshift](@entry_id:159945) becomes more complex for distant objects. The very notion of "distance" in an expanding universe requires careful definition. The most fundamental measure is the **[comoving distance](@entry_id:158059)**, $\chi$. This is a distance measured in a coordinate system that expands along with the universe, so the [comoving distance](@entry_id:158059) between two galaxies that are only moving with the Hubble flow remains constant over time.

For a photon traveling along a radial path from a source to an observer at the origin, the Friedmann-Lemaître-Robertson-Walker (FLRW) metric tells us that it follows a [null geodesic](@entry_id:261630) ($ds^2 = 0$). This leads to the definition of the [comoving distance](@entry_id:158059) to an object that emitted light at time $t_e$ that we receive today at $t_0$:

$$ \chi = \int_{t_e}^{t_0} \frac{c}{a(t)} dt $$

To express this distance as a function of the observable redshift $z$, we must change the integration variable from time $t$ to scale factor $a$. Using the definition of the Hubble parameter, $H = \dot{a}/a$, we have $dt = \frac{da}{\dot{a}} = \frac{da}{aH(a)}$. Furthermore, $a = (1+z)^{-1}$, so $da = -(1+z)^{-2} dz$. This allows us to write:

$$ \chi(z) = c \int_{0}^{z} \frac{dz'}{H(z')} $$

where $H(z)$ describes the expansion rate as a function of [redshift](@entry_id:159945). The form of $H(z)$ is determined by the energy content of the universe via the Friedmann equation. For a spatially flat, [matter-dominated universe](@entry_id:158254) (the "Einstein-de Sitter" model), the Friedmann equation gives $H(z) = H_0(1+z)^{3/2}$. Integrating this yields a specific [distance-redshift relation](@entry_id:159875) [@problem_id:1860458]:

$$ \chi(z) = \frac{2c}{H_0} \left(1 - \frac{1}{\sqrt{1+z}}\right) $$

This explicit formula highlights the non-linear relationship between distance and redshift at high $z$. For instance, in such a universe, if galaxy G2 is at twice the current proper distance (which for a [flat universe](@entry_id:183782) is equal to the [comoving distance](@entry_id:158059), $D_0 = \chi$) of galaxy G1, its redshift $z_2$ is not simply twice $z_1$. Instead, it is given by a more complex relation derived from setting $\chi(z_2) = 2\chi(z_1)$ [@problem_id:1862787]. This non-linearity is a key feature of [cosmological models](@entry_id:161416) and allows us to test them against observations.

### Observational Distance Measures: Luminosity and Angular Diameter Distance

Comoving distance is a theoretical construct. In practice, astronomers measure distances using observable properties like brightness and apparent size. These measurements lead to the definitions of two other essential [distance measures](@entry_id:145286): the [luminosity distance](@entry_id:159432) and the [angular diameter distance](@entry_id:157817).

The **[luminosity distance](@entry_id:159432)**, $d_L$, is defined to preserve the familiar [inverse-square law](@entry_id:170450) for flux from a static Euclidean space. For a source of known intrinsic luminosity $L$, the measured flux $F$ defines $d_L$ as:

$$ F = \frac{L}{4 \pi d_L^2} $$

In an expanding FRW universe, the flux is diminished for two reasons beyond the geometric spreading of light. First, each photon's energy is reduced by a factor of $(1+z)$ due to redshift. Second, the rate of photon arrival is decreased by a factor of $(1+z)$ due to [cosmological time dilation](@entry_id:269734). This results in the total power received being suppressed by $(1+z)^2$. Accounting for this and the proper area of the sphere of light at the observer, which is $4\pi(a_0 S_k(\chi))^2$, one can derive the general relationship [@problem_id:1834134]:

$$ d_L = a_0(1+z) S_k(\chi) $$

Here, $a_0$ is the scale factor today (usually 1), and $S_k(\chi)$ is a function that depends on the [spatial curvature](@entry_id:755140) $k$. $S_k(\chi)$ is $\sin(\chi)$ for a closed universe ($k=+1$), $\chi$ for a [flat universe](@entry_id:183782) ($k=0$), and $\sinh(\chi)$ for an open universe ($k=-1$), assuming $\chi$ is scaled appropriately.

The **[angular diameter distance](@entry_id:157817)**, $d_A$, is defined by the relationship between an object's proper physical size $l$ (transverse to the line of sight) and its apparent [angular size](@entry_id:195896) $\delta\theta$ on the sky:

$$ \delta\theta = \frac{l}{d_A} $$

The object's size $l$ is measured at the time of light emission, $t_e$, where the [proper length](@entry_id:180234) corresponding to an angle $\delta\theta$ at [comoving distance](@entry_id:158059) $\chi$ is $l = a(t_e) S_k(\chi) \delta\theta$. This immediately gives the definition:

$$ d_A = a(t_e) S_k(\chi) $$

By combining the expressions for [luminosity distance](@entry_id:159432) and [angular diameter distance](@entry_id:157817), we can find a remarkably simple and powerful relationship between them. Using $a(t_e) = a_0 / (1+z)$, we have:

$$ d_L = a_0(1+z) S_k(\chi) = (1+z) [a_0 S_k(\chi)] = (1+z) \left[\frac{a_0}{a(t_e)} d_A\right] = (1+z)^2 d_A $$

This result, $d_L = (1+z)^2 d_A$, is known as the **Etherington [reciprocity relation](@entry_id:198404)** or distance duality. It is a fundamental consequence of the geometry of spacetime in any metric theory of gravity where photons travel on [null geodesics](@entry_id:158803) and photon number is conserved. Its validity is independent of the specific dynamics of the universe's expansion or its energy content [@problem_id:1019279].

### Probing Cosmic Expansion with Standard Candles

The [luminosity distance](@entry_id:159432) is of paramount practical importance because certain classes of astronomical objects, such as Type Ia [supernovae](@entry_id:161773), can be used as **[standard candles](@entry_id:158109)**—objects of known intrinsic luminosity $L$. By measuring the [apparent magnitude](@entry_id:158988) $m$ of a supernova and knowing its [absolute magnitude](@entry_id:157959) $M$ (related to $L$), one can determine its [luminosity distance](@entry_id:159432) using the [distance modulus](@entry_id:160114) equation:

$$ m - M = 5 \log_{10} \left( \frac{d_L}{10 \text{ pc}} \right) $$

Plotting the measured [apparent magnitude](@entry_id:158988) (or [distance modulus](@entry_id:160114)) against redshift for a sample of [supernovae](@entry_id:161773) creates a Hubble diagram. The shape of this diagram directly probes the [expansion history of the universe](@entry_id:162026), $H(z)$, because $d_L$ depends on the integral of $1/H(z)$.

For small redshifts, we can Taylor expand the [luminosity distance](@entry_id:159432):

$$ d_L(z) = \frac{c}{H_0} \left( z + \frac{1}{2}(1-q_0)z^2 + \mathcal{O}(z^3) \right) $$

The first-order term is simply Hubble's Law. The second-order term depends on the **deceleration parameter**, $q_0 = - \frac{\ddot{a}a}{\dot{a}^2}\Big|_{t_0}$, which measures the acceleration of the universe's expansion today. A positive $q_0$ implies deceleration (as expected from gravity), while a negative $q_0$ implies acceleration. By fitting observational data to an [empirical formula](@entry_id:137466), for example $m(z) \approx A + 5 \log_{10}(z) + B z$, we can directly relate the measured coefficient $B$ of the linear term in $z$ to the deceleration parameter $q_0$. This analysis reveals that $q_0 = 1 - \frac{2 \ln 10}{5} B$ [@problem_id:1820650]. It was precisely this type of analysis in the late 1990s that led to the astonishing discovery that the universe's expansion is accelerating ($q_0  0$), driven by a mysterious component known as dark energy.

### The Dynamic Redshift: A Real-Time Probe of Expansion

The redshift of a comoving source is not eternally fixed. As the universe continues to evolve, the expansion rate $H(z)$ changes, and this should lead to a small, real-time drift in the observed redshift of any given object. This effect, known as the **[redshift](@entry_id:159945) drift** or the Sandage-Loeb test, is a direct probe of the dynamics of the universe.

We can calculate the expected rate of change of redshift, $\dot{z} \equiv dz/dt_0$, by differentiating the definition $1+z = a(t_0)/a(t_e)$ with respect to the observer's time $t_0$. Using the [chain rule](@entry_id:147422), we find:

$$ \frac{\dot{z}}{1+z} = \frac{\dot{a}(t_0)}{a(t_0)} - \frac{\dot{a}(t_e)}{a(t_e)} \frac{dt_e}{dt_0} = H_0 - H(t_e) \frac{dt_e}{dt_0} $$

The derivative $dt_e/dt_0$ relates the change in emission time to a change in observation time for a fixed comoving source. Since the [comoving distance](@entry_id:158059) is constant, the light travel time relationship implies $dt_e/dt_0 = a(t_e)/a(t_0) = 1/(1+z)$. Substituting this back gives:

$$ \dot{z} = (1+z)H_0 - H(t_e) $$

Using the Friedmann equation to express $H(t_e) = H(z)$ in terms of present-day [cosmological parameters](@entry_id:161338) ($\Omega_{m,0}, \Omega_{r,0}, \Omega_{\Lambda,0}, \Omega_{k,0}$), we obtain a precise prediction for the [redshift](@entry_id:159945) drift [@problem_id:885205]:

$$ \dot{z}(z) = H_0(1+z) - H_0 \sqrt{\Omega_{m,0}(1+z)^3 + \Omega_{r,0}(1+z)^4 + \Omega_{k,0}(1+z)^2 + \Omega_{\Lambda,0}} $$

Measuring this effect is observationally formidable, as it predicts a change in velocity of only a few cm/s over a decade. However, future extremely large telescopes and advanced spectrographs may be able to detect this drift, offering a unique, direct measurement of the universe's expansion history in real time, completely independent of the [cosmological distance](@entry_id:270927) ladder. This would provide a powerful test of our entire cosmological model.