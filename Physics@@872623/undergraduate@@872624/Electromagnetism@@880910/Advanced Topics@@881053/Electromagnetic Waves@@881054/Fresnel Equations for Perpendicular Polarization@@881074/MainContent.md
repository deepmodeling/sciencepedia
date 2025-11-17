## Introduction
The [reflection and transmission](@entry_id:156002) of light at the boundary between two different media are among the most fundamental phenomena in optics. These interactions govern everything from the appearance of a simple reflection in a window to the operation of complex technologies like fiber optic cables and advanced microscopes. To move beyond qualitative descriptions, a rigorous quantitative framework is required. This framework is provided by the Fresnel equations, which precisely describe the amplitude and intensity of reflected and transmitted electromagnetic waves.

This article provides a focused exploration of the Fresnel equations for a specific but crucial case: perpendicular or s-polarized light, where the electric field oscillates perpendicular to the plane of incidence. By isolating this polarization, we can uncover its unique behaviors and build a solid foundation for understanding more complex polarization effects. We will bridge the gap between the abstract theory of Maxwell's equations and observable optical phenomena.

You will learn how to derive the core equations from first principles, analyze the flow of energy across an interface, and explore the fascinating consequences of these laws. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, deriving the coefficients for [reflection and transmission](@entry_id:156002) and examining key scenarios like [normal incidence](@entry_id:260681) and [total internal reflection](@entry_id:267386). The second chapter, **Applications and Interdisciplinary Connections**, showcases the immense practical utility of these equations, explaining everything from the nature of glare and the design of anti-reflection coatings to the operation of [optical fibers](@entry_id:265647) and the surprising analogies with quantum mechanics. Finally, the **Hands-On Practices** section allows you to solidify your understanding by applying these concepts to solve concrete problems.

The journey begins with the fundamental physics governing the wave's interaction at the boundary.

## Principles and Mechanisms

This chapter elucidates the fundamental principles governing the [reflection and transmission](@entry_id:156002) of s-polarized electromagnetic waves at a dielectric interface. Building upon the foundational Maxwell's equations and the associated boundary conditions, we will derive and analyze the Fresnel equations for [perpendicular polarization](@entry_id:261458), explore the implications for energy conservation, and examine the rich phenomena that arise in different physical scenarios, including total internal reflection.

### Derivation of the Fresnel Equations for s-Polarization

Let us consider a [monochromatic plane wave](@entry_id:263295) propagating in a linear, non-magnetic, dielectric medium with refractive index $n_1$. The wave is incident upon a planar interface at $z=0$, which separates it from a second medium of refractive index $n_2$. We define the plane of incidence as the $xz$-plane. For **[s-polarization](@entry_id:262966)**, also known as transverse electric (TE) polarization, the electric field vector $\vec{E}$ is perpendicular to the plane of incidence, and thus oscillates along the $y$-axis.

The interaction at the boundary gives rise to a reflected wave and a transmitted (or refracted) wave. The electric fields of the incident ($I$), reflected ($R$), and transmitted ($T$) waves at the interface can be described by their complex amplitudes $E_{0,I}$, $E_{0,R}$, and $E_{0,T}$. The behavior of these fields is governed by the boundary conditions of electromagnetism. At an interface between two [dielectrics](@entry_id:145763) with no free charges or surface currents, the tangential components of the electric field $\vec{E}$ and the magnetic field $\vec{H}$ must be continuous across the boundary.

First, let us apply the continuity of the tangential component of $\vec{E}$. Since the electric fields for [s-polarization](@entry_id:262966) are entirely tangential to the interface (oriented along the $y$-axis), the total electric field in medium 1 at $z=0$ must equal the total electric field in medium 2 at $z=0$. This yields the relation:

$E_{0,I} + E_{0,R} = E_{0,T}$

This simple but powerful equation provides a direct link between the three electric field amplitudes. By dividing by the incident amplitude $E_{0,I}$, we can express this in terms of the **[amplitude reflection coefficient](@entry_id:171753)** ($r_s = E_{0,R} / E_{0,I}$) and the **[amplitude transmission coefficient](@entry_id:165894)** ($t_s = E_{0,T} / E_{0,I}$). This gives the fundamental relationship [@problem_id:1799967]:

$1 + r_s = t_s$

To find a unique solution for $r_s$ and $t_s$, we must invoke the second boundary condition: the continuity of the tangential component of $\vec{H}$. For a plane wave in a non-magnetic medium, the magnetic field amplitude $B$ is related to the electric field amplitude $E$ by $B = (n/c)E$, and the magnetic field vector $\vec{B}$ is perpendicular to both the electric field vector $\vec{E}$ and the wave vector $\vec{k}$. For [s-polarization](@entry_id:262966), $\vec{E}$ is along the $y$-axis, so $\vec{B}$ (and thus $\vec{H} = \vec{B}/\mu_0$) lies in the $xz$-plane.

The tangential component of the magnetic field lies along the $x$-axis. Projecting the magnetic field vectors of the incident, reflected, and transmitted waves onto the $x$-axis requires careful consideration of their geometry. Denoting the angle of incidence as $\theta_i$ and the angle of transmission as $\theta_t$, the continuity of tangential $\vec{H}$ leads to the equation [@problem_id:1582916]:

