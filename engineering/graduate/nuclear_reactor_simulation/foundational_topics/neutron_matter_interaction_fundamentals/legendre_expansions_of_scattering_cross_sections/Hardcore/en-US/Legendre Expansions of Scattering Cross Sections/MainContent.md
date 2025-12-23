## Introduction
In the intricate world of nuclear reactor physics, accurately predicting the fate of every neutron is paramount to ensuring safety and efficiency. While the total [scattering cross section](@entry_id:150101) tells us the probability of a neutron interacting with a nucleus, it offers no insight into a crucial question: in which direction will the neutron travel next? This gap in knowledge is significant, as the angular distribution of scattered neutrons profoundly influences neutron migration, leakage, and the overall power distribution within a reactor core.

This article addresses this challenge by providing a comprehensive guide to Legendre expansions, the standard mathematical framework used to describe anisotropic scattering. By mastering this topic, you will gain a fundamental understanding of how modern simulation tools model the complex directional behavior of neutrons. The following chapters will guide you through this essential concept:

-   **Principles and Mechanisms** will lay the theoretical groundwork, introducing the [differential scattering cross section](@entry_id:1123684), explaining the role of Legendre polynomials as an [orthogonal basis](@entry_id:264024), and interpreting the physical meaning of the expansion moments.
-   **Applications and Interdisciplinary Connections** will demonstrate how these principles are put into practice in reactor analysis codes, from generating multigroup cross-section libraries to their implementation in $P_N$ and $S_N$ solvers, and explore its use in related scientific fields.
-   **Hands-On Practices** will offer opportunities to apply this knowledge through targeted exercises, connecting analytical theory to the numerical methods used in computational [transport theory](@entry_id:143989).

We begin by establishing the fundamental principles that make the Legendre expansion the ideal tool for describing the angular nature of [neutron scattering](@entry_id:142835).

## Principles and Mechanisms

In the study of neutron transport, a precise description of the scattering process is paramount. While the total scattering cross section, $\Sigma_s$, quantifies the probability of a scattering interaction per unit path length, it provides no information about the direction of the scattered neutron. To accurately model the behavior of a neutron population within a reactor, we must characterize the [angular distribution](@entry_id:193827) of scattering events. This is the role of the [differential scattering cross section](@entry_id:1123684).

### The Differential Scattering Cross Section

The fundamental quantity describing the angular dependence of scattering is the **microscopic [differential scattering cross section](@entry_id:1123684)**, denoted $\frac{d\sigma_s}{d\Omega}$. It is defined as the effective target area per nucleus for scattering an incident neutron into a specific differential solid angle, $d\Omega$. Consequently, it has units of area per steradian (e.g., barns/sr). Although the steradian is a dimensionless unit in the SI system, it is retained by convention to emphasize that this quantity is an angular density. The total microscopic scattering cross section, $\sigma_s$, which has units of area, is recovered by integrating the [differential cross section](@entry_id:159876) over all possible outgoing directions, a solid angle of $4\pi$ steradians  :

$$ \sigma_s = \int_{4\pi} \frac{d\sigma_s}{d\Omega} \, d\Omega $$

In reactor physics, we are typically concerned with macroscopic phenomena. The **macroscopic [differential scattering cross section](@entry_id:1123684)**, $\frac{d\Sigma_s}{d\Omega}$, is obtained by multiplying its microscopic counterpart by the nuclide [number density](@entry_id:268986), $N$:

$$ \frac{d\Sigma_s}{d\Omega} = N \frac{d\sigma_s}{d\Omega} $$

This quantity has units of inverse length per steradian (e.g., cm⁻¹·sr⁻¹) and represents the probability per unit path length of scattering into a given solid angle. Integrating it over all solid angles yields the total macroscopic scattering cross section, $\Sigma_s = N \sigma_s$. It is crucial to distinguish that $\Sigma_s$ is an integrated probability per unit path length, not an angular density itself .

### Azimuthal Symmetry and the Scattering Cosine

