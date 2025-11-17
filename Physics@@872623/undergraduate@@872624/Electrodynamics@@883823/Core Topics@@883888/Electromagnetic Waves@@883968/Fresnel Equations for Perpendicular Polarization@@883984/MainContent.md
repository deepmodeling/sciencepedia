## Introduction
When light strikes the surface of a material like glass or water, a portion of it bounces back while the rest passes through—a familiar yet profound phenomenon. To move beyond this qualitative observation and precisely predict how much light is reflected and transmitted, physicists turn to a cornerstone of [classical electrodynamics](@entry_id:270496): the Fresnel equations. These equations provide the mathematical link between a material's intrinsic properties, like its refractive index, and the behavior of light at its surface. This article focuses on a crucial and common scenario: the [reflection and refraction](@entry_id:184887) of light whose electric field is polarized perpendicular to the plane of incidence, known as [s-polarization](@entry_id:262966) or Transverse Electric (TE) waves.

This article is structured to build your understanding from the ground up. In the first chapter, **Principles and Mechanisms**, we will derive the Fresnel equations for [s-polarization](@entry_id:262966) directly from the fundamental boundary conditions of Maxwell's equations, exploring the laws of [reflection and refraction](@entry_id:184887), phase shifts, and the fascinating case of [total internal reflection](@entry_id:267386). The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the practical power of these equations by examining their role in [optical coatings](@entry_id:174911), fiber optics, plasma physics, and even their formal connection to quantum mechanics. Finally, the **Hands-On Practices** section provides selected problems to test and deepen your grasp of these essential concepts. We begin by establishing the fundamental principles that govern the wave's behavior at the boundary.

## Principles and Mechanisms

When an [electromagnetic wave](@entry_id:269629) encounters a boundary between two different media, it is partially reflected and partially transmitted. The quantitative description of this phenomenon is governed by the **Fresnel equations**, which provide the amplitudes of the reflected and transmitted waves relative to the incident wave. This chapter will derive and analyze these equations for a specific, yet common, case: when the electric field of the incident wave is polarized perpendicular to the plane of incidence. This is known as **[s-polarization](@entry_id:262966)** (from the German *senkrecht*, meaning perpendicular) or **Transverse Electric (TE)** polarization.

### Boundary Conditions and Phase Matching

Let us consider a planar interface at $z=0$ separating two linear, isotropic, homogeneous, non-magnetic, and non-conducting (dielectric) media. The incident medium (for $z0$) has a refractive index $n_1$, and the transmission medium (for $z>0$) has a refractive index $n_2$. A [monochromatic plane wave](@entry_id:263295) with [angular frequency](@entry_id:274516) $\omega$ is incident upon this boundary. The plane of incidence, which contains the incident [wave vector](@entry_id:272479) $\vec{k}_I$, the reflected wave vector $\vec{k}_R$, and the transmitted [wave vector](@entry_id:272479) $\vec{k}_T$, is defined as the $xz$-plane.

For **[s-polarization](@entry_id:262966)**, the electric field vector $\vec{E}$ is perpendicular to this plane, meaning it oscillates purely along the $y$-axis. The electric fields of the incident, reflected, and transmitted waves at the boundary can be written as:

$\vec{E}_I(\vec{r}, t) = \hat{y} E_{0,I} \exp(i(\vec{k}_I \cdot \vec{r} - \omega t))$
$\vec{E}_R(\vec{r}, t) = \hat{y} E_{0,R} \exp(i(\vec{k}_R \cdot \vec{r} - \omega t))$
$\vec{E}_T(\vec{r}, t) = \hat{y} E_{0,T} \exp(i(\vec{k}_T \cdot \vec{r} - \omega t))$

where $E_{0,I}$, $E_{0,R}$, and $E_{0,T}$ are the complex amplitudes.