$n_1 (E_{0,I} - E_{0,R}) \cos\theta_i = n_2 E_{0,T} \cos\theta_t$

We now have a system of two linear equations for the amplitudes. Substituting $E_{0,T} = E_{0,I} + E_{0,R}$ into the second equation and rearranging to solve for the ratio $r_s = E_{0,R}/E_{0,I}$ yields the Fresnel equation for the s-polarized [amplitude reflection coefficient](@entry_id:171753):

$r_s = \frac{n_1 \cos\theta_i - n_2 \cos\theta_t}{n_1 \cos\theta_i + n_2 \cos\theta_t}$

Using the relation $t_s = 1 + r_s$, we can similarly solve for the [amplitude transmission coefficient](@entry_id:165894):

$t_s = \frac{2 n_1 \cos\theta_i}{n_1 \cos\theta_i + n_2 \cos\theta_t}$

These two equations are the cornerstone of this chapter. They describe the amplitude and phase of the reflected and transmitted waves for any pair of non-magnetic dielectric media and any angle of incidence. By applying Snell's Law, $n_1 \sin\theta_i = n_2 \sin\theta_t$, it is possible to eliminate the refractive indices from the expression for $r_s$ and express it purely in terms of the angles of incidence and transmission. This leads to a historically important and elegant alternative form [@problem_id:1582879]:

$r_s = - \frac{\sin(\theta_i - \theta_t)}{\sin(\theta_i + \theta_t)}$

### Reflectance, Transmittance, and Conservation of Energy

While the amplitude coefficients $r_s$ and $t_s$ describe the behavior of the fields, a more practical concern is often the flow of energy. The **reflectance** $R_s$ is the fraction of incident power that is reflected, and the **[transmittance](@entry_id:168546)** $T_s$ is the fraction that is transmitted.

The power per unit area carried by an electromagnetic wave is given by the time-averaged Poynting vector, whose magnitude (the intensity, $I$) is proportional to $n E_0^2$, where $n$ is the refractive index and $E_0$ is the real electric field amplitude. To calculate the total power crossing the interface, we must consider the cross-sectional area of the beams. A beam of cross-sectional area $A$ incident at an angle $\theta_i$ illuminates an area $A/\cos\theta_i$ on the interface. The reflected and transmitted beams originate from this same area. Therefore, the power flowing across a unit area of the interface is $I \cos\theta$.

The [reflectance](@entry_id:172768) $R_s$ is the ratio of reflected power to incident power:

$R_s = \frac{I_R \cos\theta_i}{I_I \cos\theta_i} = \frac{n_1 E_{0,R}^2}{n_1 E_{0,I}^2} = \left(\frac{E_{0,R}}{E_{0,I}}\right)^2 = r_s^2$

The [transmittance](@entry_id:168546) $T_s$, however, is more subtle. It involves a change in both the medium and the beam's projection angle [@problem_id:1799981].

$T_s = \frac{I_T \cos\theta_t}{I_I \cos\theta_i} = \frac{n_2 E_{0,T}^2 \cos\theta_t}{n_1 E_{0,I}^2 \cos\theta_i} = \left(\frac{n_2 \cos\theta_t}{n_1 \cos\theta_i}\right) \left(\frac{E_{0,T}}{E_{0,I}}\right)^2 = \left(\frac{n_2 \cos\theta_t}{n_1 \cos\theta_i}\right) t_s^2$

The factor $\frac{n_2 \cos\theta_t}{n_1 \cos\theta_i}$ corrects for the change in medium impedance and the geometric projection of the [energy flux](@entry_id:266056). A common error is to assume $T_s = t_s^2$, which neglects these crucial physical effects. For non-absorbing media, energy must be conserved, meaning $R_s + T_s = 1$. It can be rigorously shown that the expressions for $r_s$ and $t_s$ derived from the boundary conditions perfectly satisfy this conservation law for all angles and refractive indices.

### Analysis of Reflection Phenomena

The Fresnel equations predict a variety of behaviors depending on the angle of incidence and the relative refractive indices of the two media.

#### Normal and Near-Normal Incidence

The simplest case is **[normal incidence](@entry_id:260681)**, where $\theta_i = 0$. By Snell's law, $\theta_t = 0$ as well. The Fresnel equations for [s-polarization](@entry_id:262966) simplify significantly:

$r_s(\theta_i=0) = \frac{n_1 - n_2}{n_1 + n_2}$

$t_s(\theta_i=0) = \frac{2n_1}{n_1 + n_2}$

The reflectance at [normal incidence](@entry_id:260681) is $R_s(0) = \left(\frac{n_1 - n_2}{n_1 + n_2}\right)^2$. This value represents the minimum possible [reflectance](@entry_id:172768) for any interface, a key parameter in designing anti-reflection coatings. For small deviations from [normal incidence](@entry_id:260681), the [reflectance](@entry_id:172768) can be analyzed using a Taylor expansion. The reflectance $R_s$ increases quadratically with the [angle of incidence](@entry_id:192705) $\theta_i$ for small angles, meaning the function is flat at $\theta_i=0$ and begins to curve upwards [@problem_id:1800008].