For a [neutron scattering](@entry_id:142835) in a medium, the change in direction is described by two angles: a polar or deflection angle, $\theta$, and an [azimuthal angle](@entry_id:164011), $\phi$. However, in the vast majority of reactor physics applications, the scattering medium (e.g., fuel, moderator, coolant) is considered **isotropic**. This means the material has no intrinsic preferred direction. The target nuclei are unpolarized, their thermal motions are random (with no bulk flow), and if the material is polycrystalline, the crystal grains are randomly oriented. Furthermore, we assume the absence of external fields that could introduce a directional preference .

Under these conditions, the physical system possesses [rotational symmetry](@entry_id:137077) about the axis defined by the incident neutron's direction. Consequently, the probability of scattering is independent of the [azimuthal angle](@entry_id:164011) $\phi$. The scattering process depends only on the deflection angle $\theta$, the angle between the neutron's initial direction $\boldsymbol{\Omega}$ and its final direction $\boldsymbol{\Omega}'$. This is the principle of **[azimuthal symmetry](@entry_id:181872)**.

This symmetry allows us to simplify the description of the [scattering angle](@entry_id:171822). Instead of two variables, we need only one. For mathematical convenience, we use the cosine of the scattering angle, denoted by $\mu$:

$$ \mu = \cos\theta = \boldsymbol{\Omega} \cdot \boldsymbol{\Omega}' $$

Since the physical range for the deflection angle is $\theta \in [0, \pi]$ (from forward scattering to backward scattering), the domain for $\mu$ is correspondingly $[-1, 1]$. The [differential cross section](@entry_id:159876) can now be written as a function of this single variable, $\sigma_s(\mu)$. It is important to recognize that anisotropy in scattering (e.g., a tendency for forward scattering) is fully compatible with [azimuthal symmetry](@entry_id:181872); the former refers to a non-uniform dependence on $\theta$, while the latter refers to a uniform dependence on $\phi$ .

### The Legendre Polynomial Basis

The reduction of the angular dependence to a function $\sigma_s(\mu)$ on the interval $[-1, 1]$ invites the use of a suitable basis of functions to represent it. The **Legendre polynomials**, $P_l(\mu)$, are the ideal choice for this purpose. They are a set of orthogonal polynomials on the interval $[-1, 1]$ and arise naturally as solutions to the Legendre differential equation:

$$ (1-\mu^2)\frac{d^2y}{d\mu^2} - 2\mu\frac{dy}{d\mu} + l(l+1)y = 0 $$

This equation can be expressed in Sturm-Liouville form, which reveals a crucial property. By rewriting it as $\frac{d}{d\mu}\left((1-\mu^2)\frac{dy}{d\mu}\right) + l(l+1)y = 0$, we can identify the Sturm-Liouville weight function as $w(\mu)=1$ . This means the Legendre polynomials are orthogonal with respect to a simple, unweighted inner product:

$$ \int_{-1}^{1} P_l(\mu) P_m(\mu) \, d\mu = \frac{2}{2l+1} \delta_{lm} $$

where $\delta_{lm}$ is the Kronecker delta. This mathematical property aligns perfectly with the physical integration measure used in [transport theory](@entry_id:143989), which, after accounting for [azimuthal symmetry](@entry_id:181872), involves integrating over $d\mu$ without any additional weighting factors.

The Legendre polynomials can be generated using the **Rodrigues' formula**  :

$$ P_l(\mu) = \frac{1}{2^l l!} \frac{d^l}{d\mu^l} (\mu^2 - 1)^l $$

The first few Legendre polynomials, which are fundamental to describing the primary features of [anisotropic scattering](@entry_id:148372), are:

-   **$P_0(\mu) = 1$**: Represents isotropic (angle-independent) behavior.
-   **$P_1(\mu) = \mu$**: Represents linear anisotropy (forward or backward bias).
-   **$P_2(\mu) = \frac{1}{2}(3\mu^2 - 1)$**: Represents quadratic anisotropy (preference for forward/backward vs. sideways scattering).

### The Legendre Expansion and its Moments

With this basis, we can expand the azimuthally symmetric [differential cross section](@entry_id:159876) as an infinite series:

$$ \frac{d\sigma_s}{d\Omega}(\mu) = \sum_{l=0}^{\infty} \frac{2l+1}{4\pi} \sigma_{sl} P_l(\mu) $$