The fundamental laws of [reflection and refraction](@entry_id:184887) arise from the universal boundary conditions of Maxwell's equations. At an interface with no free charges or currents, the tangential components of both the electric field $\vec{E}$ and the magnetic field $\vec{H}$ must be continuous across the boundary. For this continuity to hold for all points $(x,y)$ on the interface and at all times $t$, the phase factors of the three waves must be identical at the boundary plane $z=0$. This crucial requirement is known as the **[phase-matching](@entry_id:189362) condition**:

$(\vec{k}_I \cdot \vec{r})_{z=0} = (\vec{k}_R \cdot \vec{r})_{z=0} = (\vec{k}_T \cdot \vec{r})_{z=0}$

This single condition dictates the entire geometry of [reflection and refraction](@entry_id:184887). Since $\vec{r}$ lies in the $xy$-plane at the boundary, this means the tangential components of the wave vectors must be equal: $k_{I,x} = k_{R,x} = k_{T,x}$ and $k_{I,y} = k_{R,y} = k_{T,y}$. Given our choice of the $xz$-plane as the plane of incidence, the $y$-components are all zero. The equality of the $x$-components yields:

$k_I \sin\theta_i = k_R \sin\theta_r = k_T \sin\theta_t$

where $\theta_i$, $\theta_r$, and $\theta_t$ are the angles of incidence, reflection, and transmission, respectively, measured from the normal ($z$-axis). In a given medium with refractive index $n$, the wave number is $k = n\omega/c$. Since the incident and reflected waves are in the same medium ($n_1$), $k_I = k_R$. This leads directly to the **Law of Reflection**:

$\sin\theta_i = \sin\theta_r \implies \theta_i = \theta_r$

The equality between the incident and transmitted tangential wave vectors, $k_I \sin\theta_i = k_T \sin\theta_t$, gives:

$\frac{n_1 \omega}{c} \sin\theta_i = \frac{n_2 \omega}{c} \sin\theta_t \implies n_1 \sin\theta_i = n_2 \sin\theta_t$

This is **Snell's Law of Refraction**. The [phase-matching](@entry_id:189362) condition also implies that the pattern formed by the intersection of the wavefronts with the boundary moves along the interface with a single, well-defined speed. This [phase velocity](@entry_id:154045) along the boundary, $v_{\parallel}$, is given by $v_{\parallel} = \omega/k_x = \omega/(k_1 \sin\theta_i) = c/(n_1 \sin\theta_i)$ [@problem_id:1582933].

### Derivation of the Amplitude Coefficients

With the geometric laws established, we can now use the boundary conditions to find the dynamic relationships between the wave amplitudes. We define the amplitude **[reflection coefficient](@entry_id:141473)** $r_s$ and **[transmission coefficient](@entry_id:142812)** $t_s$ as:

$r_s = \frac{E_{0,R}}{E_{0,I}} \quad \text{and} \quad t_s = \frac{E_{0,T}}{E_{0,I}}$

**1. Continuity of Tangential $\vec{E}$:**
For [s-polarization](@entry_id:262966), the entire electric field is tangential to the surface (in the $y$-direction). At $z=0$, the total electric field in medium 1 must equal the electric field in medium 2. After canceling the common phase factor, this gives:

$E_{0,I} + E_{0,R} = E_{0,T}$

Dividing by $E_{0,I}$, we obtain a simple, fundamental relationship between the coefficients [@problem_id:1799967]:

$1 + r_s = t_s$

**2. Continuity of Tangential $\vec{H}$:**
The magnetic field for a plane wave is given by $\vec{H} = \frac{1}{\mu_0 \omega} (\vec{k} \times \vec{E})$. For [s-polarization](@entry_id:262966) ($\vec{E} = E_y \hat{y}$), the tangential component of the magnetic field lies along the $x$-axis. The calculation yields $H_x = -\frac{k_z}{\mu_0 \omega} E_y$. The $z$-component of the [wave vector](@entry_id:272479) changes sign upon reflection: $k_{I,z} = k_1 \cos\theta_i$ and $k_{R,z} = -k_1 \cos\theta_i$. The continuity of $H_x$ at $z=0$ thus requires:

$H_{I,x} + H_{R,x} = H_{T,x}$
$-\frac{k_1 \cos\theta_i}{\mu_0 \omega} E_{0,I} + \frac{k_1 \cos\theta_i}{\mu_0 \omega} E_{0,R} = -\frac{k_2 \cos\theta_t}{\mu_0 \omega} E_{0,T}$

Using $k=n\omega/c$, this simplifies to:

$n_1 \cos\theta_i (E_{0,I} - E_{0,R}) = n_2 \cos\theta_t E_{0,T}$

We now have a system of two equations. Substituting $E_{0,T} = E_{0,I} + E_{0,R}$ into the second equation gives:

$n_1 \cos\theta_i (E_{0,I} - E_{0,R}) = n_2 \cos\theta_t (E_{0,I} + E_{0,R})$

Solving for the ratio $r_s = E_{0,R}/E_{0,I}$ yields the Fresnel equation for the [s-polarization](@entry_id:262966) [reflection coefficient](@entry_id:141473):

$r_s = \frac{n_1 \cos\theta_i - n_2 \cos\theta_t}{n_1 \cos\theta_i + n_2 \cos\theta_t}$

Using the relation $t_s = 1 + r_s$, we immediately find the transmission coefficient:

$t_s = \frac{2 n_1 \cos\theta_i}{n_1 \cos\theta_i + n_2 \cos\theta_t}$

### Analysis of the Reflection Coefficient

The [reflection coefficient](@entry_id:141473) $r_s$ encapsulates the key physics of the reflection process, including intensity and phase changes.

#### Phase Shift on Reflection

Let's consider **external reflection**, where light travels from a rarer medium to a denser medium ($n_1  n_2$). From Snell's law, this implies $\theta_t  \theta_i$. The denominator of $r_s$ is always positive. The sign of $r_s$ depends on the numerator, $n_1 \cos\theta_i - n_2 \cos\theta_t$. A rigorous comparison shows that for all possible angles of incidence, the term $n_2 \cos\theta_t$ is always greater than $n_1 \cos\theta_i$ [@problem_id:1582905]. The proof involves squaring both terms and using Snell's law:
$(n_2 \cos\theta_t)^2 - (n_1 \cos\theta_i)^2 = (n_2^2 - n_2^2\sin^2\theta_t) - (n_1^2 - n_1^2\sin^2\theta_i) = n_2^2 - n_1^2 > 0$.
Since both terms are positive, we have $n_2 \cos\theta_t > n_1 \cos\theta_i$.

Therefore, for external reflection ($n_1  n_2$), the numerator of $r_s$ is always negative. This means $r_s$ is always a negative real number, which corresponds to a **phase shift of $\pi$ [radians](@entry_id:171693) ($180^\circ$)** in the reflected electric field for all angles of incidence.

For **internal reflection** ($n_1 > n_2$), where light travels from a denser to a rarer medium, the situation is different. Here $\theta_t > \theta_i$, and the numerator can be positive or negative. However, as we will see, it never becomes zero.

#### Absence of a Brewster's Angle

For [p-polarized light](@entry_id:266884), there exists a special angle of incidence, Brewster's angle, at which the [reflection coefficient](@entry_id:141473) is zero. For [s-polarization](@entry_id:262966), this is not the case. The condition for zero reflection would be $r_s=0$, which implies $n_1 \cos\theta_i = n_2 \cos\theta_t$. As shown in the analysis above, this leads to the condition $n_1^2 = n_2^2$, or $n_1=n_2$. This means reflection can only vanish if there is no interface. Thus, for s-[polarized light](@entry_id:273160) incident on an interface between two different media ($n_1 \neq n_2$), the [reflectance](@entry_id:172768) is never zero for any non-normal [angle of incidence](@entry_id:192705) [@problem_id:1582950]. The minimum reflection always occurs at [normal incidence](@entry_id:260681) ($\theta_i = 0$).