#### External Reflection ($n_1  n_2$)

When light travels from a lower-index medium to a higher-index medium (e.g., from air to glass), this is termed **external reflection**. A key feature of this scenario can be deduced by analyzing the sign of $r_s$. Since $n_1  n_2$, Snell's law implies $\theta_t  \theta_i$, and consequently $\cos\theta_t > \cos\theta_i$. A rigorous analysis shows that for all possible angles of incidence ($0 \le \theta_i \le 90^\circ$), the term $n_2 \cos\theta_t$ is always greater than $n_1 \cos\theta_i$ [@problem_id:1582905].

As a result, the numerator of $r_s$, $(n_1 \cos\theta_i - n_2 \cos\theta_t)$, is always negative. Since the denominator is always positive, $r_s$ is always negative for external reflection. A negative real [reflection coefficient](@entry_id:141473) signifies a **phase shift of $\pi$ radians ($180^\circ$)** in the reflected electric field wave relative to the incident wave.

The [reflectance](@entry_id:172768) $R_s = r_s^2$ is a monotonically increasing function of the [angle of incidence](@entry_id:192705) $\theta_i$. It starts at its minimum value $R_s(0)$ at [normal incidence](@entry_id:260681) and increases smoothly to $R_s = 1$ at grazing incidence ($\theta_i = 90^\circ$). The specific angle at which the [reflectance](@entry_id:172768) reaches a certain value, such as the average of its minimum and maximum, can be calculated directly from the Fresnel equations, providing a concrete illustration of this monotonic behavior [@problem_id:1800014].

#### Internal Reflection ($n_1 > n_2$)

When light travels from a higher-index medium to a lower-index medium (e.g., from glass to air), this is **internal reflection**. The behavior is markedly different.

For angles of incidence below a certain threshold, the reflection coefficient $r_s$ is positive, indicating **no phase shift** upon reflection. The [reflectance](@entry_id:172768) $R_s$ again starts at its minimum value $R_s(0) = \left(\frac{n_1-n_2}{n_1+n_2}\right)^2$ at [normal incidence](@entry_id:260681) and increases with $\theta_i$. An important distinction from [p-polarization](@entry_id:275469) is that for [s-polarization](@entry_id:262966), $r_s$ (and thus $R_s$) can never be zero unless the indices are identical ($n_1 = n_2$). This means some reflection always occurs, with the absolute minimum happening at [normal incidence](@entry_id:260681) [@problem_id:1800013].

As the [angle of incidence](@entry_id:192705) $\theta_i$ increases, Snell's law predicts that $\sin\theta_t = (n_1/n_2)\sin\theta_i$ will eventually reach 1. This occurs at the **critical angle**, $\theta_c$:

$\theta_c = \arcsin\left(\frac{n_2}{n_1}\right)$

For angles of incidence $\theta_i > \theta_c$, $\sin\theta_t > 1$, which has no solution for a real angle $\theta_t$. This signals the onset of **Total Internal Reflection (TIR)**. In this regime, the mathematics reveals that the term $\cos\theta_t$ becomes a purely imaginary number:

$\cos\theta_t = \sqrt{1 - \sin^2\theta_t} = i \sqrt{\sin^2\theta_t - 1} = i \frac{\sqrt{n_1^2 \sin^2\theta_i - n_2^2}}{n_2}$

Substituting this into the formula for $r_s$ yields a complex number of the form $\frac{A - iB}{A + iB}$, where $A$ and $B$ are real quantities. The magnitude of such a number is always 1.

$|r_s| = \left| \frac{n_1 \cos\theta_i - i \sqrt{n_1^2 \sin^2\theta_i - n_2^2}}{n_1 \cos\theta_i + i \sqrt{n_1^2 \sin^2\theta_i - n_2^2}} \right| = 1$

This means the [reflectance](@entry_id:172768) $R_s = |r_s|^2 = 1$. All incident power is reflected back into the first medium; no energy is transmitted on average into the second medium. Although there is no transmitted wave, an [evanescent field](@entry_id:165393) does exist, decaying exponentially into the second medium.

While the amplitude of the reflected wave is unchanged, its phase is shifted. The complex [reflection coefficient](@entry_id:141473) can be written as $r_s = \exp(i\delta_s)$, where $\delta_s$ is the phase shift. From the complex form of $r_s$, the phase shift can be calculated as [@problem_id:1799982] [@problem_id:1799961]:

$\delta_s = -2 \arctan\left(\frac{\sqrt{n_1^2 \sin^2\theta_i - n_2^2}}{n_1 \cos\theta_i}\right)$

This phase shift is not constant but varies with the [angle of incidence](@entry_id:192705), ranging from $0$ at $\theta_i = \theta_c$ to $-\pi$ [radians](@entry_id:171693) at $\theta_i = 90^\circ$. This angle-dependent phase shift is a crucial phenomenon exploited in many optical devices, from [optical fibers](@entry_id:265647) to advanced spectroscopic techniques like Attenuated Total Reflection (ATR) spectroscopy.