This particular normalization is conventional in [transport theory](@entry_id:143989) because it imparts a direct physical meaning to the expansion coefficients, $\sigma_{sl}$, known as the **Legendre moments**. To find these moments, we exploit the orthogonality of the polynomials. Multiplying the expansion by $P_m(\mu)$ and integrating over the full [solid angle](@entry_id:154756) gives:

$$ \int_{4\pi} \frac{d\sigma_s}{d\Omega}(\mu) P_m(\mu) \, d\Omega = \sum_{l=0}^{\infty} \frac{2l+1}{4\pi} \sigma_{sl} \int_{4\pi} P_l(\mu) P_m(\mu) \, d\Omega $$

Using $d\Omega = 2\pi d\mu$ for azimuthally [symmetric functions](@entry_id:149756) and the orthogonality relation, the integral on the right-hand side simplifies to $\frac{4\pi}{2l+1}\delta_{lm}$. This isolates the coefficient $\sigma_{sm}$, leading to the [projection formula](@entry_id:152164) for the moments:

$$ \sigma_{sm} = \int_{4\pi} \frac{d\sigma_s}{d\Omega}(\mu) P_m(\mu) \, d\Omega = 2\pi \int_{-1}^{1} \sigma_s(\mu) P_m(\mu) \, d\mu $$

where $\sigma_s(\mu)$ is simply another notation for $\frac{d\sigma_s}{d\Omega}(\mu)$. Critically, since the polynomials $P_m(\mu)$ and the [solid angle](@entry_id:154756) element $d\Omega$ are dimensionless, all Legendre moments $\sigma_{sl}$ have the same units as the total cross section $\sigma_s$: area .

#### Deeper Connection to Spherical Harmonics

The Legendre expansion is not merely a convenient choice; it is a direct consequence of [rotational symmetry](@entry_id:137077). A general angular function without [azimuthal symmetry](@entry_id:181872) would be expanded in **[spherical harmonics](@entry_id:156424)**, $Y_l^m(\theta, \phi)$, which form a complete basis on the surface of a sphere. When [azimuthal symmetry](@entry_id:181872) is imposed, only the terms with azimuthal mode number $m=0$ survive. The spherical harmonics for $m=0$ are directly proportional to the Legendre polynomials, $Y_l^0(\theta, \phi) \propto P_l(\cos\theta)$. Thus, the assumption of an isotropic medium mathematically reduces the general [spherical harmonic expansion](@entry_id:188485) to the Legendre series we use .

### Physical Interpretation of Legendre Moments

The power of the Legendre expansion lies in the physical meaning of its leading terms. By truncating the series at a low order (a $P_N$ approximation), we can capture the most important features of the scattering distribution.

-   **The Zeroth Moment ($l=0$):**
    The zeroth Legendre polynomial is $P_0(\mu)=1$. The zeroth moment is therefore:
    $$ \sigma_{s0} = \int_{4\pi} \frac{d\sigma_s}{d\Omega}(\mu) (1) \, d\Omega = \sigma_s $$
    The zeroth moment, $\sigma_{s0}$, is identical to the total microscopic [scattering cross section](@entry_id:150101) . If all higher moments are zero, the [differential cross section](@entry_id:159876) is constant: $\frac{d\sigma_s}{d\Omega} = \frac{\sigma_{s0}}{4\pi}$. This describes **isotropic scattering**, where neutrons are scattered with equal probability in all directions.

-   **The First Moment ($l=1$):**
    The first moment, $\sigma_{s1}$, is associated with $P_1(\mu)=\mu$. It quantifies the degree of forward or backward bias in scattering. This is captured by the **anisotropy factor**, $g$, which is defined as the average cosine of the scattering angle:
    $$ g = \langle\mu\rangle = \frac{\int_{4\pi} \mu \frac{d\sigma_s}{d\Omega}(\mu) \, d\Omega}{\int_{4\pi} \frac{d\sigma_s}{d\Omega}(\mu) \, d\Omega} = \frac{\sigma_{s1}}{\sigma_{s0}} $$
    If $g > 0$, scattering is predominantly in the forward direction ($\mu > 0$). If $g  0$, it is backward-biased. For isotropic scattering, $g=0$. This parameter is also denoted as $\bar{\mu}$ .