#### Special Cases and Alternative Forms

Using Snell's law, we can eliminate the refractive indices from the expression for $r_s$ to obtain a form that depends only on the angles [@problem_id:1582879]:

$r_s = - \frac{\sin(\theta_i - \theta_t)}{\sin(\theta_i + \theta_t)}$

This elegant form makes the phase behavior clear. For external reflection ($n_1  n_2 \implies \theta_t  \theta_i$), the term $\sin(\theta_i - \theta_t)$ is positive, making $r_s$ negative.

At the two extremes of the range of incidence angles:
*   **Normal Incidence ($\theta_i \to 0$):** Here, $\theta_t \to 0$ as well. Using L'Hôpital's rule or simply setting $\cos\theta \approx 1$ gives the well-known result:
    $r_s(\theta_i=0) = \frac{n_1 - n_2}{n_1 + n_2}$
*   **Grazing Incidence ($\theta_i \to \pi/2$):** In this limit, regardless of whether $n_1 > n_2$ or $n_1  n_2$ (provided $n_1 \neq n_2$), the [reflection coefficient](@entry_id:141473) approaches -1. This means the [reflectance](@entry_id:172768) approaches 1. Any smooth surface becomes a perfect mirror for s-[polarized light](@entry_id:273160) at grazing incidence [@problem_id:1799975].

A special geometric condition occurs when the reflected and transmitted rays are perpendicular, meaning $\theta_i + \theta_t = \pi/2$. Under this specific condition, a straightforward substitution into the primary Fresnel equation yields $r_s = (n_1^2 - n_2^2)/(n_1^2 + n_2^2)$ [@problem_id:1582937].

### Energy Flow: Reflectance and Transmittance

The fraction of incident power that is reflected or transmitted is given by the **reflectance ($R_s$)** and **[transmittance](@entry_id:168546) ($T_s$)**. These are defined by the ratio of the power flow across the interface. The time-averaged power per unit area normal to the direction of propagation (intensity) is given by $I \propto n E_0^2$. The power flow across a unit area of the interface involves the projection of this intensity onto the normal, introducing a factor of $\cos\theta$.

The incident power on an area $A$ of the interface is $P_I = I_I \cos\theta_i A$. Similarly, $P_R = I_R \cos\theta_r A$ and $P_T = I_T \cos\theta_t A$.

The [reflectance](@entry_id:172768) is then:
$R_s = \frac{P_R}{P_I} = \frac{I_R \cos\theta_r A}{I_I \cos\theta_i A} = \frac{n_1 E_{0,R}^2}{n_1 E_{0,I}^2} = \left|\frac{E_{0,R}}{E_{0,I}}\right|^2 = |r_s|^2$

The [transmittance](@entry_id:168546) calculation is more subtle:
$T_s = \frac{P_T}{P_I} = \frac{I_T \cos\theta_t A}{I_I \cos\theta_i A} = \frac{n_2 E_{0,T}^2 \cos\theta_t}{n_1 E_{0,I}^2 \cos\theta_i} = \frac{n_2 \cos\theta_t}{n_1 \cos\theta_i} \left|\frac{E_{0,T}}{E_{0,I}}\right|^2$

$T_s = \frac{n_2 \cos\theta_t}{n_1 \cos\theta_i} |t_s|^2$

It is a common error to assume $T_s = |t_s|^2$. The additional factor, $\eta = \frac{n_2 \cos\theta_t}{n_1 \cos\theta_i}$, accounts for both the change in the [wave impedance](@entry_id:276571) of the medium (via the ratio $n_2/n_1$) and the change in the beam's cross-sectional area as it crosses the boundary (via the ratio $\cos\theta_t/\cos\theta_i$) [@problem_id:1799981].