-   **The Transport Cross Section:**
    The first moment is used to define the **[transport cross section](@entry_id:1133392)**, $\sigma_{tr}$:
    $$ \sigma_{tr} = \sigma_{s0} - \sigma_{s1} = \sigma_s(1 - g) $$
    This is a corrected scattering cross section widely used in [diffusion theory](@entry_id:1123718). It accounts for the fact that a forward-peaked scattering event (where $\mu \approx 1$ and $g$ is large) does little to change a neutron's overall direction of travel. The [transport cross section](@entry_id:1133392) effectively removes the forward-scattering component, treating it as if no interaction occurred, thus better representing the net [momentum transfer](@entry_id:147714) in a collision .

As an illustrative example, consider a simple linearly anisotropic scattering kernel given by $\sigma_s(\mu) = \alpha + \beta\mu$. Applying the moment formulas, we find $\sigma_{s0} = 4\pi\alpha$ and $\sigma_{s1} = \frac{4\pi}{3}\beta$. The [transport cross section](@entry_id:1133392) is then $\sigma_{tr} = 4\pi(\alpha - \frac{\beta}{3})$ . A more complex quadratic kernel, such as $\Sigma_s(\mu) = \Sigma_0(1+\alpha\mu+\beta\mu^2)$, can also be decomposed. By expressing powers of $\mu$ in terms of $P_l(\mu)$ (e.g., $\mu^2 = \frac{2}{3}P_2(\mu) + \frac{1}{3}P_0(\mu)$), one can find the coefficients by inspection .

### Center-of-Mass versus Laboratory Frame

The physics of a two-body collision is simplest in the **center-of-mass (CM) frame**, where the total momentum is zero. For [elastic scattering](@entry_id:152152), the scattering process in the CM frame is often isotropic or has a simple anisotropy. However, our measurement instruments and reactor calculations exist in the **laboratory (lab) frame**, where the target nucleus is typically assumed to be initially at rest. The angular distributions in these two frames are different, and it is essential to know how to transform between them.

For [elastic scattering](@entry_id:152152) of a neutron (mass $m$) from a stationary nucleus (mass $M$), with [mass ratio](@entry_id:167674) $A = M/m$, the relationship between the cosine of the [scattering angle](@entry_id:171822) in the lab frame ($\mu_{\text{lab}}$) and the CM frame ($\mu_{\text{cm}}$) is derived from conservation of momentum and energy :

$$ \mu_{\text{lab}} = \frac{1 + A\mu_{\text{cm}}}{\sqrt{1 + A^2 + 2A\mu_{\text{cm}}}} $$

A profound consequence of this transformation is that even if scattering is perfectly isotropic in the CM frame, it will be anisotropic and forward-peaked in the lab frame. For isotropic CM scattering, the probability distribution of $\mu_{\text{cm}}$ is uniform, $p(\mu_{\text{cm}}) = 1/2$ on $[-1, 1]$. We can calculate the average cosine in the lab frame under this condition:

$$ \langle\mu_{\text{lab}}\rangle = \int_{-1}^{1} \mu_{\text{lab}}(\mu_{\text{cm}}) p(\mu_{\text{cm}}) \, d\mu_{\text{cm}} = \frac{1}{2}\int_{-1}^{1} \frac{1 + A\mu_{\text{cm}}}{\sqrt{1 + A^2 + 2A\mu_{\text{cm}}}} \, d\mu_{\text{cm}} $$

Evaluating this integral yields a remarkably simple and important result :

$$ \langle\mu_{\text{lab}}\rangle = \frac{2}{3A} $$

This result, which is the anisotropy factor $g$ for isotropic CM scattering, shows that the degree of forward-peaking in the lab frame depends inversely on the target mass.
-   For a very heavy target nucleus ($A \gg 1$), $\langle\mu_{\text{lab}}\rangle \to 0$, and the scattering becomes nearly isotropic in the lab frame.
-   For a very light target nucleus, such as hydrogen in water ($A \approx 1$), $\langle\mu_{\text{lab}}\rangle = 2/3$. This indicates strong [forward scattering](@entry_id:191808), a critical phenomenon for [neutron moderation](@entry_id:1128702).

This transformation is fundamental for processing nuclear data, which is often calculated or evaluated in the CM frame, into the Legendre moments in the [lab frame](@entry_id:181186) required by [neutron transport simulation](@entry_id:1128710) codes.