With these correct definitions, one can rigorously show that for non-absorbing media, energy is conserved:
$R_s + T_s = 1$

### Total Internal Reflection

A remarkable phenomenon occurs during internal reflection ($n_1 > n_2$) when the [angle of incidence](@entry_id:192705) exceeds a certain **critical angle, $\theta_c$**. From Snell's Law, $\sin\theta_t = (n_1/n_2)\sin\theta_i$. Since $n_1/n_2 > 1$, it is possible for the right-hand side to be greater than 1. The [critical angle](@entry_id:275431) is the angle of incidence for which $\sin\theta_t=1$:

$\theta_c = \arcsin\left(\frac{n_2}{n_1}\right)$

For any [angle of incidence](@entry_id:192705) $\theta_i > \theta_c$, $\sin\theta_t > 1$, which has no solution for a real angle $\theta_t$. The physics is revealed by examining the term $\cos\theta_t$:

$\cos\theta_t = \sqrt{1 - \sin^2\theta_t} = \sqrt{1 - \left(\frac{n_1}{n_2}\right)^2 \sin^2\theta_i} = i \sqrt{\left(\frac{n_1}{n_2}\right)^2 \sin^2\theta_i - 1}$

The cosine of the transmission angle becomes purely imaginary. Substituting this into the [reflection coefficient](@entry_id:141473) $r_s$:

$r_s = \frac{n_1 \cos\theta_i - i \sqrt{n_1^2 \sin^2\theta_i - n_2^2}}{n_1 \cos\theta_i + i \sqrt{n_1^2 \sin^2\theta_i - n_2^2}}$

This is a complex number of the form $(A - iB)/(A + iB)$, which has a magnitude of exactly 1. Therefore, the reflectance is $R_s = |r_s|^2 = 1$. All the incident energy is reflected, a phenomenon called **Total Internal Reflection (TIR)**.

Although no energy is transmitted, the reflection is not instantaneous at the boundary. The reflected wave experiences a phase shift $\delta_s$, given by the argument of the complex $r_s$:

$\delta_s = -2 \arctan\left(\frac{\sqrt{n_1^2 \sin^2\theta_i - n_2^2}}{n_1 \cos\theta_i}\right)$

This phase shift depends on the [angle of incidence](@entry_id:192705) and the refractive indices, unlike the constant $\pi$ shift in external reflection. For example, for an s-polarized wave in glass ($n_1=1.48$) reflecting from a core-cladding interface ($n_2=1.465$) at $\theta_i=85^\circ$, the phase shift is calculated to be approximately $-104^\circ$ [@problem_id:1800006]. Similarly, a glass-air interface ($n_1=1.5, n_2=1.0$) at $\theta_i=50^\circ$ yields a phase shift of about $-60.8^\circ$ [@problem_id:1799961].

The imaginary wave vector component in the second medium implies the existence of a non-propagating field called the **[evanescent wave](@entry_id:147449)**. The transmitted electric field takes the form:

$\vec{E}_T(\vec{r}, t) \propto \exp(-\alpha z) \exp(i(k_x x - \omega t))$

where $\alpha = \frac{2\pi}{\lambda_0}\sqrt{n_1^2 \sin^2\theta_i - n_2^2}$ is the decay constant and $\lambda_0$ is the vacuum wavelength. This wave propagates along the interface (in the $x$-direction) but decays exponentially with distance $z$ into the second medium. It carries no net [energy flow](@entry_id:142770) away from the boundary. The characteristic **[penetration depth](@entry_id:136478)**, $d=1/\alpha$, is the distance over which the field amplitude drops to $1/e$ of its value at the interface [@problem_id:1582887]. This depth is typically on the order of the wavelength of light and is fundamental to technologies such as [optical waveguides](@entry_id:198354), fiber optics, and various sensing techniques that probe the surface of a medium.